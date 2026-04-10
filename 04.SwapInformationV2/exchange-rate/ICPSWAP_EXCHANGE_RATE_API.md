# ICPSwap Exchange Rate API Documentation

## Overview
The ICPSwap Exchange Rate API provides reference exchange rates for selected assets against USD. The rate data is calculated from leading exchanges.

## Endpoint

### Get Exchange Rate
**URL:** `https://api.icpswap.com/info/exchange/rate/{pair}`  
**Method:** `GET`  
**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `pair` | String | Yes | Exchange rate pair in the path parameter |

## Supported Pairs

| Pair | Description |
|------|-------------|
| `icp-usd` | Internet Computer to USD exchange rate |
| `usdc-usd` | USDC to USD exchange rate |
| `usdt-usd` | USDT to USD exchange rate |
| `xdr-usd` | XDR to USD exchange rate |

## Response Format

### Success Response
```json
{
  "code": 200,
  "message": null,
  "data": "2.298"
}
```

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `code` | Integer | HTTP status code (200 for success) |
| `message` | String/null | Response message (null for successful requests) |
| `data` | String | Exchange rate value as a decimal string |

## Example Request

```http
GET https://api.icpswap.com/info/exchange/rate/icp-usd
```

## Example Response

```json
{
  "code": 200,
  "message": null,
  "data": "2.298"
}
```

## Notes

- The `pair` path parameter supports `icp-usd`, `usdc-usd`, `usdt-usd`, and `xdr-usd`
- Exchange rate data is calculated from leading exchanges
- The exchange rate is returned as a string to preserve precision
- No authentication is required for this endpoint

In case of errors, the response will include an appropriate error message in the `message` field.
