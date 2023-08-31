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

| Code        | Description          |
|-------------| -------------------- |
| zh-CN       | Simple Chinese       |
| zh-TW       | Tranditional Chinese |
| en or en-US | English              |
| th          | Thai                 |
| id          | Indonesian           |
| ko          | Korean               |
| ja          | Japanese             |
| vi or vn    | Vietnamese           |
| ms          | Malay |
| pt          | Portuguese |


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

### Baccarat(GameType = 1)
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
| 27 | AnyPair           | Any Pair                |
| 28 | PerfectPairs           | Perfect Pairs                |
| 29 | BankerBonus           | Banker Bonus                |
| 30 | PlayerBonus           | Player Bonus                |
| 31 | BankerNatural           | Banker Natural                |
| 32 | PlayerNatural           | Player Natural                |
| 33 | Lucky6           | Lucky 6                |

### Sicbo(GameType = 2)

| id | name | Description |
| --- | --- | --- |
| 1 | ThreeForces1 | Three Forces 1 | 
| 2 | ThreeForces2 | Three Forces 2 | 
| 3 | ThreeForces3 | Three Forces 3 | 
| 4 | ThreeForces4 | Three Forces 4 | 
| 5 | ThreeForces5 | Three Forces 5 | 
| 6 | ThreeForces6 | Three Forces 6 | 
| 7 | Big | Big | 
| 8 | Small | Small | 
| 9 | Odd | Odd | 
| 10 | Even | Even | 
| 11 | Total4 | Total of points is 4 | 
| 12 | Total5 | Total of points is 5 | 
| 13 | Total6 | Total of points is 6 | 
| 14 | Total7 | Total of points is 7 | 
| 15 | Total8 | Total of points is 8 | 
| 16 | Total9 | Total of points is 9 | 
| 17 | Total10 | Total of points is 10 | 
| 18 | Total11 | Total of points is 11 | 
| 19 | Total12 | Total of points is 12 | 
| 20 | Total13 | Total of points is 13 | 
| 21 | Total14 | Total of points is 14 | 
| 22 | Total15 | Total of points is 15 | 
| 23 | Total16 | Total of points is 16 | 
| 24 | Total17 | Total of points is 17 | 
| 25 | PaiGow12 | Two Dice Combination 1、2 | 
| 26 | PaiGow13 | Two Dice Combination 1、3 | 
| 27 | PaiGow14 | Two Dice Combination 1、4 | 
| 28 | PaiGow15 | Two Dice Combination 1、5 | 
| 29 | PaiGow16 | Two Dice Combination 1、6 | 
| 30 | PaiGow23 | Two Dice Combination 2、3 | 
| 31 | PaiGow24 | Two Dice Combination 2、4 | 
| 32 | PaiGow25 | Two Dice Combination 2、5 | 
| 33 | PaiGow26 | Two Dice Combination 2、6 | 
| 34 | PaiGow34 | Two Dice Combination 3、4 | 
| 35 | PaiGow35 | Two Dice Combination 3、5 | 
| 36 | PaiGow36 | Two Dice Combination 3、6 | 
| 37 | PaiGow45 | Two Dice Combination 4、5 | 
| 38 | PaiGow46 | Two Dice Combination 4、6 | 
| 39 | PaiGow56 | Two Dice Combination 5、6 | 
| 40 | Pair1 | Pair 1 | 
| 41 | Pair2 | Pair 2 | 
| 42 | Pair3 | Pair 3 | 
| 43 | Pair4 | Pair 4 | 
| 44 | Pair5 | Pair 5 | 
| 45 | Pair6 | Pair 6 | 
| 46 | TripleAny | Any Triple | 
| 47 | Triple1 | Specific Triple 1 | 
| 48 | Triple2 | Specific Triple 2 | 
| 49 | Triple3 | Specific Triple 3 | 
| 50 | Triple4 | Specific Triple 4 | 
| 51 | Triple5 | Specific Triple 5 | 
| 52 | Triple6 | Specific Triple 6 | 
| 53 | Hi | Hi | 
| 54 | Lo | Lo | 
| 55 | 11-Hi-Lo | 11-Hi-Lo | 
| 56 | 1-Lo | 1-Lo | 
| 57 | 2-Lo | 2-Lo | 
| 58 | 3-Lo | 3-Lo | 
| 59 | 4-Lo | 4-Lo | 
| 60 | 5-Lo | 5-Lo | 
| 61 | 6-Lo | 6-Lo | 
| 62 | 1-Hi | 1-Hi | 
| 63 | 2-Hi | 2-Hi | 
| 64 | 3-Hi | 3-Hi | 
| 65 | 4-Hi | 4-Hi | 
| 66 | 5-Hi | 5-Hi | 
| 67 | 6-Hi | 6-Hi | 
| 68 | 1,2,3 | 1,2,3 | 
| 69 | 2,3,4 | 2,3,4 | 
| 70 | 3,4,5 | 3,4,5 | 
| 71 | 4,5,6 | 4,5,6 |
| 72 | HiLoThreeForces1 | Hi-Lo Three Forces 1 | 
| 73 | HiLoThreeForces2 | Hi-Lo Three Forces 2 | 
| 74 | HiLoThreeForces3 | Hi-Lo Three Forces 3 | 
| 75 | HiLoThreeForces4 | Hi-Lo Three Forces 4 | 
| 76 | HiLoThreeForces5 | Hi-Lo Three Forces 5 | 
| 77 | HiLoThreeForces6 | Hi-Lo Three Forces 6 |  

