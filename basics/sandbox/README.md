# Sandbox

{% hint style="info" %}
We do not use real money and do not allow external transactions in the sandbox environment. 
{% endhint %}

## Sandbox API keys

There are 4 ways to generate a bunq sandbox API key:

1. create it from the [sandbox app](https://lexy.gitbook.io/bunq/basics/sandbox/android-emulator)
2. [connect to Tinker](https://lexy.gitbook.io/bunq/quickstart/tinker) _\(it will auto connect you to the sandbox\)_
3. [use Postman](https://github.com/bunq/postman)
4. run the cURL command

`curl https://public-api.sandbox.bunq.com/v1/sandbox-user -X POST --header "Content-Type: application/json" --header "Cache-Control: none" --header "User-Agent: curl-request" --header "X-Bunq-Client-Request-Id: $(date)randomId" --header "X-Bunq-Language: nl_NL" --header "X-Bunq-Region: nl_NL" --header "X-Bunq-Geolocation: 0 0 0 0 000"`

Once you have your API key, create more sandbox users to use as test customer accounts users, and start playing with the API. The sandbox base url is [`https://public-api.sandbox.bunq.com/v1/`](https://public-api.sandbox.bunq.com/v1/).

## Sandbox money

Without money, it's not always sunny in the sandbox world. Fortunately, getting money on the bunq sandbox is easy. All you need to do is ask Sugar Daddy for it.

Send a [**POST v1/request-inquiry**](https://doc.bunq.com/#/request-inquiry/Create_RequestInquiry_for_User_MonetaryAccount) request passing _sugardaddy@bunq.com_  in the `counterparty_alias` field. Specify the `type` for the alias and set the `allow_bunqme` field.

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
    "description": "Gimme some",
    "allow_bunqme": false
}
```

