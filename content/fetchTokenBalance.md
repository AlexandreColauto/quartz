---
title: "Fetch Token Balance"
enableToc: false
tags: 
- getter
- refactor
---

[github](https://github.com/AlexandreColauto/conpay-backend/blob/main/pages/api/fetchTokenBalance.js)

This endpoint will take the JWT token send in the body and retrieve the user's [[wallet object]] , then simply call `wallet.getBalance()`, parse and return the value.

``` Javascript
const wallet = await getUserWallet(token);

if (wallet) {

const balance = await wallet.getBalance();

res.status(200).json({

success: true,

message: "Success",

balance: ethers.utils.formatEther(balance),

});

return;
```
