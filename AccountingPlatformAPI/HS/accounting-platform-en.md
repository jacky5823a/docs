# Accounting Platform API

- [Notice](#Notice)
- [Encryption Flow](../encryption-en.md)
- [API Spec](#API-Spec) 
    - [Member&Agent](#MemberAgent)
    - [Wager](#Wager)
    - [Transfer](#Transfer)
    - [Seamless2.0](#Seamless20)
- [Table Limit(Bet Limit)](#table-limitbet-limit)
- [Reference of API](../reference-en.md)

## Notice

Please read the following notes before using our API.

- Please read the [Notice](../notice-en.md) to get more information.
- The following table presents the Table ID by game type in game. 

    | Game Type | Table Id  |
    | --- | --- |
    | Baccarat | BC01, BC02, BC03, BC04, BC05, BC06, BC07, BC08, BC09, BC10，BC05, BC08 are the feature baccarat|
    | DragonTiger | DT01 |  
    | Roulette | RT01 |  
    | Sicbo | SB01, SB02 |  
    | Sedie | SD01, SD02 |
    
- The table below is supported currencies, and the currency code is refer to [ISO_4217](https://en.wikipedia.org/wiki/ISO_4217)

    | Code | Currency     |
    | ---- | -------- |
    | TWD  | Taiwan dollar   |
    | VND  | Vietnamese đồng   |
    | KVND  | 1000 VND   | 
    | USD  | 美金   |
    | USDT  | 泰達幣   |

## API Spec

### Member&Agent

Provide creating member, member login, managing member or agent data, please refer to [Member&Agent API](https://staging-agent.olacak.live/swagger/public/index.html?lang=en#/Member%2FAgent)

### Wager

Asynchronous, about 5 mins delay. Our system will merge bets in the same member and game round(run) to a wager. Only settled wagers able to be found. Please refer to [Wager API](https://staging-agent.olacak.live/swagger/public/index.html?lang=en#/Wager)

### Transfer

Only transfer wallet agents available, please refer to [Transfer API](https://staging-agent.olacak.live/swagger/public/index.html?lang=en#/Transfer)

### Seamless2.0

- Only Seamless wallet agents available. The 2.0 Version only needs to implement two callbacks which are focus on the balance changing. The encryption rule is also simpler and more flexible.
- Refer to the [SeamlessWallet API 2.0](../../SeamlessWalletAPI2.0/SeamlessWalletAPI-2.0.md) documents to implement all of seamless callbacks.
- Please setting the seamless callbacks(getBalance/updateBalance) on the System Management/Personal Setting page of the backstage.
- Because of avoid settling repeatedly, our system only invokes the callback once when updating balance. If there is timeout or something unexpected response, our system won't re-invoke again. So please check the failed cases from [GetRequestHistoryByTime api](https://staging-agent.olacak.live/swagger/public/index.html?lang=en#/Seamless2.0/post_api_keno_api_xg_casino_GetRequestHistoryByTime) regularly, and according to the `RequestJson` in response to fix the balance of members.  
- There are some test cases on the Developer Zone/Seamless Callbacks page. We'll send the request from our seamless server to your system when clicking the button in the test case. This is only for testing on the staging env, and there is no real bet record in our system.
- Please provide test account on staging(test) environment of your system after completing all of seamless callbacks. We need to test its working fine on staging. 

### Seamless1.1(EOL)

- The 1.1 version will no longer be updated, please upgrade to the 2.0 version.
- Only Seamless wallet agents available. 
- Refer to the [How to handle the balance of members](../../SeamlessWalletAPI1.x/handle-balance.md) and [XG Seamless Wallet API ](https://github.com/jacky5823a/docs/blob/master/SeamlessWalletAPI1.x/SeamlessWallet1.1.md) documents to implement all of seamless callbacks.
- Please setting the seamless callbacks(balance/bet/settle/rollback) on the System Management/Personal Setting page of the backstage.
- If the game round canceled before settlement, our system will invoke the rollback callback.
- If the bet canceled after settlement, our system doesn't inform your system by rollback callback. Your system needs to check the `ModifiedStatus` of bet by [GetReplenishmentByTime api](https://staging-agent.olacak.live/swagger/public/index.html?lang=en#/Seamless1.x/post_api_keno_api_xg_casino_GetReplenishmentByTime) regularly and handle the member's balance.
- There are some test cases on the Developer Zone/Seamless Callbacks page. We'll send the request from our seamless server to your system when clicking the button in the test case. This is only for testing on the staging env, and there is no real bet record in our system.
- Please provide test account on staging(test) environment of your system after completing all of seamless callbacks. We need to test its working fine on staging.

## Table Limit(Bet Limit)

- Different currency has different table limit ids. The member able to switch the table limit in the game which be set by the table limit ids. The bet chips would be changed by the different min/max limits. Please refer to [this doc](./table-limit.md) to get the table limit ids.
- The Table Limit able to be set by the backstage or the apis

### Backstage
- Preset table limit: Only be using by invoking CreateMember api. **The table limit of members wouldn't change when modifying the preset table limit.** The Table Limit Setting on the System Management/Personal page provides the personal preset table limit setting. And the Table Limit Setting on the Account Management/Agent Management page provides the preset table limit setting of the downline agents. Every agent allows to set the preset table limit by each currency, and also allows to set multiple limit ids to be the preset table limit.    
- Get/Set the table limit of member: The Account Management/Member Management page shows the table limit of your and your downline agents' members. But only allow to modify the table limit of your members.

### APIs
- POST /api/keno-api/xg-casino/CreateMember: The LimitStake param is optional and able to put multiple table limit ids in the LimitStake. If there is no the LimitStake param when invoking the CreateMember api, our system will set the **preset table limit** to the new member
- GET /api/keno-api/xg-casino/Template: Fetch the specific member’s table limit
- POST /api/keno-api/xg-casino/Template: Set the specific member’s table limit. Putting the table limit ids in the Template param, it would **overwrite** the original table limit of the specific member
- POST /api/keno-api/xg-casino/AllPlayersTemplate: Modify all member’s table limits of the specific currency one time

