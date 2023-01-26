#giturl https://github.com/AlexandreColauto/conpay-backend/blob/main/pages/api/fetchFriend.js

#refactor
<details>
<summary>refactor details</summary>
Update function to perform a single query to supabase instead of nested queries.
</details>

In supabase we have   [[friend_list table]], this endpoint takes the JWT send in the request to define the user, then query this table the user's friends ids then query again those ids to get full information (note: this function will be update later for a single query to supabase).

	Core function code, inside api_helpers.js
``` Javascript
const getFriendsIds = async (token) => {

const {

data: { user },

error: errorUser,

} = await supabase.auth.getUser(token);

  

const { data: friend_list, error } = await supabase

.from("friend_list")

.select("friends")

.eq("user", user.id)

.single();

  

if (error) {

console.log(error);

}

if (friend_list) {

return friend_list.friends;

}

};

  

const getFriends = async (token) => {

const friendsIds = await getFriendsIds(token);

if (friendsIds) {

const { data: friends, error } = await supabase

.from("profiles")

.select("*")

.in("id", friendsIds);

if (error) {

console.log(error);

}

if (friends) {

return friends;

}

}

};

```