# Moving to Production

Have you tested your bunq integration to the fullest and are now ready to introduce your application to the world? It's time to move it to the production environment!

Here is what you need to do to get started:

1. Generate a production API key via the bunq app. Go _Profile → Security & Settings → Developers → API keys_. 
2. Change your API Key and redo the [sequence of calls to open a session](https://lexy.gitbook.io/bunq/basics/authentication).

{% hint style="info" %}
We highly recommend using a standard production API Key instead of a [Wildcard API Key](https://together.bunq.com/d/1997-the-new-wildcard-api-key). The former is significantly safer and it protects you from malicious intrusions and attacks.
{% endhint %}

 The bunq Public API production environment is hosted at `https://api.bunq.com`.

{% hint style="info" %}
Please be aware that if you will gain access to account information of other bunq users or initiate a payment for them, you require a PSD2 permit.
{% endhint %}



