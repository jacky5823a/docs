#

## **TableName**

桌台名稱

| Name | Description | Code |
|------| ----------- | ---- |
|Baccarat | 百家樂 | Baccarat |
|Sicbo | 骰寶 | Sicbo |
|Roulette | 輪盤 | Roulette |
|DragonTiger | 龍虎 | DragonTiger |
|Sedie|色碟|Sedie|
|SpeedSicbo|急速骰寶|SpeedSicbo|
|MultipleTable | 多桌 | MultipleTable |
|Lobby | 大廳(只有在公告處使用) | Lobby |
---

## **GameStatus**

遊戲狀態

| Name | Description | Code |
| ---- | ----------- | ---- |
|CountDown|倒數|1|
|Dealing|開牌|2|
|Computing|結算|3|
|HalfTime|中場|4|
|Maintenance|維修|5|
|NewRoundRun|新輪新局|6|
|ComputingFinish|結算完畢|7|
|EndBetTime|下注時間結束|8|
|MiCard|眯牌|9|
|EndMiCardTime|眯牌時間結束|10|
|CancellThisRun|取消此局|11|
|DealerChanged|更換荷官|12|
---

## **WinFlags**

遊戲開獎旗標

| Name | Description | Code |
| ---- | ----------- | ---- |
|NoResult|沒有結果|0|
|BankerWin|莊家贏|1|
|PlayerWin|閒家贏|2|
|Draw|和(Tie)|3|
|DragonWin|龍贏|4|
|TigerWin|虎贏|5|
|Roulette00  |輪盤 0 | 100|
|Roulette01  |輪盤 1 | 101|
|Roulette02  |輪盤 2 | 102|
|Roulette03  |輪盤 3 | 103|
|Roulette04  |輪盤 4 | 104|
|Roulette05  |輪盤 5 | 105|
|Roulette06  |輪盤 6 | 106|
|Roulette07  |輪盤 7 | 107|
|Roulette08  |輪盤 8 | 108|
|Roulette09  |輪盤 9 | 109|
|Roulette10 |輪盤 10| 110|
|Roulette11 |輪盤 11| 111|
|Roulette12 |輪盤 12| 112|
|Roulette13 |輪盤 13| 113|
|Roulette14 |輪盤 14| 114|
|Roulette15 |輪盤 15| 115|
|Roulette16 |輪盤 16| 116|
|Roulette17 |輪盤 17| 117|
|Roulette18 |輪盤 18| 118|
|Roulette19 |輪盤 19| 119|
|Roulette20 |輪盤 20| 120|
|Roulette21 |輪盤 21| 121|
|Roulette22 |輪盤 22| 122|
|Roulette23 |輪盤 23| 123|
|Roulette24 |輪盤 24| 124|
|Roulette25 |輪盤 25| 125|
|Roulette26 |輪盤 26| 126|
|Roulette27 |輪盤 27| 127|
|Roulette28 |輪盤 28| 128|
|Roulette29 |輪盤 29| 129|
|Roulette30 |輪盤 30| 130|
|Roulette31 |輪盤 31| 131|
|Roulette32 |輪盤 32| 132|
|Roulette33 |輪盤 33| 133|
|Roulette34 |輪盤 34| 134|
|Roulette35 |輪盤 35| 135|
|Roulette36 |輪盤 36| 136|
|Sedie0|色碟 0 紅|140|
|Sedie1|色碟 1 紅|141|
|Sedie2|色碟 2 紅|142|
|Sedie3|色碟 3 紅|143|
|Sedie4|色碟 4 紅|144|
|Sicbo3|骰寶總和 3|150|
|Sicbo4|骰寶總和 4|151|
|Sicbo5|骰寶總和 5|152|
|Sicbo6|骰寶總和 6|153|
|Sicbo7|骰寶總和 7|154|
|Sicbo8|骰寶總和 8|155|
|Sicbo9|骰寶總和 9|156|
|Sicbo10|骰寶總和 10|157|
|Sicbo11|骰寶總和 11|158|
|Sicbo12|骰寶總和 12|159|
|Sicbo13|骰寶總和 13|160|
|Sicbo14|骰寶總和 14|161|
|Sicbo15|骰寶總和 15|162|
|Sicbo16|骰寶總和 16|163|
|Sicbo17|骰寶總和 17|164|
|Sicbo18|骰寶總和 18|165|
|SpeedSicbo1|急速骰寶1|170|
|SpeedSicbo2|急速骰寶2|171|
|SpeedSicbo3|急速骰寶3|172|
|SpeedSicbo4|急速骰寶4|173|
|SpeedSicbo5|急速骰寶5|174|
|SpeedSicbo6|急速骰寶6|175|
---

