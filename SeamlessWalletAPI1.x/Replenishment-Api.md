# Replenishment Api

遊戲方提供給錢包方請求查詢單一錢包注單資訊Api

若其屬性值為空或null則忽略
decimal欄位皆必須精準至小數後四位，example 200.0000
請求簽名
針對queryString，固定的排序，生成token
回應簽名
針對回應內容Json序列化，生成token，Json字串格式為 Properties Key 升序

Token驗證方式

我們提供快速生成 X-API-TOKEN 的套件，使用方式參見各專案，目前支援以下語言:

[JAVA XG Token](https://gitlab.kaixi.cc/api-libaray/java-xg-token)
[PHP XG Token](https://gitlab.kaixi.cc/api-libaray/php-xg-token)
[Node.js XG Token](https://gitlab.kaixi.cc/api-libaray/js-xg-token)
[C# XG Token](https://gitlab.kaixi.cc/api-libaray/csharp-xg-token)
如果尚未支援的語言或是想自行處理，可參考下列流程生成：

## Get

#### Request

|  Column | Format | Description |
| -------- | -------- | -------- |
| X-API-KEY     | string     | provided by the game side     |
| X-API-TOKEN     | string     | [Encryption](#generate-token)    |
| gameType | string     |  [GameType](https://github.com/jacky5823a/docs/blob/master/AccountingPlatformAPI/reference-en.md#game-types)  |
| startTime  | date     | 搜尋起始時間 yyyy/MM/dd HH:mm:ss    |
| endTime   | date     | 搜尋結束時間 yyyy/MM/dd HH:mm:ss    |
| pageLimit    | number     | 單頁限制數量 0 < Value <= 10000   |
| pageNumber     | number     | 頁數 Value > 0  |
| isNormal     | boolean     | optional, 是否回傳包含結算成功資料,可選擇不傳,若傳值只接收true若此欄位不添加,則預設只回傳 Modified 及 Canceled 資料  |

#### Response

```json
{
  "betList": [
    {
      "bet": "Baccarat_Banker",
      "betAmount": 20000,
      "betTime": "2021/06/12 22:55:53",
      "gameResult": "[\"C7\",\"H6\",\"H2\",\"D8\",\"\",\"\"]",
      "gameType": "Baccarat",
      "isRollack": false,
      "isSettle": true,
      "modifiedStatus": "Canceled",
      "round": 1612341153,
      "run": 51,
      "settleAmount": 0,
      "settleTime": "2021/07/05 03:18:51",
      "table": "R",
      "transactionId": "c2a95054-1bea-4e53-bd2d-48d271bc90be",
      "wagerId": "P81RFZ157G77TFF4U81"
    },
    {
      "bet": "Baccarat_PlayerPair",
      "betAmount": 1000,
      "betTime": "2021/06/14 18:08:58",
      "gameResult": "[\"S9\",\"H9\",\"H3\",\"H0\",\"\",\"\"]",
      "gameType": "Baccarat",
      "isRollack": false,
      "isSettle": true,
      "round": 1612341153,
      "run": 51,
      "settleAmount": 0,
      "settleTime": "2021/07/03 22:19:30",
      "table": "R",
      "transactionId": "66ade8a1-7c13-4429-b7b7-f061e66b6d7e",
      "wagerId": "P81RFZ157G77TFF4U81",
      "modifiedStatus": "Canceled"
    }
  ],
  "pagination": [
    {
      "pageLimit": 20,
      "totalNumber": 2,
      "totalPages": 1
    }
  ]
}
```

## Generate Token
> 排序字串(順序固定)
>
requestOrderedString = endTime=2021/07/18 21:17&gameType=Baccarat&isNormal=true&pageLimit=20&pageNumber=1&startTime=2021/06/26 20:15:00

> 若isNormal=False或沒傳入則為

requestOrderedString = endTime=2021/07/18 21:17&gameType=Baccarat&pageLimit=20&pageNumber=1&startTime=2021/06/26 20:15:00

> 若isNormal=true為

requestOrderedString = endTime=2021/07/18 21:17&gameType=Baccarat&isNormal=true&pageLimit=20&pageNumber=1&startTime=2021/06/26 20:15:00

Sha1(apikey+requestOrderedString+secret) 轉 base64 小寫

### C#範例程式碼
```
public static string EncryptBySHA1(string apiKey,string secret, string needEncryptString)
{
    string result = null;
    using (var sha = SHA1.Create())
    {
        var bytes = Encoding.UTF8.GetBytes($"{apiKey}{needEncryptString}{secret}}");
        var computedBytes = sha.ComputeHash(bytes);
        result = Convert.ToBase64String(computedBytes).ToLower();
    }
    return result;
}
```
### example

> 請求Get Url 為 =>

http://15.164.219.147:80/api/Replenishment/Get?gameType=Baccarat&startTime=2021/06/26 20:15:00&endTime=2021/07/18 21:17:00&pageLimit=20&pageNumber=1&isNormal=true

> 即參數為
> 
```
gameType=Baccarat
startTime=2021/06/26 20:15:00
endTime=2021/07/18 21:17:00
pageLimit=20
pageNumber=1
isNormal=true(注意請以小寫加密)
apikey=3fa85f64-5717-4562-b3fc-2c963f66afa6
secret=a73a9aea-e5a3-4fe7-9a32-7e48a66f611e
```

組成排序簽名字串
requestOrderedString = endTime=2021/07/18 21:17:00&gameType=Baccarat&isNormal=true&pageLimit=20&pageNumber=1&startTime=2021/06/26 20:15:00

signText = 3fa85f64-5717-4562-b3fc-2c963f66afa6endTime=2021/07/18 21:17:00&gameType=Baccarat&isNormal=true&pageLimit=20&pageNumber=1&startTime=2021/06/26 20:15:00a73a9aea-e5a3-4fe7-9a32-7e48a66f611e

token = sha1(signText) 轉 base64 小寫

token = p7yycr7qgr2sxmg+ktompat2qj8=
