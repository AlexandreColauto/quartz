#giturl https://github.com/AlexandreColauto/conpay-backend/blob/main/pages/api/addFriend.js
#setter

With the finality of adding a new friend to the friend list, this endpoint will alter the respective user's row in the [[friend_list table]]. To do that user must send the token and a **target**, that could be either a email, phone or wallet address of another conpay user. The data base will query for either field, find the respective id and append to the friend list array.

