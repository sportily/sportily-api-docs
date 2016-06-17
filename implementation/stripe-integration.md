# Stripe Integration

1. In the admin panel, the user selects from a list of unpaid fees.

2. The user submits card details via Stripe.js, in exchange for a one-time charge token (starting `tok_`).

3. The admin panel then creates a new _Transaction_ object via the Sportily API, attaching the one-time charge token.

  ```json
  {
    "amount": 2000,
    "organisation_id": 2,
    "status": "pending",
    "source_id": 42,
    "source_token": "tok_18N63oCHtal4Uud6tJgCYD6X"
  }
  ```
  
4. In the Sportily API, the `TransactionObserver` spots the pending transaction, sees that it has a `source_token` value, indicating that it is a transaction that can be completed using Stripe.

5. The observer creates a new _Customer_ object via the Stripe API.

6. The observer then attaches the customer identifier (starting `cust_`) to the User object in the Sportily API.

7. The observer then creates a new _Charge_ object via the Stripe API, setting the `customer` field to the identifier of the newly created customer.

8. Depending on the response from the Stripe API, the `status` field of the _Transaction_ object is updated.

9. The final _Transaction_ object is returned as the response from the Sportily API.

## Questions

1. What happens if multiple transactions are created with the same token?
2. What happens when the user pays more fees at a later date?
3. What if the user then wants to pay fees with a different card?
