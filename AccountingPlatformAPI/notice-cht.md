# 注意事項

## 代理後台

請參考 [代理後台操作手冊](../AgentBackend/manual-cht.md) 了解更多內容

## 個人 API 資訊

代理後台 [開發者專區/開發者文件](../AgentBackend/manual-cht.md#開發者專區) 頁面可查看 `API Host`、`Agent ID` 跟 `Agent Key`，請務必妥善保存 `Agent Key`

## IP 限制

- 所有 API 只通過代理所設定的 IP 白名單，除此之外的 IP 皆無法通過，可在代理後台 [帳號管理/個人資料](../AgentBackend/manual-cht.md#代理基本資料) 查看自身的 IP 白名單，下層代理的白名單可至 `帳號管理/代理管理` 頁面設定 
- 若要調整自身的 IP 白名單，請上層代理協助修改

## HTTPS encryption

要透過 HTTPS 呼叫我方 API，需支援 TLS 1.2 以上版本的加密方式

## API 語系
API 支援語系切換,只需 request 參數中加上 `ApiLang` 或 `lang`參數

- zh-CN:簡體(預設值)
- zh-TW:繁體
- en-US:英文
- ja:日文
- vi:越南文

## Request
- 所有請求需要包含以下參數，`Key` 生成方式請參考加密流程

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
- 使用 GET method，請將參數放入 [query string](https://en.wikipedia.org/wiki/Query_string)，請勿在 message body 放入參數，有些雲端服務會阻擋 message body 帶有參數的 GET 請求，更多資訊請參考 [HTTP GET method](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/GET)。
- 使用 POST method 請將參數放入 message body，格式為 JSON 格式，請勿使用 `form-data`、`x-www-form-urlencoded` 等格式。

