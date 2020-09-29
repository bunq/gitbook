# Connect as a PSD2 service provider

As a service provider, either an Account Information Service Provider \(AISP\) or Payment Initiation Service Provider \(PISP\), you have obtained or are planning to obtain a license from your local supervisor. You will need your unique eIDAS certificate number to start using the PSD2-compliant bunq API on production.

We accept pseudo certificates in the sandbox environment so you could test the flow. You can generate a test certificate using the command below. 

{% hint style="warning" %}
Make sure to include `AISP` and/or `PISP` in the name to generate a certificate with the roles.
{% endhint %}

`openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365 -nodes -subj '/CN=My App PISP AISP/C=NL'`

{% page-ref page="../../basics/sandbox/" %}

## Register as a service provider

Before you can read the information on bunq users or initiate payments, you need to register a PSD2 account and receive credentials that will enable you to access the bunq user accounts.

1. Execute `POST v1/installation` and get your installation _Token_ with a unique random key pair.
2. Use the installation _Token_ and your unique PSD2 certificate to call `POST v1/payment-service-provider-credential`. This will register your software.
3. Receive your API key in return. It will identify you as a PSD2 bunq API user. You will use it to start an OAuth flow. The session will last 90 days. After it closes, start a new session using the same API key.
4. Register a device by using `POST v1/device-server` using the API key for the secret and passing the installation _Token_ in the `X-Bunq-Client-Authentication` header.
5. Create your first session by executing `POST v1/session-server`. Provide the installation _Token_ in the `X-Bunq-Client-Authentication` header. You will receive a session _Token_. Use it in any following request in the `X-Bunq-Client-Authentication` header.

{% hint style="info" %}
The first session will last 1 hour. Start a new session within 60 minutes.
{% endhint %}

![](../../.gitbook/assets/creating-api-context-as-a-psd2-user-revised-.jpg)

## Register your OAuth application

Before you can start authenticating on behalf of a bunq user, you need to get a _Client ID_ and a _Secret_, which will identify you in authorization requests to the user accounts.

1. Call `POST /v1/user/{userID}/oauth-client` to create an OAuth Client.
2. Add a redirect URL to the OAuth Client via `POST /user/{userID}/oauth-client/{oauth-clientID}/callback-url`.
3. Call `GET /v1/user/{userID}/oauth-client/{oauth-clientID}`. We will return your _Client ID_ and _Client Secret_.
4. You are ready to [initiate authorization requests](https://beta.doc.bunq.com/basics/oauth#authorization-request).

The flow below will guide you through the full OAuth connection process. Note that you only need to create OAuth credentials once.

![](../../.gitbook/assets/authorization-oauth-flow.jpg)



