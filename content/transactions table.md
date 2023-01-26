---
title: "Transactions Table"
enableToc: false
---

it holds  all transactions made in conpay. This table is composed of 6 columns:
- **id**: unique's transaction id
- **created at**: timestamp of transaction.
- **from**: initiator's id (the id of the user who start the transaction)
- **to**: reciever's id.
- **amount**: quantity of tokens transfered in transaction.
- **hash**: the transaction hash on the blockchain.
- **external_wallet**: if the transaction is made **to** an external wallet (outside of conpay), then the address is stored here. ( ==Disclaimer==: only **send** transactions to external wallet will be recorded because is handled by our system, since to record a **receive** transaction a event watcher shold be developed to monitor the blockchain for transactions to user wallet)

![[img4.png]]

