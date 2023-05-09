# Replenishment Api

�C���责�ѵ����]��ШD�d�߳�@���]�`���TApi

�Y���ݩʭȬ��ũ�null�h����
decimal���ҥ�����Ǧܤp�ƫ�|��Aexample 200.0000
�ШDñ�W
�w��queryString�A�T�w���ƧǡA�ͦ�token
�^��ñ�W
�w��^�����eJson�ǦC�ơA�ͦ�token�AJson�r��榡�� Properties Key �ɧ�

Token���Ҥ覡

�ڭ̴��ѧֳt�ͦ� X-API-TOKEN ���M��A�ϥΤ覡�Ѩ��U�M�סA�ثe�䴩�H�U�y��:

[JAVA XG Token](https://gitlab.kaixi.cc/api-libaray/java-xg-token)
[PHP XG Token](https://gitlab.kaixi.cc/api-libaray/php-xg-token)
[Node.js XG Token](https://gitlab.kaixi.cc/api-libaray/js-xg-token)
[C# XG Token](https://gitlab.kaixi.cc/api-libaray/csharp-xg-token)
�p�G�|���䴩���y���άO�Q�ۦ�B�z�A�i�ѦҤU�C�y�{�ͦ��G

## Get

#### Request

|  Column | Format | Description |
| -------- | -------- | -------- |
| X-API-KEY     | string     | provided by the game side     |
| X-API-TOKEN     | string     | [Encryption](#generate-token)    |
| gameType | string     |  [GameType](https://github.com/jacky5823a/docs/blob/master/AccountingPlatformAPI/reference-en.md#game-types)  |
| startTime  | date     | �j�M�_�l�ɶ� yyyy/MM/dd HH:mm:ss    |
| endTime   | date     | �j�M�����ɶ� yyyy/MM/dd HH:mm:ss    |
| pageLimit    | number     | �歶����ƶq 0 < Value <= 10000   |
| pageNumber     | number     | ���� Value > 0  |
| isNormal     | boolean     | optional, �O�_�^�ǥ]�t���⦨�\���,�i��ܤ���,�Y�ǭȥu����true�Y����줣�K�[,�h�w�]�u�^�� Modified �� Canceled ���  |

#### Response

```json
{
  "betList": [
    {
      "bet": "Baccarat_Banker",
      "betAmount": 20000,
      "betTime": "2021/06/12 22:55:53",
      "gameResult": "[\"C7\",\"H6\",\"H2\",\"D8\",\"\",\"\"]",
      "gameType": "Baccarat",
      "isRollack": false,
      "isSettle": true,
      "modifiedStatus": "Canceled",
      "round": 1612341153,
      "run": 51,
      "settleAmount": 0,
      "settleTime": "2021/07/05 03:18:51",
      "table": "R",
      "transactionId": "c2a95054-1bea-4e53-bd2d-48d271bc90be",
      "wagerId": 17725961
    },
    {
      "bet": "Baccarat_PlayerPair",
      "betAmount": 1000,
      "betTime": "2021/06/14 18:08:58",
      "gameResult": "[\"S9\",\"H9\",\"H3\",\"H0\",\"\",\"\"]",
      "gameType": "Baccarat",
      "isRollack": false,
      "isSettle": true,
      "round": 1612341153,
      "run": 51,
      "settleAmount": 0,
      "settleTime": "2021/07/03 22:19:30",
      "table": "R",
      "transactionId": "66ade8a1-7c13-4429-b7b7-f061e66b6d7e",
      "wagerId": 17725962,
      "modifiedStatus": "Canceled"
    }
  ],
  "pagination": [
    {
      "pageLimit": 20,
      "totalNumber": 2,
      "totalPages": 1
    }
  ]
}
```

## Generate Token
> �ƧǦr��(���ǩT�w)
>
requestOrderedString = endTime=2021/07/18 21:17&gameType=Baccarat&isNormal=true&pageLimit=20&pageNumber=1&startTime=2021/06/26 20:15:00

> �YisNormal=False�ΨS�ǤJ�h��

requestOrderedString = endTime=2021/07/18 21:17&gameType=Baccarat&pageLimit=20&pageNumber=1&startTime=2021/06/26 20:15:00

> �YisNormal=true��

requestOrderedString = endTime=2021/07/18 21:17&gameType=Baccarat&isNormal=true&pageLimit=20&pageNumber=1&startTime=2021/06/26 20:15:00

Sha1(apikey+requestOrderedString+secret) �� base64 �p�g

### C#�d�ҵ{���X
```
public static string EncryptBySHA1(string apiKey,string secret, string needEncryptString)
{
    string result = null;
    using (var sha = SHA1.Create())
    {
        var bytes = Encoding.UTF8.GetBytes($"{apiKey}{needEncryptString}{secret}}");
        var computedBytes = sha.ComputeHash(bytes);
        result = Convert.ToBase64String(computedBytes).ToLower();
    }
    return result;
}
```
### example

> �ШDGet Url �� =>

http://15.164.219.147:80/api/Replenishment/Get?gameType=Baccarat&startTime=2021/06/26 20:15:00&endTime=2021/07/18 21:17:00&pageLimit=20&pageNumber=1&isNormal=true

> �Y�ѼƬ�
> 
```
gameType=Baccarat
startTime=2021/06/26 20:15:00
endTime=2021/07/18 21:17:00
pageLimit=20
pageNumber=1
isNormal=true(�`�N�ХH�p�g�[�K)
apikey=3fa85f64-5717-4562-b3fc-2c963f66afa6
secret=a73a9aea-e5a3-4fe7-9a32-7e48a66f611e
```

�զ��Ƨ�ñ�W�r��
requestOrderedString = endTime=2021/07/18 21:17:00&gameType=Baccarat&isNormal=true&pageLimit=20&pageNumber=1&startTime=2021/06/26 20:15:00

signText = 3fa85f64-5717-4562-b3fc-2c963f66afa6endTime=2021/07/18 21:17:00&gameType=Baccarat&isNormal=true&pageLimit=20&pageNumber=1&startTime=2021/06/26 20:15:00a73a9aea-e5a3-4fe7-9a32-7e48a66f611e

token = sha1(signText) �� base64 �p�g

token = p7yycr7qgr2sxmg+ktompat2qj8=
