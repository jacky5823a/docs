# How to handle the balance of members for Seamless Wallet(EOL)

**NOTICE: The 1.1 version will no longer be updated, please upgrade to the 2.0 version.**

This doucment provide a simple case to explain how the seamless callbacks and replenishment api work of our system.


## Seamless callbacks

Please setting the seamless callbacks(balance/bet/settle/rollback) on backstages. And follow the swagger document to implement all of apis.


### Balance

Our system will invoke `/user/balance` api to get the balance when the member enters to our game.

### Betting
If a member has $1500 balance. Then he bets $500 on the player hand which odds is 1 to 1, our system will invoke `/transaction/bet` api
 to your system. The request such as this

```json
{
  "amount": 500,
  "bet": "Baccarat_Player",
  "betTime": "2022/02/25 17:30:24",
  "currency": "USD",
  "gameType": "Baccarat",
  "requestId": "351cf430-480b-4a67-9372-1bb0fd64bb28",
  "round": 1645780474,
  "run": 26,
  "table": "H",
  "transactionId": "b9548386-7623-4fa0-af89-2201ba68bc21",
  "user": "uu001"
}
```

Your system needs to take off the bet amount from the member, so the balance of the member will change into $1000

### Rollback

If the game round is canceled before settlement, our system will invoke `/transaction/rollback` api to your system. The request such as this

```json
{
  "requestId": "6f1cd735-2fea-4079-baa0-9b0afc235358",
  "user": "uu001",
  "transactionId": "b9548386-7623-4fa0-af89-2201ba68bc21"
}
```

According to the transactionId in request body, Your system needs to return the bet amount to the member. In the above example, the balance of the member will change into $1500

### Settlement

If not rollback, the bet would be settled at the end of game round. There are two kinds of situations which is winning or losing for a single bet.

#### The winning case

Your system will receive the `/transaction/settle` request from our side, such as this

```json
{
  "requestId": "a27281b0-679b-4c0d-99b4-b1926aa15f31",
  "settleItems": [
    {
      "amount": 1000,
      "currency": "USD",
      "transactionId": "b9548386-7623-4fa0-af89-2201ba68bc21",
      "user": "uu001",
      "wagerId": 43969435
    }
  ]
}
```

Because the odds is 1 to 1, so the amount in the `/transaction/settle` request would be 1000. Your system needs to pay the amount $1000 to the member, the balance of the member will change into $2000

#### The losing case

Your system will receive the `/transaction/settle` request from our side, such as this

```json
{
  "requestId": "a27281b0-679b-4c0d-99b4-b1926aa15f31",
  "settleItems": [
    {
      "amount": 0,
      "currency": "USD",
      "transactionId": "b9548386-7623-4fa0-af89-2201ba68bc21",
      "user": "uu001",
      "wagerId": 43969435
    }
  ]
}
```


The amount in the `/transaction/settle` request would be 0, so your system won't pay any amount to the member


## Replenishment

If there are something unexpected errors or 
temporary maintenance, we are probably going to cancel the game round or modify the game result after settlement. This situation would affect the balance of members. Your system able to handle this situation by manual or by implementing the replenishment api we providing.

**Note: our system doesn't inform your system if the bet is Canceled or Modified after settlement**

If your system wants to handle it by replenishment api, it's necessary to store the relation between transactionId, bet amount and settle amount which members have bet. Also needs to implement replenishment api frequently to check `ModifiedStatus` in settleItems property. Your system needs to handle the `ModifiedStatus` is `Canceled` and `Modified` cases. The response of replenishment api such as this

```json
{
  "ErrorCode": 0,
  "Message": "",
  "Data": {
    "Pagination": {
      "CurrentPage": 1,
      "TotalPages": 1,
      "PageLimit": 100,
      "TotalNumber": 2
    }      
    "Result": [
      {
        "Bet": "Baccarat_Player",
        "BetAmount": 500,
        "BetTime": "2022-02-25T18:10:56",
        "GameResult": "[\"C1\",\"C0\",\"H6\",\"CJ\",\"\",\"H6\"]",
        "GameType": 1,
        "IsRollback": false,
        "IsSettle": true,
        "ModifiedStatus": "Canceled",
        "Round": 1645780474,
        "Run": 26,
        "SettleAmount": 1000,
        "SettleTime": "2022-02-25T18:13:42",
        "Table": "H",
        "TransactionId": "b9548386-7623-4fa0-af89-2201ba68bc21",
        "WagerId": 43969435
      },
      {
        "Bet": "Baccarat_Player",
        "BetAmount": 500,
        "BetTime": "2022-03-01T16:28:17",
        "GameResult": "[\"HJ\",\"S8\",\"S3\",\"HQ\",\"\",\"\"]",
        "GameType": "Baccarat",
        "IsRollback": false,
        "IsSettle": true,
        "ModifiedStatus": "Modified",
        "Round": 1646121023,
        "Run": 56,
        "SettleAmount": 0,
        "SettleTime": "2022-03-01T16:30:45",
        "Table": "F",
        "TransactionId": "88d6b060-6538-4db4-b503-23ba91961b16",
        "WagerId": 43969489
      }
    ]
  }
}
```

The following shows some situations how the balance is handled:

### ModifiedStatus is `Canceled`

#### The winning case

There is an example data your system stored in the above example for winning case.

| transactionId | betAmount | settleAmount |
| -------- | -------- | -------- |
| xxxxxxx     | 500     | 1000     |

According to the relation between transactionId, bet amount and settle amount your system stored, your system needs to take off the settle amount and return the bet amount to the member. So the balance of member would change into $1500 ($2000 - $1000 + $500 = $1500) 


#### The losing case
There is an example data your system stored in the above example for losing case.

| transactionId | betAmount | settleAmount |
| -------- | -------- | -------- |
| xxxxxxx     | 500     | 0     |

Because of the settleAmount is 0 for the losing case, just handle it as same as the winning case. Take off the settle amount and return the bet amount to the member. So the balance of member would change into $1500 ($1000 - $0 + $500 = $1500) 


### ModifiedStatus is `Modified`

If ModifiedStatus is Modified, your system needs to compare the SettleAmount of the bet in the response of replenishment api.

#### The winning to losing case

There is an example data your system stored in the above example for winning case.

| transactionId | betAmount | settleAmount |
| -------- | -------- | -------- |
| xxxxxxx     | 500     | 1000     |

If the `SettleAmount` of the bet is 0 which means the game result of bet changes winning to losing. Your system needs to take off the settle amount which your system stored. So the balance of member would change into $1000 ($2000 - $1000)

#### The losing to winning case

There is an example data your system stored in the above example for losing case.

| transactionId | betAmount | settleAmount |
| -------- | -------- | -------- |
| xxxxxxx     | 500     | 0     |

If the `SettleAmount` of the bet is 1000 which means the game result of bet changes losing to winning. Your system needs to pay the SettleAmount from the replenishment api. So the balance of member would change into $2000 ($1000 + $1000)

#### No changed case

If the `SettleAmount` of the bet is as same as the settle amount which your system stored. Your system doesn't need to do anything

## Testing

Please provide test account on staging(test) environment of your system after completing all of seamless callbacks. We need to test its working fine on staging.

