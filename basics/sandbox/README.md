---
description: 'The sandbox base URL is https://public-api.sandbox.bunq.com/v1/'
---

# Sandbox

{% hint style="info" %}
We do not use real money and do not allow external transactions in the sandbox environment. 
{% endhint %}

## Sandbox user accounts

You need to create a sandbox user to test the bunq API. The easiest way to do it is by using [our developer portal](http://developer.bunq.com/):

1. Log in using your bunq account or [create a free developer account ](https://developer.bunq.com/portal/signup)with sandbox-only access.
2. Go to _Sandbox Users_.
3. Generate up to 5 users.
4. Use the sandbox API key to create an [API context](https://beta.doc.bunq.com/basics/authentication#creating-api-context) and/or use the user credentials to log in to the [sandbox bunq app](https://beta.doc.bunq.com/basics/sandbox/android-emulator).

### Alternative ways to generate sandbox API keys

There are 3 other ways you can generate a bunq sandbox API key:

1. [connect to Tinker](https://lexy.gitbook.io/bunq/quickstart/tinker) _\(it will also return login credentials for the sandbox app\)_;
2. create it in[ the sandbox app](https://beta.doc.bunq.com/basics/sandbox/android-emulator) _\(you need to be logged in as a sandbox user\)_;
3. call the sandbox user endpoints directly, [using our Postman collection](https://github.com/bunq/postman), or by running a cURL command \(change `sandbox-user-person` to `sandbox-user-company` to generate a business user\):

`curl https://public-api.sandbox.bunq.com/v1/sandbox-user-person -X POST --header "Content-Type: application/json" --header "Cache-Control: none" --header "User-Agent: curl-request" --header "X-Bunq-Client-Request-Id: $(date)randomId" --header "X-Bunq-Language: nl_NL" --header "X-Bunq-Region: nl_NL" --header "X-Bunq-Geolocation: 0 0 0 0 000"`

{% hint style="info" %}
Once you have a sandbox API key, create more sandbox users to use as test customer accounts, and start playing with the API. 

The sandbox base URL is `https://public-api.sandbox.bunq.com/v1/`.
{% endhint %}

## Sandbox money

Without money, it's not always sunny in the sandbox world. Fortunately, getting money on the bunq sandbox is easy. All you need to do is ask Sugar Daddy for it.

Send a [**POST v1/request-inquiry**](https://doc.bunq.com/#/request-inquiry/Create_RequestInquiry_for_User_MonetaryAccount) request passing _sugardaddy@bunq.com_  in the `counterparty_alias` field. Specify the `type` for the alias and set the `allow_bunqme` field. Request up to €500 at a time.

```text
{
    "amount_inquired": {
        "value": "100",
        "currency": "EUR"
    },
    "counterparty_alias": {
        "type": "EMAIL",
        "value": "sugardaddy@bunq.com",
        "name": "Sugar Daddy"
    },
    "description": "You're the best!",
    "allow_bunqme": false
}
```

