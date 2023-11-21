# HMAC Signature

新版 api 採用 HMAC(Hash-based Message Authentication Code) 機制驗證請求參數，Client 端每筆 request 參數透過公私鑰進行 SHA256 Hash，產生唯一的 HMAC Signature，Server 端對 Signature 進行驗證。

我們提供快速生成 `Signature` 的套件，使用方式參見各專案，目前支援以下語言:

- [PHP Token](https://gitlab.com/token-library/php-token)

如果尚未支援的語言或是想自行處理，請按照下方 [API HMAC Authentication](#api-hmac-authentication) 步驟，另外後台 開發者專區/API Signature 產生器 頁面可自行比對產出的 `Signature` 是否正確

## API HMAC Authentication

### Headers
- X-Agent-Id: Agent ID
- X-Agent-Timestamp: 請求當下 Unix Timestamp(秒)，必須在 15 分鐘內
- X-Agent-Signature: HMAC Signature

#### Hmac Signature

- Payload:
  - GET: query string, ex: `account=Test1&lang=zh-CN`
  - POST: JSON encode the request body, ex: `{"account":"Test1","lang":"zh-CN"}`
- Message = {Agent ID} + {Payload} + {Request Unix Timestamp(秒)}
- Signature = Base64(HMAC-SHA-256({Agent Key}, {Message}))

### 範例

以下使用 nodejs 及 [crypto-js](https://www.npmjs.com/package/crypto-js) 套件產生 Signature

```javascript
const axios = require('axios');
const base64 = require('crypto-js/enc-base64');
const hmacSha256 = require('crypto-js/hmac-sha256');

const agentId = 'Your AgentId';
const agentKey = 'Your AgentKey';

const requestData = {
    'parameter1': 'value1',
    'parameter2': 'value2',
    'parameter3': 'value3'
};
const payload = JSON.stringify(requestData);
const requestTimestamp = Math.floor(Date.now() / 1000);

const message = agentId + payload + requestTimestamp;
const signature = base64.stringify(hmacSha256(message, agentKey));

// 發請請求
axios.post('api-url', requestData, {
  headers: {
    'Content-Type': 'application/json',
    'X-Agent-Id': agentId,
    'X-Agent-Timestamp': requestTimestamp,
    'X-Agent-Signature': signature,
  }
});
```


