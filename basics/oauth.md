# OAuth

{% hint style="info" %}
[OAuth 2.0](https://www.oauth.com/oauth2-servers/getting-ready/) is a protocol that will let your app connect to bunq users in a safe and easy way. Please be aware that if you will gain access to account information of other bunq users or initiate a payment for them, you require a PSD2 permit.
{% endhint %}

## What can my apps do with OAuth?

The permissions OAuth allows are the following:

* read _Monetary Accounts;_
* read _Payments_ & _Transactions;_
* create _Payments_, however you can only transfer money between _Monetary Accounts_ of the same user;
* create _Draft-Payments;_
* assign a Monetary account to a _Card;_
* read _Request-Inquiries_ and _Request-Responses_.

## Get started with OAuth

Follow these steps to get started with OAuth:

1. Register an OAuth Client in the bunq app. You can find the OAuth menu by going _Profile → Security & Settings → Developers → OAuth._
2. Add one or more redirect URLs.
3. Get your _Client ID_ and _Client Secret_ from the bunq app.
4. Redirect your users to the OAuth authorization URL as described [here](https://doc.bunq.com/###authorization-request).
5. If the user accepts the authorization request, they will be redirected to the previously specified `redirect_uri` with an authorization _Code_ parameter.
6. Use the [token endpoint](https://lexy.gitbook.io/bunq/basics/oauth#token-exchange) to exchange the authorization _Code_ for an _Access Token_.
7. Use the _Access Token_ as a normal API Key. Open a session or use our SDKs to get started.

## Authorization Request

Your web or mobile app must redirect users `https://oauth.bunq.com/auth` using the following parameters:

* `response_type` - bunq supports the authorization code grant. Provide `code` as a parameter **\(required\)**;
* `client_id` - your _Client ID_ that you can get from the bunq app **\(required\)**;
* `redirect_uri` - the URL you wish the user to be redirected to after the authorization is complete **\(required\)**;
* `state` - a unique string to be passed back upon completion **\(optional\).**

#### **Authorization request example:**

```text
https://oauth.bunq.com/auth?response_type=code
&client_id=1cc540b6e7a4fa3a862620d0751771500ed453b0bef89cd60e36b7db6260f813
&redirect_uri=https://www.bunq.com
&state=594f5548-6dfb-4b02-8620-08e03a9469e6
```

#### **Authorization request response example:**

```text
https://www.bunq.com/?code=7d272be434a75933f40c13d56aef6c31496005b653074f7d6ac57029d9995d30
&state=594f5548-6dfb-4b02-8620-08e03a9469e6
```

## Token Exchange

If the authorization request is accepted by the user, you get the authorization _Code._ Exchange it for an _Access Token_.

Make a POST call to `https://api.oauth.bunq.com/v1/token` Pass the following parameters as GET variables:

* `grant_type` - the grant type used, use `authorization_code` for now **\(required\)**
* `code` - the authorization _Code_ you received after the authorization request was accepted **\(required\)**
* `redirect_uri` - the same redirect URL you used with the authorization request **\(required\)**
* `client_id` - your _Client ID_ **\(required\)**
* `client_secret` - your _Client Secret_ **\(required\)**

**Token request example:**

```text
https://api.oauth.bunq.com/v1/token?grant_type=authorization_code
&code=7d272be434a75933f40c13d56aef6c31496005b653074f7d6ac57029d9995d30
&redirect_uri=https://www.bunq.com/
&client_id=1cc540b6e7a4fa3a862620d0751771500ed453b0bef89cd60e36b7db6260f813
&client_secret=184f969765f6f74f53bf563ae3e9f891aec9179157601d25221d57f2f1151fd5
```

{% hint style="info" %}
The request only contains URL parameters.
{% endhint %}

**Example of a successful response:**

```text
{
    "access_token": "8baec0ac1aafca3345d5b811042feecfe0272514c5d09a69b5fbc84cb1c06029",
    "token_type": "bearer",
    "state": "594f5548-6dfb-4b02-8620-08e03a9469e6"
}
```

**Example of an error response:**

```text
{
    "error": "invalid_grant",
    "error_description": "The authorization code is invalid or expired."
}
```

{% hint style="info" %}
#### What's next?

The `access_token` you've received can be used as a normal API key. Use it to [create an authorized session](https://lexy.gitbook.io/bunq/basics/authentication) with the user account. 
{% endhint %}

## Using the Connect button

Ready to connect to bunq users to your application? Do it with a **Connect to bunq** button. Feel free to use our style guide and prebuilt design assets.

* [Style guide](https://bunq.com/info/oauth-styleguide)
* [Connect button assets](https://bunq.com/info/oauth-connect-buttons)

