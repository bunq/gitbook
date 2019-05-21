# Tab payment

{% hint style="info" %}
A **tab payment** is a payment made via a browser or POS tab. 
{% endhint %}

This tutorial will help you create a tab that can be paid once by a single user \(a so-called TagUsageSingle\). It explains two ways to make the Tab visible to your customers:

* QR code from the CashRegister
* QR code from the Tab.

### Before you start

* [ ] Open a session 
* [ ] Pass the session _Token_ in the `X-Bunq-Client-Authentication` header in every following request of this session.

## Call Sequence

### 1. POST /attachment-public

Start by creating an attachment that will be used for the avatar for the cash register.

#### **Header**

* [ ] Make sure you set the `Content-Type` header to match the MIME type of the image.
* [ ] Pass a description of the image via the `X-Bunq-Attachment-Description` header.

#### **Body**

The payload of this request is the binary representation of the image file. Do not use any JSON formatting.

#### **Response**

* [ ] Save the `uuid` of the posted attachment. You'll need it to create the avatar in the next step.

### 2. POST /avatar

* [ ] Make an avatar using the public attachment you've just created.

#### **Body**

The payload of this request is the `uuid` of the attachment public.

#### **Response**

* [ ] Receive the `UUID` of the avatar created using the Attachment object.
* [ ] Save the `UUID`. You will use it as the avatar for the cash register you're about to create.

### 3. GET /monetary-account

* [ ] List all your monetary accounts. 
* [ ] Choose the one you want your cash register to be connected to and save its `id` . Each paid tab for the cash register will transfer the money to this account.

### 4a. POST /cash-register

* [ ] Create a cash register using the `id` of the monetary account you want to connect the cash register to in the URL of the request.

#### **Body**

* Provide the `uuid` of the avatar you created for this cash register. 
* Make sure to provide a unique name for your cash register. 
* Change the status of the cash register to `PENDING_APPROVAL`.

#### **Response**

The response contains the `id` of the cash register you created. Save this `id`. You will need it to create subsequent tabs and tab items.

### 4b. Wait for approval

* **Production:** a bunq admin will review and approve your cash register. 
* **Sandbox:** your cash register will be automatically approved.

### 5. POST /tab-usage-single

* [ ] Create a new tab that is connected to your cash register using the `id` of the cash register in the request URL request.

#### **Body**

* Give the tab a name in `merchant_reference`. 
* Create the tab with the `OPEN` status and give the tab a starting amount. You can update this amount later.

#### **Response**

The response contains the `uuid` of the tab you created.

### 6. POST /tab-item \(optional\)

You can add items to a tab. This will display the products or services the customer is going to pay for. Adding items to a tab is does not change the total amount of the tab itself. 

{% hint style="info" %}
Make sure the sum of the item prices equals the `total_amount` of the tab when you change its status to `WAITING_FOR_PAYMENT`.
{% endhint %}

### 7. PUT /tab-usage-single

Once the tab is ready for a customer to pay for the order, update the status of the tab to `WAITING_FOR_PAYMENT`. This will make the tab visible to your costumers.

#### **Visibility**

To decide how you are going to make your tab visible, pass a visibility object in the payload.

Set `cash_register_qr_code` _true_ to connect the tab to the QR code from the cash register. If this cash register does not have a QR code yet, it is created automatically. 

{% hint style="info" %}
Only one Tab can be connected to the QR code of the cash register at a time.
{% endhint %}

Set `tab_qr_code` _true_ to create a QR code specifically for the tab. The QR code can not be linked to anything else.

