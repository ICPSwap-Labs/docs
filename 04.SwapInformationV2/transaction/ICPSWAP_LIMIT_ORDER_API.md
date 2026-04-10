# ICPSwap Limit Order Record API Documentation

## Overview
The ICPSwap Limit Order Record API provides paginated limit order history for a user and/or a pool. You can use this endpoint to retrieve limit order creation and execution records within an optional time range.

## Endpoint

### Get Limit Order Records
**URL:** `https://api.icpswap.com/info/record/limitOrder/list`  
**Method:** `GET`  
**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `poolId` | String | No | Pool canister ID used to filter records |
| `principal` | String | No | User principal used to filter records |
| `page` | Integer | No | Page number for pagination. Default behavior is determined by the service |
| `limit` | Integer | No | Number of records per page. Using a smaller value is recommended |
| `begin` | Integer | No | Start timestamp in milliseconds |
| `end` | Integer | No | End timestamp in milliseconds |
| `actionTypes` | String | No | Comma-separated action filters, such as `LimitOrder,AddLimitOrder,ExecuteLimitOrder,RemoveLimitOrder` |

## Response Format

### Success Response
```json
{
  "code": 200,
  "message": null,
  "data": {
    "totalElements": 3,
    "content": [
      {
        "recordKind": "LimitOrder",
        "action": "ExecuteLimitOrder",
        "from": "string",
        "to": "string",
        "recipient": "string",
        "sender": "string",
        "timestamp": 1775114049,
        "txId": 724,
        "poolId": "string",
        "poolFee": 3000,
        "positionId": 28,
        "sqrtPrice": "string",
        "tick": "string",
        "tickLimit": "string",
        "liquidityChange": "string",
        "liquidityTotal": "string",
        "token0Id": "string",
        "token0Standard": "string",
        "token0Symbol": "string",
        "token0Decimals": 8,
        "token0ChangeAmount": "string",
        "token0InAmount": "string",
        "token0Price": null,
        "token0Fee": "string",
        "token1Id": "string",
        "token1Standard": "string",
        "token1Symbol": "string",
        "token1Decimals": 8,
        "token1ChangeAmount": "string",
        "token1InAmount": "string",
        "token1Price": null,
        "token1Fee": "string",
        "amountToken0": "string",
        "amountToken1": "string",
        "amountUsd": "string"
      }
    ],
    "page": 1,
    "limit": 2
  }
}
```

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `code` | Integer | HTTP status code (200 for success) |
| `message` | String/null | Response message (null for successful requests) |
| `data` | Object | Container for paginated limit order records |

### Data Object Fields

| Field | Type | Description |
|-------|------|-------------|
| `totalElements` | Integer | Total number of available records |
| `content` | Array | Array of limit order record objects |
| `page` | Integer | Current page number |
| `limit` | Integer | Number of records per page |

### Limit Order Record Fields

| Field | Type | Description |
|-------|------|-------------|
| `recordKind` | String | Record category. For this endpoint the value is `LimitOrder` |
| `action` | String | Limit order action, such as `LimitOrder`, `AddLimitOrder`, `ExecuteLimitOrder`, or `RemoveLimitOrder` |
| `from` | String | Principal or canister initiating the record |
| `to` | String | Target principal or canister for the record |
| `recipient` | String | Recipient principal recorded by the transaction |
| `sender` | String | Sender principal recorded by the transaction |
| `timestamp` | Integer | Transaction timestamp in seconds |
| `txId` | Integer | Transaction ID within the record system |
| `poolId` | String | Pool canister ID |
| `poolFee` | Integer | Pool fee rate in basis points |
| `positionId` | Integer | Position ID associated with the limit order |
| `sqrtPrice` | String | Square-root price value recorded for the transaction |
| `tick` | String | Tick at the time of the record |
| `tickLimit` | String/null | Limit-order tick configured for the position |
| `liquidityChange` | String | Liquidity delta recorded by the action |
| `liquidityTotal` | String | Total liquidity after the action |
| `token0Id` | String | Token0 ledger canister ID |
| `token0Standard` | String | Token0 standard, such as `ICRC2` |
| `token0Symbol` | String | Token0 symbol |
| `token0Decimals` | Integer | Token0 decimals |
| `token0ChangeAmount` | String | Net token0 amount changed by the record |
| `token0InAmount` | String/null | Token0 amount provided as input for the action |
| `token0Price` | String/null | Token0 price at record time when available |
| `token0Fee` | String | Token0 fee amount |
| `token1Id` | String | Token1 ledger canister ID |
| `token1Standard` | String | Token1 standard, such as `ICRC2` |
| `token1Symbol` | String | Token1 symbol |
| `token1Decimals` | Integer | Token1 decimals |
| `token1ChangeAmount` | String | Net token1 amount changed by the record |
| `token1InAmount` | String/null | Token1 amount provided as input for the action |
| `token1Price` | String/null | Token1 price at record time when available |
| `token1Fee` | String | Token1 fee amount |
| `amountToken0` | String | Aggregated token0 amount for analytics |
| `amountToken1` | String | Aggregated token1 amount for analytics |
| `amountUsd` | String | USD value for analytics |

