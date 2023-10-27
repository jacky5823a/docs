# Seamless Wallet API 1.1(EOL)

**NOTICE: The 1.1 version will no longer be updated, please upgrade to the 2.0 version.**

## GetBalance

#### Request

Headers

|  Column | Format | Description |
| -------- | -------- | -------- |
| X-API-KEY     | string     | provided by the game side     |
| X-API-TOKEN     | string     | [Encryption](#generate-x-api-token)    |

Body

|  Column | Format | Description |
| -------- | -------- | -------- |
| requestId     | string     |  unique key by request  |
| user     | string     | player's account     |

#### Response

Headers

|  Column | Format | Description |
| -------- | -------- | -------- |
| X-API-KEY     | string     | provided by the game side     |
| X-API-TOKEN     | string     | [Encryption](#generate-x-api-token)    |

Body

|  Column | Format | Description |
| -------- | -------- | -------- |
| requestId     | string     |  must same as request  |
| status     | string     | if process success, return ok    |
| user     | string     | player's account     |
| currency     | string     | player's currency     |
| balance     | decimal(20, 4)     | player's balance     |

Request example
```json
{
  "requestId": "6f1cd735-2fea-4079-baa0-9b0afc235358",
  "user": "jacky11"
}
```

Response example
```json
{
  "requestId": "6f1cd735-2fea-4079-baa0-9b0afc235358",
  "status": "ok",
  "user": "jacky11",
  "currency": "USD",
  "balance": 851100.0000
}
```

## Bet
> We will send each request by bet, one request one bet.

#### Request
> For security reason, response should return back in **3** seconds, if not, task will cancel.
> We will record timeout message in [Message] such as  **[Response Timeout] Response time over 3 seconds, Task Canceled.**
Headers

|  Column | Format | Description |
| -------- | -------- | -------- |
| X-API-KEY     | string     | provided by the game side     |
| X-API-TOKEN     | string     | [Encryption](#generate-x-api-token)    |

Body

|  Column | Format | Description |
| -------- | -------- | -------- |
| requestId     | string     |  unique key by request  |
| user     | string     | player's account     |
| currency     | string     | player's currency     |
| amount     | decimal(20, 4)     | player bet amount    |
| gameType     | string     | game type of bet, example: Baccarat  |
| table     | string     | table of betting table, example: A  |
| round     | int     | round of table, example: 1608715823  |
| run     | int     | run of table, example: 12  |
| bet     | string     | betting area, example: Player  |
| betTime     | datetime     | betting time (yyyy/MM/dd HH:mm:ss), example: 2022/01/25 13:55:25  |
| transactionId     | Guid     | uniqe id of each betting process  |

#### Response

Headers

|  Column | Format | Description |
| -------- | -------- | -------- |
| X-API-KEY     | string     | provided by the game side     |
| X-API-TOKEN     | string     | [Encryption](#generate-x-api-token)    |

Body

|  Column | Format | Description |
| -------- | -------- | -------- |
| requestId     | string     |  must same as request  |
| status     | string     | if process success, return ok    |
| user     | string     | player's account     |
| currency     | string     | player's currency     |
| balance     | decimal(20, 4)     | player's balance     |
| transactionId     | Guid     | transactionId from request  |

Request example
```json
{
  "requestId": "6f1cd735-2fea-4079-baa0-9b0afc235358",
  "user": "jacky11",
  "currency": "USD",
  "amount": 400.0000,
  "gameType": "Baccarat",
  "table": "A",
  "round": 1608715823,
  "run": 12,
  "bet": "Player",
  "betTime": "2022/01/25 13:55:25",
  "transactionId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

Response example
```json
{
  "status": "ok",
  "requestId": "6f1cd735-2fea-4079-baa0-9b0afc235358",
  "user": "jacky11",
  "balance": 855500.0000,
  "currency": "USD",
  "transactionId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

## Settle
>If run not cancel, the bet would be settled at the end of game round.
#### Request
> For security reason, response should return back in **3** seconds, if not, task will cancel.
> We will record timeout message in [Message] such as  **[Response Timeout] Response time over 3 seconds, Task Canceled.**
> We will send each request, which request includ mutiple players betting in same run.
Headers

|  Column | Format | Description |
| -------- | -------- | -------- |
| X-API-KEY     | string     | provided by the game side     |
| X-API-TOKEN     | string     | [Encryption](#generate-x-api-token)    |

Body

|  Column | Format | Description |
| -------- | -------- | -------- |
| gameResult     | string array  |  game result of game, example: ["H6","SJ","CK","DQ","","S6"]  |
| requestId     | string     |  unique key by request  |
| settleItems     | [SettleItem](#settleitem)[]|[SettleItem](#settleitem) Array|
| settleTime     | datetime     | settle time (yyyy/MM/dd HH:mm:ss), example: 2022/01/25 13:55:25  |

*Amount = Sum(betAmount+settleAmount)*

*gameResult: spade 黑桃 => S, heart 紅心 => H, diamond 方塊 => D, club 梅花 => C*

#### SettleItem
| Column | Format | Description |
| -------- | -------- | -------- |
| user     | string     | player's account     |
| currency     | string     | player's currency     |
| amount     | decimal(20, 4)     | win or loss amount     |
| transactionId     | Guid     | uniqe id of each betting process  |
| wagerId     | string     | Bet ticket , equal  BetFormId |

#### Response

Headers

|  Column | Format | Description |
| -------- | -------- | -------- |
| X-API-KEY     | string     | provided by the game side     |
| X-API-TOKEN     | string     | [Encryption](#generate-x-api-token)    |

Body

|  Column | Format | Description |
| -------- | -------- | -------- |
| requestId     | string     |  must same as request  |
| status     | string     | if process success, return ok    |
| settleUserBalanceList     | [SettleUserBalanceList](#settleuserbalancelist)[]|[settleUserBalanceList](#settleuserbalancelist) Array|

#### SettleUserBalanceList
| Column | Format | Description |
| -------- | -------- | -------- |
| user     | string     | player's account     |
| currency     | string     | player's currency     |
| balance     | decimal(20, 4)     | player's balance     |


Request example
```json
{
  "gameResult": "[\"H6\",\"SJ\",\"CK\",\"DQ\",\"\",\"S6\"]",
  "requestId": "64d92694-b78f-4748-826d-7a3f96c1610f",
  "settleItems": [
    {
      "amount": 800,
      "currency": "USD",
      "transactionId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "user": "jacky11",
      "wagerId": "P81RFZ157G77TFF4U81"
    },
    {
      "amount": 0,
      "currency": "USD",
      "transactionId": "152c1c9f-6662-498a-ae1b-73bb706de0b0",
      "user": "jacky22",
      "wagerId": "P81RFZ157G77TFF4U81"
    }
  ],
  "settleTime": "2021-08-30T16:41:27.0531715+08:00"
}
```

Response example
```json
{
  "requestId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "status": "ok",
  "settleUserBalanceList": [
    {
      "user": "jacky11",
      "currency": "USD",
      "balance": 856300.0000
    },
    {
      "user": "jacky22",
      "currency": "USD",
      "balance": 665000.0000
    }
  ]
}
```

## Rollback
>Bet fail or Run cancel will send rollback request to revert player's balance.
#### Request

Headers

|  Column | Format | Description |
| -------- | -------- | -------- |
| X-API-KEY     | string     | provided by the game side     |
| X-API-TOKEN     | string     | [Encryption](#generate-x-api-token)    |

Body

|  Column | Format | Description |
| -------- | -------- | -------- |
| requestId     | string     |  unique key by request  |
| user     | string     | player's account     |
| transactionId     | Guid     | uniqe id which bet need to rollback |

#### Response

Headers

|  Column | Format | Description |
| -------- | -------- | -------- |
| X-API-KEY     | string     | provided by the game side     |
| X-API-TOKEN     | string     | [Encryption](#generate-x-api-token)    |

Body

|  Column | Format | Description |
| -------- | -------- | -------- |
| requestId     | string     |  must same as request  |
| status     | string     | if process success, return ok    |
| user     | string     | player's account     |
| currency     | string     | player's currency     |
| balance     | decimal(20, 4)     | player's balance     |
| transactionId     | Guid     | uniqe id which bet need to rollback  |

Request example
```json
{
  "requestId": "6f1cd735-2fea-4079-baa0-9b0afc235358",
  "user": "jacky11",
  "transactionId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

Response example
```json
{
  "status": "ok",
  "requestId": "6f1cd735-2fea-4079-baa0-9b0afc235358",
  "user": "jacky11",
  "balance": 855500.0000,
  "currency": "USD",
  "transactionId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

## Generate X-API-TOKEN

We provide X-API-TOKEN generation plugin:

[JAVA Token](https://gitlab.com/token-library/java/-/packages/17448487)

[PHP Token](https://gitlab.com/token-library/php-token)

[Node.js Token](https://gitlab.com/token-library/js-token)

[C# Token](https://gitlab.com/token-library/csharp-token)

For languages that are not yet supported, please refer to the following generate process：

### 流程生成條件

signtext = apikey+jsonbody+secret

token = SHA(signtext) 轉 Base-64 格式 轉小寫

1. Json字串格式為 Properties Key 升序
2. 若其屬性值為空或null則忽略
3. decimal欄位皆必須精準至小數後四位，example 200.0000 

#### Request Content
```json!
jsonbody = {"requestId":"736b0822-baf0-4227-972d-a7b935129683","settleUserBalanceList":[{"balance":3830.0000,"currency":"NTD","user":"zaqx1994"}],"status":"ok"}
```

apiKey = a778ec58-b9c2-419f-91dc-b0c1ed10873e

secret = 10b8ac75-4cac-4a77-a921-9a7c51ae1db6

```json!
signtext = a778ec58-b9c2-419f-91dc-b0c1ed10873e{"requestId":"736b0822-baf0-4227-972d-a7b935129683","settleUserBalanceList":[{"balance":3830.0000,"currency":"NTD","user":"zaqx1994"}],"status":"ok"}10b8ac75-4cac-4a77-a921-9a7c51ae1db6
```

token = dvzaj57uxbmbeo2escgmynmzihq=

### C# Example

```csharp=
public static string EncryptBySHA1(string apiKey,string secret, string jsonBody)
{
    string result = null;
    using (var sha = SHA1.Create())
    {
        var bytes = Encoding.UTF8.GetBytes($"{apiKey}{jsonBody}{secret}");
        var computedBytes = sha.ComputeHash(bytes);
        result = Convert.ToBase64String(computedBytes).ToLower();
    }
    return result;
}
```

### PHP Example
Sha1(signtext) 轉 base6

```php!
strtolower(base64_encode(hex2bin(sha1($this->agent->uid . json_encode($this->signtext) . $this->agent->privateKey))))
```
