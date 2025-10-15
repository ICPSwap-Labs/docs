# ICPSwap Pool Chart Data API Documentation

## Overview
The ICPSwap Pool Chart Data API provides historical price and trading data for specific liquidity pools on the ICPSwap platform. This endpoint returns time-series data with configurable time intervals and pagination.

## Endpoint

### Get Pool Chart Data
**URL:** `https://api.icpswap.com/info/pool/{poolId}/chart/{level}?page={page}&limit={limit}`  
**Method:** `GET`  
**Parameters:** 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `poolId` | String | Yes | The pool canister ID (path parameter) |
| `level` | String | Yes | Time interval level (e.g., "d1" for daily data) (path parameter) |
| `page` | Integer | Yes | Page number for pagination (query parameter) |
| `limit` | Integer | Yes | Number of records per page (query parameter) |

## Response Format

### Success Response
```json
{
  "code": 200,
  "message": null,
  "data": {
    "totalElements": 269,
    "content": [
      {
        "snapshotTime": 1760294545000,
        "level": "d1",
        "poolId": "p2gzi-iyaaa-aaaag-qneta-cai",
        "poolFee": 3000,
        "token0LedgerId": "k25mb-qiaaa-aaaap-qpodq-cai",
        "token0LiquidityAmount": "21621731.25134156",
        "token0Price": "0.000330526065925922",
        "token1LedgerId": "ryjl3-tyaaa-aaaaa-aaaba-cai",
        "token1LiquidityAmount": "1599.49989802",
        "token1Price": "3.471978652683048500",
        "tvlUSD": "16444.696905779667000000",
        "txCount": "2",
        "low": "0.000095200000000000",
        "high": "0.000095200000000000",
        "open": "0.000095200000000000",
        "close": "0.000095200000000000",
        "volumeToken0": "140.781714290000000000",
        "volumeToken1": "0.013402170000000000",
        "volumeUSD": "0.046199431785489030",
        "feesUSD": "0.000110878636285173",
        "sqrtPrice": "0.000000000000000000",
        "openTime": 1760271553000,
        "closeTime": 1760294521000,
        "beginTime": 1760227200000,
        "endTime": 1760313600000
      }
    ],
    "page": 1,
    "limit": 10
  }
}
```

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `code` | Integer | HTTP status code (200 for success) |
| `message` | String/null | Response message (null for successful requests) |
| `data` | Object | Container for chart data |

### Data Object Fields

| Field | Type | Description |
|-------|------|-------------|
| `totalElements` | Integer | Total number of available records |
| `content` | Array | Array of chart data points |
| `page` | Integer | Current page number |
| `limit` | Integer | Number of records per page |

### Chart Data Point Fields

| Field | Type | Description |
|-------|------|-------------|
| `snapshotTime` | Integer | Timestamp of the data snapshot (milliseconds) |
| `level` | String | Time interval level (e.g., "d1") |
| `poolId` | String | The pool canister ID |
| `poolFee` | Integer | Pool fee rate (in basis points, e.g., 3000 = 0.3%) |
| `token0LedgerId` | String | Ledger canister ID of the first token |
| `token0LiquidityAmount` | String | Amount of token0 in the pool (decimal string) |
| `token0Price` | String | Price of token0 at snapshot time (decimal string) |
| `token1LedgerId` | String | Ledger canister ID of the second token |
| `token1LiquidityAmount` | String | Amount of token1 in the pool (decimal string) |
| `token1Price` | String | Price of token1 at snapshot time (decimal string) |
| `tvlUSD` | String | Total Value Locked in USD (decimal string) |
| `txCount` | String | Number of transactions in this period |
| `low` | String | Lowest price in this period (decimal string) |
| `high` | String | Highest price in this period (decimal string) |
| `open` | String | Opening price for this period (decimal string) |
| `close` | String | Closing price for this period (decimal string) |
| `volumeToken0` | String | Trading volume for token0 in this period (decimal string) |
| `volumeToken1` | String | Trading volume for token1 in this period (decimal string) |
| `volumeUSD` | String | Trading volume in USD for this period (decimal string) |
| `feesUSD` | String | Fees generated in USD for this period (decimal string) |
| `sqrtPrice` | String | Square root of price (decimal string) |
| `openTime` | Integer | Opening time timestamp (milliseconds) |
| `closeTime` | Integer | Closing time timestamp (milliseconds) |
| `beginTime` | Integer | Period begin time timestamp (milliseconds) |
| `endTime` | Integer | Period end time timestamp (milliseconds) |

## Time Levels

| Level | Description |
|-------|-------------|
| `d1` | Daily data (one record per day) |
| `h1` | Hourly data (one record per hour) |
| `m1` | Minute data (one record per minute) |

## Data Ordering
The data is returned in **descending chronological order** (most recent first). The `snapshotTime` field shows the most recent data points first.

## Example Request

```
GET https://api.icpswap.com/info/pool/p2gzi-iyaaa-aaaag-qneta-cai/chart/d1?page=1&limit=10
```

## Example Response

```json
{
  "code": 200,
  "message": null,
  "data": {
    "totalElements": 269,
    "content": [
      {
        "snapshotTime": 1760294545000,
        "level": "d1",
        "poolId": "p2gzi-iyaaa-aaaag-qneta-cai",
        "poolFee": 3000,
        "token0LedgerId": "k25mb-qiaaa-aaaap-qpodq-cai",
        "token0LiquidityAmount": "21621731.25134156",
        "token0Price": "0.000330526065925922",
        "token1LedgerId": "ryjl3-tyaaa-aaaaa-aaaba-cai",
        "token1LiquidityAmount": "1599.49989802",
        "token1Price": "3.471978652683048500",
        "tvlUSD": "16444.696905779667000000",
        "txCount": "2",
        "low": "0.000095200000000000",
        "high": "0.000095200000000000",
        "open": "0.000095200000000000",
        "close": "0.000095200000000000",
        "volumeToken0": "140.781714290000000000",
        "volumeToken1": "0.013402170000000000",
        "volumeUSD": "0.046199431785489030",
        "feesUSD": "0.000110878636285173",
        "sqrtPrice": "0.000000000000000000",
        "openTime": 1760271553000,
        "closeTime": 1760294521000,
        "beginTime": 1760227200000,
        "endTime": 1760313600000
      }
    ],
    "page": 1,
    "limit": 10
  }
}
```

## Notes

- All numeric values are returned as strings to maintain precision
- Timestamps are in milliseconds since Unix epoch
- Data is returned in descending chronological order (newest first)
- The `level` parameter determines the time interval for each data point
- Pagination allows you to retrieve large datasets in manageable chunks
- The `totalElements` field helps determine the total number of pages available
- No authentication is required for this endpoint
- Pool fees are represented as integers in basis points (e.g., 3000 = 0.3%)
- The response includes comprehensive pool data including both tokens in the pair

In case of errors, the response will include an appropriate error message in the `message` field.

## Pagination

To retrieve all available data:
1. Start with `page=1` and your desired `limit`
2. Check the `totalElements` field to determine total records
3. Calculate total pages: `Math.ceil(totalElements / limit)`
4. Continue fetching subsequent pages until you have all data
