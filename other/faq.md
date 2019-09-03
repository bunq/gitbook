# FAQ

## **What is a tab?**

A tab is a page that allows a bunq user to pay for a product or service using a QR code or app redirect. You have seen tabs when paying online or making a POS purchase via bunq.

{% hint style="warning" %}
A tab has nothing to do with a browser tab. It is a bill in a restaurant or in a store.
{% endhint %}

## **What is a Wildcard API key?**

A Wildcard API key allows you to make API calls from any IP address after registering a device via `POST v1/device-server`. 

You can switch to using a Wildcard API Key in 2 ways:

1. **Manually** by tapping on “Allow All IP Addresses” in the settings of your API key in the bunq app.
2. **Programmatically** by passing your current IP and a `*` \(asterisk\) in the _permitted\_ips_ field of the `POST v1/device-server` call \(e.g: `["1.2.3.4", "*"]`\).

## I'm setting up the OAuth flow. How do I overcome German households not having a static IP address?

You can use Wildcard IP on the `device-server` step when using the token you get after going through the OAuth flow. So it will look like this:

1. You establish a connection with the account via OAuth.
2. You get an authorization token.
3. You use the token as an API key to start a session \(at this step, you register the token as an API key\):
4. You create an API context. On the `device-server` step, you switch to using the wildcard option.

## How do I display the OAuth QR code in my application?

Open an in-app browser.



