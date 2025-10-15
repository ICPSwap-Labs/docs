# ICPSwap Pool Information API Documentation

## Overview
The ICPSwap Pool Information API provides comprehensive data about all liquidity pools available on the ICPSwap platform, including pool details, token information, pricing, trading volume, and market statistics.

## Endpoint

### Get All Pool Information
**URL:** `https://api.icpswap.com/info/pool/all`  
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
      "poolId": "string",
      "poolFee": "integer",
      "token0LedgerId": "string",
      "token0Name": "string",
      "token0Symbol": "string",
      "token0LiquidityAmount": "string",
      "token0Price": "string",
      "token1LedgerId": "string",
      "token1Name": "string",
      "token1Symbol": "string",
      "token1LiquidityAmount": "string",
      "token1Price": "string",
      "tvlUSD": "string",
      "tvlUSDChange24H": "string",
      "txCount24H": "string",
      "feesUSD24H": "string",
      "token0Volume24H": "string",
      "token1Volume24H": "string",
      "token0TotalVolume": "string",
      "token1TotalVolume": "string",
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
| `data` | Array | Array of pool objects |

### Pool Object Fields

| Field | Type | Description |
|-------|------|-------------|
| `poolId` | String | Unique identifier for the liquidity pool |
| `poolFee` | Integer | Pool fee rate (in basis points, e.g., 3000 = 0.3%) |
| `token0LedgerId` | String | Ledger canister ID of the first token in the pair |
| `token0Name` | String | Full name of the first token |
| `token0Symbol` | String | Symbol of the first token |
| `token0LiquidityAmount` | String | Amount of token0 in the pool (decimal string) |
| `token0Price` | String | Current price of token0 (decimal string) |
| `token1LedgerId` | String | Ledger canister ID of the second token in the pair |
| `token1Name` | String | Full name of the second token |
| `token1Symbol` | String | Symbol of the second token |
| `token1LiquidityAmount` | String | Amount of token1 in the pool (decimal string) |
| `token1Price` | String | Current price of token1 (decimal string) |
| `tvlUSD` | String | Total Value Locked in USD (decimal string) |
| `tvlUSDChange24H` | String | 24-hour TVL change percentage (decimal string) |
| `txCount24H` | String | Number of transactions in the last 24 hours |
| `feesUSD24H` | String | Fees generated in USD in the last 24 hours (decimal string) |
| `token0Volume24H` | String | 24-hour trading volume for token0 (decimal string) |
| `token1Volume24H` | String | 24-hour trading volume for token1 (decimal string) |
| `token0TotalVolume` | String | Total historical trading volume for token0 (decimal string) |
| `token1TotalVolume` | String | Total historical trading volume for token1 (decimal string) |
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
      "poolId": "pgcdz-7yaaa-aaaag-qnera-cai",
      "poolFee": 3000,
      "token0LedgerId": "pwba7-ciaaa-aaaam-qcxia-cai",
      "token0Name": "GarfieldCoin",
      "token0Symbol": "GFC",
      "token0LiquidityAmount": "284725212.5504625",
      "token0Price": "0.000001822970284217",
      "token1LedgerId": "ryjl3-tyaaa-aaaaa-aaaba-cai",
      "token1Name": "Internet Computer",
      "token1Symbol": "ICP",
      "token1LiquidityAmount": "502.94227519",
      "token1Price": "3.033635345639373400",
      "tvlUSD": "2115.921549552215800000",
      "tvlUSDChange24H": "8.258402722357666000",
      "txCount24H": "0",
      "feesUSD24H": "0.000000000000000000",
      "token0Volume24H": "0.000000000000000000",
      "token1Volume24H": "0.000000000000000000",
      "token0TotalVolume": "0.000000000000000000",
      "token1TotalVolume": "0.000000000000000000",
      "volumeUSD24H": "0.000000000000000000",
      "volumeUSD7D": "0.674812719954383695",
      "totalVolumeUSD": "68904.725027099255421016",
      "priceLow24H": "0.000000600000000000",
      "priceHigh24H": "0.000001230000000000",
      "priceLow7D": "0.000000600000000000",
      "priceHigh7D": "0.000001240000000000",
      "priceLow30D": "0.000000600000000000",
      "priceHigh30D": "0.000001310000000000"
    },
    {
      "poolId": "h2bmy-uaaaa-aaaag-qnffq-cai",
      "poolFee": 3000,
      "token0LedgerId": "k45jy-aiaaa-aaaaq-aadcq-cai",
      "token0Name": "Motoko",
      "token0Symbol": "MOTOKO",
      "token0LiquidityAmount": "3953178.11639281",
      "token0Price": "0.013422828608873625",
      "token1LedgerId": "ryjl3-tyaaa-aaaaa-aaaba-cai",
      "token1Name": "Internet Computer",
      "token1Symbol": "ICP",
      "token1LiquidityAmount": "14978.23736458",
      "token1Price": "3.478594293357040000",
      "tvlUSD": "105738.975642125590000000",
      "tvlUSDChange24H": "10.314578447437644400",
      "txCount24H": "23",
      "feesUSD24H": "0.000000000000000000",
      "token0Volume24H": "169279.827929880000000000",
      "token1Volume24H": "641.197314880000000000",
      "token0TotalVolume": "0.000000000000000000",
      "token1TotalVolume": "0.000000000000000000",
      "volumeUSD24H": "2157.779817277150805807",
      "volumeUSD7D": "18298.423502830747719290",
      "totalVolumeUSD": "6539218.122745290602341615",
      "priceLow24H": "0.003444190000000000",
      "priceHigh24H": "0.019941330000000000",
      "priceLow7D": "0.003444190000000000",
      "priceHigh7D": "0.048196280000000000",
      "priceLow30D": "0.003444190000000000",
      "priceHigh30D": "0.048196280000000000"
    }
  ]
}
```

## Notes

- All numeric values are returned as strings to maintain precision
- Pool fees are represented as integers in basis points (e.g., 3000 = 0.3%)
- Price changes are represented as percentages (e.g., "8.258402722357666000" = 8.26% increase)
- Zero values are represented as "0.000000000000000000"
- The API returns data for all liquidity pools on the ICPSwap platform
- No authentication is required for this endpoint
- The response includes comprehensive market data for each pool including both tokens in the pair
- Token0 and Token1 represent the two tokens in each liquidity pool pair
- Some fields may be null for pools with no trading activity

In case of errors, the response will include an appropriate error message in the `message` field.
