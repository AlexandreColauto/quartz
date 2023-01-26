---
title: "Send Token"
enableToc: false
tags: setter
---

[github](https://github.com/AlexandreColauto/conpay-backend/blob/main/pages/api/sendToken.js)

it expects a target (address, email or phone) and the token amount to be sent to another Conpay user or external wallet. The back end mount a HD wallet with the mnemonic and invoke the send function of the ethers library.
