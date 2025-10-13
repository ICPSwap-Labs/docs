# ICPSwap Token Information API Documentation

## Overview
The ICPSwap Token Information API provides comprehensive data about all tokens available on the ICPSwap platform, including pricing, trading volume, and market statistics.

## Endpoint

### Get All Token Information
**URL:** `https://api.icpswap.com/info/token/all`  
**Method:** `GET`  
**Parameters:** None

## Response Format

### Success Response
```json
{
  "code": 200,
  "message": null,
  "data": [
    {
      "tokenLedgerId": "string",
      "tokenName": "string", 
      "tokenSymbol": "string",
      "price": "string",
      "priceChange24H": "string",
      "tvlUSD": "string",
      "tvlUSDChange24H": "string",
      "txCount24H": "string",
      "volumeUSD24H": "string",
      "volumeUSD7D": "string",
      "totalVolumeUSD": "string",
      "priceLow24H": "string",
      "priceHigh24H": "string",
      "priceLow7D": "string",
      "priceHigh7D": "string",
      "priceLow30D": "string",
      "priceHigh30D": "string"
    }
  ]
}
```

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `code` | Integer | HTTP status code (200 for success) |
| `message` | String/null | Response message (null for successful requests) |
| `data` | Array | Array of token objects |

### Token Object Fields

| Field | Type | Description |
|-------|------|-------------|
| `tokenLedgerId` | String | Unique identifier for the token's ledger canister |
| `tokenName` | String | Full name of the token |
| `tokenSymbol` | String | Symbol for the token |
| `price` | String | Current price of the token (decimal string) |
| `priceChange24H` | String | 24-hour price change percentage (decimal string) |
| `tvlUSD` | String | Total Value Locked in USD (decimal string) |
| `tvlUSDChange24H` | String | 24-hour TVL change percentage (decimal string) |
| `txCount24H` | String | Number of transactions in the last 24 hours |
| `volumeUSD24H` | String | 24-hour trading volume in USD (decimal string) |
| `volumeUSD7D` | String | 7-day trading volume in USD (decimal string) |
| `totalVolumeUSD` | String | Total historical trading volume in USD (decimal string) |
| `priceLow24H` | String | Lowest price in the last 24 hours (decimal string) |
| `priceHigh24H` | String | Highest price in the last 24 hours (decimal string) |
| `priceLow7D` | String | Lowest price in the last 7 days (decimal string) |
| `priceHigh7D` | String | Highest price in the last 7 days (decimal string) |
| `priceLow30D` | String | Lowest price in the last 30 days (decimal string) |
| `priceHigh30D` | String | Highest price in the last 30 days (decimal string) |

## Example Response

```json
{
  "code": 200,
  "message": null,
  "data": [
    {
      "tokenLedgerId": "k2iiu-naaaa-aaaam-qdbya-cai",
      "tokenName": "Baby jade 8",
      "tokenSymbol": "Babe",
      "price": "0.000008583216191659",
      "priceChange24H": "0.958253955536774600",
      "tvlUSD": "2338.182883547660257355",
      "tvlUSDChange24H": "0.265086977639030400",
      "txCount24H": "13",
      "volumeUSD24H": "14.719851697960286329",
      "volumeUSD7D": "232.232375461443547246",
      "totalVolumeUSD": "11266.703972985822831506",
      "priceLow24H": "0.000000000000000000",
      "priceHigh24H": "0.000011494497118124",
      "priceLow7D": "0.000000000000000000",
      "priceHigh7D": "0.000011494497118124",
      "priceLow30D": "0.000000000000000000",
      "priceHigh30D": "0.000011494497118124"
    }
  ]
}
```

## Notes

- All numeric values are returned as strings to maintain precision
- Price changes are represented as percentages (e.g., "0.958253955536774600" = 95.83% increase)
- Zero values are represented as "0.000000000000000000"
- The API returns data for all swap tokens on the ICPSwap platform
- No authentication is required for this endpoint
- The response includes comprehensive market data for each token


In case of errors, the response will include an appropriate error message in the `message` field.
