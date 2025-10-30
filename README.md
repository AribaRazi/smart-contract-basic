````markdown
# 💰 SimplePayment Smart Contract

A beginner-friendly Move smart contract that enables users to create wallets, deposit virtual tokens, and send payments securely on the Aptos blockchain.

## ✅ Deployment Screenshot

![Deployed Contract Screenshot](https://github.com/user-attachments/assets/afd13047-f32d-4706-b334-6e24140be35f)



## 🚀 Project Description

**SimplePayment** is a decentralized wallet system written in the Move language.  
Each user can:
- Create their personal wallet.
- Deposit coins into it.
- Send coins to another user’s wallet.
- Check their balance anytime.

This contract is ideal for learning how to manage on-chain storage and resources using Move.

---

## 🧩 Features

- 🏦 **Create Wallet:** Initializes a new wallet for each user.  
- 💸 **Deposit Funds:** Add coins to your wallet balance.  
- 🔁 **Send Coins:** Transfer funds to another user's wallet.  
- 📊 **Check Balance:** View your current wallet balance.  
- 🧪 **Test Function:** Built-in test case to verify wallet creation, deposit, and transfer logic.

---

## 🧠 Smart Contract Code

```move
module 0xf40aa9684befc2d71929527fa8722114c08cbfa91364d8caaaad78ec79c2de45::SimplePayment {

    use std::signer;

    const E_NOT_ENOUGH_BALANCE: u64 = 1;
    const E_RECEIVER_NOT_READY: u64 = 2;

    struct Wallet has key {
        balance: u64,
    }

    public entry fun create_wallet(account: &signer) {
        let user = signer::address_of(account);
        if (!exists<Wallet>(user)) {
            let wallet = Wallet { balance: 0 };
            move_to(account, wallet);
        };
    }

    public entry fun deposit(account: &signer, amount: u64) acquires Wallet {
        let user = signer::address_of(account);
        let wallet = borrow_global_mut<Wallet>(user);
        wallet.balance = wallet.balance + amount;
    }

    public entry fun send(
        sender: &signer,
        receiver: address,
        amount: u64
    ) acquires Wallet {
        let sender_addr = signer::address_of(sender);
        let sender_wallet = borrow_global_mut<Wallet>(sender_addr);

        if (sender_wallet.balance < amount) {
            abort E_NOT_ENOUGH_BALANCE;
        };

        if (!exists<Wallet>(receiver)) {
            abort E_RECEIVER_NOT_READY;
        };

        sender_wallet.balance = sender_wallet.balance - amount;
        let receiver_wallet = borrow_global_mut<Wallet>(receiver);
        receiver_wallet.balance = receiver_wallet.balance + amount;
    }

    #[view]
    public fun get_balance(addr: address): u64 acquires Wallet {
        if (!exists<Wallet>(addr)) {
            return 0
        };
        borrow_global<Wallet>(addr).balance
    }

    #[test(user1 = @0x1111, user2 = @0x2222)]
    public entry fun test_payment(user1: signer, user2: signer) acquires Wallet {
        create_wallet(&user1);
        create_wallet(&user2);
        deposit(&user1, 100);
        send(&user1, signer::address_of(&user2), 40);
        let b1 = get_balance(signer::address_of(&user1));
        let b2 = get_balance(signer::address_of(&user2));
        assert!(b1 == 60, 0);
        assert!(b2 == 40, 0);
    }
}
````

---

## 🌐 Deployment Details

* **Deployed Address:**
  `0x72385f141c3af5a4350fabf809b80f979f575d5d91e521f6d0354eb6cbeebc40`

* **Explorer Link:**
  [View on Aptos Explorer](https://explorer.aptoslabs.com/txn/0x72385f141c3af5a4350fabf809b80f979f575d5d91e521f6d0354eb6cbeebc40/changes?network=testnet)

* **Network:** Aptos Testnet

---

## 🛠️ How to Use

1. **Create Wallet**

   ```bash
   aptos move run --function-id 0x72385f141c3af5a4350fabf809b80f979f575d5d91e521f6d0354eb6cbeebc40::SimplePayment::create_wallet
   ```

2. **Deposit Funds**

   ```bash
   aptos move run --function-id 0x72385f141c3af5a4350fabf809b80f979f575d5d91e521f6d0354eb6cbeebc40::SimplePayment::deposit --args u64:100
   ```

3. **Send Coins**

   ```bash
   aptos move run --function-id 0x72385f141c3af5a4350fabf809b80f979f575d5d91e521f6d0354eb6cbeebc40::SimplePayment::send --args address:<receiver_address> u64:50
   ```

4. **Check Balance**

   ```bash
   aptos move view --function-id 0x72385f141c3af5a4350fabf809b80f979f575d5d91e521f6d0354eb6cbeebc40::SimplePayment::get_balance --args address:<your_address>
   ```

---

## 📚 License

This project is released under the [MIT License](LICENSE).

---

```
```
