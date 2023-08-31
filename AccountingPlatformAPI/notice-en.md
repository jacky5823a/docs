# Notice

## Manual of backstage

See the [Manual of backstage](../AgentBackend/manual-en.md) for more information

## Persional API info

The `API URL`, `Agent ID` and `Agent Key` are on the [Developer Zone/Development Document](../AgentBackend/manual-en.md#Developer-Zone) page of backstage

## IP Restriction

- The ip form the request of the agent must in the whitelist IP list when invoking our apis. The [Account Management/Profile](../AgentBackend/manual-en.md#Profile-of-agent) shows the personal whitelist IP list. If you'd like to set downline agent's whitelist IP list, please go to the [Account Management/Agent Management] page. 
- Please ask the upline agent if you'd like to modify personal whitelist IP list

## HTTPS encryption

Please support TLS 1.2 or later version of protocol when invoking our APIs

## Language Families
Append the `ApiLang` or `lang` parameter in the request if you'd like to switch the API language.

- zh-CN: Simplified Chinese (default)
- zh-TW: Traditional Chinese
- en: English
- ja: Japanese
- vi: Vietnamese

## Request
- All requests include the following parameters. Please follow the encryption flow to generate the `Key`.

| Parameter | Type   | Description    |
| --------- | ------ | -------------- |
| `AgentId` | string | Agent ID |
| `Key`     | string | Encryption key       |

## Response
- All responses include the following fields

| Parameter   | Type   | Description |
| ----------- | ------ | ----------- |
| `ErrorCode` | String | Error code      |
| `Message`   | String | Error message    |
| `Data`      | Object | Data    |

```json
{ 
    "ErrorCode":"0",
    "Message":"",
    "Data":{
        ......
    }
}
```

## Other FAQ
- Please put parameters in [query string](https://en.wikipedia.org/wiki/Query_string) for GET method. It would be blocked if put parameters in message body for GET method by some cloud providers. Please refer to [HTTP GET method](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/GET) to get more information.
- Please put parameters in message body for POST method. And whose format is JSON, **DO NOT** using `form-data` or `x-www-form-urlencoded` format.
