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
- `create(array $data): Xeviant\Collection<Customer>`
- `fetch(string $email_or_id_or_customer_code): Customer`
- `update(string $id_or_customer_code, array $data): Customer`
- `whitelist(string $id_or_customer_code): bool`
- `blacklist(string $id_or_customer_code): bool`
- `deactivateAuthorization(string $authorization_code): bool`

## subAccounts(): SubAccounts
- `list(): Xeviant\Collection<SubAccount>`
- `create(array $data): SubAccount`
- `fetch(string $id_or_slug): SubAccount`
- `update(string $id_or_slug, array $data): SubAccount`

## plans(): Plans
- `list(): Xeviant\Collection<Plan>`
- `create(array $data): Plan`
- `fetch(string $id_or_plan_code): Plan`
- `update(string $id_or_plan_code, array $data): Plan`

## subscriptions(): Subscription
- `list(): Xeviant\Collection<Subscription>`
- `create(array $data): Subscription`
- `fetch(string $id_or_plan_code): Subscription`
- `disable(string $code): bool`
- `enable(string $code): bool`

## pages(): Payment Pages
- `list(): Xeviant\Collection<Page>`
- `create(array $data): Page`
- `fetch(string $id_or_slug): Page`
- `update(string $id_or_slug, array $data): Page`
- `checkSlugAvailability(string $slug): bool`

## settlements(): Settlements
- `fetch(): Xeviant\Collection`

## invoices(): Invoices
- `list(): Xeviant\Collection<Invoice>`
- `create(array $data): Invoice`
- `view(string $invoice_id_or_code): Invoice`
- `verify(string $invoice_code): Invoice`
- `notify(string $id_or_code): array`
- `totals(string $id_or_code): array`
- `finalize(string $invoiceId, array $parameters = [])`
- `archive(string $invoiceId, array $parameters = [])`
- `markAsPaid(string $invoiceId, array $parameters = [])`
- `update(string $invoiceId, array $parameters = [])`

## transferRecipients(): Transfer Recipients
- `deleteTransferRecipient(string $recipientCode)`
- `list(array $parameters = []): Collection<TransferRecipient>`
- `create(array $parameters)`
- `update(string $recipientCode, array $parameters)`

## transfers(): Transfers
- `fetch(string $transferId): Transfer`
- `list(array $parameters = []): Collection<Transfer>`
- `initiate(array $parameters): Transfer`
- `finalize(array $parameters): Transfer`
- `bulk(array $parameters)`
- `resendOtp(array $parameters)`
- `disableOtp(array $parameters = [])`
- `enableOtp(array $parameters = [])`
- `disableOtpFinalize(array $parameters)`

[1]: https://developers.paystack.co/reference
[2]: /api
