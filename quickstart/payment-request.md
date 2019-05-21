---
description: You want to offer bunq payments on a website or in an application.
---

# Payment request

### Scenario you want to achieve

0. Both the consumer and the merchant have a bunq account.

1. The consumer wants to pay with bunq. They enter their alias in the bunq payment field at checkout and press the enter button. 
2. The merchant sends a payment request to the consumer. 
3. The consumer receives a push notification, opens the bunq app and accepts to the payment request in the bunq app.
4. The merchant gets an immediate confirmation of the payment. 

{% hint style="info" %}
Please be aware that if you will gain access to account information of other bunq users or initiate a payment for them, you require a PSD2 permit.
{% endhint %}

### Before you start

* [ ] Make sure that you have opened a session
* [ ] Make sure you pass the session _Token_ in the `X-Bunq-Client-Authentication` header in all the following requests of the session.

## Call Sequence

{% hint style="info" %}
The perfect time to open a session on the bunq server is when the consumer is at checkout and selects the bunq payment method.
{% endhint %}

### 1. GET /monetary-account

List all your monetary accounts and choose the one you want to use to receive the payments to. Save its `id` and later use it in the payment request.

### 2. POST /attachment \(optional\)

Optionally, you can attach an image to the request for payment.

#### **Headers**

* [ ] Make sure you set the `Content-Type` header to match the MIME type of the image. 
* [ ] Pass a description of the image via the `X-Bunq-Attachment-Description` header.

#### **Body**

The payload of this request is the binary representation of the image file. Do not use any JSON formatting.

#### **Response**

Save the `id` of the posted attachment. You’ll need it to attach the attachment to the payment request. payment.

### 3. POST /request-inquiry

Request a payment by sending a `POST /request-inquiry` request. 

{% hint style="info" %}
A **request inquiry** is a request for payment that your customer can respond to by either accepting or rejecting it.
{% endhint %}

#### **Body**

* [ ] Pass the customer’s email address, phone number or IBAN in the `counterparty_alias` field. 
* [ ] Set the correct `type` for the alias \(e.g. EMAIL\). Note that if you choose to pass the IBAN, the name of the `counterparty_alias` is required. 
* [ ] Provide the `id` of the created attachment **\(optional\)**.

#### **Response**

* [ ] Receive the `id` of the created request inquiry in the response
* [ ] Save this `id`. 
* [ ] Use it to check if the customer has responded to the request yet.

### 4. GET /request-inquiry

After you send the payment request and get its `id`, you can poll it to see if its status has changed.

#### **Response**

* If the `status` is `ACCEPTED`, the customer has accepted the request and paid the money. You will have received the money on the connected monetary account. 
* If the `status` is `REJECTED`, the customer did not accept the request.

