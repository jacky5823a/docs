# Reference

## Game Types

| Name           | Game Type ID     | Notice             |
| -------------- | ---------------- | ------------------ |
| Baccarat       | 1                |                    |
| Sic-Bo         | 2                |    |
| Roulette       | 3                |                    |
| Multi-Tables       | 4                |  only using when member login game, the wager hasn't this type                 |
| Dragon Tiger   | 5                |                    |
| Se Die         | 6                |                    |
| Speed Sic-Bo   | 7                | under development      |


## Game Play

| Name                              | GameMethod |
| --------------------------------- | ---------- |
| Standard Baccarat                 | 1          |
| Western Baccarat                  | 2          |
| Commission Free Baccarat(Super 6) | 3          |


## Modified Status
| Status        | Description |
| ----------- | -------------- |
| Normal      | Settle successful |
| Modified    | The game result modified |
| Canceled    | The game round(run) canceled |

## Member Status
| Status | Description      |
| ---- | ----------- |
| 3    | Normal      |
| 2    | Can not bet |
| -2   | Banned      |

## Wager(Betting Slip) Status
| Status | Description                | |
| ---- | --------------------- | --- |
| 1    | winning | Member winning on any spot    | 
| 2    | losing | Member not winning on any spot                 |
| 3    | tie | The win/loss is 0 and the [valid bet amount](#Valid-Bet-Amount) is 0 |
| ~~4~~  | ~~in progress~~ |  There is no unsettled wagers for asynchronous bet records           |
| 6    | canceled | The game round(run) canceled |
| 7    | modified | The game result modified |

## Error Code

| code | description               |http status code |
| ---- | ---------------------- |----------------------
| 3    | Invaild hash     |401|
| 4    | The data was not found           |404|
| 5    | Http method not allowed |405|
| 6    | Function not found              |404|
| 8    | Account already exists             |404|
| 15    | The param is required / Data Format Error / The param validation failed          |422|
|19 | The member has no credit |400|
| 36   | IP not allow            |401|
| 65   | Remote API error        |500|
| 77   | Member not exists              |404|
|78   | Member logining blocked            |401|
|999   | Unknown error / Other errors             |(Not fixed)|

## Game Languages

| Code  | Description          |
| ----- | -------------------- |
| zh-CN | Simple Chinese       |
| zh-TW | Tranditional Chinese |
| en / en-US | English              |
| th    | Thai                 |
| id    | Indonesian           |
| ko    | Korean               |
| ja    | Japanese             |
| vi / vn   | Vietnamese           |
| ms | Malay |


## Game Result

- Baccarat: [Player 1st,Banker 1st,Player 2nd,Banker 2nd,Player 3rd,Banker 3rd], empty if no third card, ex: `D2,DK,C4,H7,,`
- Sicbo: [dice number,dice number,dice number]，ex: `3,5,1`
- Roulette: [number]，ex: `15`
- Dragon Tiger: [Dragon 1st,Tiger 1st]，ex: `C4,H7`
- Sedie: [count of red]，ex: `2`
- Speed Sicbo: [dice number]，ex: `3`

### Playing Card Code

The playing card code is a combination of suits and numbers, ex. SA stands for Ace of Spades.

#### Suits

| Code | Corresponding |
| ---- | ------------- |
| S    | Spade         |
| H    | Heart         |
| D    | Diamond       |
| C    | Club          |

#### Numbers

| Code | Corresponding |
| ---- | ------------- |
| 1    | A             |
| 2    | 2             |
| 3    | 3             |
| 4    | 4             |
| 5    | 5             |
| 6    | 6             |
| 7    | 7             |
| 8    | 8             |
| 9    | 9             |
| 0    | 10            |
| J    | J             |
| Q    | Q             |
| K    | K             |

## Bet Type

| Property  | Type | Description |
| ----- | -------------------- | -------------------- |
| odds | number | The odd of the spot |
| spotId | int | [Spot](#Spot) |
| spotName | string | [Spot](#Spot) |
| betAmount | number |  Sum of bet amount by spot |
| loseWinAmount | number | Sum of win/lose by spot |

If a member place Banker 100, Banker 100, Banker Pair 100, there are two records in `BetType` which are Banker 200 and Banker Pair 100 

```json
[
  {
    "spotId": 1,
    "spotName": "Banker",
    "betAmount": 200,
    "loseWinAmount": -200,
    "odds": 0.95
  },
  {
    "spotId": 1,
    "spotName": "BankerPair",
    "betAmount": 100,
    "loseWinAmount": -100,
    "odds": 11
   }
]
```

## Spot

### Baccarat
| id | name | Description |
| --- | --- | --- |
| 1 | Banker           | Bankder                |
| 2 | Player           | Player                 |
| 3 | Big              | High                    |
| 4 | Small            | Low                  |
| 5 | PlayerJQK        | Player J.Q.K           |
| 6 | BankerJQK        | Banker J.Q.K           |
| 7 | PlayerOdd        | Player Odd             |
| 8 | PlayerEven       | Player Even            |
| 9 | BankerOdd        | Banker Odd             |
| 10 | BankerEven       | Banker Even            | 
| 11 | PlayerBankerJQK  | Player Banker J.Q.K    |
| 12 | PlayerA          | Player A               |
| 13 | BankerA          | Banker A               |
| 14 | Tie              | Tie                    |
| 15 | PlayerPair       | Player Pair            |
| 16 | BankerPair       | Banker Pair            |
| 17 | PlayerJQKA       | Player J.Q.K.A         |
| 18 | BankerJQKA       | Banker J.Q.K.A         |
| 19 | PlayerBankerA    | Player Banker A        |
| 20 | PlayerBankerJQKA | Player Bannker J.Q.K.A |
| 21 | BankerNoRefund   | Banker and no refund   | 
| 22 | PlayerNoRefund   | Player and no refund   |
| 23 | TieNoRefund      | Tie and no refund      |
| 24 | BankerPairNoRefund | Banker pair and no refund   |
| 25 | PlayerPairNoRefund | Player Pair and no refund   |
| 26 | Super6           | Super 6                |


### Roulette
| id | name | Description |
| --- | --- | --- |
| 27 | 1 | Number 01 | 
| 28 | 2 | Number 02 | 
| 29 | 3 | Number 03 | 
| 30 | 4 | Number 04 | 
| 31 | 5 | Number 05 | 
| 32 | 6 | Number 06 | 
| 33 | 7 | Number 07 | 
| 34 | 8 | Number 08 | 
| 35 | 9 | Number 09 | 
| 36 | 10 | Number 10 | 
| 37 | 11 | Number 11 | 
| 38 | 12 | Number 12 | 
| 39 | 13 | Number 13 | 
| 40 | 14 | Number 14 | 
| 41 | 15 | Number 15 | 
| 42 | 16 | Number 16 | 
| 43 | 17 | Number 17 | 
| 44 | 18 | Number 18 | 
| 45 | 19 | Number 19 | 
| 46 | 20 | Number 20 | 
| 47 | 21 | Number 21 | 
| 48 | 22 | Number 22 | 
| 49 | 23 | Number 23 | 
| 50 | 24 | Number 24 | 
| 51 | 25 | Number 25 | 
| 52 | 26 | Number 26 | 
| 53 | 27 | Number 27 | 
| 54 | 28 | Number 28 | 
| 55 | 29 | Number 29 | 
| 56 | 30 | Number 30 | 
| 57 | 31 | Number 31 | 
| 58 | 32 | Number 32 | 
| 59 | 33 | Number 33 | 
| 60 | 34 | Number 34 | 
| 61 | 35 | Number 35 | 
| 62 | 36 | Number 36 | 
| 63 | 0 | Number 0 | 
| 64 | Big | High | 
| 65 | Small | Low | 
| 66 | Odd | Odd | 
| 67 | Even | Even | 
| 68 | Red | Red | 
| 69 | Black | Black | 
| 70 | Split_1_2 | Split(01,02) | 
| 71 | Split_1_4 | Split(01,04) | 
| 72 | Split_2_3 | Split(02,03) | 
| 73 | Split_2_5 | Split(02,05) | 
| 74 | Split_3_6 | Split(03,06) | 
| 75 | Split_4_6 | Split(04,05) | 
| 76 | Split_4_7 | Split(04,07) | 
| 77 | Split_5_6 | Split(05,06) | 
| 78 | Split_5_8 | Split(05,08) | 
| 79 | Split_6_9 | Split(06,09) | 
| 80 | Split_7_8 | Split(07,08) | 
| 81 | Split_7_10 | Split(07,10) | 
| 82 | Split_8_9 | Split(08,09) | 
| 83 | Split_8_11 | Split(08,11) | 
| 84 | Split_9_12 | Split(09,12) | 
| 85 | Split_10_11 | Split(10,11) | 
| 86 | Split_10_13 | Split(10,13) | 
| 87 | Split_11_12 | Split(11,12) | 
| 88 | Split_11_14 | Split(11,14) | 
| 89 | Split_12_15 | Split(12,15) | 
| 90 | Split_13_14 | Split(13,14) | 
| 91 | Split_13_16 | Split(13,16) | 
| 92 | Split_14_15 | Split(14,15) | 
| 93 | Split_14_17 | Split(14,17) | 
| 94 | Split_15_18 | Split(15,18) | 
| 95 | Split_16_17 | Split(16,17) | 
| 96 | Split_16_19 | Split(16,19) | 
| 97 | Split_17_18 | Split(17,18) | 
| 98 | Split_17_20 | Split(17,20) | 
| 99 | Split_18_21 | Split(18,21) | 
| 100 | Split_19_20 | Split(19,20) | 
| 101 | Split_19_22 | Split(19,22) | 
| 102 | Split_20_21 | Split(20,21) | 
| 103 | Split_20_23 | Split(20,23) | 
| 104 | Split_21_24 | Split(21,24) | 
| 105 | Split_22_23 | Split(22,23) | 
| 106 | Split_22_25 | Split(22,25) | 
| 107 | Split_23_24 | Split(23,24) | 
| 108 | Split_23_26 | Split(23,26) | 
| 109 | Split_24_27 | Split(24,27) | 
| 110 | Split_25_26 | Split(25,26) | 
| 111 | Split_25_28 | Split(25,28) | 
| 112 | Split_26_27 | Split(26,27) | 
| 113 | Split_26_29 | Split(26,29) | 
| 114 | Split_27_30 | Split(27,30) | 
| 115 | Split_28_29 | Split(28,29) | 
| 116 | Split_28_31 | Split(28,31) | 
| 117 | Split_29_30 | Split(29,30) | 
| 118 | Split_29_32 | Split(29,32) | 
| 119 | Split_30_33 | Split(30,33) | 
| 120 | Split_31_32 | Split(31,32) | 
| 121 | Split_31_34 | Split(31,34) | 
| 122 | Split_32_33 | Split(32,33) | 
| 123 | Split_32_35 | Split(32,35) | 
| 124 | Split_33_36 | Split(33,36) | 
| 125 | Split_34_35 | Split(34,35) | 
| 126 | Split_35_36 | Split(35,36) | 
| 127| ThreeNumber_0_1_2 | Three Number(00,01,02) | 
| 128 | ThreeNumber_0_2_3 | Three Number(00,02,03) | 
| 129 | Street_1 | Street(01,02,03) | 
| 130 | Street_4 | Street(04,05,06) | 
| 131 | Street_7 | Street(07,08,09) | 
| 132 | Street_10 | Street(10,11,12) | 
| 133 | Street_13 | Street(13,14,15) | 
| 134 | Street_16 | Street(16,17,18) | 
| 135 | Street_19 | Street(19,20,21) | 
| 136 | Street_22 | Street(22,23,24) | 
| 137 | Street_25 | Street(25,26,27) | 
| 138 | Street_28 | Street(28,29,30) | 
| 139 | Street_31 | Street(31,32,33) | 
| 140 | Street_34 | Street(34,35,36) | 
| 141 | FourNumber | Four Number(00,01,02,03) | 
| 142 | Corner_3 | Corner(01,02,04,05) | 
| 143| Corner_4 | Corner(02,03,05,06) | 
| 144 | Corner_6 | Corner(04,05,07,08) | 
| 145 | Corner_7 | Corner(05,06,08,09) | 
| 146 | Corner_9 | Corner(07,08,10,11) | 
| 147 | Corner_10 | Corner(08,09,11,12) | 
| 148 | Corner_12 | Corner(10,11,13,14) | 
| 149 | Corner_13 | Corner(11,12,14,15) | 
| 150 | Corner_15 | Corner(13,14,16,17) | 
| 151 | Corner_16 | Corner(14,15,17,18) | 
| 152 | Corner_18 | Corner(16,17,19,20) | 
| 153 | Corner_19 | Corner(17,18,20,21) | 
| 154 | Corner_21 | Corner(19,20,22,23) | 
| 155 | Corner_22 | Corner(20,21,23,24) | 
| 156 | Corner_24 | Corner(22,23,25,26) | 
| 157 | Corner_25 | Corner(23,24,26,27) | 
| 158 | Corner_27 | Corner(25,26,28,29) | 
| 159 | Corner_28 | Corner(26,27,29,30) | 
| 160 | Corner_30 | Corner(28,29,31,32) | 
| 161 | Corner_31 | Corner(29,30,32,33) | 
| 162 | Corner_33 | Corner(31,32,34,35) | 
| 163 | Corner_34 | Corner(32,33,35,36) | 
| 164 | Line_1 | Line(01~06) | 
| 165 | Line_4 | Line(04~09) | 
| 166 | Line_7 | Line(07~12) | 
| 167 | Line_10 | Line(10~15) | 
| 168 | Line_13 | Line(13~18) | 
| 169 | Line_16 | Line(16~21) | 
| 170 | Line_19 | Line(19~24) | 
| 171 | Line_22 | Line(22~27) | 
| 172 | Line_25 | Line(25~30) | 
| 173 | Line_28 | Line(28~33) | 
| 174 | Line_31 | Line(31~36) | 
| 175 | Dozen_1st | 1st Dozen | 
| 176 | Dozen_2nd | 2nd Dozen | 
| 177 | Dozen_3rd | 3rd Dozen| 
| 178 | Column_1st | 1st Column | 
| 179 | Column_2nd | 2nd Column | 
| 180 | Column_3rd | 3rd Column | 


### Dragon Tiger

| id | name | Description |
| --- | --- | --- |
| 181  Dragon           | Dragon                 |
| 182 | Tiger            | Tiger                  |
| 183 | Tie | Tie |


### Sedie

| id | name | Description |
| --- | --- | --- |
| 192 | Big | High | 
| 193 | Small | Low | 
| 194 | Odd | Odd | 
| 195 | Even | Even | 
| 196 | Zero | Red 0 | 
| 197 | One | Red 1 | 
| 198 | Three | Red 3 | 
| 199 | Four | Red 4 | 

### Sicbo

| id | name | Description |
| --- | --- | --- |
| 200 | ThreeForces1 | Three Forces 1 | 
| 201 | ThreeForces2 | Three Forces 2 | 
| 202 | ThreeForces3 | Three Forces 3 | 
| 203 | ThreeForces4 | Three Forces 4 | 
| 204 | ThreeForces5 | Three Forces 5 | 
| 205 | ThreeForces6 | Three Forces 6 | 
| 206 | Big | Big | 
| 207 | Small | Small | 
| 208 | Odd | Odd | 
| 209 | Even | Even | 
| 210 | Total4 | Total of points is 4 | 
| 211 | Total5 | Total of points is 5 | 
| 212 | Total6 | Total of points is 6 | 
| 213 | Total7 | Total of points is 7 | 
| 214 | Total8 | Total of points is 8 | 
| 215 | Total9 | Total of points is 9 | 
| 216 | Total10 | Total of points is 10 | 
| 217 | Total11 | Total of points is 11 | 
| 218 | Total12 | Total of points is 12 | 
| 219 | Total13 | Total of points is 13 | 
| 220 | Total14 | Total of points is 14 | 
| 221 | Total15 | Total of points is 15 | 
| 222 | Total16 | Total of points is 16 | 
| 223 | Total17 | Total of points is 17 | 
| 224 | PaiGow12 | Two Dice Combination 1、2 | 
| 225 | PaiGow13 | Two Dice Combination 1、3 | 
| 226 | PaiGow14 | Two Dice Combination 1、4 | 
| 227 | PaiGow15 | Two Dice Combination 1、5 | 
| 228 | PaiGow16 | Two Dice Combination 1、6 | 
| 229 | PaiGow23 | Two Dice Combination 2、3 | 
| 230 | PaiGow24 | Two Dice Combination 2、4 | 
| 231 | PaiGow25 | Two Dice Combination 2、5 | 
| 232 | PaiGow26 | Two Dice Combination 2、6 | 
| 233 | PaiGow34 | Two Dice Combination 3、4 | 
| 234 | PaiGow35 | Two Dice Combination 3、5 | 
| 235 | PaiGow36 | Two Dice Combination 3、6 | 
| 236 | PaiGow45 | Two Dice Combination 4、5 | 
| 237 | PaiGow46 | Two Dice Combination 4、6 | 
| 238 | PaiGow56 | Two Dice Combination 5、6 | 
| 239 | Pair1 | Pair 1 | 
| 240 | Pair2 | Pair 2 | 
| 241 | Pair3 | Pair 3 | 
| 242 | Pair4 | Pair 4 | 
| 243 | Pair5 | Pair 5 | 
| 244 | Pair6 | Pair 6 | 
| 245 | TripleAny | Any Triple | 
| 246 | Triple1 | Specific Triple 1 | 
| 247 | Triple2 | Specific Triple 2 | 
| 248 | Triple3 | Specific Triple 3 | 
| 249 | Triple4 | Specific Triple 4 | 
| 250 | Triple5 | Specific Triple 5 | 
| 251 | Triple6 | Specific Triple 6 | 
| 252 | Hi | Hi | 
| 253 | Lo | Lo | 
| 254 | 11-Hi-Lo | 11-Hi-Lo | 
| 255 | 1-Lo | 1-Lo | 
| 256 | 2-Lo | 2-Lo | 
| 257 | 3-Lo | 3-Lo | 
| 258 | 4-Lo | 4-Lo | 
| 259 | 5-Lo | 5-Lo | 
| 260 | 6-Lo | 6-Lo | 
| 261 | 1-Hi | 1-Hi | 
| 262 | 2-Hi | 2-Hi | 
| 263 | 3-Hi | 3-Hi | 
| 264 | 4-Hi | 4-Hi | 
| 265 | 5-Hi | 5-Hi | 
| 266 | 6-Hi | 6-Hi | 
| 267 | 1,2,3 | 1,2,3 | 
| 268 | 2,3,4 | 2,3,4 | 
| 269 | 3,4,5 | 3,4,5 | 
| 270 | 4,5,6 | 4,5,6 |
| 271 | HiLoThreeForces1 | Hi-Lo Three Forces 1 | 
| 272 | HiLoThreeForces2 | Hi-Lo Three Forces 2 | 
| 273 | HiLoThreeForces3 | Hi-Lo Three Forces 3 | 
| 274 | HiLoThreeForces4 | Hi-Lo Three Forces 4 | 
| 275 | HiLoThreeForces5 | Hi-Lo Three Forces 5 | 
| 276 | HiLoThreeForces6 | Hi-Lo Three Forces 6 |  


### Speed Sicbo

| id | name | Description |
| --- | --- | --- |
| 277 | 1 | 1 | 
| 278 | 2 | 2 | 
| 279 | 3 | 3 | 
| 280 | 4 | 4 | 
| 281 | 5 | 5 | 
| 282 | 6 | 6 | 
| 283 | Big | High | 
| 284 | Small | Low | 
| 285 | Odd | Odd | 
|286 | Even | Even | 

## Valid Bet Amount
- The diff between Banker/Player, or High/Low. If a player place on the Banker 200 and on the Player 100 and game result is not tie. The valid bet amount would be 100 
- If the game result of Baccarat is tie, the valid bet amount of Banker and Player would be 0. If a player place on the Banker 200 and on the Player 200 and game result is tie, the valid bet amount would be 0
- If the game result of DragonTiger is tie,  the valid bet amount would be the half of bet amount. If a player place on the Dragon 200 and game result is tie, the valid bet amount would be 100
- Other than the conditions above, the valid bet amount would be as same as the bet amount


## Tables

| Property  | Type | Description |
| ----- | -------------------- | -------------------- |
| TableId | string | Please refer to the main doc |
| GameType | string | Baccarat、DragonTiger、Roulette、Sedie、SpeedSicbo |
| IsEnabled | boolean |  |

## Transactions

All of single bets in a wager by a player

| Property  | Type | Description |
| ----- | -------------------- | -------------------- |
| transactionId | string | Transaction ID |
| spotId | int | [Spot](#Spot) |
| spotName | string | [Spot](#Spot) |
| betAmount | number |  The bet amount |
| payoffAmount | number | The win/lose amount |

If a member place Banker 100, Banker 100, Banker Pair 100, there are three records in `Transactions`.

```json
[
  {
    "transactionId": "c4a24b88-2405-4b00-910c-a252405e5945",
    "spotId": 1,
    "spotName": "Banker",
    "betAmount": 100,
    "payoffAmount": -100
  },
  {
    "transactionId": "1feeb813-5bd5-468c-be48-0355f0116cd8",
    "spotId": 1,
    "spotName": "Banker",
    "betAmount": 100,
    "payoffAmount": -100
  },
  {
    "transactionId": "6b74b2ce-dca8-4a71-9b94-4a410d5a3568",
    "spotId": 1,
    "spotName": "BankerPair",
    "betAmount": 100,
    "payoffAmount": -100
   }
]
```
