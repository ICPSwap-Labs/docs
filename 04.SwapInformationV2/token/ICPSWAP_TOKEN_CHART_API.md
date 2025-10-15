# ICPSwap Token Chart Data API Documentation

## Overview
The ICPSwap Token Chart Data API provides historical price and trading data for specific tokens on the ICPSwap platform. This endpoint returns time-series data with configurable time intervals and pagination.

## Endpoint

### Get Token Chart Data
**URL:** `https://api.icpswap.com/info/token/{tokenLedgerId}/chart/{level}?page={page}&limit={limit}`  
**Method:** `GET`  
**Parameters:** 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `tokenLedgerId` | String | Yes | The ledger canister ID of the token (path parameter) |
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
    "totalElements": 969,
    "content": [
      {
        "snapshotTime": 1756820523000,
        "level": "d1",
        "tokenLedgerId": "ryjl3-tyaaa-aaaaa-aaaba-cai",
        "price": "4.795472580794851000",
        "liquidityAmount": "932131495.275076370000000000",
        "tvlUSD": "2631659.798485842777613371",
        "txCount": "2776",
        "low": "4.676362636468302000",
        "high": "4.850285524824097000",
        "open": "4.676420090809413000",
        "close": "4.837632717942553000",
        "amount": "33237.177315410000000000",
        "volumeUSD": "158596.676785362619399355",
        "openTime": 1756771505000,
        "closeTime": 1756820239000,
        "beginTime": 1756771200000,
        "endTime": 1756857600000
      }
    ],
    "page": 1,
    "limit": 365
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
| `tokenLedgerId` | String | The ledger canister ID of the token |
| `price` | String | Price at snapshot time (decimal string) |
| `liquidityAmount` | String | Liquidity amount (decimal string) |
| `tvlUSD` | String | Total Value Locked in USD (decimal string) |
| `txCount` | String | Number of transactions in this period |
| `low` | String | Lowest price in this period (decimal string) |
| `high` | String | Highest price in this period (decimal string) |
| `open` | String | Opening price for this period (decimal string) |
| `close` | String | Closing price for this period (decimal string) |
| `amount` | String | Trading amount in this period (decimal string) |
| `volumeUSD` | String | Trading volume in USD for this period (decimal string) |
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
GET https://api.icpswap.com/info/token/ryjl3-tyaaa-aaaaa-aaaba-cai/chart/d1?page=1&limit=500
```

## Example Response

```json
{
  "code": 200,
  "message": null,
  "data": {
    "totalElements": 969,
    "content": [
      {
        "snapshotTime": 1756820523000,
        "level": "d1",
        "tokenLedgerId": "ryjl3-tyaaa-aaaaa-aaaba-cai",
        "price": "4.795472580794851000",
        "liquidityAmount": "932131495.275076370000000000",
        "tvlUSD": "2631659.798485842777613371",
        "txCount": "2776",
        "low": "4.676362636468302000",
        "high": "4.850285524824097000",
        "open": "4.676420090809413000",
        "close": "4.837632717942553000",
        "amount": "33237.177315410000000000",
        "volumeUSD": "158596.676785362619399355",
        "openTime": 1756771505000,
        "closeTime": 1756820239000,
        "beginTime": 1756771200000,
        "endTime": 1756857600000
      }
    ],
    "page": 1,
    "limit": 365
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

In case of errors, the response will include an appropriate error message in the `message` field.

## Pagination

To retrieve all available data:
1. Start with `page=1` and your desired `limit`
2. Check the `totalElements` field to determine total records
3. Calculate total pages: `Math.ceil(totalElements / limit)`
4. Continue fetching subsequent pages until you have all data
