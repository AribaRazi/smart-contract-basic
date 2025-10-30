```markdown
# 💸 SimplePayment Smart Contract (Move Language)

A basic **Move smart contract** that allows users to create wallets, deposit funds, and send payments between accounts securely.

<img width="1920" height="1080" alt="Screenshot (122)" src="https://github.com/user-attachments/assets/a434bace-f538-4b45-87d7-e3fc3950d4b8" />


## 📘 Overview

The **SimplePayment** module implements a lightweight wallet system where:
- Each user can create their own wallet.
- Users can deposit funds into their wallet.
- Users can send payments to other wallets.
- Anyone can check a wallet’s balance.

This contract demonstrates **fund transfers**, **Move resource management**, and **error handling** in the Move language.

---

## 🚀 Features

- 🏦 **Create Wallet:** Initializes a wallet for any user (required before use).  
- 💰 **Deposit:** Add funds to your wallet balance.  
- 🔁 **Send Payment:** Transfer funds to another user’s wallet.  
- 📊 **Check Balance:** View the balance of any wallet.  
- ✅ **Built-in Test:** Includes a test function (`test_payment`) that verifies deposits and transfers.

---

## ⚙️ Functions

### `create_wallet(account: &signer)`
Creates a wallet for the account if one doesn’t already exist.

---

### `deposit(account: &signer, amount: u64)`
Deposits a specific amount into the user’s wallet.

---

### `send(sender: &signer, receiver: address, amount: u64)`
Sends coins from one wallet to another.  
- Aborts with `E_NOT_ENOUGH_BALANCE` if the sender has insufficient funds.  
- Aborts with `E_RECEIVER_NOT_READY` if the receiver doesn’t have a wallet.

---

### `get_balance(addr: address): u64`
Returns the balance of the specified wallet.  
Returns `0` if the wallet doesn’t exist.

---

## 🧪 Test Function

### `test_payment(user1: signer, user2: signer)`
A simple unit test:
1. Creates wallets for `user1` and `user2`.
2. Deposits `100` coins to `user1`.
3. Sends `40` coins from `user1` to `user2`.
4. Verifies resulting balances:  
   - `user1` → `60`  
   - `user2` → `40`

---

## ⚠️ Error Codes

| Code | Name | Description |
|------|------|-------------|
| `1` | `E_NOT_ENOUGH_BALANCE` | Sender’s wallet does not have enough funds. |
| `2` | `E_RECEIVER_NOT_READY` | Receiver has not created a wallet yet. |

---

## 📍 Module Address
```

0xf40aa9684befc2d71929527fa8722114c08cbfa91364d8caaaad78ec79c2de45::SimplePayment

````

---

## 🧩 Example Usage

```move
// Create your wallet
SimplePayment::create_wallet(&account);

// Deposit 100 units
SimplePayment::deposit(&account, 100);

// Send 40 units to another user
SimplePayment::send(&account, @0x2222, 40);

// Check balance
let balance = SimplePayment::get_balance(@0x1111);
````

---

## 📜 License

This project is open-source and available for educational and demonstration purposes.

```
```