## Data Ordering
The data is returned in **descending chronological order** (most recent first).

## Example Request

```http
GET https://api.icpswap.com/info/record/limitOrder/list?poolId=splxr-cqaaa-aaaar-qbmyq-cai&principal=tvrhj-lrsxa-hunxj-f6o5c-ggvwk-exolk-yg66g-fn5ag-67cr6-gxotu-uae&page=1&limit=10&begin=1774114049000&end=1776114049000&actionTypes=LimitOrder,AddLimitOrder,ExecuteLimitOrder,RemoveLimitOrder
```

## Example Response

```json
{
  "code": 200,
  "message": null,
  "data": {
    "totalElements": 3,
    "content": [
      {
        "recordKind": "LimitOrder",
        "action": "ExecuteLimitOrder",
        "from": "tvrhj-lrsxa-hunxj-f6o5c-ggvwk-exolk-yg66g-fn5ag-67cr6-gxotu-uae",
        "to": "splxr-cqaaa-aaaar-qbmyq-cai",
        "recipient": "tvrhj-lrsxa-hunxj-f6o5c-ggvwk-exolk-yg66g-fn5ag-67cr6-gxotu-uae",
        "sender": "tvrhj-lrsxa-hunxj-f6o5c-ggvwk-exolk-yg66g-fn5ag-67cr6-gxotu-uae",
        "timestamp": 1775114049,
        "txId": 724,
        "poolId": "splxr-cqaaa-aaaar-qbmyq-cai",
        "poolFee": 3000,
        "positionId": 28,
        "sqrtPrice": "17660830184383035782434860818",
        "tick": "-30022",
        "tickLimit": "-30480",
        "liquidityChange": "0",
        "liquidityTotal": "5268732133571",
        "token0Id": "4c4fd-caaaa-aaaaq-aaa3a-cai",
        "token0Standard": "ICRC2",
        "token0Symbol": "CLAY",
        "token0Decimals": 8,
        "token0ChangeAmount": "0",
        "token0InAmount": "1224997.41249998",
        "token0Price": null,
        "token0Fee": "0",
        "token1Id": "ifwyg-gaaaa-aaaaq-aaeqq-cai",
        "token1Standard": "ICRC2",
        "token1Symbol": "ICE",
        "token1Decimals": 8,
        "token1ChangeAmount": "57930.90628673",
        "token1InAmount": "0",
        "token1Price": null,
        "token1Fee": "0",
        "amountToken0": "0",
        "amountToken1": "0",
        "amountUsd": "0"
      }
    ],
    "page": 1,
    "limit": 10
  }
}
```

## Notes

- All query parameters are optional, but supplying filters is recommended to reduce the result set
- `actionTypes` accepts multiple values separated by commas, including `LimitOrder`, `AddLimitOrder`, `ExecuteLimitOrder`, and `RemoveLimitOrder`
- `begin` and `end` use millisecond timestamps
- `timestamp` uses seconds
- Numeric amounts are generally returned as strings to preserve precision
- Some fields may be `null`, such as `token0Price`, `token1Price`, or `tickLimit`
- No authentication is required for this endpoint

In case of errors, the response will include an appropriate error message in the `message` field.
