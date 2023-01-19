# Accounting Platform API

- [Notice](#Notice)
- [Encryption Flow](#Encryption-Flow)
- [API Spec](#API-Spec) 
    - [Member&Agent](#MemberAgent)
    - [Wager](#Wager)
    - [Transfer](#Transfer)
    - [Seamless2.0](#Seamless20)
    - [Seamless1.1](#Seamless11)
- [Reference of API](../reference-en.md)

## Notice

Please read the following notes before using our API.

- Please read the [Notice](../notice-en.md) to get more information.
- The following table presents the Table ID by game type in game. 

    | Table Id            | 名稱            |
    | ---------------- | ---------------------- |
    | **Baccarat**     |                        |
    | H | BC01 |
    | E | BC02 |
    | O | BC03 |
    | P | BC04 |
    | J | BC05 |
    | L | BC06 |
    | G | BC07 |
    | I | BC08 |
    | F | BC09 |
    | K | BC10 |
    | X | BC99 |
    | **DragonTiger**     |                        |
    | A | DT01 |
    | **Roulette**     |                        |
    | B | RT01 |
    | **Sicbo**     |                        |
    | W | SB01 |
    | V | SB02 |
    | **Sedie**     |                        |
    | C | SD01 |
    | D | SD02 |

- The table below is supported currencies, and the currency code is refer to [ISO_4217](https://en.wikipedia.org/wiki/ISO_4217)

    | Code | Currency     |
    | ---- | -------- |
    | TWD  | Taiwan dollar   |
    | VND  | Vietnamese đồng   |
    | KVND  | 1000 VND   | 

## Encryption Flow

We provide some simple libraries to generate `Key`(Those libraries also support to generate `token` for seamless callbacks). The following languages are currently supported:

- [JAVA Token](https://gitlab.com/token-library/java/-/wikis/README)
- [PHP Token](https://gitlab.com/token-library/php-token)
- [Node.js Token](https://gitlab.com/token-library/js-token)
- [C# Token](https://gitlab.com/token-library/csharp-token)

If the language of library hasn't supported or you'd like to handle it yourself, please follow [this doc to generate the `Key`](../encryption-en.md)

## API Spec

### Member&Agent

Provide creating member, member login, managing member or agent data, please refer to [Member&Agent API](https://staging-agent.olacak.live/swagger/public/index.html?lang=en#/Member%2FAgent)

### Wager

Asynchronous, about 5 mins delay. Our system will merge bets in the same member and game round(run) to a wager. Only settled wagers able to be found. Please refer to [Wager API](https://staging-agent.olacak.live/swagger/public/index.html?lang=en#/Wager)

### Transfer

Only transfer wallet agents available, please refer to [Transfer API](https://staging-agent.olacak.live/swagger/public/index.html?lang=en#/Transfer)

### Seamless2.0

- Only Seamless wallet agents available. The 2.0 Version only needs to implement two callbacks which are focus on the balance changing. The encryption rule is also simpler and more flexible.
- Please setting the seamless callbacks(getBalance/updateBalance) on the personal game setting page of the backstage. 
- Refer to the [SeamlessWallet API 2.0](../../SeamlessWalletAPI2.0/SeamlessWalletAPI-2.0.md) documents to implement all of seamless callbacks.
- Because of avoid settling repeatedly, our system only invokes the callback once when updating balance. If there is timeout or something unexpected response, our system won't re-invoke again. So please check the failed cases from [GetRequestHistoryByTime api](https://staging-agent.olacak.live/swagger/public/index.html?lang=en#/Seamless2.0/post_api_keno_api_xg_casino_GetRequestHistoryByTime) regularly, and according to the `RequestJson` in response to fix the balance of members.  
- Please provide test account on staging(test) environment of your system after completing all of seamless callbacks. We need to test its working fine on staging. 

### Seamless1.1

- Only Seamless wallet agents available. The 1.0 version was deprecated, and our system force upgraded to the 1.1 version after 2022-10-17.
- Please setting the seamless callbacks(balance/bet/settle/rollback) on the personal game setting page of the backstage. 
- Refer to the [How to handle the balance of members](../../SeamlessWalletAPI1.x/handle-balance.md) and [XG Seamless Wallet API ](https://app.swaggerhub.com/apis/x-gaming-bet/xg-seamless_wallet_api_en/1.1) documents to implement all of seamless callbacks.
- If the game round canceled before settlement, our system will invoke the rollback callback.
- If the bet canceled after settlement, our system doesn't inform your system by rollback callback. Your system needs to check the `ModifiedStatus` of bet by [GetReplenishmentByTime api](https://staging-agent.olacak.live/swagger/public/index.html?lang=en#/Seamless1.x/post_api_keno_api_xg_casino_GetReplenishmentByTime) regularly and handle the member's balance.
- Please provide test account on staging(test) environment of your system after completing all of seamless callbacks. We need to test its working fine on staging.

