# How to generate the key

Key = {6 arbitrary characters} + MD5(all request parameter list strings + KeyG) + {6 arbitrary characters}

- Arbitrary Character
  Arbitrarily fill in 6 characters in the two blanks, which are not required to be the same. When verifying, remove the head and tail and compare the encrypted part in the middle.
- Request parameter list string
  Tabulate the parameters according to each API method, string them in the format of key1=value1&key2=value2 in order. It's would be make sure the parameters isn't tampered
  EX:
    - For GET case if the query string is
      `Account=Test1&GameId=A01&Lang=zh-CN&AgentId=10081`
      The parameter list string would be：
        ```bash
        "Account=Test1&GameId=A01&Lang=zh-CN&AgentId=10081"
        ```
    - For POST case if the request body is
        ```json
        {
          "Account": "Test1",
          "GameId": "A01",
          "Lang": "zh-CN",
          "AgentId": "10081"
        }
        ```
        The parameter liststring would be：
        ```bash
        "Account=Test1&GameId=A01&Lang=zh-CN&AgentId=10081"
        ```
- KeyG
    ```bash
    KeyG = MD5(DateTime.now().setZone("UTC-4").toString("yyMMd") + AgentId + AgentKey)
    ```
    - The Timezone must be UTC-4.
    - The date format is `yyMMd`：
      2018/2/7 => the 7th would be `7`, not `07`
      2018/2/18 => 180218
      
## Example

The following is an example for encryption flow which using nodejs and [Luxon](https://github.com/moment/luxon)


```javascript
const agentId = 'Your AgentId';
const agentKey = 'Your AgentKey';

let requestData = {
    'parameter1': 'value1',
    'parameter2': 'value2',
    'parameter3': 'value3'
};

const date = DateTime.now().setZone('UTC-4').toFormat('yyMMd');
const keyG = md5(date + agentId + agentKey);

let paramsString = '';
for (const [key, value] of Object.entries(requestData)) {
  if (paramsString !== '') {
    paramsString += '&';
  }
  paramsString += key + '=' + value;
}
// Generate key
requestData.Key = Math.random().toString(36).substr(2,6) + md5(paramsString + keyG) + Math.random().toString(36).substr(2,6));

// Send request
...

```
