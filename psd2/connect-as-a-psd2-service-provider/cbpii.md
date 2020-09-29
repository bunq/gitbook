# CBPII

As a CBPII, you are allowed to authenticate in a user’s account to validate the availability of funds for the payment in question. 

1. Collect an alias for the bunq user's account \(their name and IBAN, email address, or phone number\).
2. Check the availability of funds via `POST /user/{userID}/confirmation-of-funds` passing the following information:
   * your `userId`;
   * the amount of money needed for the payment;
   * the name of the bunq user and the IBAN of the account \(email address or phone number pointing at the user are also possible\).

