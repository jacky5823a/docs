# SeamlessWallet API 2.0

![](https://i.imgur.com/ISO1p1X.png)

## GetBalance
HTTP Request Method: Post
Our system will invoke api to get the balance when the member enters to our game.

### Request
| Column | Format | Encrypt | Description |
| -------- | -------- | -------- | -------- |
| JsonText| string | Y | request object json string |
| RequestId| string | N | unique key by request |
| UnixTimeSeconds| long | N | UnixTime format |
| Signature| string | N | [Encryption](#encryption-of-request)|

#### JsonText Content
| Column | Format |Description |
| -------- | -------- | -------- |
| Account| string |player's account|

Content to Json
```json
{
  "Account": "player1"
}
```

```json
{
  "JsonText": "{\"Account\": \"player1\"}",
  "RequestId": "a501caf2-ac17-4afc-83e3-8712a169ca7e",
  "UnixTimeSeconds": 1647920033,
  "Signature": "8c2d7564909af5667098fa9baa8b97ef"
}
```

### Response
> For security reason, response should return back in **3** seconds, if not, task will cancel.

| Column | Format | Description |
| -------- | --------  | -------- |
| Balance| decimal | player's balance|
| UpdateTime| long  | balance update time (UnixTime format)|
| ErrorCode| int | Success = 1, Fail = 2 |

```json
{
  "Balance": 500,
  "UpdateTime": 1647920033,
  "ErrorCode": 1
}
```

## Update Balance
HTTP Request Method: Post
### Request
| Column | Format | Encrypt | Description |
| -------- | -------- | -------- | -------- |
| JsonText| string | Y |  request object json string |
| RequestId| string | N | unique key by request|
| UnixTimeSeconds| long | N | unix timestamp |
| Signature| string | N | Signature|

#### JsonText Content
| Column | Format |Description |
| -------- | -------- | -------- |
| Account | string | player's account |
| BetFormId | long | *Settlement only* |
| Transactions| [TransactionItem](#transactionItem)[]|[TransactionItem](#transactionItem) Array|

#### TransactionItem
| Column | Format | Description |
| -------- | -------- | -------- |
| TransactionId | Guid| |
| Amount| decimal| Amount need add or cost (+-) |
| OperationCode| int | Bet = 1, Settle = 2, Rollback = 3 |

#### Request
```json
{
  "JsonText": "{\"Account\":\"player1\",\"Transactions\":[{\"TransactionId\":\"566105bf-2349-439b-ac14-00becdcec0cc\",\"Amount\":-100,\"OperationCode\":1}]}",
  "RequestId": "a501caf2-ac17-4afc-83e3-8712a169ca7e",
  "UnixTimeSeconds": 1647920033,
  "Signature": "8c2d7564909af5667098fa9baa8b97ef"
}
```

### Response

> For security reason, response should return back in **3** seconds, if not, task will cancel.
> We will notify timeout message in [ResponseJson] such as  **[Response Timeout] Response time over 3 seconds, Task Canceled.**
> 
| Column | Format | Description |
| -------- | --------  | -------- |
| Balance| decimal | player's balance|
| UpdateTime| long  | balance update time (UnixTime format)|
| ErrorCode| int | Success = 1, Fail = 2 |

```json
{
  "Balance": 500,
  "UpdateTime": 1647920033,
  "ErrorCode": 1
}
```
#### ErrorCode=2
We suggest return user balance before the action of Update Balance.
But there is some situations, we suggest return 0 of balance.
1. When player not exsit, balance return 0.
2. When Signature verify fail, balance return 0.
 
## Example of JsonText Content

### Betting case
> We will send each request by bet, one request one bet.
```json
{
  "Account": "player1",
  "Transactions": [
    {
      "TransactionId": "566105bf-2349-439b-ac14-00becdcec0cc",
      "Amount": -100,
      "OperationCode": 1
    }
  ]
}
```

### Settlement case
If run not cancel, the bet would be settled at the end of game round. There are two kinds of situations which is winning or losing for a single bet.

Amount = Sum(betAmount+settleAmount)
> We will send each request by player, one request one player in one round.
#### Win
```json
{
  "Account": "player1",
  "BetFormId": 111,
  "Transactions": [
    {
      "TransactionId": "566105bf-2349-439b-ac14-00becdcec0cc",
      "Amount": 200,
      "OperationCode": 2
    },
    {
      "TransactionId": "06f9baf6-6b2c-42dd-9b6c-4cd0fdc05cd1",
      "Amount": 200,
      "OperationCode": 2
    }
  ]
}
```
#### Lose
```json
{
  "Account": "player2",
  "BetFormId": 111,
  "Transactions": [
    {
      "TransactionId": "566105bf-2349-439b-ac14-00becdcec0cc",
      "Amount": 0,
      "OperationCode": 2
    },
    {
      "TransactionId": "06f9baf6-6b2c-42dd-9b6c-4cd0fdc05cd1",
      "Amount": 0,
      "OperationCode": 2
    }
  ]
}
```

### Rollback case

There are three situation will trigger rollback case, our system will invoke api to your system.
1. The game round is canceled, this happen in game or after game is settled.
2. The game round is modified, this happen after game is settled.

#### Win to lose
```json
{
  "Account": "player1",
  "BetFormId": 111,
  "ModifiedStatus": "modified",
  "Transactions": [
    {
      "TransactionId": "566105bf-2349-439b-ac14-00becdcec0cc",
      "Amount": -200,
      "OperationCode": 3
    },
    {
      "TransactionId": "06f9baf6-6b2c-42dd-9b6c-4cd0fdc05cd1",
      "Amount": -200,
      "OperationCode": 3
    }
  ]
}
```
#### Lose to win
```json
{
  "Account": "player2",
  "BetFormId": 111,
  "ModifiedStatus": "modified",
  "Transactions": [
    {
      "TransactionId": "566105bf-2349-439b-ac14-00becdcec0cc",
      "Amount": 200,
      "OperationCode": 3
    },
    {
      "TransactionId": "06f9baf6-6b2c-42dd-9b6c-4cd0fdc05cd1",
      "Amount": 200,
      "OperationCode": 3
    }
  ]
}
```
#### Sample of Rollback scenario
If a member bets $100 which odds is 1 to 1, here is rollback scenario

**Modified**

| Amount | Lost to Win | Win to Lose | Tie to Win | Tie to Lose | Win to Tie | Lose to Tie |
| -------- | -------- | -------- |  -------- | -------- | -------- | -------- |
| Bet | 100 | 100 | 100 | 100 | 100 | 100 | 100 |
| Settle | 0 | 200 | 100 | 100 | 200 | 0 |
| Rollback | 200 | -200 | 100 | -100 | -100 | 100 |

**Canceld**
| Amount | Win to Cancel | Lose to Cancel | Tie to Cancel|
| -------- | -------- | -------- |  -------- |
| Bet | 100 | 100 | 100 |
|Settle | 200 | 0 | 100 |
| Rollback | -100 | 100 | 0 |

## Encryption of Request
MD5(AgentSecret + UnixTimeSeconds + JsonText)
> AgentSecret is AgentKey.
```csharp
var agentSecret = "exampleSecrect";
var jsonText = "{\"Account\":\"player1\",\"Transactions\":[{\"TransactionId\":\"566105bf-2349-439b-ac14-00becdcec0cc\",\"Amount\":-100,\"OperationCode\":1},{\"BetListId\":8889,\"Amount\":-100,\"OperationCode\":1}]}";
//jsonText is {"Account":"player1","Transactions":[{"TransactionId":"566105bf-2349-439b-ac14-00becdcec0cc","Amount":-100,"OperationCode":1},{"BetListId":8889,"Amount":-100,"OperationCode":1}]}
var unixTimeSeconds = 1647920033;
 var signature = MD5($"{agentSecret}{unixTimeSeconds}{jsonText}");
//signature is 21c66cb218146d2c6c8a576bd0a8982d
```