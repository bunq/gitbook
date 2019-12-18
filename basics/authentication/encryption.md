# Encryption

Some API calls such as `POST /user/{userID}/card-debit` and `POST /user/{userID}/card-credit` require additional encryption to protect the sensitive data that they pass. 

Here is how to encrypt a request:

1. Generate a random [Initialization Vector](https://en.wikipedia.org/wiki/Initialization_vector) \(IV\) of 16 bytes.
2. Generate a random [Advanced Encryption Standard](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard) \(AES\) key of 32 bytes.
3. Encrypt the AES key with the public key of your installation.
4. Encrypt the request body using the AES-256-CBC mode \(apply the [PKCS1](https://en.wikipedia.org/wiki/PKCS_1) padding\).
5. Determine the [HMAC](https://en.wikipedia.org/wiki/HMAC) hash of the body prefixed with the IV using the [SHA-1 algorithm](https://en.wikipedia.org/wiki/SHA-1) and the AES key.
6. Send the request using the encrypted body and the following headers: 
   * `X-Bunq-Client-Encryption-Hmac` set to the base64-encoded HMAC hash;
   * `X-Bunq-Client-Encryption-Iv` set to the base64-encoded IV; and
   * `X-Bunq-Client-Encryption-Key` set to the base64-encoded _**\(!!!\) ENCRYPTED**_ AES key.

Voilà! Enjoy your encrypted API request work!

