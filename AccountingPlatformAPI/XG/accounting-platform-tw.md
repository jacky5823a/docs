# 帳務平台 API

API 路徑 `Game` 參數固定為 `xg-casino`，遊戲桌台編號請參考[桌台對應](#桌台對應)

- [注意事項](../notice-tw.md)
- [加密流程](#加密流程)
- 共用 API
- 轉帳錢包 API
- 單一錢包 API
- [API 欄位參考資料](../reference-tw.md)

## 加密流程

我們提供快速生成 `Key` 的套件（套件另外包含生成單一錢包所需的 `token`），使用方式參見各專案，目前支援以下語言:

- [JAVA XG Token](https://gitlab.kaixi.cc/api-libaray/java-xg-token)
- [PHP XG Token](https://gitlab.kaixi.cc/api-libaray/php-xg-token)
- [Node.js XG Token](https://gitlab.kaixi.cc/api-libaray/js-xg-token)
- [C# XG Token](https://gitlab.kaixi.cc/api-libaray/csharp-xg-token)

如果尚未支援的語言或是想自行處理，請按照[此份文件生成 `Key`](../encryption-tw.md)

## 桌台對應
    
本表僅供參考，實際開桌狀況以遊戲顯示為準

| 遊戲類別 | Table Id  |
| --- | --- |
| Baccarat | E, F, G, H, I, J, K, L, O, P, X |
| DragonTiger | A |  
| Roulette | B |  
| Sicbo | W, V |  
| Sedie | C, D |


