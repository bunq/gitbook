# Changelog

{% hint style="success" %}
Stay up-to-date with the bunq API updates! [Subscribe to our API newsletter](https://bunq.us8.list-manage.com/subscribe?u=c00d0d6daea4e1cf7c863d52e&id=b08680cdc7)!
{% endhint %}

## Upcoming changes

### Near future

1. Due to internal backend changes, all active [device-server](https://doc.bunq.com/#/device-server/Create_DeviceServer) installations created before April 9, 2019, will stop being validated \(previously announced dates: January 15, 2020; April 8, 2020\). To communicate with the bunq API again, [create a new API context](https://beta.doc.bunq.com/basics/authentication#creating-api-context).

### November 4, 2020

1. The `ShareInviteBankInquiry` object is changing its name to `ShareInviteMonetaryAccountInquiry` on November 4th, 2020. Please plan on changing the _ShareInviteBankResponse_ field to _ShareInviteMonetaryAccountResponse_ in your integration on that date.
2. We are removing the following `ShareDraftInquiry` endpoints on November 4, 2020 \(previously announced date: August 26, 2020\)
   * `/user/{userID}/draft-share-invite-bank/`
   * `/user/{userID}/draft-share-invite-bank/{itemId}`
   * `/user/{userID}/draft-share-invite-bank/{draft-share-invite-bankID}/qr-code-content`

{% hint style="warning" %}
If your application is using Connect as an authentication method, please switch to OAuth by November 4, 2020.
{% endhint %}

## Released

### September 10, 2020

We removed the `/sandbox-user` endpoint. You can use the following endpoints instead:

* `/sandbox-user-company`
* `/sandbox-user-person`

### July 1, 2020

1. It is now possible to get a tracking link for the ordered card via the `card_shipment_tracking_url` field.
2. You can read how much money the card saved the user via the `amount_saved_zero_fx` field.
3. You can provide a more accurate card tracking experience via the updated list of possible card order statuses:

* `NEW_CARD_REQUEST_RECEIVED`
* `CARD_REQUEST_PENDING`
* `SENT_FOR_PRODUCTION`
* `ACCEPTED_FOR_PRODUCTION`
* `DELIVERED_TO_CUSTOMER`
* `CARD_UPDATE_REQUESTED`
* `CARD_UPDATE_PENDING`
* `CARD_UPDATE_SENT`
* `CARD_UPDATE_ACCEPTED` 
* `VIRTUAL_DELIVERY`
* `NEW_CARD_REQUEST_PENDING_USER_APPROVAL`
* `SENT_FOR_DELIVERY`
* `NEW_CARD_REQUEST_CANCELLED`

### May 27, 2020

Requests with full request signatures stopped being validated on May 27, 2020 \(previously announced date: April 28, 2020\). 

{% hint style="warning" %}
If you are still signing ****full requests, please switch to [signing the body solely](https://beta.doc.bunq.com/basics/authentication/signing).
{% endhint %}

### April 28, 2020

We switched to [only signing the response body](https://beta.doc.bunq.com/basics/authentication/signing#response-verifying-example). 

### April 24, 2020

1. We introduced an OAUTH callback category. Use it to receive notifications on revoked OAuth connections.
2. We added the following resources for Slice group management:
   * [registry](https://doc.bunq.com/#/registry)
   * [registry-entry](https://doc.bunq.com/#/registry-entry)
   * [registry-setting](https://doc.bunq.com/#/registry-setting)
   * [registry-settlement](https://doc.bunq.com/#/registry-settlement)
   * [registry-settlement-pending](https://doc.bunq.com/#/registry-settlement-pending)

### March 25, 2020

1. We deprecated the `ShareDraftInquiry` object. The following endpoints will be removed on June 10, 2020:
   * `/user/{userID}/draft-share-invite-bank/`
   * `/user/{userID}/draft-share-invite-bank/{itemId}`
   * `/user/{userID}/draft-share-invite-bank/{draft-share-invite-bankID}/qr-code-content`
2. We have deprecated the [/sandbox-user](https://doc.bunq.com/#/sandbox-user/Create_SandboxUser) endpoint and will remove it on June 10, 2020. You can use the following endpoints instead:
   * `/sandbox-user-company`
   * `/sandbox-user-person`
3. We have added the following endpoints for creating international payments in [39 currencies](https://together.bunq.com/d/5185-transferwise-currencies/2):
   * `/user/{userID}/transferwise-currency`
   * `/user/{userID}/transferwise-quote-temporary`
   * `/user/{userID}/transferwise-quote-temporary/{transferwise-quote-temporaryID}`
   * `/user/{userID}/transferwise-user`
   * `/user/{userID}/transferwise-quote`
   * `/user/{userID}/transferwise-quote/(transferwise-quoteID)`
   * `/user/{userID}/transferwise-quote/{transferwise-quoteID}/transferwise-recipient`
   * `/user/{userID}/transferwise-quote/{transferwise-quoteID}/transferwise-recipient-requirement`
   * `/user/{userID}/transferwise-quote/{transferwise-quoteID}/transferwise-transfer-requirement`
   * `/user/{userID}/monetary-account/{monetary-accountID}/transferwise-quote/{transferwise-quoteID}/transferwise-transfer`

{% hint style="info" %}
[Follow this sequence of steps](https://beta.doc.bunq.com/quickstart/transferwise-payment) to make your first non-euro payment.
{% endhint %}

### January 28, 2020 \(bunq Update 13 edition\)

#### Changes

1. Request signing became mandatory only for creating a session and creating a payment. The use of signing for other API requests is optional. 
2. We introduced [request body signing](https://beta.doc.bunq.com/basics/authentication/signing). URL and headers do not need to be signed. Body signing completely replaced entire request signing on May 27, 2020 \(previously announced date: April 28, 2020\).
3. The following headers are now optional:
   1. `X-Bunq-Geolocation`;
   2. `X-Bunq-Language` \(`en_US` is the default language setting for responses and error descriptions\);
   3. `X-Bunq-Region` \(`en_US` is the default region for currency formatting\);
   4. `X-Bunq-Request-Id`.
4. We extended the [OAuth scopes ](https://beta.doc.bunq.com/basics/oauth#what-can-my-apps-do-with-oauth)with the following permissions:
   1. create payment requests using the request-inquiry API resource;
   2. create monetary accounts \(bank, savings, and joint ones\);
   3. order cards;
   4. manage cards.

#### Deprecations

1. We have deprecated the signing of the entire API request \(the URL, headers and body\). Requests with full request signatures will stop being validated on April 28, 2020. Please switch to [signing the body solely](https://beta.doc.bunq.com/basics/authentication/signing) by that date.
2. We are switching to [only signing the response body](https://beta.doc.bunq.com/basics/authentication/signing#response-verifying-example) on April 28, 2020. 
3. We have deprecated additional encryption.

### January 15, 2020

We removed the _limit\_card\_debit\_replacement_ field from `/v1/user/{user_id}/limit` and replaced it with _limit\_card\_replacement_.

### December 17, 2019

It’s now possible to retrieve the tree planting progress of the user via the [`/user/{userID}/tree-progress`](https://doc.bunq.com/#/tree-progress/List_all_TreeProgress_for_User) ``endpoint.

### December 11, 2019

1. It’s now possible to order Green and Travel cards via the [`/user/{userID}/card-credit`](https://doc.bunq.com/#/card-credit/Create_CardCredit_for_User) endpoint.
2. We have added an option to [disable request signature validation in sandbox](https://beta.doc.bunq.com/basics/sandbox#sandbox-request-signing).
3. We have changed the default SMS verification code for the [sandbox app](https://beta.doc.bunq.com/basics/sandbox/android-emulator) from 123456 to 992266.

### October 9, 2019

We have replaced _primary\_account\_numbers\_virtual_ and _primary\_account\_number\_four\_digit_ from the [card](https://doc.bunq.com/?utm_source=What%27s+new+with+the+bunq+API&utm_campaign=d65e4c4f05-API_Partners&utm_medium=email&utm_term=0_0aa6b52aaa-d65e4c4f05-#/card) resource with _primary\_account\_numbers_.  
  
The field returns the same string for _primary\_account\_numbers_ and the same field + canceled cards for _primary\_account\_numbers\_virtual_.

### October 8, 2019

We have removed creating push notifications through updating _notification\_filters_ in the User and MonetaryAccount objects.

Instead, we introduced separate endpoints for the callbacks and notifications.

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

We have removed the following share-invite-bank endpoints:

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



