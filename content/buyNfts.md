#giturl https://github.com/AlexandreColauto/conpay-backend/blob/main/pages/api/buyNFTs.js
#setter

This endpoint expect ERC1155  address. When a new transaction is initiated, the address and id passed in the body of the request will be used to populate one transaction using [[ERC1155 ABI]] , address and id.
The unsigned transaction is then inserted on the [[orders table]], which will be broadcasted to mobile app so the user can [[sign transaction]]. 




```js
const { token, address, id } = req.body;

const wallet = await getUserWallet(token);

if (wallet) {

const tx = await buyNFT(address, id);

console.log(tx);

const { data, error } = await supabase.from("orders").insert({

user_id: _user.id,

payload: JSON.stringify(tx),

status: "initiated",

});
```