## **EnumRestoreCreditStatus**

回復信用狀態

| Name | Description| Code |
| ---- | ---------- | ---- |
|ReStoreStart|回復開始|1|
|RestoreStop|回復結束|2|
---

## **EnumKeyUserReason**

玩家被踢原因

| Name | Description| Code |
| ---- | ---------- | ---- |
|NoReason|沒原因|1|
|DisableUser|停用|2|
|DuplicateLogin|重複登入|3|
---

## **EnumGameMode**

遊戲玩法

| Name | Description| Code |
| ---- | ---------- | ---- |
| None | 無結果 | 0 |
| Standard | 標準 | 1 |
| Western | 西洋(百家樂) | 2 |
| NoRefund | 免水(百家樂) | 3 |
| HiLo |泰式(骰寶)|4|

---

## **EnumBetTypes**

下注模式

| Name | Description| Code |
| ---- | ---------- | ---- |
| SingleTableBet | 單桌下注 | 1 |
| MultipleTableBet | 多台下注 | 2 |
---

## **EnumTableMode**

百家樂桌台類型

| Name | Description | Code |
| ---- | ----------- | ---- |
|Unknown|未知|0|
|Standard|一般|1|
|Speed|快速|2|
|MiCard|咪牌|3|
---

## **EnumVideoProvider**

視訊提供商

| Name | Description| Code |
| ---- | ---------- | ---- |
| Demo | 測試機 | 1 |
| HotleAndCasino | 柬埔寨 | 2 |
| WaterCube | 水立方 | 3 |
| Vivo | Vivo  | 4|
---

## **EnumJackpotKind**

中獎種類

| Name | Description | Code |
|------| ----------- | ---- |
| NonJackpot | 累積中或沒中獎 | 0 |
| JackpotBonus | 中第一階段小獎金 | 1 |
| JackpotBigWin | 中JP獎(15局~19局) | 2 |
| JackpotBigWinNotArrive | 已達15局(含以上)但是未達該局中Jackpot的下注金額 | 3 |
| FinalJackpotBigWin | 中最終的JP(第20局) | 4 |
---

## **EnumCurrencyType**

幣別

| Name | Description| Code |
| ---- | ---------- | ---- |
|NONE|未定義|0|
|NTD|台幣|1|
|CNY|人民幣|2|
|USD|美金|3|
|THB|泰銖|4|
|IDR|印尼盾|5|
|MYR|馬幣|6|
|VND|越南盾|7|
|KRW|韓元|8|
|SGD|新加坡幣|9|
|NZD|紐西蘭幣|10|
|AUD|澳幣|11|
|JPY|日圓|12|
|INR|印度盧比|13|
|HKD|港幣|14|
|USDT|泰達幣|15|
|PHP|菲律賓披索|16|
|KVND|千越南盾|17|
|KIDR|千印尼盾|18|
|SDCREDIT|百分之一台幣|19|
|NFCREDIT|美金對日幣|20|
---

## **EnumPlatform**

執行平台
| Name | Description| Code |
| ---- | ---------- | ---- |
|Web|網頁版|1|
|App|手機版|2|
