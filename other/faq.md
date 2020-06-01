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

## Can I access my account via API as a Travel user?

You need to have a Premium \(SuperGreen\) or Business \(SuperGreen\) account to use the bunq API. 

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

{% embed url="https://github.com/bunq/sdk\_python/blob/develop/tests/context/test\_psd2\_context.py" %}

## Do we _always_ need an AISP or PISP license to access/use the bunq API? 

No, there are two ways to get access to the API:

1. as a AISP/PISP license holder, by means of a PSD2 certificate; or 
2. as a bunq customer, by means of an API-key issued via the bunq app. 

## Is there a difference between the bunq Public API and the bunq PSD2 API? 

The bunq Public API and the bunq PSD2 API are essentially the same API, however, there are different ways to access the API and there are differences in accessible endpoints depending on how you access the API. See the above mentioned answer for more information on how you can get access to the API.

As a general rule, when you access the API by means of a PSD2 certificate, you will only have access to the endpoints required for your respective PSD2 role \(PISP and/or AISP\). In other words, as a PISP you will solely have access to the endpoints for initiating a payment and as a AISP you will solely have access to the endpoints for account information. 

When you are considering to use our API, please consider which API endpoints you would like to use, because certain endpoints are only accessible for bunq customers. 

## Do we need a license if we use the bunq API solely for internal use?

No, you can use the bunq API to manage your own accounts without a license. A license is only needed in case you use the API to provide services to one or more third parties. 

## Can we use the bunq API to offer services to third parties?

Yes, but in this case you might need a license and it is your own responsibility to ensure that you comply with any and all license requirements. We strongly advice you to get an expert legal opinion in case you are considering to use our API to offer services to third parties.

## Is it possible to provide services to third parties by means of the bunq API _without_ a license?

Whether or not you need a license depends on the activities you \(intend to\) perform by means of the bunq API. 

According to the Dutch Central Bank a PISP/AISP license is not always required when using a banking API to provide services to third parties \(see: [https://www.toezicht.dnb.nl/en/3/50-237764.jsp](https://www.toezicht.dnb.nl/en/3/50-237764.jsp)\). 

Based on the aforementioned webpage from DNB we believe a license might not be required in case:  

1. you sign-up for a bunq account;
2. accept the bunq API terms and conditions;
3. get an API-Key via the bunq app;
4. use your API-Key to access the bunq API; 
5. use OAuth to get access to the accounts of one or more third parties; and  
6. use the OAuth access to provide services to the third parties.

However, we do not guarantee in any way that you do not need a license in case you follow the above mentioned process. Every situation is different and it is your own responsibility to assess whether or not your situation requires you to get a license. 

## What happens in case we perform licensed activities without a license?

Performing activities subject licensing without the respective license\(s\) is illegal and can have very serious consequences. For example, you might be fined by the regulators, and we could decide to block or close your account. 

