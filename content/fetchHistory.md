---
title: "Fetch History"
enableToc: false
tags: 
- getter
- refactor
---

[github](https://github.com/AlexandreColauto/conpay-backend/blob/main/pages/api/fetchHistory.js)






This endpoint will fetch all users transaction on the [[transactions table]]. The table desn't specify if the transaction is from a type *send* or *receive*, it only retrieve all transactions that the user was involved, being responsability of the front end to diferentiate a *send* transaction when the user's id is on the **from** column, and define a *receive* transaction when the user's id is on the **to** column.

If the transaction was made to an external wallet, the **to** column will be empty, and **external_wallet** column will hold the destiny address.


#refactor
<details>
<summary>refactor details</summary>

currently conpay will only register outgoing transactions (from conpay to external wallet), to register ongoing transactions a blockchain event watcher must be implemented for pooling on chain transactions and populate  [[transactions table]] accourdingly, but this is not a priority now

</details>





	Core function code, inside api_helpers.js
``` Javascript
const getUserHistory = async (token) => {

const {

data: { user },

error: errorUser,

} = await supabase.auth.getUser(token);

  

if (errorUser) {

console.log(errorUser);

return false;

}

const { data: history, error: errorHistory } = await supabase

.from("transactions")

.select(

`*, from (wallet_address, username), to (wallet_address, username)`

)

.or(`from.eq.${user.id},to.eq.${user.id}`)

.order("created_at", { ascending: false });

if (errorHistory) {

console.log(errorHistory);

return false;

}

return history;

};

```