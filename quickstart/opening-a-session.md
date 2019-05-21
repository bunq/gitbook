# Opening a Session

So, you want to start using the bunq API, awesome! To do this, you have to open a session in which you will be making those calls.

## Getting an API key

The only way to **get a production API key** is to generate it from within the bunq app \(_Profile → Security & Settings → Developers → API keys\)_. As for sandbox API keys, there are [4 ways you can create them](https://lexy.gitbook.io/bunq/basics/sandbox#sandbox-api-keys).

{% hint style="info" %}
* Production API keys are only usable on the production and sandbox API keys are only usable on the sandbox. 
* Sandbox keys contain a `sandbox_` prefix while production keys do not have any noticeable prefixes.
{% endhint %}

## Call Sequence

Before you can start a session, you need to register your API key, device and IP address\(es\). You can do it following the sequence of calls described below.

### 1. POST /installation

Each [call needs to be signed ](https://lexy.gitbook.io/bunq/basics/authentication/signing)with your own private key. An Installation is used to tell the server about the public key of your key pair. The server uses this key to verify you are sending the subsequent calls.

Start by generating a[ 2048-bit RSA key pair](https://en.wikipedia.org/wiki/RSA_%28cryptosystem%29). You can find examples in the source code of [our SDKs](https://github.com/bunq).

#### **Headers**

On the [headers page](https://lexy.gitbook.io/bunq/basics/headers), you can find out about the mandatory headers. Make sure to set an `Authorization` header if you are working in the sandbox environment. 

{% hint style="info" %}
You do not need to use the `X-Bunq-Client-Authentication` or `X-Bunq-Client-Signature`headers in the `POST /installation`call.
{% endhint %}

#### **Body**

POST your public key to the Installation endpoint. Use `\n` for newlines in your public key.

#### **Response**

Save the installation _Token_ and _server\_public\_key_ returned in the response. Use the _Token_ in the `Authentication` header to register a `DeviceServer` and to start a `SessionServer`. Use s_erver\_public\_key_ to verify the responses you will receive from the bunq API.

### 2. POST /device-server

All the following calls made to the server must be sent from a registered device. `POST /device-server`registers your current device and the IP address\(es\) it uses to connect to the bunq API.

#### **Headers**

Use the _Token_ you received in the `X-Bunq-Client-Authentication`header of the response to `POST /installation`. 

* [ ] Make sure you sign your call, passing the [call signature](https://lexy.gitbook.io/bunq/basics/authentication/signing) in the`X-Bunq-Client-Signature` header.

#### **Body**

Use your API key for the _secret_ parameter. If you want to create and use another API key assign it to one or multiple IP addresses using `POST /device-server` within 4 hours before it becomes invalid. As soon as you start using your API key, it will remain valid until the next sandbox reset.

### 3. POST /session-server

To make any calls besides `/installation` and `/device-server`, you need to open a session.

#### **Headers**

Use the _Token_ you received in the `X-Bunq-Client-Authentication`header of the response to `POST /installation` . 

* [ ] Make sure you sign your call, passing the call signature in `X-Bunq-Client-Signature`header.

#### **Body**

Use your API key for the _secret_ parameter.

#### **Response**

Use the _Token_ received in the response to `POST /session-server` to authenticate your calls in this session. Pass this session _Token_ in the `X-Bunq-Client-Authentication` header with every call you make in this session.

