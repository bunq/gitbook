# Headers

HTTP headers allow your application and bunq to pass additional information about with the request or response. 

Though headers are already implemented in our [SDKs](https://github.com/bunq), we recommend that you follow these instructions to make sure you set appropriate headers when calling the bunq API directly.

## Request Headers

### Mandatory request headers

#### **Cache-Control**

`Cache-Control: no-cache`

The standard HTTP Cache-Control header is ****required for all requests.

#### **User-Agent**

`User-Agent: bunq-TestServer/1.00 sandbox/0.17b3`

The User-Agent header field must contain information about the user agent originating the request. There are no restrictions on the value of this header.

#### **X-Bunq-Language**

`X-Bunq-Language: en_US`

The X-Bunq-Language header must carry the preferred language indicator. The value of this header must follow this format: _an ISO 639-1 language code_ plus _a ISO 3166-1 alpha-2 country code_ separated by an underscore.

{% hint style="info" %}
We currently only support _en\_US_ and _nl\_NL_. Any other language will default to _en\_US_.
{% endhint %}

#### **X-Bunq-Region**

`X-Bunq-Region: en_US`

The X-Bunq-Region header must contain the region \(country\) of the client device. The value of this header  must follow this format: _an ISO 639-1 language code_ plus _a ISO 3166-1 alpha-2 country code_ separated by an underscore.

#### **X-Bunq-Client-Request-Id**

`X-Bunq-Client-Request-Id: a4f0de`

~~This header must specify an ID with each request that is unique for the logged in user.~~ There are no restrictions for the format of this ID. However, the server will respond with an error when the same ID is used again on the same DeviceServer.

#### **X-Bunq-Geolocation**

`X-Bunq-Geolocation: 4.89 53.2 12 100 NL`

`X-Bunq-Geolocation: 0 0 0 0 000`

This header must specify the geolocation of the device. The format of this value is _longitude latitude altitude radius country_. The country is expected to take the form of an _ISO 3166-1 alpha-2 country code_. 

{% hint style="info" %}
If no geolocation is available or known, the header must contain zero values.
{% endhint %}

#### **X-Bunq-Client-Signature**

```text
X-Bunq-Client-Signature: 
XLOwEdyjF1d+tT2w7a7Epv4Yj7w74KncvVfq9mDJVvFRlsUaMLR2q4ISgT+5mkwQsSygRRbooxBqydw7IkqpuJay9g8eOngsFyIxSgf2vXGAQatLm47tLoUFGSQsRiYoKiTKkgBwA+/3dIpbDWd+Z7LEYVbHaHRKkEY9TJ22PpDlVgLLVaf2KGRiZ+9/+0OUsiiF1Fkd9aukv0iWT6N2n1P0qxpjW0aw8mC1nBSJuuk5yKtDCyQpqNyDQSOpQ8V56LNWM4Px5l6SQMzT8r6zk5DvrMAB9DlcRdUDcp/U9cg9kACXIgfquef3s7R8uyOWfKLSNBQpdVIpzljwNKI1Q
```

The signature header is included in all API requests except `POST /v1/installation`. See the [signing page](https://lexy.gitbook.io/bunq/basics/authentication/signing) for details on how to create this signature.

{% page-ref page="authentication/signing.md" %}

#### **X-Bunq-Client-Authentication**

`X-Bunq-Client-Authentication: 622749ac8b00c81719ad0c7d822d3552e8ff153e3447eabed1a6713993749440`

The authentication _Token_ is used to identify the sender of the API call. It is required for all API calls except `POST /v1/installation`. 

{% hint style="info" %}
* Pass the **installation** _**Token**_ ****you get in the response to the `POST /installation` call in the `/device-server` and `/session-server` calls.
* Pass the **session** _**Token**_ you get in the response to the `POST /session-server` call in all the other calls.
{% endhint %}

### Attachment headers

#### **Content-Type**

`Content-Type: image/jpeg`

Use this header when uploading an attachment to pass its MIME type. We support the following content types: 

* _image/png;_
* _image/jpeg;_
* _image/gif._

#### **X-Bunq-Attachment-Description**

Use this header to provide a description of an attachment.

## Response Headers

### All Responses

#### **X-Bunq-Client-Request-Id**

`X-Bunq-Client-Request-Id: a4f0de`

The header contains the same `id` that was provided in the `X-Bunq-Client-Request-Id` header of the request. It is included in the response \(and request\) signature so it can be used to ensure this is the response to _the_ request.

#### **X-Bunq-Client-Response-Id**

`X-Bunq-Client-Response-Id: 76cc7772-4b23-420a-9586-8721dcdde174`

The header carries a unique `id`  of the response formatted as a `UUID`. You can use it to add extra protection against replay attacks.

#### **X-Bunq-Server-Signature**

```text
X-Bunq-Server-Signature: 
XBBwfDaOZJapvcBpAIBT1UOmczKqJXLSpX9ZWHsqXwrf1p+H+eON+TktYksAbmkSkI4gQghw1AUQSJh5i2c4+CTuKdZ4YuFT0suYG4sltiKnmtwODOFtu1IBGuE5XcfGEDDSFC+zqxypMi9gmTqjl1KI3WP2gnySRD6PBJCXfDxJnXwjRkk4kpG8Ng9nyxJiFG9vcHNrtRBj9ZXNdUAjxXZZFmtdhmJGDahGn2bIBWsCEudW3rBefycL1DlpJZw6yRLoDltxeBo7MjgROBpIeElh5qAz9vxUFLqIQC7EDONBGbSBjaXS0wWrq9s2MGuOi9kJxL2LQm/Olj2g==
```

The header contains the signature of the bunq server for this response. See the [signing page](https://lexy.gitbook.io/bunq/basics/authentication/signing) for details on how to verify this signature.

### Warning header

#### **X-Bunq-Warning**

`X-Bunq-Warning: "You have a negative balance. Please check the app for more details."`

We use it to warn you something is impacting your bunq account and/or API access.  


