#giturl https://github.com/AlexandreColauto/conpay-backend/blob/main/pages/api/fetchUserNfts.js

This endpoit make use of another API, Moralis.
<details><summary>Why Moralis?</summary>
 Moralis indexes all nft transactions on a chain and provide all transactions information, with that it's possible to query all nft's that a certain wallet hold. it's possible to build our own indexer, but seems like reinventing the whell.</details>

This and the [[onramp]], will be the only external services that conpay will be using.

When invoked, this endpoint will retrieve the user's wallet address from database, then call Morali's API that will return all NFT's addresses and id's of a specific address. With that we invoke the ERC1155 function *uri*, that will return the nft metadata.

we need to do this iteractive process because moralis returns only address and id's, we still have to fetch the metadata uri for every single nft, which can slowdown the process of retrieving. #refactor 

This issue happens most for external nfts, for conpay for business we will have total control over urls and metadata.

There are two functions fetchUserNFTsIndex ,that will call Moralis API and return all address and id's, and fetchUserNFTsMetadata that will query for every single nft contract for the url and call it for the nft's metadata.



	Core function code, inside api_helpers.js
``` Javascript
const fetchUserNFTsIndex = async (address) => {

const options = {

method: "GET",

url: `https://deep-index.moralis.io/api/v2/${address}/nft`,

params: { chain: "0x61", format: "decimal" },

headers: {

accept: "application/json",

"X-API-Key":

"OWkwoRwEpX25DCOw8Tm932gCp4mwRsfafJZXQmZ0DAzWRo3x0T9vU1zmp2H0IfzU",

},

};

const result = await axios.request(options);

return result.data.result;

};

const fetchUserNFTsMetadata = async (address) => {

const nfts = await fetchUserNFTsIndex(address);

const nftsWithMetadata = [];

const nftsMetadataMissing = [];

console.log("nfts:", nfts.length);

nfts.map((nft) => {

if (!nft.metadata) {

nftsMetadataMissing.push(nft);

} else {

if (typeof nft.metadata === "string") {

nft.metadata = JSON.parse(nft.metadata);

}

nftsWithMetadata.push(nft);

}

});

await Promise.all(

nftsMetadataMissing.map(async (nft) => {

try {

const metadata = await axios.get(nft.token_uri);

nft.metadata = metadata.data;

} catch (error) {}

})

);

const nftsArray = nftsWithMetadata.concat(nftsMetadataMissing);

return nftsArray;

};

```