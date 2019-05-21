# Authentication

Here is what you need to know about how the bunq authentication works:

* All requests must use HTTPS. HTTP calls will fail. 
* We use extra signing on top of HTTPS encryption that you must implement yourself if you are not using the SDKs.

{% hint style="info" %}
We use [asymmetric cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) for signing requests and encryption.

The client _\(you\)_ and the server _\(bunq\)_ must have a pair of keys: a private key and a public key. You need to pre-generate your own pair of 2048-bit [RSA keys](https://en.wikipedia.org/wiki/RSA_%28cryptosystem%29) in the [PEM format](https://en.wikipedia.org/wiki/Privacy-Enhanced_Mail).

The parties _\(you and bunq\)_ exchange their public keys in the first step of the [API context creation flow](https://lexy.gitbook.io/bunq/basics/authentication#creating-api-context). All the following requests must be signed by both your application and the server. Pass your signature in the _X-Bunq-Client-Signature_ header, and the server will return its signature in the _X-Bunq-Server-Signature_ header.
{% endhint %}

* You should use SSL Certificate Pinning and Hostname Verification to ensure your connection with bunq is secure.
* The auto logout time that you set in the app applies to all your sessions including the API ones. If a request is made 30 minutes before a session expires, the session will automatically be extended.

## Creating API Context 

Before you can start calling the bunq API, you must do the following:

* register your API key and IP address\(es\);
* register your device;
* create a session. 

We call this intro "creating an API context". There are a couple of ways to carry out the sequence of steps. Let's dwell on each of them.

### Using our SDKs

1. Go to our [GitHub](https://github.com/bunq) page.
2. Choose the SDK in your language of choice.
3. Find and use the part dedicated to creating an API context.

{% hint style="info" %}
[Run Tinker](https://lexy.gitbook.io/bunq/quickstart/tinker) to see a sample project using bunq SDK in action.
{% endhint %}

### Using our API directly

1. Create an _Installation_ by calling `POST v1/installation` and passing your pre-generated public key. You will receive an installation _Token._ Use it when making the two following API calls.
2. Create a _DeviceServer_ via `POST v1/device-server`. Provide a description and a secret \(API key in this case\).
3. Create a _SessionServer_ by executing `POST v1/session-server`. You will receive an authentication _Token._ Use it in the API requests in this active session.​

{% hint style="info" %}
[Import our Postman collection](https://github.com/bunq/postman) to see our pre-setup API context creation calls. It will automatically generate and pre-fill everything in the API calls that create context so you can inspect the process.
{% endhint %}

### Locking IP addresses that can use the API

When you create a context in `POST v1/device-server`, it ties the API key to your current IP address so it will not be useable from other IPs.

If you have several IPs \(e. g. several servers\), you can set a list of allowed IPs in `device-server` request as an array. You must include your current IP in this array as to not lock yourself out.

As a last resort, you can also [set a wildcard as an IP](https://together.bunq.com/d/1997-the-new-wildcard-api-key). In that case there will be no IP check for that API key. Please only do that if you have no other option.

### Changing allowed IP addresses after initializing API key

It is possible to add trusted IP addresses using the [IP endpoint](https://doc.bunq.com/#/ip/Create_Ip_for_User_CredentialPasswordIp). Obviously you need to make that request from an IP address that was allowed previously.

You will not be able to switch from concrete IPs to a wildcard IP after you've created a device-server. You can either request a new API key from the user or ask them to use _Allow all IP Addresses_ option in the app.

