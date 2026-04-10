# ICPSwap Transaction API Documentation

## Overview
The ICPSwap Transaction API provides paginated transaction history across swap, liquidity, and claim actions. You can use this endpoint to query transactions by pool, token, principal, time range, and action type.

## Endpoint

### Find Transactions
**URL:** `https://api.icpswap.com/info/transaction/find`  
**Method:** `GET`  
**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `poolId` | String | No | Pool canister ID used to filter transactions |
| `tokenId` | String | No | Token ledger canister ID used to filter transactions |
| `principal` | String | No | User principal used to filter transactions |
| `page` | Integer | No | Page number for pagination. Default behavior is determined by the service |
| `limit` | Integer | No | Number of records per page. Using a smaller value is recommended |
| `begin` | Integer | No | Start timestamp in milliseconds |
| `end` | Integer | No | End timestamp in milliseconds |
| `actionTypes` | String | No | Comma-separated action filters, such as `Swap,AddLiquidity,DecreaseLiquidity,Claim` |

## Response Format

### Success Response
```json
{
  "code": 200,
  "message": null,
  "data": {
    "totalElements": 488,
    "content": [
      {
        "poolId": "string",
        "poolFee": 3000,
        "positionId": 0,
        "token0LedgerId": "string",
        "token0Price": "string",
        "token0Name": "string",
        "token0Symbol": "string",
        "token1LedgerId": "string",
        "token1Price": "string",
        "token1Name": "string",
        "token1Symbol": "string",
        "actionType": "Swap",
        "fromPrincipalId": "string",
        "fromSubaccount": "string",
        "fromAccountId": "string",
        "fromTextualId": "string",
        "fromAlias": null,
        "toPrincipalId": "string",
        "toSubaccount": "string",
        "toAccountId": "string",
        "toTextualId": "string",
        "toAlias": "string",
        "token0AmountIn": "string",
        "token1AmountIn": "string",
        "token0AmountOut": "string",
        "token1AmountOut": "string",
        "token0Fee": "string",
        "token1Fee": "string",
        "sqrtPrice": "string",
        "tickLimit": "string",
        "tick": "string",
        "liquidity": "string",
        "currentLiquidity": "string",
        "txHash": "string",
        "txTime": 1775211598000,
        "token0TxValue": "string",
        "token1TxValue": "string"
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
| `data` | Object | Container for paginated transaction records |

### Data Object Fields

| Field | Type | Description |
|-------|------|-------------|
| `totalElements` | Integer | Total number of available records |
| `content` | Array | Array of transaction record objects |
| `page` | Integer | Current page number |
| `limit` | Integer | Number of records per page |

### Transaction Record Fields

| Field | Type | Description |
|-------|------|-------------|
| `poolId` | String | Pool canister ID |
| `poolFee` | Integer | Pool fee rate in basis points |
| `positionId` | Integer | Position ID related to the transaction, if applicable |
| `token0LedgerId` | String | Token0 ledger canister ID |
| `token0Price` | String | Token0 price at transaction time |
| `token0Name` | String | Token0 name |
| `token0Symbol` | String | Token0 symbol |
| `token1LedgerId` | String | Token1 ledger canister ID |
| `token1Price` | String | Token1 price at transaction time |
| `token1Name` | String | Token1 name |
| `token1Symbol` | String | Token1 symbol |
| `actionType` | String | Transaction action type, such as `Swap`, `AddLiquidity`, `DecreaseLiquidity`, or `Claim` |
| `fromPrincipalId` | String | Sender principal ID |
| `fromSubaccount` | String | Sender subaccount hex string |
| `fromAccountId` | String | Sender account ID |
| `fromTextualId` | String | Sender textual identifier |
| `fromAlias` | String/null | Sender alias when available |
| `toPrincipalId` | String | Recipient principal or canister ID |
| `toSubaccount` | String | Recipient subaccount hex string |
| `toAccountId` | String | Recipient account ID |
| `toTextualId` | String | Recipient textual identifier |
| `toAlias` | String/null | Recipient alias when available |
| `token0AmountIn` | String | Token0 input amount |
| `token1AmountIn` | String | Token1 input amount |
| `token0AmountOut` | String | Token0 output amount |
| `token1AmountOut` | String | Token1 output amount |
| `token0Fee` | String | Token0 fee amount |
| `token1Fee` | String | Token1 fee amount |
| `sqrtPrice` | String | Square-root price value recorded for the transaction |
| `tickLimit` | String | Tick limit recorded for the transaction |
| `tick` | String | Tick at the time of the transaction |
| `liquidity` | String | Liquidity delta or transaction liquidity value |
| `currentLiquidity` | String | Current liquidity value after the transaction |
| `txHash` | String | Transaction hash or unique transaction identifier |
| `txTime` | Integer | Transaction timestamp in milliseconds |
| `token0TxValue` | String | Token0-side transaction value used for analytics |
| `token1TxValue` | String | Token1-side transaction value used for analytics |

## Data Ordering
The data is returned in **descending chronological order** (most recent first).

## Example Request

```http
GET https://api.icpswap.com/info/transaction/find?poolId=mohjv-bqaaa-aaaag-qjyia-cai&tokenId=&principal=ehq2s-mlmrx-xvogi-adg5n-dowp3-qasvb-nvdjl-ijj3m-e6ijc-pmrmb-dqe&page=1&limit=10&begin=1774114049000&end=1776114049000&actionTypes=Swap,AddLiquidity,DecreaseLiquidity,Claim
```

## Example Response

```json
{
  "code": 200,
  "message": null,
  "data": {
    "totalElements": 488,
    "content": [
      {
        "poolId": "mohjv-bqaaa-aaaag-qjyia-cai",
        "poolFee": 3000,
        "positionId": 0,
        "token0LedgerId": "xevnm-gaaaa-aaaar-qafnq-cai",
        "token0Price": "1.0001",
        "token0Name": "ckUSDC",
        "token0Symbol": "ckUSDC",
        "token1LedgerId": "ryjl3-tyaaa-aaaaa-aaaba-cai",
        "token1Price": "2.307979714541204",
        "token1Name": "Internet Computer",
        "token1Symbol": "ICP",
        "actionType": "Swap",
        "fromPrincipalId": "ehq2s-mlmrx-xvogi-adg5n-dowp3-qasvb-nvdjl-ijj3m-e6ijc-pmrmb-dqe",
        "fromSubaccount": "0000000000000000000000000000000000000000000000000000000000000000",
        "fromAccountId": "4e18c7452ec8a54c87c3751b6e93ab2b26d5ada04ecdacc63452b4b945c5e580",
        "fromTextualId": "ehq2s-mlmrx-xvogi-adg5n-dowp3-qasvb-nvdjl-ijj3m-e6ijc-pmrmb-dqe",
        "fromAlias": null,
        "toPrincipalId": "mohjv-bqaaa-aaaag-qjyia-cai",
        "toSubaccount": "0000000000000000000000000000000000000000000000000000000000000000",
        "toAccountId": "bca85666f3d2de1d135d399a9ccc96d38090601e784e1e5467b87fb3334ec1e0",
        "toTextualId": "mohjv-bqaaa-aaaag-qjyia-cai",
        "toAlias": "ICPSwap:ICP/ckUSDC",
        "token0AmountIn": "1.156358",
        "token1AmountIn": "0",
        "token0AmountOut": "0",
        "token1AmountOut": "0.50107617",
        "token0Fee": "0.01",
        "token1Fee": "0.0001",
        "sqrtPrice": "",
        "tickLimit": "",
        "tick": "0",
        "liquidity": "0",
        "currentLiquidity": "0",
        "txHash": "mohjv-bqaaa-aaaag-qjyia-cai_mohjv-bqaaa-aaaag-qjyia-cai733445",
        "txTime": 1775211598000,
        "token0TxValue": "1.15647364",
        "token1TxValue": "1.15647364"
      }
    ],
    "page": 1,
    "limit": 10
  }
}
```

## Notes

- All query parameters are optional, but supplying filters is recommended to reduce the result set
- `actionTypes` accepts multiple values separated by commas
- `begin`, `end`, and `txTime` use millisecond timestamps
- Numeric amounts are generally returned as strings to preserve precision
- Some fields may be empty strings, such as `sqrtPrice` or `tickLimit`, depending on the action type
- Some alias fields may be `null`
- No authentication is required for this endpoint

In case of errors, the response will include an appropriate error message in the `message` field.
