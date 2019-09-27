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

## Do you have any examples of signing requests? 

Use [our SDKs](https://github.com/bunq). They will handle signing for you.

## Do you have any examples of how to register a PSD2 certificate correctly?

Our SDKs contain examples and tests that will help you register as a service provider.

### **C\# examples** 

{% embed url="https://github.com/bunq/psd2\_sample\_csharp" %}

{% embed url="https://github.com/bunq/sdk\_csharp/blob/develop/BunqSdk.Tests/Context/Psd2ApiContextTest.cs" %}

{% embed url="https://github.com/bunq/tinker\_csharp/blob/develop/TinkerSrc/CreatePsd2Configuration.cs" %}

### **PHP examples**

{% embed url="https://github.com/bunq/sdk\_php/tree/develop/tests/Context/PSD2" %}

{% embed url="https://github.com/bunq/sdk\_php/blob/develop/tests/Context/Psd2ApiContextTest.php" %}

{% embed url="https://github.com/bunq/tinker\_php/blob/develop/tinker/create-psd2-configuration.php" %}

### **Java examples**

{% embed url="https://github.com/bunq/sdk\_java/blob/develop/src/test/java/com/bunq/sdk/context/Psd2ContextTest.java" %}

{% embed url="https://github.com/bunq/tinker\_java/blob/develop/src/main/java/com/bunq/tinker/CreatePsd2Configuration.java" %}

### **Python examples** 

No examples yet, but we're working on it.

