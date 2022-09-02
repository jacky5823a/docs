# 注意事項

使用 API 前請詳閱下列注意事項

## 個人 API 資訊

請登入代理後台，在開發人員文件頁面可找到 `API URL`、`Agent ID` 跟 `Agent Key`

## IP 限制

所有API只通過貴方所提供給我方的IP,除此之外的IP皆無法通過 

## 語系
平台API支援語系切換,只需 request 參數中加上 `lang` 或 `ApiLang` 參數

- zh-CN:簡體(預設值)
- zh-TW:繁體
- en-US:英文

## API 調用精度限制

所有的點數值只保留小數點後兩位, 例如：1000.23, 89.32, 1002304.89 

## Request
- 所有請求需要包含以下參數

| Parameter | Type   | Description    |
| --------- | ------ | -------------- |
| `AgentId` | string | 公鑰(代理編號) |
| `Key`     | string | 驗證參數       |

## Response
- 所有回應需要包含以下欄位

| Parameter   | Type   | Description |
| ----------- | ------ | ----------- |
| `ErrorCode` | String | 錯誤代碼      |
| `Message`   | String | 錯誤訊息    |
| `Data`      | Object | 數據資料    |

```json
{ 
    "ErrorCode":"0",
    "Message":"",
    "Data":{
        ......
    }
}
```

## 其他常見問題
- 使用 GET method，請將參數放入 [query string](https://en.wikipedia.org/wiki/Query_string)，請勿在 message body 放入參數，有些雲端服務會阻擋 message body 帶有參數的 GET 請求，更多資訊請參考 [HTTP GET method](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/GET)。`AgentId` 和 `Key` 則放入 query string 中，`Key` 產生方式請參考下面的 [加密流程](#加密流程)
- 使用 POST method 請將參數放入 message body，格式為 JSON 格式，請勿使用 `form-data`、`x-www-form-urlencoded` 等格式。

