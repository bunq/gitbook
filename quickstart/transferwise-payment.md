---
description: You want to send an international payment in currency other than euro
---

# TransferWise payment

You can send international payments in any currency using the bunq API. Though bunq uses TransferWise for payments outside the SEPA zone, you don’t need to base your flow on both APIs. Just follow the steps below to create a non-Euro payment the bunq API.

{% hint style="info" %}
bunq relies on TransferWise for payments in currencies other than EUR, so you need to create a TransferWise account linked to a bunq account to be able to create international transfers. You can do it either from the bunq app or using our API.
{% endhint %}

### Before you start

* [ ] Make sure that you have opened a session
* [ ] Make sure you pass the session _Token_ in the `X-Bunq-Client-Authentication` header in all the following requests of the session.

## Get the up-to-date exchange rate \(optional\)

You might want to check the latest currency exchange rate before making a transfer. Here’s how you can do it using the bunq API:

1. Check the list of supported currencies via `GET /user/{userID}/transferwise-currency`. Copy the needed currency code.
2. Create a temporary quote for the currency of your choice via `POST /user/{userID}/transferwise-quote-temporary`. Save its ID.
3. Read the temporary quote via `GET /user/{userID}/transferwise-quote-temporary/{transferwise-quote-temporaryID}`.

{% hint style="info" %}
A quote is the exchange rate at the exact timestamp. Temporary quotes carry solely informative value and cannot be used for creating a transfer.
{% endhint %}

## Create a TransferWise account

You need a TransferWise account linked to your bunq account to make TransferWise payments via the bunq API. Create one via `POST /user/{userID}/transferwise-user`, and save its ID. 

{% hint style="warning" %}
You cannot use an existing TransferWise account.
{% endhint %}

## Create a TransferWise account

1. Create a quote via `POST /user/{userID}/transferwise-quote` and save its ID. 
2. Get the exchange rate by reading the quote via `GET /user/{userID}/transferwise-quote/(transferwise-quoteID)`.

{% hint style="info" %}
Use `amount_target` to indicate the sum the recipient must get. `amount_source`, on the other hand, will indicate the sum you want to send, but it will not necessarily be the final sum the recipient gets.
{% endhint %}

{% hint style="info" %}
Quotes are valid for 30 minutes so if you do not manage to create a transfer within this time, you will need to create another quote.
{% endhint %}

## Create a recipient

If you have sent money via the TransferWise account linked to your bunq account, you can reuse the recipients. You can list their IDs via `GET /user/{userID}/transferwise-quote/{transferwise-quoteID}/transferwise-recipient`.

To create a new, previously unused recipient, follow these steps:

1. Retrieve the fields required for creating the recipient as the requirements vary for the type of recipient in each country. Iterate sending the following request pair till there are no more required fields:
   * `GET /user/{userID}/transferwise-quote/{transferwise-quoteID}/transferwise-recipient-requirement`
   * `POST /user/{userID}/transferwise-quote/{transferwise-quoteID}/transferwise-recipient-requirement`
2. Create a recipient account using the final request body from the previous step with `POST /user/{userID}/transferwise-quote/{transferwise-quoteID}/transferwise-recipient-requirement`

## Create a transfer

Finally, having both the quote ID and the recipient ID, you can create a transfer. 🎉

1. Check if there are any additional transfer requirements via `POST /user/{userID}/transferwise-quote/{transferwise-quoteID}/transferwise-transfer-requirement`
2. Create a transfer via `POST /user/{userID}/monetary-account/{monetary-accountID}/transferwise-quote/{transferwise-quoteID}/transferwise-transfer`. You need to specify the ID of the monetary account from which you want the payment to be made.

