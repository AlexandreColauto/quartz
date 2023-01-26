
Conpay backend

the present documentation aims to explain and describe the functionalities and the technologic stack used on this project. 

This API service is build using Next and Supabase and it provides all the necessary paths to interact with Conpay. The authentication is made in the front-end using Supabase sdk. Then on every call the user's  JWT token must be provided for authentication on the server. The JWT token will be used for query the user id and perform all  CRUD operations on the user's behalf, wich will enforce all row level security on the database, meaning that the user only can alter data that belong to him (except for the public tables).

## API ENDPOINTS 

We can split the endpoints into two categories getter and setters that will handle users tokens, nfts, friends and history. Getters will be responsible for fetching users information (read data). Setters will then be responsible for changing states (write data).

- Getters
	- [[fetchFriends]]
	- [[fetchHistory]]
	- [[fetchTokenBalance]]
	- [[fetchUserNfts]]
	Getters expect an authenticated user's token and should return the specific desired object.

- Setters
	[[addFriend]]
	[[buyNfts]]
	[[removeFriend]]
	[[sendNft]]
	[[sendToken]]

Those endpoints can be organized accourding to its functions:

#### Tokens
 - [[fetchTokenBalance]]
 - [[fetchHistory]]
 - [[sendToken]]

### Nfts
- [[fetchUserNfts]]
- [[sendNft]]
- [[buyNfts]]

### Friendlist 
 - [[addFriend]]
 - [[removeFriend]]

This application handles only the features above, the signup process aswell the profile update will be done directly on the front end calling the respectives [[Supabase functions]] to authentication and profile creation.



