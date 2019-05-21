# Callbacks

Callbacks are used to send real-time notifications on the events that happen on a bunq account. The updates information is sent to a URL of your choice.

## Notification Filters

To subscribe to specific events from a bunq account, you have to create notification filters. In practice, this means updating the UserPerson, UserCompany, MonetaryAccount or CashRegister object with `notification_filters`.

Here is what the `notification_filters` object looks like:

```text
{
    "notification_filters": [
        {
            "notification_delivery_method": "URL",
            "notification_target": “{YOUR_CALLBACK_URL}",
            "category": "REQUEST"
        },
        {
            "notification_delivery_method": "URL",
            "notification_target": "{YOUR_CALLBACK_URL}",
            "category": "PAYMENT"
        }
    ]
}
```

### Notification Filter Fields

* `notification_delivery_method`: specify the delivery method: 
  * URL \(_for sending an HTTP request to the provided URL\)._  Choose this method to receive callbacks.
  * PUSH _\(for sending a push notification to user's phone\)._
* `notification_target`: provide the URL you want to receive the callbacks on. This URL must use HTTPS.
* `category`: specify the types of events you would like to receive callbacks on.

### Callback categories

| Category | Description |
| :--- | :--- |
| BILLING | notifications for all bunq invoices |
| CARD\_TRANSACTION\_SUCCESSFUL | notifications for successful card transactions |
| CARD\_TRANSACTION\_FAILED | notifications for failed card transaction |
| CHAT | notifications for received chat messages |
| DRAFT\_PAYMENT | notifications for creation and updates of draft payments |
| IDEAL | notifications for iDEAL-deposits towards a bunq account |
| SOFORT | notifications for SOFORT-deposits towards a bunq account |
| MUTATION | notifications for any action that affects a monetary account’s balance |
| PAYMENT | notifications for payments created from, or received on a bunq account \(doesn’t include payments that result out of paying a Request, iDEAL, Sofort or Invoice\). Outgoing payments have a negative value while incoming payments have a positive value |
| REQUEST | notifications for incoming requests and updates on outgoing requests |
| SCHEDULE\_RESULT | notifications for when a scheduled payment is executed |
| SCHEDULE\_STATUS | notifications about the status of a scheduled payment, e.g. when the scheduled payment is updated or cancelled |
| SHARE | notifications for any updates or creation of Connects \(ShareInviteBankInquiry\) |
| TAB\_RESULT | notifications for updates on Tab payments |
| BUNQME\_TAB | notifications for updates on bunq.me Tab \(open request\) payments |
| SUPPORT | notifications for messages received from us through support chat |

### Mutation Category

A _Mutation_ is a change in the balance of a monetary account. A _Mutation_ is created for each payment-like object, such as a request, iDEAL-payment or a regular payment. Therefore, the `MUTATION`category can be used to keep track of a monetary account's balance change.

### Receiving Callbacks

* Callbacks for the sandbox environment will be made from different IP's at AWS.
* Callbacks for the production environment will be made from 185.40.108.0/22.

_The IP addresses might change_. We will notify you in a timely fashion if such a change is planned.

### Retry mechanism

When the execution of a callback fails \(e.g. the callback server is down or the response contains an error\), we try to resend it for a maximum of 5 times, with an interval of one minute between each try. If your server is not reachable by the callback after the 6th total try, the callback is not sent anymore.

## Certificate Pinning

We recommend that you use certificate pinning as an extra security measure. We will check if the certificate of the recipient server matches the pinned certificate that you provided and cancel the callback if the check fails or we detect a mismatch.

### How to set up certificate pinning

1. Retrieve the SSL certificate of your server using the following command:

   `openssl s_client -servername www.example.com -connect www.example.com:443 < /dev/null | sed -n "/-----BEGIN/,/-----END/p" > www.example.com.pem`

2. `POST` the certificate to the `certificate-pinned`endpoint.

Once ready, every callback will be checked against the pinned certificate that you provided. Note that if the SSL certificate on your server expires or is changed, our callbacks will fail.

