# Errors

We use the HTTP response codes to indicate the success or failure of an API request:

* codes in the 2xx range indicate success;
* codes in the 4xx range indicate an error having to do with the provided information \(e.g. a required parameter was missing, insufficient funds, etc.\);
* codes in the 5xx range indicate an error having to do with the bunq servers. If you get such an error, please report it to us via chat.

## Response Codes

| Code | Error | Description |
| :--- | :--- | :--- |
| 200 | OK | Successful HTTP request |
| 399 | NOT MODIFIED | Same as 304. It implies you have a local cached copy of the data. |
| 400 | BAD REQUEST | A parameter is missing or invalid. |
| 401 | UNAUTHORISED | A token or signature provided is not valid. |
| 403 | FORBIDDEN | You're not allowed to make this call. |
| 404 | NOT FOUND | The object you're looking for cannot be found. |
| 405 | METHOD NOT ALLOWED | The method you are using is not allowed for this endpoint. |
| 429 | RATE LIMIT | Too many API calls have been made in a too short period of time. |
| 490 | USER ERROR | A parameter is missing or invalid. |
| 491 | MAINTENANCE ERROR | bunq is in maintenance mode. |
| 500 | INTERNAL SERVER ERROR | Something went wrong on our end. |

{% hint style="info" %}
All 4xx errors include a JSON body explaining what went wrong.
{% endhint %}

## Rate Limits

If you are receiving the 429 error, please make sure you are sending requests at rates that are below our rate limits.

Here are our **rate limits per IP address per endpoint:**

* **GET requests:** 3 requests within any 3 consecutive seconds
* **POST requests:** 5 requests within any 3 consecutive seconds
* **PUT requests:** 2 requests within any 3 consecutive seconds

{% hint style="info" %}
We have a lower rate limit for `/session-server`: 1 request within 30 consecutive seconds.
{% endhint %}

