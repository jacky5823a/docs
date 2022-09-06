# 帳務平台 API

- [注意事項](#注意事項)
- [加密流程](#加密流程)
- [API規格](#API規格) 
    - [會員/代理](#會員/代理)
    - [注單查詢](#注單查詢)
    - [轉帳](#轉帳)
    - [單一錢包2.0](#單一錢包2.0)
    - [單一錢包1.x](#單一錢包1.x)
- [API 欄位參考資料](../reference-cht.md)

## 注意事項

使用 API 前請詳閱下列注意事項:

- 請詳閱[注意事項](../notice-cht.md)
- API 路徑 `GameCode` 參數固定為 `casino`
- 遊戲`桌台編號`請參考下表，實際開桌狀況以遊戲顯示為準

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

## 加密流程

我們提供快速生成 `Key` 的套件（套件另外包含生成單一錢包所需的 `token`），使用方式參見各專案，目前支援以下語言:

- [JAVA Token](https://gitlab.com/token-library/java/-/wikis/README)
- [PHP Token](https://gitlab.com/token-library/php-token)
- [Node.js Token](https://gitlab.com/token-library/js-token)
- [C# Token](https://gitlab.com/token-library/csharp-token)

如果尚未支援的語言或是想自行處理，請按照[此份文件生成 `Key`](../encryption-cht.md)

## API 規格 

### 會員/代理

提供建立會員、會員登入、修改會員/代理等操作，詳見 [會員/代理 API](https://staging-agent.olacak.live/swagger/public/index.html#/%E6%9C%83%E5%93%A1%2F%E4%BB%A3%E7%90%86)

### 注單查詢

注單資料非同步，約有五分鐘延遲，同一局同一位玩家的所有單注會合併成一個 wager，只能查詢已結算的單，詳見 [注單查詢 API](https://staging-agent.olacak.live/swagger/public/index.html#/%E6%B3%A8%E5%96%AE%E6%9F%A5%E8%A9%A2)

### 轉帳

轉帳錢包(現金)代理才能使用，詳見 [轉帳 API](https://staging-agent.olacak.live/swagger/public/index.html#/%E8%BD%89%E5%B8%B3)

### 單一錢包2.0

- 單一錢包代理才能使用，相較於 1.x 版，2.0 版只需實作兩支 callbacks，專注於會員金額上的更新，加密方式也更精簡和彈性
- 到後台個人遊戲設定單一錢包 callbacks(getBalance/updateBalance)
- 參考 [SeamlessWallet API 2.0](../../SeamlessWalletAPI2.0/SeamlessWalletAPI-2.0.md) 文件實作 `Get Balance` 及 `Update Balance` callbacks
- update balance 只會呼叫一次，未避免發生重複結算金額，我方遇到 time out 或非預期的 response 等錯誤時不會重新呼叫，請錢包方定期調用 [GetRequestHistoryByTime api](https://staging-agent.olacak.live/swagger/public/index.html#/%E5%96%AE%E4%B8%80%E9%8C%A2%E5%8C%852.0/post_api_keno_api__GameCode__GetRequestHistoryByTime) 檢查我方呼叫失敗的紀錄，並依據 `RequestJson` 內容修正玩家額度
- 請提供貴系統測試環境(staging)的測試帳號，我方將會安排測試 callbacks 是否正常運作

### 單一錢包1.x

- 單一錢包代理才能使用
- 到後台個人遊戲設定單一錢包 callbacks(balance/bet/settle/rollback)
- 參考 [How to handle the balance of members](../../SeamlessWalletAPI1.x/handle-balance.md) 和 [XG Seamless Wallet API](https://app.swaggerhub.com/apis/x-gaming-bet/xg-seamless_wallet_api/1.1) 文件實作各類型 callbacks
- 如果注單在結算前被取消，我方會調用 rollback 通知錢包方的系統
- 如果注單在結算後被取消，我方不會通知錢包方，錢包方必須定期呼叫 [取得會員單注紀錄 API](https://staging-agent.olacak.live/swagger/public/index.html#/%E5%96%AE%E4%B8%80%E9%8C%A2%E5%8C%851.x/post_api_keno_api__GameCode__GetReplenishmentByTime) 檢查下注的 `ModifiedStatus`，並處理會員的額度
- 請提供貴系統測試環境(staging)的測試帳號，我方將會安排測試 callbacks 是否正常運作

