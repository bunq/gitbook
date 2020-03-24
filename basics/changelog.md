# Changelog

{% hint style="success" %}
Stay up-to-date with the bunq API updates! [Subscribe to our API newsletter](https://bunq.us8.list-manage.com/subscribe?u=c00d0d6daea4e1cf7c863d52e&id=b08680cdc7)!
{% endhint %}

## Upcoming changes

### April 28, 2020

{% hint style="warning" %}
1. Requests with full request signatures will stop being validated on April 28, 2020. Please switch to [signing the body solely](https://beta.doc.bunq.com/basics/authentication/signing) by that date.
2. We are switching to [only signing the response body](https://beta.doc.bunq.com/basics/authentication/signing#response-verifying-example) on April 28, 2020. 
{% endhint %}

### April 8, 2020

Due to internal backend changes, all active [device-server](https://doc.bunq.com/#/device-server/Create_DeviceServer) installations created before April 9, 2019, will stop being validated on April 8, 2020 \(previously announced date: January 15, 2019\). To communicate with the bunq API again, [create a new API context](https://beta.doc.bunq.com/basics/authentication#creating-api-context).

## Released

### January 28, 2020 \(bunq Update 13 edition\)

#### Changes

1. Request signing has become mandatory only for creating a session and creating a payment. The use of signing for other API requests is optional. 
2. We have introduced [request body signing](https://beta.doc.bunq.com/basics/authentication/signing). URL and headers do not need to be signed. Body signing will completely replace entire request signing on April 28, 2020.
3. The following headers are now optional:
   1. `X-Bunq-Geolocation`;
   2. `X-Bunq-Language` \(`en_US` is the default language setting for responses and error descriptions\);
   3. `X-Bunq-Region` \(`en_US` is the default region for currency formatting\);
   4. `X-Bunq-Request-Id`.
4. We have extended the [OAuth scopes ](https://beta.doc.bunq.com/basics/oauth#what-can-my-apps-do-with-oauth)with the following permissions:
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



