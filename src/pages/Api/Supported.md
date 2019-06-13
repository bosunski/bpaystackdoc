This Paystack Client currently supports all endpoints covered [here][1] in the API reference. To make going through this section easier understand, we recommend that you read through the [Introduction][2] to this section as it explains in details about the major part of the Client APIs.

# API Reference

## transactions(): Transactions
- `list(): Xeviant\Collection<Transaction>`
- `initialize(array $data): ArrayAccess|Transaction`
- `fetch(string $transactionId): ArrayAccess|Transaction`
- `authorize(string $transactionId): ArrayAccess|Transaction`
- `verify(string $transactionId): ArrayAccess|Transaction`
- `timeline(string $transactionId): ArrayAccess|Transaction`
- `export(string $transactionId): ArrayAccess|Transaction`
- `checkAuthorization(string $transactionId): ArrayAccess|Transaction`
- `reauthorize(string $transactionId): ArrayAccess|Transaction`

## customers(): Customers
- `list(): Xeviant\Collection<Customer>`


[1]: https://developers.paystack.co/reference
[2]: /api
