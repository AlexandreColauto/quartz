
---
title: "Send Nft"
enableToc: false
tags: setter
---

[github](https://github.com/AlexandreColauto/conpay-backend/blob/main/pages/api/sendNft.js)

it expects a target (address, email or phone), the nft address and nft id to be sent to another Conpay user or external wallet. The back end mount a HD wallet with the mnemonic and invoke the [[ERC1155]] contract to transfer the ownership.
