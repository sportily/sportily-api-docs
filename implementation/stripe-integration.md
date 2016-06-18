# Stripe Integration

1. In the admin panel, the user selects from a list of unpaid fees.

2. The user submits card details via Stripe.js, in exchange for a one-time charge token (starting `tok_`).

3. The admin panel then creates a new (Sportily) _Card_ object via the Sportily API, attaching the ont-time charge token from Stripe.

  `POST: /users/{id}/cards`
  
  ```json
  {
    "provider": "stripe",
    "provider_token": "tok_..."
  }
  ```

4. An observer in the Sportiyl API will spot the new card and resolve it as necessary, creating the appropriate entities in the Stripe API. If the user does not have a linked Stripe account, then a (Stripe) _Customer_ object will be created, which also creates a new (Stripe) _Card_ object.

5. The (Sportily) _Card_ object will be updated with details of the newly created (Stripe) _Card_ object.

6. The (Sportily) _User_ object will be updated with the Stripe customer identifier.

7. The augmented (Sportily) _Card_ object will be returned from the Sportily API call.

  ```json
  {
    "provider": "stripe",
    "provider_id": "card_...",
    "provider_token": "tok_...",
    "details": {
      "brand": "visa",
      "last4": "4242",
      "exp_month": 5,
      "exp_year": 2017
    }
  ```
  