### Roulette(Game Type = 3)
| id | name | Description |
| --- | --- | --- |
| 1 | 1 | Number 01 | 
| 2 | 2 | Number 02 | 
| 3 | 3 | Number 03 | 
| 4 | 4 | Number 04 | 
| 5 | 5 | Number 05 | 
| 6 | 6 | Number 06 | 
| 7 | 7 | Number 07 | 
| 8 | 8 | Number 08 | 
| 9 | 9 | Number 09 | 
| 10 | 10 | Number 10 | 
| 11 | 11 | Number 11 | 
| 12 | 12 | Number 12 | 
| 13 | 13 | Number 13 | 
| 14 | 14 | Number 14 | 
| 15 | 15 | Number 15 | 
| 16 | 16 | Number 16 | 
| 17 | 17 | Number 17 | 
| 18 | 18 | Number 18 | 
| 19 | 19 | Number 19 | 
| 20 | 20 | Number 20 | 
| 21 | 21 | Number 21 | 
| 22 | 22 | Number 22 | 
| 23 | 23 | Number 23 | 
| 24 | 24 | Number 24 | 
| 25 | 25 | Number 25 | 
| 26 | 26 | Number 26 | 
| 27 | 27 | Number 27 | 
| 28 | 28 | Number 28 | 
| 29 | 29 | Number 29 | 
| 30 | 30 | Number 30 | 
| 31 | 31 | Number 31 | 
| 32 | 32 | Number 32 | 
| 33 | 33 | Number 33 | 
| 34 | 34 | Number 34 | 
| 35 | 35 | Number 35 | 
| 36 | 36 | Number 36 | 
| 37 | 0 | Number 0 | 
| 38 | Big | High | 
| 39 | Small | Low | 
| 40 | Odd | Odd | 
| 41 | Even | Even | 
| 42 | Red | Red | 
| 43 | Black | Black | 
| 47 | Split_1_2 | Split(01,02) | 
| 48 | Split_1_4 | Split(01,04) | 
| 49 | Split_2_3 | Split(02,03) | 
| 50 | Split_2_5 | Split(02,05) | 
| 51 | Split_3_6 | Split(03,06) | 
| 52 | Split_4_6 | Split(04,05) | 
| 53 | Split_4_7 | Split(04,07) | 
| 54 | Split_5_6 | Split(05,06) | 
| 55 | Split_5_8 | Split(05,08) | 
| 56 | Split_6_9 | Split(06,09) | 
| 57 | Split_7_8 | Split(07,08) | 
| 58 | Split_7_10 | Split(07,10) | 
| 59 | Split_8_9 | Split(08,09) | 
| 60 | Split_8_11 | Split(08,11) | 
| 61 | Split_9_12 | Split(09,12) | 
| 62 | Split_10_11 | Split(10,11) | 
| 63 | Split_10_13 | Split(10,13) | 
| 64 | Split_11_12 | Split(11,12) | 
| 65 | Split_11_14 | Split(11,14) | 
| 66 | Split_12_15 | Split(12,15) | 
| 67 | Split_13_14 | Split(13,14) | 
| 68 | Split_13_16 | Split(13,16) | 
| 69 | Split_14_15 | Split(14,15) | 
| 70 | Split_14_17 | Split(14,17) | 
| 71 | Split_15_18 | Split(15,18) | 
| 72 | Split_16_17 | Split(16,17) | 
| 73 | Split_16_19 | Split(16,19) | 
| 74 | Split_17_18 | Split(17,18) | 
| 75 | Split_17_20 | Split(17,20) | 
| 76 | Split_18_21 | Split(18,21) | 
| 77 | Split_19_20 | Split(19,20) | 
| 78 | Split_19_22 | Split(19,22) | 
| 79 | Split_20_21 | Split(20,21) | 
| 80 | Split_20_23 | Split(20,23) | 
| 81 | Split_21_24 | Split(21,24) | 
| 82 | Split_22_23 | Split(22,23) | 
| 83 | Split_22_25 | Split(22,25) | 
| 84 | Split_23_24 | Split(23,24) | 
| 85 | Split_23_26 | Split(23,26) | 
| 86 | Split_24_27 | Split(24,27) | 
| 87 | Split_25_26 | Split(25,26) | 
| 88 | Split_25_28 | Split(25,28) | 
| 89 | Split_26_27 | Split(26,27) | 
| 90 | Split_26_29 | Split(26,29) | 
| 91 | Split_27_30 | Split(27,30) | 
| 92 | Split_28_29 | Split(28,29) | 
| 93 | Split_28_31 | Split(28,31) | 
| 94 | Split_29_30 | Split(29,30) | 
| 95 | Split_29_32 | Split(29,32) | 
| 96 | Split_30_33 | Split(30,33) | 
| 97 | Split_31_32 | Split(31,32) | 
| 98 | Split_31_34 | Split(31,34) | 
| 99 | Split_32_33 | Split(32,33) | 
| 100 | Split_32_35 | Split(32,35) | 
| 101 | Split_33_36 | Split(33,36) | 
| 102 | Split_34_35 | Split(34,35) | 
| 103 | Split_35_36 | Split(35,36) | 
| 104| ThreeNumber_0_1_2 | Three Number(00,01,02) | 
| 105 | ThreeNumber_0_2_3 | Three Number(00,02,03) | 
| 106 | Street_1 | Street(01,02,03) | 
| 107 | Street_4 | Street(04,05,06) | 
| 108 | Street_7 | Street(07,08,09) | 
| 109 | Street_10 | Street(10,11,12) | 
| 110 | Street_13 | Street(13,14,15) | 
| 111 | Street_16 | Street(16,17,18) | 
| 112 | Street_19 | Street(19,20,21) | 
| 113 | Street_22 | Street(22,23,24) | 
| 114 | Street_25 | Street(25,26,27) | 
| 115 | Street_28 | Street(28,29,30) | 
| 116 | Street_31 | Street(31,32,33) | 
| 117 | Street_34 | Street(34,35,36) | 
| 118 | FourNumber | Four Number(00,01,02,03) | 
| 119 | Corner_3 | Corner(01,02,04,05) | 
| 120| Corner_4 | Corner(02,03,05,06) | 
| 121 | Corner_6 | Corner(04,05,07,08) | 
| 122 | Corner_7 | Corner(05,06,08,09) | 
| 123 | Corner_9 | Corner(07,08,10,11) | 
| 124 | Corner_10 | Corner(08,09,11,12) | 
| 125 | Corner_12 | Corner(10,11,13,14) | 
| 126 | Corner_13 | Corner(11,12,14,15) | 
| 127 | Corner_15 | Corner(13,14,16,17) | 
| 128 | Corner_16 | Corner(14,15,17,18) | 
| 129 | Corner_18 | Corner(16,17,19,20) | 
| 130 | Corner_19 | Corner(17,18,20,21) | 
| 131 | Corner_21 | Corner(19,20,22,23) | 
| 132 | Corner_22 | Corner(20,21,23,24) | 
| 133 | Corner_24 | Corner(22,23,25,26) | 
| 134 | Corner_25 | Corner(23,24,26,27) | 
| 135 | Corner_27 | Corner(25,26,28,29) | 
| 136 | Corner_28 | Corner(26,27,29,30) | 
| 137 | Corner_30 | Corner(28,29,31,32) | 
| 138 | Corner_31 | Corner(29,30,32,33) | 
| 139 | Corner_33 | Corner(31,32,34,35) | 
| 140 | Corner_34 | Corner(32,33,35,36) | 
| 141 | Line_1 | Line(01~06) | 
| 142 | Line_4 | Line(04~09) | 
| 143 | Line_7 | Line(07~12) | 
| 144 | Line_10 | Line(10~15) | 
| 145 | Line_13 | Line(13~18) | 
| 146 | Line_16 | Line(16~21) | 
| 147 | Line_19 | Line(19~24) | 
| 148 | Line_22 | Line(22~27) | 
| 149 | Line_25 | Line(25~30) | 
| 150 | Line_28 | Line(28~33) | 
| 151 | Line_31 | Line(31~36) | 
| 152 | Dozen_1st | 1st Dozen | 
| 153 | Dozen_2nd | 2nd Dozen | 
| 154 | Dozen_3rd | 3rd Dozen| 
| 155 | Column_1st | 1st Column | 
| 156 | Column_2nd | 2nd Column | 
| 157 | Column_3rd | 3rd Column | 


