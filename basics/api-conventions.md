# API Conventions

Make sure to follow these indications when using the bunq API. Alternatively, use one of our SDKs to get started.

### Responses

All JSON responses have one top level object. This object contains a Response field the value of which is always an array. This also applies to responses that contain only one object.

**Example** **response** **body structure:**

```text
{
    "Response": [
        {
            "DataObject": {}
        }
    ]
}
```

### Errors

* Error responses also have one top level Error object.
* The contents of the array is a JSON object with the _error\_description_ and _error\_description\_translated_ fields.
* The _error\_description_ field contains the error explanation in the English language
* The _error\_description\_translated_ field can be shown to the end users. It is automatically translated into the language specified in the `X-Bunq-Language` header. The default language is en\_US.
* If you are using one of the bunq SDKs, error responses will be always raised in form of an exception.

**Example response body:**

```text
{
    "Error": [
        {
            "error_description": "Error description",
            "error_description_translated": "User facing error description"
        }
    ]
}
```

### Object Type Indications

If the API returns different types of objects for the same field, they are nested in a group JSON object that, in its turn,  contains a separate field for each of the objects. If you use one of the bunq SDKs, a BunqResponse object will be returned as the top level object.

**Example.** The _content_ field can contain multiple types of objects such as ChatMessageContentText in this case. Be sure to follow this convention or use one of the bunq SDKs instead.

```text
{
    "content": {
        "ChatMessageContentText": {
            "text": "Hi! This is an automated security message. We saw you just logged in on an My Device Description. If you believe someone else logged in with your account, please get in touch with Support."
        }
    }
}
```

### Time Formats

We use the UTC date and time standard and so expect you to use this format `YYYY-MM-DD hh:mm:ss.ssssss` . The meaning of the letters is defined in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601). 

**Example:** `2017-01-13 13:19:16.215235`.  


