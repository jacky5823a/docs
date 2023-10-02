# 帳務平台 API

- [注意事項](#注意事項)
- [加密流程](#加密流程)
- [API規格](#API規格) 
    - [會員&代理](#會員代理)
    - [注單查詢](#注單查詢)
    - [轉帳](#轉帳)
    - [單一錢包2.0](#單一錢包20)
- [限紅說明](#限紅說明) 
- [API 欄位參考資料](../reference-cht.md)

## 注意事項

使用 API 前請詳閱下列注意事項:

- 請詳閱[注意事項](../notice-cht.md)
- 遊戲`桌台編號`請參考下表，實際開桌狀況以遊戲顯示為準
 
    | 遊戲類別 | Table Id  |
    | --- | --- |
    | Baccarat | BC01, BC02, BC03, BC04, BC05, BC06, BC07, BC08, BC09, BC10，BC05, BC08 為特色百家|
    | DragonTiger | DT01 |  
    | Roulette | RT01 |  
    | Sicbo | SB01, SB02 |  
    | Sedie | SD01, SD02 |
   

- 支援幣別請參考下表，幣別代碼依照 [ISO_4217](https://en.wikipedia.org/wiki/ISO_4217) 制定
 
    | 代碼 | 幣別     |
    | ---- | -------- |
    | TWD  | 新台幣   |
    | VND  | 越南盾   |
    | KVND  | 千越南盾   |
    | USD  | 美金   |
    | USDT  | 泰達幣   |

## 加密流程

我們提供快速生成 `Key` 的套件（套件另外包含生成單一錢包所需的 `token`），使用方式參見各專案，目前支援以下語言:

- [JAVA Token](https://gitlab.com/token-library/java/-/packages/17448487)
- [PHP Token](https://gitlab.com/token-library/php-token)
- [Node.js Token](https://gitlab.com/token-library/js-token)
- [C# Token](https://gitlab.com/token-library/csharp-token)

如果尚未支援的語言或是想自行處理，請按照[此份文件生成 `Key`](../encryption-cht.md)

## API 規格 

### 會員&代理

提供建立會員、會員登入、修改會員/代理等操作，詳見 [會員&代理 API](https://staging-agent.olacak.live/swagger/public/index.html#/%E6%9C%83%E5%93%A1%26%E4%BB%A3%E7%90%86)

### 注單查詢

注單資料非同步，約有五分鐘延遲，同一局同一位玩家的所有單注會合併成一個 wager，只能查詢已結算的單，詳見 [注單查詢 API](https://staging-agent.olacak.live/swagger/public/index.html#/%E6%B3%A8%E5%96%AE%E6%9F%A5%E8%A9%A2)

### 轉帳

轉帳錢包(現金)代理才能使用，詳見 [轉帳 API](https://staging-agent.olacak.live/swagger/public/index.html#/%E8%BD%89%E5%B8%B3)

### 單一錢包2.0

- 單一錢包代理才能使用，相較於 1.1 版，2.0 版只需實作兩支 callbacks，專注於會員金額上的更新，加密方式也更精簡和彈性
- 參考 [SeamlessWallet API 2.0](../../SeamlessWalletAPI2.0/SeamlessWalletAPI-2.0.md) 文件實作 `Get Balance` 及 `Update Balance` callbacks
- 請至後台系統管理/個人設定的遊戲設定頁籤設定單一錢包 callbacks(getBalance/updateBalance)
- update balance 只會呼叫一次，未避免發生重複結算金額，我方遇到 time out 或非預期的 response 等錯誤時不會重新呼叫，請錢包方定期調用 [GetRequestHistoryByTime api](https://staging-agent.olacak.live/swagger/public/index.html#/%E5%96%AE%E4%B8%80%E9%8C%A2%E5%8C%852.0/post_api_keno_api_casino_GetRequestHistoryByTime) 檢查我方呼叫失敗的紀錄，並依據 `RequestJson` 內容修正玩家額度
- 後台 開發者專區/單一錢包設定/測試 提供一些測試案例，點擊按鈕會實際從我方 seamless server 發出 request 到貴系統，開發時可以依此進行測試，該測試僅供 staging 環境模擬發出相關測試案例時使用，不會產生實際注單
- 請提供貴系統測試環境(staging)的測試帳號，我方將會安排測試 callbacks 是否正常運作

### 單一錢包1.1(EOL)

- 1.1 版本不再進行功能更新，請升級到 2.0
- 參考 [How to handle the balance of members](../../SeamlessWalletAPI1.x/handle-balance.md) 和 [XG Seamless Wallet API](https://github.com/jacky5823a/docs/blob/master/SeamlessWalletAPI1.x/SeamlessWallet1.1.md) 文件實作各類型 callbacks
- 請至後台系統管理/個人設定的遊戲設定頁籤設定單一錢包 callbacks(balance/bet/settle/rollback)
- 如果注單在結算前被取消，我方會調用 rollback 通知錢包方的系統
- 如果注單在結算後被取消，我方不會通知錢包方，錢包方必須定期呼叫 [取得會員單注紀錄 API](https://staging-agent.olacak.live/swagger/public/index.html#/%E5%96%AE%E4%B8%80%E9%8C%A2%E5%8C%851.x/post_api_keno_api_casino_GetReplenishmentByTime) 檢查下注的 `ModifiedStatus`，並處理會員的額度
- 後台 開發者專區/單一錢包設定/測試 提供一些測試案例，點擊按鈕會實際從我方 seamless server 發出 request 到貴系統，開發時可以依此進行測試，該測試僅供 staging 環境模擬發出相關測試案例時使用，不會產生實際注單
- 請提供貴系統測試環境(staging)的測試帳號，我方將會安排測試 callbacks 是否正常運作

## 限紅說明

- 不同幣別有不同限紅編號。會員在遊戲中可依所設定的限紅編號，切換不同的限紅範圍，下注籌碼會根據限紅範圍做調整，各幣別限紅編號對應限紅範圍可參考 [Table Limit ID](./table-limit.md)
- 可透過後台或 API 調整限紅設定

### 後台
- 預設限紅：僅調用建立會員 API 時會使用到，**調整預設值並不會修改現有會員的限紅**。**系統管理/個人設定** 的限紅設定頁籤可調整自身的預設限紅組， **帳號管理/代理管理** 選取某位下層代理，預設限紅的頁籤可調整該下層代理的預設限紅組。每位代理針對每種幣別設定預設限紅組，初始預設值是最小範圍的限紅，可自由調整多個編號當預設限紅。
- 取得/設定會員限紅：**帳號管理/會員管理** 頁面查看直屬跟下層代理的所有會員限紅，只有直屬的會員才可設定限紅，下層代理的會員限紅必須由下層代理才能調整

### APIs
- POST /api/keno-api/xg-casino/CreateMember 建立會員，可帶入限紅(LimitStake)參數，限紅參數可包含多筆限紅編號，若有帶入限紅(LimitStake)參數，將依 LimitStake 設定值為準，若無，將會根據會員幣別抓取上述後台的**預設限紅**設定
- GET /api/keno-api/xg-casino/Template 取得指定會員限紅
- POST /api/keno-api/xg-casino/Template 設定指定會員限紅，Template 參數可調整該會員限紅編號，會員原本的限紅會被 Template 參數覆寫
- POST /api/keno-api/xg-casino/AllPlayersTemplate 設定指定幣別的所有會員限紅，可一次性調整指定幣別的所有現有會員限紅


