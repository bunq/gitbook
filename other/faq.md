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



