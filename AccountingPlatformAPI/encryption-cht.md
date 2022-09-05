# Key 產生方式

Key = {6個任意字元} + MD5(所有請求參數串 + KeyG) + {6個任意字元}

- 任意字元
  任意填入，前後各 6 字元不需相同，驗證時會去頭尾後比對中間加密部份
- 請求參數串
  依各 API 方法參數列表，務必**按請求參數順序**以 `parameter1=value1&parameter2=value2&...` 格式串起，API 端將會檢查請求參數串內容及順序，以確保請求參數未被竄改
  EX:
    - 如果 GET query string 是
      `Account=Test1&GameId=A01&Lang=zh-CN&AgentId=10081`
      請求參數串即為：
        ```bash
        "Account=Test1&GameId=A01&Lang=zh-CN&AgentId=10081"
        ```
    - 如果 POST request body 是
        ```json
        {
          "Account": "Test1",
          "GameId": "A01",
          "Lang": "zh-CN",
          "AgentId": "10081"
        }
        ```
        請求參數串即為：
        ```bash
        "Account=Test1&GameId=A01&Lang=zh-CN&AgentId=10081"
        ```
- KeyG
    ```bash
    KeyG = MD5(DateTime.now().setZone("UTC-4").toString("yyMMd") + 公鑰(AgentId) + 私鑰(AgentKey))
    ```
    - 日期為當下 UTC-4 時間
    - 日期格式為 `yyMMd`，例如：
      2018/2/7 => 18027, 7 號是 `7` 而不是 `07`
      2018/2/18 => 180218
## 範例

以下使用 nodejs 及 [Luxon](https://github.com/moment/luxon) 時間套件進行加密範例

```javascript=
const agentId = 'Your AgentId';
const agentKey = 'Your AgentKey';

let requestData = {
    'parameter1': 'value1',
    'parameter2': 'value2',
    'parameter3': 'value3'
};

const date = DateTime.now().setZone('UTC-4').toFormat('yyMMd');
const keyG = md5(date + agentId + agentKey);

let paramsString = '';
for (const [key, value] of Object.entries(requestData)) {
  if (paramsString !== '') {
    paramsString += '&';
  }
  paramsString += key + '=' + value;
}
// 帶入 Key
requestData.Key = Math.random().toString(36).substr(2,6) + md5(paramsString + keyG) + Math.random().toString(36).substr(2,6));

// 發請請求
...

```
