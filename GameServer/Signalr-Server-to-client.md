#

* [updateUserCredit](#updateusercredit)
* [kickUser](#kickuser)
* [initialCasinoTable](#initialcasinotable)
* [updateRoadmap](#updateroadmap)
* [dealing](#dealing)
* [newRoundRun](#newroundrun)
* [gameStatistics](#gamestatistics)
* [gameStatusUpdateMessageReceived](#gamestatusupdatemessagereceived)
* [updateBettingPool](#updatebettingpool)
* [updateComputingResult](#updatecomputingresult)
* [updateJackpotPoolAmount](#updatejackpotpoolamount)
* [updateJackpotInfo](#updatejackpotinfo)
* [updateAllMarquee](#updateallmarquee)
* [changeDealer](#changedealer)
* [updateTableStatus](#updatetablestatus)
* [GameStatusFlags](#gamestatusflags)
* [RoadmapSymbol](#roadmapsymbol)

---

## **updateUserCredit**

通知用戶信用變動

Request
| Name | Type | Comment      |
| ------------- | ------ | --------- |
|  d | decimal    | 剩餘額度|
|  now | long | 現在時間(UnixTimeMs)|

```json
{
  "d": 97500.0,
  "now": 1607611712000
}
```

---

## **kickUser**

通知玩家被踢
Request
| Name   | Type | Comment  |
| ------ | ---- | ---- |
| (NONE) | int  | [玩家被踢原因(EnumKeyUserReason)](Enums#enumkeyuserreason) |

```json
1
```

---

## **initialCasinoTable**

通知初始化遊戲桌資料(登入後只取得一次)

Request

| Name  | Type   | Comment |
| ------- | ------ | ------- |
| (NONE) | object[] |  |
| &emsp;&emsp; gm | string | [百家樂桌台類型(EnumTableMode)](Enums#enumtablemode)     |
| &emsp;&emsp;tn | string | [桌台名稱(TableName)](Enums#tablename)    |
| &emsp;&emsp;ti | int   | 桌號 |
| &emsp;&emsp;ro | int | 輪號 |
| &emsp;&emsp;ru | string | 局號 |
| &emsp;&emsp;gs | int      | [遊戲狀態(GameStatus)](Enums#gamestatus)  |
| &emsp;&emsp;op | long     | 發牌時間      |
| &emsp;&emsp;tt |int | 總倒數秒數 |
| &emsp;&emsp;a | int | 目前秒數, 眯牌當前倒數秒數   |
| &emsp;&emsp;b | object[] | 路圖列表  |
| &emsp;&emsp;&emsp;&emsp;ro |int|輪號|
| &emsp;&emsp;&emsp;&emsp;ru |int|局號|
| &emsp;&emsp;&emsp;&emsp;sbl |int|[路圖](#roadmapsymbol)|
| &emsp;&emsp;c | int      | 眯牌總倒數秒  |
| &emsp;&emsp;d | object   | 荷官資訊      |
| &emsp;&emsp;&emsp;&emsp;di | int      | 編號|
| &emsp;&emsp;&emsp;&emsp;dn | string   | 名稱|
| &emsp;&emsp;&emsp;&emsp;dp | string   | 照片位址      |
| &emsp;&emsp;e | bool | 是否18禁 |
| &emsp;&emsp;f | bool | 是否能現場驗證 |
| &emsp;&emsp;g | int | [桌台狀態](#gamestatusflags) |

```json
[
  {
    "gm": "Standard",
    "tn": "Baccarat",
    "ti": "A",
    "ro": "1542598605",
    "ru": "3",
    "gs": 1,
    "op": 1607611712,
    "tt": 27,
    "a": 7,
    "b": [
      {
        "ro": 12345678,
        "ru": 1,
        "sbl": "123"
      },
      {
        "ro": 12345678,
        "ru": 2,
        "sbl": "456"
      },
      {
        "ro": 12345678,
        "ru": 3,
        "sbl": "789"
      }
    ],
    "c": 0,
    "d": {
      "di": "000001",
      "dn": "Sally",
      "dp": "https://www.xxx.com/00001.jpg"
    },
    "e": true,
    "f": true,
    "g": "0x0"
  }
]
```

---

## **updateRoadmap**

通知路圖資料

Request

| Name | Type | Comment|
| ------- | ---- | ----------------- |
| sbl | string | [路圖](#roadmapsymbol)  |
| ro | string | 輪號|
| ru | string | 局號|
| ti | string | 桌號 (A, B, C, D) |
| tn | string | [桌台名稱](Enums#tablename)  |
| gs | int    | [遊戲狀態](Enums#gamestatus) |
| now | long | 現在時間(UnixTimeMs) |

```json
{
  "sbl":"190",
  "ro":"1542598608",
  "ru":"165",
  "ti":"B",
  "tn":"Baccarat",
  "gs":0,
  "now":1607611712000
}
```

---

## **dealing**

發牌

Request
| Name | Type | Comment |
| ------- | ---- |---------- |
| ro | string| 輪號    |
|  ru | string| 局號    |
|  ti | string| 桌號 (A, B, C, D)    |
| tn | string| [桌台名稱](Enums#tablename)  |
|  gs | int| [遊戲狀態](Enums#gamestatus) |
|  now | long | 現在時間(UnixTimeMs) |
| ---| *以下為百家資料* |  |
| p1 | string| 閒1 (Baccarat)|
|  p2 | string| 莊1 (Baccarat)|
|  p3 | string| 閒2 (Baccarat)|
|  p4 | string| 莊2 (Baccarat)|
|  p5 | string| 閒3 (Baccarat)|
|  p6 | string| 莊3 (Baccarat)|
|  bkrt | int| 莊點數和 (Baccarat)  |
|  plrt | int| 閒點數和 (Baccarat)  |
| ---| *以下為龍虎資料* |  |
|  p1 | string| 龍 (DragonTiger)     |
|  p2 | string| 虎 (DragonTiger)     |
|  dgt | int| 龍點數 (DragonTiger) |
|  tgt | int| 虎點數 (DragonTiger) |
| ---| *以下為輪盤資料* |  |
|  num | int| 投球結果|
| ---| *以下為色碟資料* |  |
|  red | int| 紅色鈕扣數量  |
|---|*以下為骰寶資料*||
|  d1 | int? | 第 1 顆骰子點數 |
|  d2 | int? | 第 2 顆骰子點數 |
|  d3 | int? | 第 3 顆骰子點數 |
|---|*以下為急速骰寶資料*||
|  d1 | int? | 第 1 顆骰子點數 |

```json
{
  "p1": "H8",
  "p2": "S6",
  "p3": "H3",
  "p4": "H1",
  "p5": "C4",
  "p6": "",
  "bkrt": 7,
  "plrt": 5,
  "ro": "1542598608",
  "ru": "167",
  "ti": "B",
  "tn": "Baccarat",
  "gs": 2,
  "now": 1607611712000
}
```

## **newRoundRun**

新輪局

Request
|Name | Type   | Comment |
| ---- | ------ | ------- |
| now | long   | 現在時間(UnixTimeMs)      |
| op | long   | 發牌時間      |
| tt | int    | 總倒數秒數    |
| ro | int | 輪號|
| ru | int | 局號|
| ti | string | 桌號 (A, B, C, D) |
| tn | string | [桌台名稱](Enums#tablename)  |
| gs | int | [遊戲狀態](Enums#gamestatus) |
| di | string | 荷官ID |
| dn | string | 荷官Name |
| dp | string | 荷官圖片連結 |

```json
{
  "now": 1607612682000,
  "op": 1607612692,
  "tt": 27,
  "ro": "1542598605",
  "ru": "170",
  "ti": "A",
  "tn": "Baccarat",
  "gs": 6,
  "di": "000001",
  "dn": "Sally",
  "dp": "https://www.xxx.com/00001.jpg"
}
```

## **gameStatistics**

開獎統計結果

Request
| Name| Type  | Comment |
| --- | -------| ------ |
| tn| string| [桌台名稱](Enums#tablename)  |
| ti| string| 桌號 (A, B, C, D)    |
| ro| string| 輪號    |
| ru| string| 局號    |
| gs| int| [遊戲狀態](Enums#gamestatus) |
| f| object| 開牌統計 (請參照下方對應遊戲欄位)   |
| now| long   | 現在時間(UnixTimeMs)      |
| --- || *以下為百家資料* |   |
| &emsp;&emsp;wf| int| [遊戲開獎旗標(WinFlags)](Enums#WinFlags)   |
| &emsp;&emsp;p1| string| 第一張牌|
| &emsp;&emsp;p2| string| 第二張牌|
| &emsp;&emsp;p3| string| 第三張牌|
| &emsp;&emsp;p4| string| 第四張牌|
| &emsp;&emsp;p5| string| 第五張牌|
| &emsp;&emsp;p6| string| 第六張牌|
| &emsp;&emsp;plrt| int| 閒家點數和     |
| &emsp;&emsp;bkrt| int| 莊家點數和     |
| &emsp;&emsp;j| int| 莊家中獎次數   |
| &emsp;&emsp;k| int| 閒家中獎累積次 |
| &emsp;&emsp;l| int| 和局中獎次數   |
| &emsp;&emsp;m| int| 莊家對子中獎次數|
| &emsp;&emsp;n| int| 閒家對子中獎次數|
| &emsp;&emsp;o| int| 「大」中獎次數 |
| &emsp;&emsp;p| int| 「小」中獎次數 |
| &emsp;&emsp;q| int| 莊家單中獎次數 |
| &emsp;&emsp;r| int| 莊家雙中獎次數 |
| &emsp;&emsp;s| int| 閒家單中獎次數 |
| &emsp;&emsp;t| int| 閒家雙中獎次數 |
| &emsp;&emsp;u| int| 莊家A中獎次數  |
| &emsp;&emsp;v| int| 閒家A中獎次數  |
| &emsp;&emsp;w| int| 莊家JQK中獎次數|
| &emsp;&emsp;x| int| 閒家JQK中獎次數|
| &emsp;&emsp;y| int| 莊家AJQK中獎次數|
| &emsp;&emsp;z| int| 閒家AJQK中獎次數|
| &emsp;&emsp;aa| int| 莊閒A中獎次數  |
| &emsp;&emsp;ab| int| 莊閒JQK中獎次數|
| &emsp;&emsp;ac| int| 莊閒AJQK中獎次數|
| &emsp;&emsp;ad| int| 超級六中獎次數 |
| --- || *以下為龍虎資料* |   |
| &emsp;&emsp;wf| int| [遊戲開獎旗標(WinFlags)](Enums#WinFlags)   |
| &emsp;&emsp;p1| string| 龍|
| &emsp;&emsp;p2| string| 虎|
| &emsp;&emsp;dgt| int| 龍點數  |
| &emsp;&emsp;tgt| int| 虎點數  |
| &emsp;&emsp;f| int| 龍中獎次數     |
| &emsp;&emsp;g| int| 虎中獎次數     |
| &emsp;&emsp;h| int| 和中獎次數     |
| --- || *以下為輪盤資料* |   |
|&emsp;&emsp; wf| int| [遊戲開獎旗標(WinFlags)](Enums#WinFlags)   |
| &emsp;&emsp;num| int?  | 輪盤點數|
| &emsp;&emsp;c| int| 0中獎次數      |
| &emsp;&emsp;d| int| 大中獎次數     |
| &emsp;&emsp;e| int| 小中獎次數     |
| &emsp;&emsp;f| int| 紅中獎次數     |
| &emsp;&emsp;g| int| 黑中獎次數     |
| &emsp;&emsp;h| int| 雙中獎次數     |
| &emsp;&emsp;i| int| 單中獎次數     |
| &emsp;&emsp;j| int[] | 近60局熱門號碼(越前面越熱門)  |
| &emsp;&emsp;k| int[] | 近60局冷門號碼(越前面越冷門)  |
| --- | *以下為色碟資料* |   |
| &emsp;&emsp;wf| int| [遊戲開獎旗標(WinFlags)](Enums#WinFlags)   |
| &emsp;&emsp;red| int| 紅色鈕扣數量   |
| &emsp;&emsp;c| int| 大區中獎次數   |
| &emsp;&emsp;d| int| 小區中獎次數   |
| &emsp;&emsp;e| int| 單區中獎次數   |
| &emsp;&emsp;f| int| 雙區中獎次數   |
| &emsp;&emsp;g| int| 0紅中獎次數    |
| &emsp;&emsp;h| int| 1紅中獎次數    |
| &emsp;&emsp;i| int| 2紅中獎次數    |
| &emsp;&emsp;j| int| 3紅中獎次數    |
| &emsp;&emsp;k| int| 4紅中獎次數    |
| --- | *以下為骰寶資料* |
| &emsp;&emsp;wf| int| [遊戲開獎旗標(WinFlags)](Enums#WinFlags)   |   |
|&emsp;&emsp;d1|int?|第1顆骰子|
|&emsp;&emsp;d2|int?|第2顆骰子|
|&emsp;&emsp;d3|int?|第3顆骰子|
|&emsp;&emsp;e|int?|骰子點數和|
|&emsp;&emsp;f|int|雙區中獎次數|
|&emsp;&emsp;g|int|單區中獎次數|
|&emsp;&emsp;h|int|大區中獎次數|
|&emsp;&emsp;i|int|小區中獎次數|
|&emsp;&emsp;j|int|全圍中獎次數|
|&emsp;&emsp;k|int|點數 1 中獎次數|
|&emsp;&emsp;l|int|點數 2 中獎次數|
|&emsp;&emsp;m|int|點數 3 中獎次數|
|&emsp;&emsp;n|int|點數 4 中獎次數|
|&emsp;&emsp;o|int|點數 5 中獎次數|
|&emsp;&emsp;p|int|點數 6 中獎次數|
|&emsp;&emsp;q|int|泰式 Hi 中獎次數|
|&emsp;&emsp;r|int|泰式 Lo 中獎次數|
|&emsp;&emsp;s|int|泰式 HiLo 中獎次數|
|&emsp;&emsp;t|int[]|近60局熱門點數和(越前面越熱門)|
|&emsp;&emsp;u|int[]|近60局冷門點數和(越前面越冷門)|
| ---| *以下為急速骰寶資料* ||
| &emsp;&emsp;wf|int|[遊戲開獎旗標(WinFlags)](Enums#WinFlags)|
|&emsp;&emsp;d1|int?|第1顆骰子|
|&emsp;&emsp;c|int|點數 1 中獎次數|
|&emsp;&emsp;d|int|點數 2 中獎次數|
|&emsp;&emsp;e|int|點數 3 中獎次數|
|&emsp;&emsp;f|int|點數 4 中獎次數|
|&emsp;&emsp;g|int|點數 5 中獎次數|
|&emsp;&emsp;h|int|點數 6 中獎次數|
|&emsp;&emsp;i|int|雙區中獎次數|
|&emsp;&emsp;j|int|單區中獎次數|
|&emsp;&emsp;k|int|大區中獎次數|
|&emsp;&emsp;l|int|小區中獎次數|

```json
{
  "tn": "Baccarat",
  "ti": "A",
  "ro": 1000000000,
  "ru": 10,
  "gs": 3,
  "now": 1607612682000,
  "f": {
    "wf": 1,
    "p1": "C2",
    "p2": "C6",
    "p3": "DJ",
    "p4": "DK",
    "p5": "C4",
    "p6": "HQ",
    "h": 0,
    "i": 0,
    "j": 0,
    "k": 0,
    "l": 0,
    "m": 0,
    "n": 0,
    "o": 0,
    "p": 0,
    "q": 0,
    "r": 0,
    "s": 0,
    "t": 0,
    "u": 0,
    "v": 0,
    "w": 0,
    "x": 0,
    "y": 0,
    "z": 0,
    "aa": 0,
    "ab": 0,
    "ac": 0,
    "ad": 0
  }
}
```

## **gameStatusUpdateMessageReceived**

通知遊戲狀態資訊

1. Request 發牌資訊 (請改用 [dealing](#dealing))
2. Request 新輪新局 (請改用 [newRoundRun](#newroundrun))
3. Request 開獎統計結果 (請改用 [gameStatistics](#gamestatistics))
4. Request 狀態資訊

| Name | Type   | Comment|
| ---- | ------ | -------- |
| tt | int    | 總倒數秒數    |
| ro  | string | 輪號|
|  ru | string | 局號|
|  ti | string | 桌號 (A, B, C, D) |
|  tn | string | [桌台名稱](Enums#tablename)  |
|  gs |int    | [遊戲狀態](Enums#gamestatus) |
| now | long   | 現在時間(UnixTimeMs) |

```json
{
  "ro": "1542598605",
  "ru": "170",
  "ti": "A",
  "tn": "Baccarat",
  "gs": 1,
  "now": 1607611712000,
}
```

---

## **updateBettingPool**

通知即時彩池變動

Request
| Name| Type     | Comment|
| -------- | -------- | --- |
| tn| string | [桌台名稱(TableName)](Enums#tablename)|
| ti| string | 桌號 (A, B, C, D)    |
| ro| string | 輪號  |
| ru| string | 局號  |
| a | object[] | 即時彩池注區列表 |
| &emsp;&emsp; si | int | [注區編號(Spots)](Spots)|
| &emsp;&emsp; a| int | 下注人數  |
| &emsp;&emsp; b| decimal | 下注金額  |



```json
{
  "tn": "Baccarat",
  "ti": "A",
  "ro": "1542598605",
  "ru": "3",
  "a": [
    {
      "si": 11001,
      "a": 1,
      "b": 100,
    }
  ]
}
```

---

## **updateComputingResult**

通知結算

Request
| Name| Type     | Comment|
| ------ | --- |---|
| tn| string   | [桌台名稱](Enums#tablename)|
| ti| string   | 桌號 (A, B, C, D)    |
| a| int[]    | [中獎注區編號](Spots)|
| b| object[] | 玩家押注輸贏明細     |
| &emsp;&emsp;si      | int      | 玩家壓注注區  |
| &emsp;&emsp;a | decimal      | 該注輸贏  |
| &emsp;&emsp;b    | decimal      | 該注本金  |

```json
{
  "tn": "Baccarat",
  "ti": "A",
  "a": [
    11002,
    11003,
    11008,
    11010,
    11022
  ],
  "b": [
    {
      "si": 11001,
      "a": -5000,
      "b": 5000
    },
    {
      "si": 11002,
      "a": 2000,
      "b": 2000
    }
  ]
}
```

---

## **updateJackpotPoolAmount**

通知目前Jackpot累積(每3秒會推送一次)

Request
| Name   | Type | Comment      |
| ------ | ---- | ------------ |
| (NONE) | int  | 目前累積金額 |

```json
70846
```

---

## **updateJackpotInfo**

通知該玩家Jackpot累積資訊

Request
| Name      | Type    | Comment |
| ------------------------ | ------- | -------------------------------------------------- |
| NextBigWinRatio| int     | 下一個BigWin倍率(非可已領取狀態下均為0.0)|
| BaseBigWinAmount  | int     | 首局達BigWin時取的jp金額 |
| NextWinExpectedWinAmount | int     | 下一個預期該局會贏的jp金額|
| ContinueWin| int     | 連贏累積次數|
| Kind      | int     | [中獎種類(EnumJackpotKind)](Enums#enumjackpotkind) |
| WinAmount | decimal |  |
| TotalBetAmount| decimal |  |
| ExpectedWinAmount | decimal |  |

```json
{
  "NextBigWinRatio":0.0,
  "BaseBigWinAmount":0.0,
  "NextWinExpectedWinAmount":0.0,
  "ContinueWin":1,
  "Kind":0,
  "WinAmount":0.0,
  "TotalBetAmount":5000.0,
  "ExpectedWinAmount":0.0
}
```

---

## **updateAllMarquee**

通知公告訊息

Request
| Name  | Type     | Comment      |
| --------------------------------- | -------- | --------------------------- |
| (NONE)| object[] | 公告列表     |
|&emsp;&emsp;a     | int      | 公告編號     |
|&emsp;&emsp;b     | object[] | 桌台列表     |
|&emsp;&emsp;&emsp;&emsp;tn | string   | [桌台名稱](Enums#tablename) |
|&emsp;&emsp;&emsp;&emsp;ti   | string   | 桌號(A, B, C, D) |
|&emsp;&emsp;c|object[]|公告語系訊息|
|&emsp;&emsp;&emsp;&emsp;zh_TW|string|繁中|
|&emsp;&emsp;&emsp;&emsp;zh_CN|string|簡中|
|&emsp;&emsp;&emsp;&emsp;en|string|英文|
|&emsp;&emsp;&emsp;&emsp;th|string|泰文|
|&emsp;&emsp;&emsp;&emsp;id|string|印尼文|
|&emsp;&emsp;&emsp;&emsp;ms|string|馬來文|
|&emsp;&emsp;&emsp;&emsp;ko|string|韓文|
|&emsp;&emsp;&emsp;&emsp;ja|string|日文|
|&emsp;&emsp;&emsp;&emsp;vn|string|越南文|
|&emsp;&emsp;d| bool     | 公告是否關閉 |
|&emsp;&emsp;st  | long   | 開始時間 (UnixTimeMs)    |
|&emsp;&emsp;et| long   | 結束時間 (UnixTimeMs)    |

```json

```

---

## **changeDealer**

荷官變更
Request
| Name  | Type   | Comment      |
|  --------| ------ | ------------ |
|  tn | string | 桌台名稱     |
|  ti | string | 桌台編號     |
|  di | string| 荷官編號     |
| dn |string | 荷官名稱     |
|  dp | string | 荷官照片網址 |
| now | long | 現在時間(UnixTimeMs) |

```json
{
   "tn": "Baccarat",
   "ti": "A",
   "di": "000001",
   "dn": "Naccy",
   "dp": "https://xxx.com/000001.jpg",
   "now": 1607611712000
}
```

## **updateTableStatus**

更新遊戲狀態(單桌, 並針對Comapany發送)

Request
| Name      | Type   | Comment|
| --------- | ------ | ------- |
| tn | string | 桌台名稱      |
| ti   | string | 桌台編號      |
| ts    | int    | [桌台狀態](#gamestatusflags) |

```json
{
  "tn": "Baccarat",
  "ti": "A",
  "ts":0
}
```

## GameStatusFlags

桌台狀態 (flag)
>
> * 0x0 Normal 正常狀態
> * 0x1 Suspend 維護
> * 0x2 Closed 關閉(開放時間以外)

## RoadmapSymbol

> 牌局結果會轉換成一個數值作為路圖資料，每局的結果以逗點 ',' 分隔，每個遊戲實際路圖資料代表的意義不太相同，請參考說明
>
> 百家樂
>
> * digits 1: 贏家種類(1:Banker; 2:Player; 3:Tie)
> * digits 2:  贏家點數(1~9)
> * digits 3: 對子種類(0:無對子; 1:閒對; 2:莊對; 3:莊對+閒對)
>
>> 例如: 192 代表莊家9點贏，開莊對
>
> 龍虎
>
> * 3:和局；4:龍贏；5:虎贏
>
> 輪盤
>
> * 數字 0~36 代表該局輪盤結果
>
> 色碟
>
> * 代表紅色鈕扣的數量
>
> 骰寶
>
> * digits 1: 第1顆骰子點數(1-6)
> * digits 2: 第2顆骰子點數(1-6)
> * digits 3: 第3顆骰子點數(1-6)
>
>> 例如: 362 代表三顆骰子分別為 3、6、2
>
> 急速骰寶
>
> * 數字 1~6 代表該局骰子結果
