

# StackedToken-Hub - Token Management Smart Contract

This Clarity smart contract implements a token management system on the Stacks blockchain. It supports creating tokens with categories and prices, managing balances and allowances, transferring tokens, and maintaining price history with timestamps.

## Features

* **Token Minting:** Admin can mint new tokens with a name, category, max supply, and initial price.
* **Price Management:** Admin can update token prices, and all price changes are recorded with timestamps.
* **Balances & Allowances:** Users can hold token balances and authorize other principals to spend on their behalf.
* **Transfers:** Tokens can be transferred between users, either directly or by authorized spenders.
* **Admin Management:** The contract admin can be changed securely.
* **Read-only Views:** Functions to query token details, balances, allowances, and historical prices.
* **Error Handling:** Comprehensive error constants ensure clear failure reasons.

## Contract Data Structures

* `tokens`: Stores token metadata including name, category, max supply, price, and last price update time.
* `balances`: Tracks token balances per holder.
* `allowances`: Manages spend authorizations.
* `price-history`: Logs token prices at specific timestamps.
* `token-counter`: Auto-incremented counter for unique token IDs.
* `contract-admin`: Principal address of the contract administrator.

## How to Use

### Minting Tokens

Only the contract admin can mint tokens using `mint-token`. Parameters:

* `token-name` (string, max 64 ASCII chars)
* `token-category` (string, max 32 ASCII chars)
* `max-supply` (uint)
* `token-price` (uint)

Returns the new `token-id`.

### Updating Token Price

Admin calls `update-token-price` with:

* `token-id`
* `new-price` (must be > 0)

Records price updates in `price-history`.

### Authorizing Spending

Token holders can authorize another principal to spend tokens on their behalf using `authorize-spending`.

### Transferring Tokens

* `transfer`: Direct token transfer by holder.
* `transfer-as-authorized`: Transfer by authorized spender.

### Admin Control

Use `set-contract-admin` to transfer admin rights.

### Read-only Queries

* `get-token-details(token-id)`
* `get-holder-balance(holder, token-id)`
* `get-authorized-amount(holder, authorized, token-id)`
* `get-price-at-time(token-id, timestamp)`
* `is-valid-token(token-id)`

---

## Error Codes

| Code | Meaning                 |
| ---- | ----------------------- |
| u100 | Not authorized          |
| u101 | Token already exists    |
| u102 | Token not found         |
| u103 | Insufficient funds      |
| u104 | Invalid token name      |
| u105 | Invalid category        |
| u106 | Invalid max supply      |
| u107 | Invalid token price     |
| u108 | Invalid recipient       |
| u109 | Invalid transfer amount |
| u110 | Insufficient allowance  |
| u111 | Invalid authorized addr |
| u112 | Invalid price update    |

---
