---
description: >-
  You want to export receipts and invoices attached to payments to your
  application.
---

# Quickstart: Downloading attachments

## The scenario you want to achieve

1. The bunq user has accepted the authorization request and your application can read the bunq user’s account information.
2. Your application imports all the transactions and attachments.
3. The bunq user sees the transactions matched with the receipts and invoices in your application.

## Before you start

* [x] Make sure that you have opened a session
* [x] Make sure you pass the session Token in the X-Bunq-Client-Authentication header in all the following requests of the session.

## Call sequence

{% api-method method="get" host="https://public-api.sandbox.bunq.com/v1" path="/user/{userID}/monetary-account/{monetary-accountID}/payment" %}
{% api-method-summary %}
List the payments of the user 
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="userID" type="integer" required=true %}
The ID of the user.
{% endapi-method-parameter %}

{% api-method-parameter name="monetary-accountID \*" type="integer" required=true %}
The ID of the monetary account.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="User-Agent" type="string" required=true %}
Information about the user agent originating the request. There are no restrictions on the value of this header.
{% endapi-method-parameter %}

{% api-method-parameter name="X-Bunq-Client-Authentication \*" type="string" required=true %}
The token you get in the response of the session-server call.
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
[
  {
    "id": 0,
    "created": "string",
    "updated": "string",
    "monetary_account_id": 0,
    "amount": {
      "value": "string",
      "currency": "string"
    },
    "alias": {
      "iban": "string",
      "display_name": "string",
      "avatar": {
        "uuid": "string",
        "anchor_uuid": "string",
        "image": [
          {
            "attachment_public_uuid": "string",
            "content_type": "string",
            "height": 0,
            "width": 0
          }
        ]
      },
      "label_user": {
        "uuid": "string",
        "display_name": "string",
        "country": "string",
        "avatar": {
          "uuid": "string",
          "anchor_uuid": "string",
          "image": [
            {
              "attachment_public_uuid": "string",
              "content_type": "string",
              "height": 0,
              "width": 0
            }
          ]
        },
        "public_nick_name": "string"
      },
      "country": "string",
      "bunq_me": {
        "type": "string",
        "value": "string",
        "name": "string"
      },
      "is_light": true,
      "swift_bic": "string",
      "swift_account_number": "string",
      "transferwise_account_number": "string",
      "transferwise_bank_code": "string",
      "merchant_category_code": "string"
    },
    "counterparty_alias": {
      "iban": "string",
      "display_name": "string",
      "avatar": {
        "uuid": "string",
        "anchor_uuid": "string",
        "image": [
          {
            "attachment_public_uuid": "string",
            "content_type": "string",
            "height": 0,
            "width": 0
          }
        ]
      },
      "label_user": {
        "uuid": "string",
        "display_name": "string",
        "country": "string",
        "avatar": {
          "uuid": "string",
          "anchor_uuid": "string",
          "image": [
            {
              "attachment_public_uuid": "string",
              "content_type": "string",
              "height": 0,
              "width": 0
            }
          ]
        },
        "public_nick_name": "string"
      },
      "country": "string",
      "bunq_me": {
        "type": "string",
        "value": "string",
        "name": "string"
      },
      "is_light": true,
      "swift_bic": "string",
      "swift_account_number": "string",
      "transferwise_account_number": "string",
      "transferwise_bank_code": "string",
      "merchant_category_code": "string"
    },
    "description": "string",
    "type": "string",
    "sub_type": "string",
    "bunqto_status": "string",
    "bunqto_sub_status": "string",
    "bunqto_share_url": "string",
    "bunqto_expiry": "string",
    "bunqto_time_responded": "string",
    "attachment": [
      {
        "id": 0,
        "monetary_account_id": 0
      }
    ],
    "merchant_reference": "string",
    "batch_id": 0,
    "scheduled_id": 0,
    "address_shipping": {
      "street": "string",
      "house_number": "string",
      "po_box": "string",
      "postal_code": "string",
      "city": "string",
      "country": "string",
      "extra": "string",
      "mailbox_name": "string",
      "province": "string"
    },
    "address_billing": {
      "street": "string",
      "house_number": "string",
      "po_box": "string",
      "postal_code": "string",
      "city": "string",
      "country": "string",
      "extra": "string",
      "mailbox_name": "string",
      "province": "string"
    },
    "geolocation": {
      "latitude": 0,
      "longitude": 0,
      "altitude": 0,
      "radius": 0
    },
    "request_reference_split_the_bill": [
      {
        "type": "string",
        "id": 0
      }
    ],
    "balance_after_mutation": {
      "value": "string",
      "currency": "string"
    }
  }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://public-api.sandbox.bunq.com/v1" path="/user/{userID}/monetary-account/{monetary-accountID}/payment/{paymentID}/note-attachment" %}
{% api-method-summary %}
Check if the payments have attachments
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="userID" type="integer" required=true %}
The ID of the user.
{% endapi-method-parameter %}

{% api-method-parameter name="monetary-accountID \*" type="integer" required=true %}
The ID of the monetary account.
{% endapi-method-parameter %}

{% api-method-parameter name="paymentID" type="integer" required=true %}
The ID of the payment
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="User-Agent" type="string" required=true %}
Information about the user agent originating the request. There are no restrictions on the value of this header.
{% endapi-method-parameter %}

{% api-method-parameter name="X-Bunq-Client-Authentication \*" type="string" required=true %}
The token you get in the response of the session-server call.
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
[
  {
    "id": 0,
    "created": "string",
    "updated": "string",
    "label_user_creator": {
      "uuid": "string",
      "display_name": "string",
      "country": "string",
      "avatar": {
        "uuid": "string",
        "anchor_uuid": "string",
        "image": [
          {
            "attachment_public_uuid": "string",
            "content_type": "string",
            "height": 0,
            "width": 0
          }
        ]
      },
      "public_nick_name": "string"
    },
    "description": "string",
    "attachment": [
      {
        "id": 0,
        "monetary_account_id": 0
      }
    ]
  }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
Save the attachment IDs.
{% endhint %}

{% api-method method="get" host="https://public-api.sandbox.bunq.com/v1" path="/user/{userID}/attachment/{attachmentID}/content" %}
{% api-method-summary %}
Export the raw content of the attachments
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="userID" type="integer" required=true %}
The ID of the user.
{% endapi-method-parameter %}

{% api-method-parameter name="attachmentID" type="integer" required=true %}
The ID of the attachment.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="User-Agent" type="string" required=true %}
Information about the user agent originating the request. There are no restrictions on the value of this header.
{% endapi-method-parameter %}

{% api-method-parameter name="X-Bunq-Client-Authentication \*" type="string" required=true %}
The token you get in the response of the session-server call.
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
[
  {}
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
You can use [callbacks](https://beta.doc.bunq.com/basics/callbacks) to make sure you don’t miss anything happening on the bunq account.
{% endhint %}

