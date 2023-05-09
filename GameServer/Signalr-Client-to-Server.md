#

* [Login](#login)
* [SetPushBettingPoolSpotId](#setpushbettingpoolspotid)
* [Seat](#seat)
* [MultipleTableSeat](#multipletableseat)
* [UpdateUserLimitStake](#updateuserlimitstake)
* [MultipBet](#multipbet)
* [QuickMultipBet](#quickmultipbet)
* [AcceptJackpotBigWin](#acceptjackpotbigwin)
* [GetSelfBettingList](#getselfbettinglist)
* [GetGameResult](#getgameresult)
* [GetMarquee](#getmarquee)
* [GetGameLimitStake](#getgamelimitstake)
* [Heartbeat](#heartbeat)
---

## **Login**

### 登入

Request

|Name|Type|Comment|
|----|----|-------|
|ci|int|公司編號|
|un|string|用戶名|
|tk|string|登入憑證|
|pf|int|[運行平台編號](Enums#enumplatform)|

``` json
{
  "un":"Visitor12ILA7nxglS1",
  "tk":"6e52cd4c5d60b57dd53ab82085a7eaad",  
  "ci":7,
  "pf":2
}
```

Response

 |Name|Type|Comment|
 |----|----|-------|
 |err|int|[錯誤代碼(GameCenterErrorCode)](Game-Server-Error-Code)|
 |a|object[]|範本列表|
 |&emsp;&emsp; a|int|範本編號|
 |&emsp;&emsp; b|bool|是否選擇|
 |&emsp;&emsp; c|decimal|限注下限|
 |&emsp;&emsp; d|decimal|限注上限|
 |cy|int|[幣別(EnumCurrencyType)](Enums#enumcurrencytype)|
 |b|bool|是否啟用 Jackpot|
 |c|decimal|玩家餘額|

 ```json
 {
  "err": 0,
  "a": [
    {
      "a": 1,
      "b": true,
      "c": 100,
      "d": 500
    }
  ],
  "cy": 1,
  "b": false,
  "c": 100.0
 }
 ```

---

## **SetPushBettingPoolSpotId**

### 設定玩家關注的注區ID

Request

|Name|Type|Comment|
|----|----|-------|
|spotIdList|string[] |[注區編號(Spots)](Spots)|

```json
["11001","11002","11021","11022"]
```

#### Reponse

|Name|Type|Comment|
|----|----|-------|
|(NONE)|int|[錯誤代碼(GameCenterErrorCode)](Game-Server-Error-Code)|

```json
0
```

---

## **Seat**

### 單桌入桌

Request

|Name|Type|Comment|
|----|----|-------|
|tn|string|[桌台名稱(TableName)](Enums#tablename)|
|ti|string|桌號(A, B, C, D)|

```json
{
  "tn": "Baccarat",
  "ti": "A"
}
```

Reponse

|Name| Type  | Comment |
|----|---- |---- |
|ava| bool  | 該物件是否可以使用 |
|err| int| [錯誤代碼(GameCenterErrorCode)](./Game-Server-Error-Code) |
|tn| string| [桌台名稱](Enums#tablename)   |
|ti|string| 桌號 (A, B, C, D)  |
|e| object[]  | 彩池資料|
| &emsp;&emsp;si| int| [注區編號(Spots)](Spots)      |
| &emsp;&emsp;b| int| 下注金額|
| &emsp;&emsp;c| int| 下注人數|
| f | object | 視訊網址資訊 |
|&emsp;&emsp;a|string| HD 畫質網址|
|&emsp;&emsp;b|string| SD 畫質網址|
|&emsp;&emsp;c|string| FHD 畫質網址|
|g| object| 桌檯倒數時間|
|&emsp;&emsp;a|long|目前秒數|
|&emsp;&emsp;tt|short|總倒數秒數|
|i| object[]|玩家此局下注資訊|
|&emsp;&emsp;bt|int|[下注模式](Enums#enumbettypes)|
|&emsp;&emsp;si|int|[注區編號(Spots)](Spots) |
|&emsp;&emsp;c|decimal|下注金額|
|j| object| 開獎統計   |
| --- | *以下為百家資料* |   |
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
| --- | *以下為龍虎資料* |   |
| &emsp;&emsp;wf| int| [遊戲開獎旗標(WinFlags)](Enums#WinFlags)   |
| &emsp;&emsp;p1| string| 龍|
| &emsp;&emsp;p2| string| 虎|
| &emsp;&emsp;dgt| int| 龍點數  |
| &emsp;&emsp;tgt| int| 虎點數  |
| &emsp;&emsp;f| int| 龍中獎次數     |
| &emsp;&emsp;g| int| 虎中獎次數     |
| &emsp;&emsp;h| int| 和中獎次數     |
| --- | *以下為輪盤資料* |   |
|&emsp;&emsp;wf| int| [遊戲開獎旗標(WinFlags)](Enums#WinFlags)   |
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
  "e": [
    {
      "a": 11001,
      "b": 10000.5,
      "c": 2
    },
    {
      "a": 11002,
      "b": 9000.5,
      "c": 3
    }
  ],
  "f": {
    "a": "https://flv.china-ruichi.com/bacc/p-720p.flv",
    "b": "https://flv.china-ruichi.com/bacc/p-480p.flv",
    "c": "https://flv.china-ruichi.com/bacc/p-1080p.flv"
  },
  "g": {
    "a": 10,
    "b": 30
  },
  "h": [
    {
      "c": 1,
      "d": 1,
      "e": 100.5,
      "f": 1000.5,
      "g": [
        1,
        5,
        100,
        1000
      ]
    },
    {
      "a": "Baccarat",
      "b": 1,
      "c": 2,
      "d": 1,
      "e": 1000.5,
      "f": 10000.5,
      "g": [
        1,
        5,
        100,
        1000,
        10000
      ]
    }
  ],
  "i": [
    {
      "a": 1,
      "b": 11001,
      "c": 1000.5
    },
    {
      "a": 1,
      "b": 11002,
      "c": 100.5
    }
  ],
  "j": {
    "a": 1,
    "p1": "C2",
    "p2": "C6",
    "p3": "DJ",
    "p4": "DK",
    "p5": "C4",
    "p6": "HQ",
    "plrt": 0,
    "bkrt": 0,
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
  },
  "ava": true,
  "err": 0
}
```

---

## **MultipleTableSeat**

### 多台入桌

Request

|Name|Type|Comment|
|----|----|-------|
|a|object[]|入桌列表|
|&emsp;&emsp; tn|string|[桌台名稱](Enums#tablename)|
|&emsp;&emsp; ti|string|桌號(A, B, C, D)|

```json
{
	"a": [
		{
			"tn": "Baccarat",
			"ti": "A"
		},
		{
			"tn": "Baccarat",
			"ti": "B"
		}
	]
}
```

Response

|Name|Type|Comment|
|----|----|-------|
|err|int|[錯誤代碼(GameCenterErrorCode)](Game-Server-Error-Code)|
|a|object[]|桌檯資訊|
|&emsp;&emsp;tn|string|[桌台名稱](Enums#tableName)|
|&emsp;&emsp;ti|string|桌號 (A, B, C, D)|
|&emsp;&emsp;e|object[]|即時彩池|
|&emsp;&emsp;&emsp;&emsp;si|int|[注區編號(Spots)](Spots)|
|&emsp;&emsp;&emsp;&emsp;b|int|下注金額|
|&emsp;&emsp;&emsp;&emsp;c|int|下注人數|
|&emsp;&emsp;f|Object|視訊位址資訊|
|&emsp;&emsp;&emsp;&emsp;a|string|HD 畫質網址|
|&emsp;&emsp;&emsp;&emsp;b|string|SD 畫質網址|
|&emsp;&emsp;&emsp;&emsp;c|string|FHD 畫質網址|
|&emsp;&emsp;i|object[]|該桌下注資料|
|&emsp;&emsp;&emsp;&emsp;bt|int|[下注模式](Enums#enumbettypes)|
|&emsp;&emsp;&emsp;&emsp;si|int|[注區編號](Spots)|
|&emsp;&emsp;&emsp;&emsp;c|decimal|下注金額|
| &emsp;&emsp;j| object| 開獎統計   |
| --- | *以下為百家資料* |   |
| &emsp;&emsp;&emsp;&emsp;wf| int| [遊戲開獎旗標(WinFlags)](Enums#WinFlags)   |
| &emsp;&emsp;&emsp;&emsp;b| string| 第一張牌|
| &emsp;&emsp;&emsp;&emsp;c| string| 第二張牌|
| &emsp;&emsp;&emsp;&emsp;d| string| 第三張牌|
| &emsp;&emsp;&emsp;&emsp;e| string| 第四張牌|
| &emsp;&emsp;&emsp;&emsp;f| string| 第五張牌|
| &emsp;&emsp;&emsp;&emsp;g| string| 第六張牌|
| &emsp;&emsp;&emsp;&emsp;h| int| 閒家點數和     |
| &emsp;&emsp;&emsp;&emsp;i| int| 莊家點數和     |
| &emsp;&emsp;&emsp;&emsp;j| int| 莊家中獎次數   |
| &emsp;&emsp;&emsp;&emsp;k| int| 閒家中獎累積次 |
| &emsp;&emsp;&emsp;&emsp;l| int| 和局中獎次數   |
| &emsp;&emsp;&emsp;&emsp;m| int| 莊家對子中獎次數|
| &emsp;&emsp;&emsp;&emsp;n| int| 閒家對子中獎次數|
| &emsp;&emsp;&emsp;&emsp;o| int| 「大」中獎次數 |
| &emsp;&emsp;&emsp;&emsp;p| int| 「小」中獎次數 |
| &emsp;&emsp;&emsp;&emsp;q| int| 莊家單中獎次數 |
| &emsp;&emsp;&emsp;&emsp;r| int| 莊家雙中獎次數 |
| &emsp;&emsp;&emsp;&emsp;s| int| 閒家單中獎次數 |
| &emsp;&emsp;&emsp;&emsp;t| int| 閒家雙中獎次數 |
| &emsp;&emsp;&emsp;&emsp;u| int| 莊家A中獎次數  |
| &emsp;&emsp;&emsp;&emsp;v| int| 閒家A中獎次數  |
| &emsp;&emsp;&emsp;&emsp;w| int| 莊家JQK中獎次數|
| &emsp;&emsp;&emsp;&emsp;x| int| 閒家JQK中獎次數|
| &emsp;&emsp;&emsp;&emsp;y| int| 莊家AJQK中獎次數|
| &emsp;&emsp;&emsp;&emsp;z| int| 閒家AJQK中獎次數|
| &emsp;&emsp;&emsp;&emsp;aa| int| 莊閒A中獎次數  |
| &emsp;&emsp;&emsp;&emsp;ab| int| 莊閒JQK中獎次數|
| &emsp;&emsp;&emsp;&emsp;ac| int| 莊閒AJQK中獎次數|
| &emsp;&emsp;&emsp;&emsp;ad| int| 超級六中獎次數 |
| --- | *以下為龍虎資料* |   |
| &emsp;&emsp;&emsp;&emsp;wf| int| [遊戲開獎旗標(WinFlags)](Enums#WinFlags)   |
| &emsp;&emsp;&emsp;&emsp;b| string| 龍|
| &emsp;&emsp;&emsp;&emsp;c| string| 虎|
| &emsp;&emsp;&emsp;&emsp;d| int| 龍點數  |
| &emsp;&emsp;&emsp;&emsp;e| int| 虎點數  |
| &emsp;&emsp;&emsp;&emsp;f| int| 龍中獎次數     |
| &emsp;&emsp;&emsp;&emsp;g| int| 虎中獎次數     |
| &emsp;&emsp;&emsp;&emsp;h| int| 和中獎次數     |
| --- | *以下為輪盤資料* |   |
|&emsp;&emsp;&emsp;&emsp; wf| int| [遊戲開獎旗標(WinFlags)](Enums#WinFlags)   |
| &emsp;&emsp;&emsp;&emsp;b| int?  | 輪盤點數|
| &emsp;&emsp;&emsp;&emsp;c| int| 0中獎次數      |
| &emsp;&emsp;&emsp;&emsp;d| int| 大中獎次數     |
| &emsp;&emsp;&emsp;&emsp;e| int| 小中獎次數     |
| &emsp;&emsp;&emsp;&emsp;f| int| 紅中獎次數     |
| &emsp;&emsp;&emsp;&emsp;g| int| 黑中獎次數     |
| &emsp;&emsp;&emsp;&emsp;h| int| 雙中獎次數     |
| &emsp;&emsp;&emsp;&emsp;i| int| 單中獎次數     |
| &emsp;&emsp;&emsp;&emsp;j| int[] | 近60局熱門號碼(越前面越熱門)  |
| &emsp;&emsp;&emsp;&emsp;k| int[] | 近60局冷門號碼(越前面越冷門)  |
| --- | *以下為色碟資料* |   |
| &emsp;&emsp;&emsp;&emsp;wf| int| [遊戲開獎旗標(WinFlags)](Enums#WinFlags)   |
| &emsp;&emsp;&emsp;&emsp;b| int| 紅色鈕扣數量   |
| &emsp;&emsp;&emsp;&emsp;c| int| 大區中獎次數   |
| &emsp;&emsp;&emsp;&emsp;d| int| 小區中獎次數   |
| &emsp;&emsp;&emsp;&emsp;e| int| 單區中獎次數   |
| &emsp;&emsp;&emsp;&emsp;f| int| 雙區中獎次數   |
| &emsp;&emsp;&emsp;&emsp;g| int| 0紅中獎次數    |
| &emsp;&emsp;&emsp;&emsp;h| int| 1紅中獎次數    |
| &emsp;&emsp;&emsp;&emsp;i| int| 2紅中獎次數    |
| &emsp;&emsp;&emsp;&emsp;j| int| 3紅中獎次數    |
| &emsp;&emsp;&emsp;&emsp;k| int| 4紅中獎次數    |
| --- | *以下為骰寶資料* |
| &emsp;&emsp;&emsp;&emsp;wf| int| [遊戲開獎旗標(WinFlags)](Enums#WinFlags)   |   |
|&emsp;&emsp;&emsp;&emsp;b|int?|第1顆骰子|
|&emsp;&emsp;&emsp;&emsp;c|int?|第2顆骰子|
|&emsp;&emsp;&emsp;&emsp;d|int?|第3顆骰子|
|&emsp;&emsp;&emsp;&emsp;e|int?|骰子點數和|
|&emsp;&emsp;&emsp;&emsp;f|int|雙區中獎次數|
|&emsp;&emsp;&emsp;&emsp;g|int|單區中獎次數|
|&emsp;&emsp;&emsp;&emsp;h|int|大區中獎次數|
|&emsp;&emsp;&emsp;&emsp;i|int|小區中獎次數|
|&emsp;&emsp;&emsp;&emsp;j|int|全圍中獎次數|
|&emsp;&emsp;&emsp;&emsp;k|int|點數 1 中獎次數|
|&emsp;&emsp;&emsp;&emsp;l|int|點數 2 中獎次數|
|&emsp;&emsp;&emsp;&emsp;m|int|點數 3 中獎次數|
|&emsp;&emsp;&emsp;&emsp;n|int|點數 4 中獎次數|
|&emsp;&emsp;&emsp;&emsp;o|int|點數 5 中獎次數|
|&emsp;&emsp;&emsp;&emsp;p|int|點數 6 中獎次數|
|&emsp;&emsp;&emsp;&emsp;q|int|泰式 Hi 中獎次數|
|&emsp;&emsp;&emsp;&emsp;r|int|泰式 Lo 中獎次數|
|&emsp;&emsp;&emsp;&emsp;s|int|泰式 HiLo 中獎次數|
|&emsp;&emsp;&emsp;&emsp;t|int[]|近60局熱門點數和(越前面越熱門)|
|&emsp;&emsp;&emsp;&emsp;u|int[]|近60局冷門點數和(越前面越冷門)|
| ---| *以下為急速骰寶資料* ||
| &emsp;&emsp;&emsp;&emsp;wf|int|[遊戲開獎旗標(WinFlags)](Enums#WinFlags)|
|&emsp;&emsp;&emsp;&emsp;b|int?|第1顆骰子|
|&emsp;&emsp;&emsp;&emsp;c|int|點數 1 中獎次數|
|&emsp;&emsp;&emsp;&emsp;d|int|點數 2 中獎次數|
|&emsp;&emsp;&emsp;&emsp;e|int|點數 3 中獎次數|
|&emsp;&emsp;&emsp;&emsp;f|int|點數 4 中獎次數|
|&emsp;&emsp;&emsp;&emsp;g|int|點數 5 中獎次數|
|&emsp;&emsp;&emsp;&emsp;h|int|點數 6 中獎次數|
|&emsp;&emsp;&emsp;&emsp;i|int|雙區中獎次數|
|&emsp;&emsp;&emsp;&emsp;j|int|單區中獎次數|
|&emsp;&emsp;&emsp;&emsp;k|int|大區中獎次數|
|&emsp;&emsp;&emsp;&emsp;l|int|小區中獎次數|

```json
{
  "a": [
    {
      "tn": "Baccarat",
      "ti": "A",
      "e": [
        {
          "si": 11001,
          "b": 0,
          "c": 0
        },
        {
          "si": 11002,
          "b": 0,
          "c": 0
        }
      ],
      "f": {
        "a": "https://srs.livecasino168.com/bacc/a720.flv",
        "b": "https://srs.livecasino168.com/bacc/a480.flv",
        "b": "https://srs.livecasino168.com/bacc/a1080.flv"
      },
      "j": {
        "wf": 0,
        "b": "",
        "c": "",
        "d": "",
        "e": "",
        "f": "",
        "g": "",
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
      },
      "i": [
        {
          "si": 11001,
          "bt": 1,
          "c": 100
        }
      ]
    }
  ],
  "d": {
    "a": [
      {
        "a": 3,
        "od": 1,
        "c": 5000,
        "d": 100,
        "e": [
          11005,
          11006,
          11007
        ]
      }
    ]
  },
  "h": [
    {
      "c": 3,
      "d": 0,
      "e": 100,
      "f": 5000,
      "g": [
        200,
        500,
        1000,
        2000,
        5000
      ]
    }
  ],
  "err": 0
}
```

---

## **UpdateUserLimitStake**

### 設定玩家限注

Request

|Name|Type|Comment|
|----|----|-------|
|a|int|限注範本編號|

```json
{
  "a": 1
}
```

Reponse

|Name|Type|Comment|
|----|----|-------|
|err|int|[錯誤代碼(GameCenterErrorCode)](Game-Server-Error-Code)|

 ```json
{
  "err": 0
}
```

Reponse

|Name|Type|Comment|
|----|----|-------|
|GameCenterErrorCode|int|[錯誤代碼(GameCenterErrorCode)](Game-Server-Error-Code)|

```json
0
```

---

## **MultipBet**

### 多筆下注

Request

|Name|Type|Comment|
|----|----|-------|
|tn|string|[桌台名稱](Enums#tablename)|
|ti|string|桌號(A, B, C, D)|
|a|object[]|下注列表|
|&emsp;&emsp;si|int|[注區編號(Spots)](Spots)|
|&emsp;&emsp;a|decimal|下注金額|

```json
{
  "tn": "Baccarat",
  "ti": "A",
  "a": [
    {
      "si": 11001,
      "a": 100.0
    },
    {
      "si": 11002,
      "a": 100.0
    }
  ]
}

```

Reponse

|Name|Type|Comment|
|----|----|-------|
|a|object[]|下注回應資訊|
|&emsp;&emsp;err|int|[錯誤代碼(GameCenterErrorCode)](Game-Server-Error-Code)|
|&emsp;&emsp;a|int|下注金額|
|&emsp;&emsp;si|int|[注區編號(Spots)](Spots)|

```json
{
  "a": [
    {
      "err": 0,
      "si": 11001,
      "a": 100.0
    },
    {
      "err": 0,
      "si": 11002,
      "a": 100.0
    }
  ]
}
```

## **QuickMultipBet**

### 快速下注

Request

|Name|Type|Comment|
|----|----|-------|
|tn|string|[桌台名稱](Enums#tablename)|
|ti|string|桌號(A, B, C, D)|
|a|object[]|下注列表|
|&emsp;&emsp;si|int|[注區編號(Spots)](Spots)|
|&emsp;&emsp;a|decimal|下注金額|

```json
{
  "tn": "Baccarat",
  "ti": "A",
  "a": [
    {
      "si": 11001,
      "a": 100.0
    },
    {
      "si": 11002,
      "a": 100.0
    }
  ]
}

```

Reponse

|Name|Type|Comment|
|----|----|-------|
|a|object[]|下注回應資訊|
|&emsp;&emsp;err|int|[錯誤代碼(GameCenterErrorCode)](Game-Server-Error-Code)|
|&emsp;&emsp;a|int|下注金額|
|&emsp;&emsp;si|int|[注區編號(Spots)](Spots)|

```json
{
  "a": [
    {
      "err": 0,
      "si": 11001,
      "a": 100.0
    },
    {
      "err": 0,
      "si": 11002,
      "a": 100.0
    }
  ]
}
```

---

## AcceptJackpotBigWin

### 取回 Jackpot BigWin

Request

|Name|Type|Comment|
|----|----|-------|
|bigWinResponse|int|0:Continue; 1:NotContinueAndGetBonus|

```json
[0]
```

Reponse

|Name|Type|Comment|
|----|----|-------|
|GameCenterErrorCode|int|[錯誤代碼(GameCenterErrorCode)](Game-Server-Error-Code)|
|ContinueWin|int|連贏累積次數|
|Kind|int|[中獎種類(EnumJackpotKind)](Enums#enumjackpotkind)|
|WinAmount|int|中獎金額|
|TotalBetAmount|int|當前累積的下注金額(已結算後)|

```json
{
   "Kind":0,
   "TotalBetAmount":0,
   "ExpectedWinAmount":0,
   "WinAmount":0,
   "ErrorCode":1,
   "ContinueWin":0
}
```

## GetSelfBettingList

### 取得遊戲桌當局下注列表

Request

|Name|Type|Comment|
|----|----|-------|
|tableName|string|[桌台名稱(TableName)](Enums#tablename)|
|tableId|string|桌號(A, B, C, D)|

```json
["Baccarat", "A"]
```

Reponse

|Name|Type|Comment|
|----|----|-------|
|bt|int|[下注模式](Enums#enumbettypes)
|si|int|[注區編號(Spots)](Spots)|
|c|decimal|下注金額|

```json
[
  {
    "bt": 1,
    "si": 11001,
    "c": 10000
  },
  {
    "bt": 1,
    "si": 11002,
    "c": 5000
  }
]
```

## GetGameResult

### 取得遊戲結果

Request

|Name|Type|Comment|
|----|----|-------|
|tn|string|[桌台名稱(TableName)](Enums#tablename)|
|ti|string|桌號(A, B, C, D)|
|ro|int|輪號|
|ru|int|局號|

```json
{
  "tn": "Baccarat",
  "ti": "A",
  "ro": 1234567890,
  "ru": 10
}
```

Response

|Name|Type|Comment|
|----|----|-------|
|err|int|[錯誤代碼(GameCenterErrorCode)](Game-Server-Error-Code)|
|a|string|遊戲結果，中間以逗點分隔|

 ```json
 {
  "err": 0,
  "a": "S1,S1,S1,S1,S1,S1"
 }
 ```

---

## GetMarquee

### 取得公告

Response

| Name|Type|Comment|
|---|--------|---|
|err|int|[錯誤代碼(GameCenterErrorCode)](Game-Server-Error-Code)|
|a| object[] | 公告列表     |
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
|&emsp;&emsp;st  | long   | 開始時間 (NowUnixTimeMs)    |
|&emsp;&emsp;et| long   | 結束時間 (NowUnixTimeMs)    |

```json

```

---

## GetGameLimitStake

### 取得所有遊戲範本

Response

| Name|Type|Comment|
|---|--------|---|
|a| object[] |限注範本列表|
|&emsp;&emsp;a|int|限注範本編號|
|&emsp;&emsp;od|int|賠率|
|&emsp;&emsp;c|decimal|限注上限|
|&emsp;&emsp;d|decimal|限注下限|
|&emsp;&emsp;e|int[] | [注區編號(Spots)](Spots)列表|

```json
{
  "a": [
    {
      "a": 3,
      "od": 1,
      "c": 5000.0,
      "d": 100.0,
      "e": [11005, 11006, 11007]
    },
    {
      "a": 3,
      "od": 2,
      "c": 2500.0,
      "d": 100.0,
      "e": [13152, 13153, 13154]
    }
  ]
}
```

---

## Heartbeat

### 心跳

Response

|Name|Type|Comment|
|---|---|---|
|err|int|[錯誤代碼(GameCenterErrorCode)](Game-Server-Error-Code)|

```json
{
  "err": 1
}
```