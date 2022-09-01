# 帳務平台 API

API 路徑 `Game` 參數固定為 `casino`，遊戲桌台編號請參考[桌台對應](#桌台對應)

- [注意事項](../notice-tw.md)
- [加密流程](#加密流程)
- 共用 API
- 轉帳錢包 API
- 單一錢包 API
- [API 欄位參考資料](../reference-tw.md)

## 加密流程

我們提供快速生成 `Key` 的套件（套件另外包含生成單一錢包所需的 `token`），使用方式參見各專案，目前支援以下語言:

- [JAVA Token](https://gitlab.com/token-library/java/-/wikis/README)
- [PHP Token](https://gitlab.com/token-library/php-token)
- [Node.js Token](https://gitlab.com/token-library/js-token)
- [C# Token](https://gitlab.com/token-library/csharp-token)

如果尚未支援的語言或是想自行處理，請按照[此份文件生成 `Key`](../encryption-tw.md)

## 桌台對應
    
本表僅供參考，實際開桌狀況以遊戲顯示為準

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


