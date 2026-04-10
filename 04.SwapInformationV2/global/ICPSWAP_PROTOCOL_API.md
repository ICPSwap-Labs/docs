# ICPSwap Protocol Statistics API Documentation

## Overview
The ICPSwap Protocol Statistics API provides high-level protocol metrics for the entire ICPSwap platform, including cumulative trading volume, 24-hour trading activity, fees, TVL, trading pair count, and user count.

## Endpoints

### Get Protocol Statistics
**URL:** `https://api.icpswap.com/info/global/protocol`  
**Method:** `GET`  
**Parameters:** None

### Get Daily Protocol Statistics
**URL:** `https://api.icpswap.com/info/global/protocol/d1?page={page}&limit={limit}`  
**Method:** `GET`  
**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `page` | Integer | No | Page number for pagination |
| `limit` | Integer | No | Number of records per page |

## Response Format

### Protocol Statistics Success Response

```json
{
  "code": 200,
  "message": null,
  "data": {
    "volumeUSD": "636718122.064977974772385923",
    "volumeUSD24H": "132502.899880178451758805",
    "feesUSD": "200.263848800482952112",
    "txCount": "4780",
    "tvlUSD": "3254986.960612077730845723",
    "totalTradingPairs": 1951,
    "totalUsers": 100986
  }
}
```

### Daily Protocol Statistics Success Response
```json
{
  "code": 200,
  "message": null,
  "data": {
    "totalElements": 1180,
    "content": [
      {
        "snapshotTime": 1775174102000,
        "dayId": 20545,
        "level": "d1",
        "volumeUSD": "169784.025940718845440298",
        "feesUSD": "388.239681442448391794",
        "txCount": "5057",
        "tvlUSD": "3228669.335833864455370738"
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
| `data` | Object | Container for protocol statistics |

### Data Object Fields

| Field | Type | Description |
|-------|------|-------------|
| `volumeUSD` | String | Total cumulative trading volume in USD across the entire platform |
| `volumeUSD24H` | String | Total trading volume in USD across the platform during the last 24 hours |
| `feesUSD` | String | Total trading fees in USD during the last 24 hours |
| `txCount` | String | Total number of transactions across the platform during the last 24 hours |
| `tvlUSD` | String | Total value locked in USD across the entire platform |
| `totalTradingPairs` | Integer | Total number of trading pairs across the platform |
| `totalUsers` | Integer | Total cumulative number of trading users across the platform |

### Daily Data Object Fields

| Field | Type | Description |
|-------|------|-------------|
| `totalElements` | Integer | Total number of available daily records |
| `content` | Array | Array of daily protocol statistics records |
| `page` | Integer | Current page number |
| `limit` | Integer | Number of records per page |

### Daily Protocol Record Fields

| Field | Type | Description |
|-------|------|-------------|
| `snapshotTime` | Integer | Snapshot timestamp in milliseconds |
| `dayId` | Integer | Day identifier |
| `level` | String | Aggregation level. For this endpoint the value is `d1` |
| `volumeUSD` | String | Platform trading volume in USD for the day |
| `feesUSD` | String | Platform trading fees in USD for the day |
| `txCount` | String | Platform transaction count for the day |
| `tvlUSD` | String | Platform total value locked in USD for the day snapshot |

## Example Request: Protocol Statistics

```http
GET https://api.icpswap.com/info/global/protocol
```

## Example Response: Protocol Statistics

```json
{
  "code": 200,
  "message": null,
  "data": {
    "volumeUSD": "636718122.064977974772385923",
    "volumeUSD24H": "132502.899880178451758805",
    "feesUSD": "200.263848800482952112",
    "txCount": "4780",
    "tvlUSD": "3254986.960612077730845723",
    "totalTradingPairs": 1951,
    "totalUsers": 100986
  }
}
```

## Example Request: Daily Protocol Statistics

```http
GET https://api.icpswap.com/info/global/protocol/d1?page=1&limit=10
```

## Example Response: Daily Protocol Statistics

```json
{
  "code": 200,
  "message": null,
  "data": {
    "totalElements": 1180,
    "content": [
      {
        "snapshotTime": 1775174102000,
        "dayId": 20545,
        "level": "d1",
        "volumeUSD": "169784.025940718845440298",
        "feesUSD": "388.239681442448391794",
        "txCount": "5057",
        "tvlUSD": "3228669.335833864455370738"
      }
    ],
    "page": 1,
    "limit": 10
  }
}
```

## Notes

- `GET /global/protocol` does not require query parameters
- `GET /global/protocol/d1` accepts optional `page` and `limit` parameters, though supplying them is recommended
- Monetary values are returned as strings to preserve precision
- `totalTradingPairs` and `totalUsers` are returned as integers
- Daily records are returned in descending chronological order
- No authentication is required for either endpoint
- The values represent platform-wide aggregate metrics

In case of errors, the response will include an appropriate error message in the `message` field.
