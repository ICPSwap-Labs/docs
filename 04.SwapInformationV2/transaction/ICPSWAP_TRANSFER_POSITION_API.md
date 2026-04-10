# ICPSwap Transfer Position Record API Documentation

## Overview
The ICPSwap Transfer Position Record API provides paginated LP position transfer history. You can query records by principal, one or more pool IDs, and an optional time range.

## Endpoint

### Get Transfer Position Records
**URL:** `https://api.icpswap.com/info/record/transferPosition/list`  
**Method:** `GET`  
**Use Case:** Query transfer position records filtered by a specific `principal`, one or more `poolIds`, or both.

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `poolIds` | String | No | Comma-separated pool canister IDs used to filter records |
| `principal` | String | No | User principal used to filter records |
| `page` | Integer | No | Page number for pagination. Default behavior is determined by the service |
| `limit` | Integer | No | Number of records per page. Using a smaller value is recommended |
| `begin` | Integer | No | Start timestamp in milliseconds |
| `end` | Integer | No | End timestamp in milliseconds |

## Response Format

### Success Response
```json
{
  "code": 200,
  "message": null,
  "data": {
    "totalElements": 2,
    "content": [
      {
        "recordKind": "TransferPosition",
        "action": "TransferPosition",
        "from": "string",
        "to": "string",
        "recipient": "string",
        "sender": "string",
        "timestamp": 1775110751,
        "txId": 674,
        "poolId": "string",
        "poolFee": 3000,
        "positionId": 22,
        "sqrtPrice": "string",
        "tick": "string",
        "tickLimit": null,
        "liquidityChange": "string",
        "liquidityTotal": "string",
        "token0Id": "string",
        "token0Standard": "string",
        "token0Symbol": "string",
        "token0Decimals": 8,
        "token0ChangeAmount": "string",
        "token0InAmount": null,
        "token0Price": "0",
        "token0Fee": "string",
        "token1Id": "string",
        "token1Standard": "string",
        "token1Symbol": "string",
        "token1Decimals": 8,
        "token1ChangeAmount": "string",
        "token1InAmount": null,
        "token1Price": "0",
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
| `data` | Object | Container for paginated transfer position records |

### Data Object Fields

| Field | Type | Description |
|-------|------|-------------|
| `totalElements` | Integer | Total number of available records |
| `content` | Array | Array of transfer position record objects |
| `page` | Integer | Current page number |
| `limit` | Integer | Number of records per page |

### Transfer Position Record Fields

| Field | Type | Description |
|-------|------|-------------|
| `recordKind` | String | Record category. For this endpoint the value is `TransferPosition` |
| `action` | String | Action type. For this endpoint the value is `TransferPosition` |
| `from` | String | Principal or canister sending the position |
| `to` | String | Principal or canister receiving the position |
| `recipient` | String | Recipient principal recorded by the transaction |
| `sender` | String | Sender principal recorded by the transaction |
| `timestamp` | Integer | Transaction timestamp in seconds |
| `txId` | Integer | Transaction ID within the record system |
| `poolId` | String | Pool canister ID |
| `poolFee` | Integer | Pool fee rate in basis points |
| `positionId` | Integer | Position ID being transferred |
| `sqrtPrice` | String | Square-root price value recorded for the transaction |
| `tick` | String | Tick at the time of the record |
| `tickLimit` | String/null | Tick limit for the position when available |
| `liquidityChange` | String | Liquidity delta recorded by the action |
| `liquidityTotal` | String | Total liquidity associated with the position |
| `token0Id` | String | Token0 ledger canister ID |
| `token0Standard` | String | Token0 standard, such as `ICRC2` |
| `token0Symbol` | String | Token0 symbol |
| `token0Decimals` | Integer | Token0 decimals |
| `token0ChangeAmount` | String | Net token0 amount changed by the record |
| `token0InAmount` | String/null | Token0 input amount when available |
| `token0Price` | String/null | Token0 price at record time when available |
| `token0Fee` | String | Token0 fee amount |
| `token1Id` | String | Token1 ledger canister ID |
| `token1Standard` | String | Token1 standard, such as `ICRC2` |
| `token1Symbol` | String | Token1 symbol |
| `token1Decimals` | Integer | Token1 decimals |
| `token1ChangeAmount` | String | Net token1 amount changed by the record |
| `token1InAmount` | String/null | Token1 input amount when available |
| `token1Price` | String/null | Token1 price at record time when available |
| `token1Fee` | String | Token1 fee amount |
| `amountToken0` | String | Aggregated token0 amount for analytics |
| `amountToken1` | String | Aggregated token1 amount for analytics |
| `amountUsd` | String | USD value for analytics |

## Data Ordering
The data is returned in **descending chronological order** (most recent first).

## Example Request

```http
GET https://api.icpswap.com/info/record/transferPosition/list?poolIds=splxr-cqaaa-aaaar-qbmyq-cai,tqdeg-biaaa-aaaar-qbm4a-cai&principal=t7c3d-obwte-dykfa-bow6f-eagn6-i5anp-24wes-6s3af-su4jn-mnbwf-nqe&page=1&limit=10&begin=1774114049000&end=1776114049000
```

## Example Response

```json
{
  "code": 200,
  "message": null,
  "data": {
    "totalElements": 2,
    "content": [
      {
        "recordKind": "TransferPosition",
        "action": "TransferPosition",
        "from": "t7c3d-obwte-dykfa-bow6f-eagn6-i5anp-24wes-6s3af-su4jn-mnbwf-nqe",
        "to": "dim4t-52opu-pnts4-da6ty-hbcgt-upk5t-dlqq7-wc2ik-p3lbd-mdx5z-dqe",
        "recipient": "t7c3d-obwte-dykfa-bow6f-eagn6-i5anp-24wes-6s3af-su4jn-mnbwf-nqe",
        "sender": "t7c3d-obwte-dykfa-bow6f-eagn6-i5anp-24wes-6s3af-su4jn-mnbwf-nqe",
        "timestamp": 1775110751,
        "txId": 674,
        "poolId": "splxr-cqaaa-aaaar-qbmyq-cai",
        "poolFee": 3000,
        "positionId": 22,
        "sqrtPrice": "17279758124807087099320284612",
        "tick": "-30458",
        "tickLimit": null,
        "liquidityChange": "0",
        "liquidityTotal": "8304607401032",
        "token0Id": "4c4fd-caaaa-aaaaq-aaa3a-cai",
        "token0Standard": "ICRC2",
        "token0Symbol": "CLAY",
        "token0Decimals": 8,
        "token0ChangeAmount": "0",
        "token0InAmount": null,
        "token0Price": "0",
        "token0Fee": "0",
        "token1Id": "ifwyg-gaaaa-aaaaq-aaeqq-cai",
        "token1Standard": "ICRC2",
        "token1Symbol": "ICE",
        "token1Decimals": 8,
        "token1ChangeAmount": "0",
        "token1InAmount": null,
        "token1Price": "0",
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
- `poolIds` accepts multiple pool IDs separated by commas
- `begin` and `end` use millisecond timestamps
- `timestamp` uses seconds
- Numeric amounts are generally returned as strings to preserve precision
- Some fields may be `null`, such as `tickLimit`, `token0InAmount`, or `token1InAmount`
- Some records may contain `"0"` values for price or liquidity-related fields
- No authentication is required for this endpoint

In case of errors, the response will include an appropriate error message in the `message` field.
