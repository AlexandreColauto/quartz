---
title: "wallet object"
enableToc: false
---

Conpay uses ethers js as tool for handeling wallet actions, such as create new wallet, initiate transaction, fetch balance.

Whenever a new conpay account is created  a random wallet is created at the same time and the mnemonic phrase is stored in database. 

To perform any action on the wallet, first retrieve the mnemonic from database, then mount a local hd wallet using ethers and the mnemonic:

``` Javascript
const mnemonic = jwt.verify(data.wallet, user.id);

const wallet = ethers.Wallet.fromMnemonic(mnemonic.wallet);

const url = "https://data-seed-prebsc-1-s3.binance.org:8545";

const provider = new ethers.providers.JsonRpcProvider(url);

if (provider) {

const connectedWallet = wallet.connect(provider);

return connectedWallet;

}
```

Using this object we will perform all on chain operations either reading or writing data on chain.

<details>
<summary>Futures Updates</summary>

To improve security in the future a method can be implemented at database level for returning the wallet object complete instead of the mnemonics for building locally. 

</details>
