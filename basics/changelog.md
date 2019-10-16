# Changelog

## Upcoming changes

### December 4, 2019

Due to internal backend changes, all active [device-server](https://doc.bunq.com/#/device-server/Create_DeviceServer) installations created before April 9, 2019, will stop being validated on December 4, 2019. To communicate with the bunq API again, [create a new API context](https://beta.doc.bunq.com/basics/authentication#creating-api-context).

### January 15, 2019

We are deprecating the _limit\_card\_debit\_replacement_ field from `/v1/user/{user_id}/limit` and are replacing it with _limit\_card\_replacement_.

## Released

### October 9, 2019

We are replacing _primary\_account\_numbers\_virtual_ and _primary\_account\_number\_four\_digit_ from the [card](https://doc.bunq.com/?utm_source=What%27s+new+with+the+bunq+API&utm_campaign=d65e4c4f05-API_Partners&utm_medium=email&utm_term=0_0aa6b52aaa-d65e4c4f05-#/card) resource with _primary\_account\_numbers_.  
  
The field will return the same string for _primary\_account\_numbers_ and the same field + canceled cards for _primary\_account\_numbers\_virtual_.

### October 8, 2019

We are deprecating creating push notifications through updating _notification\_filters_ in the User and MonetaryAccount objects.

Instead, we are introducing separate endpoints for the callbacks and notifications.

* `/v1/user/{userID}/notification-filter-push`
* `/v1/user/{userID}/notification-filter-url`
* `/v1/user/{userID}/monetary-account/{monetary-accountID}/notification-filter-push`
* `/v1/user/{userID}/monetary-account/{monetary-accountID}/notification-filter-url`

{% hint style="warning" %}
**NOTE:** When used via OAuth, the created push notifications expire in 90 days.
{% endhint %}

### August 29, 2019

We have added the support of [callbacks](https://beta.doc.bunq.com/basics/callbacks) to OAuth.

### July 9, 2019

We have deprecated the following share-invite-bank endpoints:

* `/user/{userID}/monetary-account/{monetary-accountID}/share-invite-bank-inquiry`
* `/user/{userID}/monetary-account/{monetary-accountID}/share-invite-bank-inquiry/{itemId}`
* `/user/{userID}/monetary-account/{monetary-accountID}/share-invite-bank-inquiry/{share-invite-bank-inquiryID}/amount-used/{itemId}`
* `/user/{userID}/share-invite-bank-response`
* `/user/{userID}/share-invite-bank-response/{itemId}`

You can use the following endpoints instead:

* `/user/{userID}/monetary-account/{monetary-accountID}/share-invite-monetary-account-inquiry`
* `/user/{userID}/monetary-account/{monetary-accountID}/share-invite-monetary-account-inquiry/{itemId}`
* `/user/{userID}/monetary-account/{monetary-accountID}/share-invite-monetary-account-inquiry/{share-invite-monetary-account-inquiryID}/amount-used/{itemId}`
* `/user/{userID}/share-invite-monetary-account-response`
* `/user/{userID}/share-invite-monetary-account-response/{itemId}`

### July 2, 2019

1. The _type_ field has become mandatory for [_card-debit_](https://doc.bunq.com/#/card-debit)_._
2. We have deprecated the _applied\_limit_ field from the [mastercard\_action](https://doc.bunq.com/#/mastercard-action) responses.
3. We have removed the _activation\_code_ field from [CardUpdate](https://doc.bunq.com/#/card/Update_Card_for_User). Instead of using the field, set the status ACTIVE when the card has been ACCEPTED\_FOR\_PRODUCTION.

### April 18, 2019

The old card limit fields in the [_card_](https://doc.bunq.com/#/card) and [_card-batch_](https://doc.bunq.com/#/card-batch) objects have been deprecated and replaced with new ones. The default limit of €1,000 is now applied to all new cards.

![](../.gitbook/assets/screenshot-2019-04-10-at-12.34.11%20%282%29.png)