### Dragon Tiger(GameType = 5)

| id | name | Description |
| --- | --- | --- |
| 1  Dragon           | Dragon                 |
| 2 | Tiger            | Tiger                  |
| 3 | Tie | Tie |

### Sedie(GameType = 6)

| id | name | Description |
| --- | --- | --- |
| 1 | Big | High | 
| 2 | Small | Low | 
| 3 | Odd | Odd | 
| 4 | Even | Even | 
| 5 | Zero | Red 0 | 
| 6 | One | Red 1 | 
| 7 | Three | Red 3 | 
| 8 | Four | Red 4 | 

### Speed Sicbo(GameType = 7)

| id | name | Description |
| --- | --- | --- |
| 1 | 1 | 1 | 
| 2 | 2 | 2 | 
| 3 | 3 | 3 | 
| 4 | 4 | 4 | 
| 5 | 5 | 5 | 
| 6 | 6 | 6 | 
| 7 | Big | High | 
| 8 | Small | Low | 
| 9 | Odd | Odd | 
|10 | Even | Even | 

## Valid Bet Amount
- The diff between Banker/Player, or High/Low. If a player place on the Banker 200 and on the Player 100 and game result is not tie. The valid bet amount would be 100 
- If the game result of Baccarat is tie, the valid bet amount of Banker and Player would be 0. If a player place on the Banker 200 and on the Player 200 and game result is tie, the valid bet amount would be 0
- If the game result of DragonTiger is tie, the valid bet amount would be the half of bet amount. If a player place on the Dragon 200 and game result is tie, the valid bet amount would be 100
- If the game result of Se Die is 2 red and 2 white, the valid bet amount would be 0 for the High/Low spot 
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
