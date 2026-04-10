# ICPSwap Data Interface Documentation

Welcome to the ICPSwap Data Interface repository! This repository provides comprehensive API documentation for accessing real-time and historical data from the ICPSwap decentralized exchange (DEX) platform.

##  Table of Contents

- [Overview](#overview)
- [API Structure](#api-structure)
- [Available APIs](#available-apis)
- [Getting Started](#getting-started)
- [Authentication](#authentication)
- [Response Format](#response-format)
- [Error Handling](#error-handling)
- [Data Types](#data-types)
- [Support](#support)

##  Overview

ICPSwap is a decentralized exchange built on the Internet Computer Protocol (ICP), providing users with seamless token swapping capabilities. This documentation repository contains comprehensive API specifications for accessing:

- **Token Information**: Real-time pricing, market data, and trading statistics
- **Pool Data**: Liquidity pool information, trading pairs, and pool statistics
- **Transaction Records**: Limit order and transfer position history
- **Exchange Rates**: Reference exchange rates for selected assets against USD
- **Global Metrics**: Platform-wide statistics, trading volumes, and market insights

##  API Structure

The ICPSwap Data APIs are organized into three main categories:

```
icpswap-info-docs/
├── token/           # Token-related APIs
├── pool/            # Pool-related APIs
├── transaction/     # Transaction-related APIs
├── exchange-rate/   # Exchange rate APIs
├── global/          # Global platform APIs
└── README.md        # This documentation
```

### Base URL
All API endpoints are served from: `https://api.icpswap.com/info/`

##  Available APIs

###  Token APIs

#### [Token Information API](./token/ICPSWAP_TOKEN_API.md)
- **Endpoint**: `GET /token/all`
- **Description**: Retrieve comprehensive information about all tokens on ICPSwap
- **Features**: 
  - Real-time pricing data
  - 24-hour price changes
  - Trading volume statistics
  - TVL (Total Value Locked) data
  - Historical price ranges

#### [Token Chart Data API](./token/ICPSWAP_TOKEN_CHART_API.md)
- **Endpoint**: `GET /token/{tokenLedgerId}/chart/{level}`
- **Description**: Access historical price and trading data for specific tokens
- **Features**:
  - Configurable time intervals (daily, hourly, minute)
  - Paginated results
  - OHLC (Open, High, Low, Close) data
  - Volume and liquidity metrics

###  Pool APIs

#### [Pool Information API](./pool/ICPSWAP_POOL_API.md)
- **Endpoint**: `GET /pool/all`
- **Description**: Retrieve comprehensive information about all liquidity pools on ICPSwap
- **Features**: 
  - Pool details and token information
  - Real-time pricing data
  - Trading volume statistics
  - TVL (Total Value Locked) data
  - Historical price ranges
  - Pool performance metrics

#### [Pool Chart Data API](./pool/ICPSWAP_POOL_CHART_API.md)
- **Endpoint**: `GET /pool/{poolId}/chart/{level}`
- **Description**: Access historical price and trading data for specific pools
- **Features**:
  - Configurable time intervals (daily, hourly, minute)
  - Paginated results
  - OHLC (Open, High, Low, Close) data
  - Volume and liquidity metrics
  - Pool-specific trading statistics

### Transaction APIs

#### [Limit Order Record API](./transaction/ICPSWAP_LIMIT_ORDER_API.md)
- **Endpoint**: `GET /record/limitOrder/list`
- **Description**: Retrieve paginated limit order history filtered by pool, user, time range, and action type
- **Features**:
  - Optional filters for `poolId`, `principal`, `begin`, `end`, and `actionTypes`
  - Paginated transaction records
  - Limit order creation and execution history
  - Pool and token context in each record

#### [Transfer Position Record API](./transaction/ICPSWAP_TRANSFER_POSITION_API.md)
- **Endpoint**: `GET /record/transferPosition/list`
- **Description**: Retrieve paginated transfer position history filtered by user, time range, or a set of pool IDs
- **Features**:
  - Optional filters for `poolIds`, `principal`, `begin`, and `end`
  - Paginated transfer records
  - Position ownership transfer history
  - Pool-specific position transfer details

#### [Transaction API](./transaction/ICPSWAP_TRANSACTION_API.md)
- **Endpoint**: `GET /transaction/find`
- **Description**: Retrieve paginated swap, liquidity, and claim transaction history filtered by pool, token, user, time range, and action type
- **Features**:
  - Optional filters for `poolId`, `tokenId`, `principal`, `begin`, `end`, and `actionTypes`
  - Paginated transaction records
  - Swap, add liquidity, decrease liquidity, and claim history
  - Account, alias, token, and pool context in each record

### Exchange Rate APIs

#### [Exchange Rate API](./exchange-rate/ICPSWAP_EXCHANGE_RATE_API.md)
- **Endpoint**: `GET /exchange/rate/{pair}`
- **Description**: Retrieve reference exchange rates for selected assets against USD
- **Features**:
  - Supports `icp-usd`, `usdc-usd`, `usdt-usd`, and `xdr-usd`
  - Rate data calculated from leading exchanges
  - Decimal-string response format
  - No authentication required

### Global APIs

#### [Protocol Statistics API](./global/ICPSWAP_PROTOCOL_API.md)
- **Endpoint**: `GET /global/protocol`, `GET /global/protocol/d1`
- **Description**: Retrieve platform-wide protocol statistics and daily protocol statistics for ICPSwap
- **Features**:
  - Cumulative trading volume in USD
  - 24-hour trading volume, fees, and transaction count
  - Daily platform statistics with pagination
  - Total platform TVL in USD
  - Total trading pair count
  - Total cumulative user count

##  Getting Started

### Prerequisites
- No authentication required for public endpoints
- HTTP client or library for making API requests
- Understanding of JSON response format

### Quick Start Example

```bash
# Get all token information
curl -X GET "https://api.icpswap.com/info/token/all"

# Get historical data for a specific token
curl -X GET "https://api.icpswap.com/info/token/ryjl3-tyaaa-aaaaa-aaaba-cai/chart/d1?page=1&limit=100"

# Get all pool information
curl -X GET "https://api.icpswap.com/info/pool/all"

# Get historical data for a specific pool
curl -X GET "https://api.icpswap.com/info/pool/p2gzi-iyaaa-aaaag-qneta-cai/chart/d1?page=1&limit=10"

# Get limit order records
curl -X GET "https://api.icpswap.com/info/record/limitOrder/list?poolId=splxr-cqaaa-aaaar-qbmyq-cai&principal=tvrhj-lrsxa-hunxj-f6o5c-ggvwk-exolk-yg66g-fn5ag-67cr6-gxotu-uae&page=1&limit=10&begin=1774114049000&end=1776114049000&actionTypes=ExecuteLimitOrder,AddLimitOrder"

# Get transfer position records for a user or pool
curl -X GET "https://api.icpswap.com/info/record/transferPosition/list?poolIds=splxr-cqaaa-aaaar-qbmyq-cai,tqdeg-biaaa-aaaar-qbm4a-cai&principal=t7c3d-obwte-dykfa-bow6f-eagn6-i5anp-24wes-6s3af-su4jn-mnbwf-nqe&page=1&limit=10&begin=1774114049000&end=1776114049000"

# Find transactions
curl -X GET "https://api.icpswap.com/info/transaction/find?poolId=mohjv-bqaaa-aaaag-qjyia-cai&tokenId=&principal=ehq2s-mlmrx-xvogi-adg5n-dowp3-qasvb-nvdjl-ijj3m-e6ijc-pmrmb-dqe&page=1&limit=10&begin=1774114049000&end=1776114049000&actionTypes=Swap,AddLiquidity,DecreaseLiquidity,Claim"

# Get exchange rate
curl -X GET "https://api.icpswap.com/info/exchange/rate/icp-usd"

# Get protocol statistics
curl -X GET "https://api.icpswap.com/info/global/protocol"

# Get daily protocol statistics
curl -X GET "https://api.icpswap.com/info/global/protocol/d1?page=1&limit=10"
```

### JavaScript Example

```javascript
// Fetch all token data
async function getAllTokens() {
  try {
    const response = await fetch('https://api.icpswap.com/info/token/all');
    const data = await response.json();
    console.log('Token data:', data);
  } catch (error) {
    console.error('Error fetching token data:', error);
  }
}

// Fetch historical chart data
async function getTokenChartData(tokenLedgerId, level = 'd1', page = 1, limit = 100) {
  try {
    const url = `https://api.icpswap.com/info/token/${tokenLedgerId}/chart/${level}?page=${page}&limit=${limit}`;
    const response = await fetch(url);
    const data = await response.json();
    console.log('Chart data:', data);
  } catch (error) {
    console.error('Error fetching chart data:', error);
  }
}

// Fetch all pool data
async function getAllPools() {
  try {
    const response = await fetch('https://api.icpswap.com/info/pool/all');
    const data = await response.json();
    console.log('Pool data:', data);
  } catch (error) {
    console.error('Error fetching pool data:', error);
  }
}

// Fetch historical pool chart data
async function getPoolChartData(poolId, level = 'd1', page = 1, limit = 10) {
  try {
    const url = `https://api.icpswap.com/info/pool/${poolId}/chart/${level}?page=${page}&limit=${limit}`;
    const response = await fetch(url);
    const data = await response.json();
    console.log('Pool chart data:', data);
  } catch (error) {
    console.error('Error fetching pool chart data:', error);
  }
}

// Fetch limit order records
async function getLimitOrderRecords({
  poolId = '',
  principal = '',
  page = 1,
  limit = 10,
  begin = '',
  end = '',
  actionTypes = ''
} = {}) {
  try {
    const params = new URLSearchParams();
    if (poolId) params.set('poolId', poolId);
    if (principal) params.set('principal', principal);
    if (page) params.set('page', page);
    if (limit) params.set('limit', limit);
    if (begin) params.set('begin', begin);
    if (end) params.set('end', end);
    if (actionTypes) params.set('actionTypes', actionTypes);

    const url = `https://api.icpswap.com/info/record/limitOrder/list?${params.toString()}`;
    const response = await fetch(url);
    const data = await response.json();
    console.log('Limit order records:', data);
  } catch (error) {
    console.error('Error fetching limit order records:', error);
  }
}

// Fetch transfer position records for a user or pool
async function getTransferPositionRecords({
  poolIds = '',
  principal = '',
  page = 1,
  limit = 10,
  begin = '',
  end = ''
} = {}) {
  try {
    const params = new URLSearchParams();
    if (poolIds) params.set('poolIds', poolIds);
    if (principal) params.set('principal', principal);
    if (page) params.set('page', page);
    if (limit) params.set('limit', limit);
    if (begin) params.set('begin', begin);
    if (end) params.set('end', end);

    const url = `https://api.icpswap.com/info/record/transferPosition/list?${params.toString()}`;
    const response = await fetch(url);
    const data = await response.json();
    console.log('Transfer position records:', data);
  } catch (error) {
    console.error('Error fetching transfer position records:', error);
  }
}

// Fetch transaction records
async function getTransactions({
  poolId = '',
  tokenId = '',
  principal = '',
  page = 1,
  limit = 10,
  begin = '',
  end = '',
  actionTypes = ''
} = {}) {
  try {
    const params = new URLSearchParams();
    if (poolId) params.set('poolId', poolId);
    if (tokenId) params.set('tokenId', tokenId);
    if (principal) params.set('principal', principal);
    if (page) params.set('page', page);
    if (limit) params.set('limit', limit);
    if (begin) params.set('begin', begin);
    if (end) params.set('end', end);
    if (actionTypes) params.set('actionTypes', actionTypes);

    const url = `https://api.icpswap.com/info/transaction/find?${params.toString()}`;
    const response = await fetch(url);
    const data = await response.json();
    console.log('Transaction records:', data);
  } catch (error) {
    console.error('Error fetching transaction records:', error);
  }
}

// Fetch exchange rate
async function getExchangeRate(pair = 'icp-usd') {
  try {
    const response = await fetch(`https://api.icpswap.com/info/exchange/rate/${pair}`);
    const data = await response.json();
    console.log('Exchange rate:', data);
  } catch (error) {
    console.error('Error fetching exchange rate:', error);
  }
}

// Fetch protocol statistics
async function getProtocolStatistics() {
  try {
    const response = await fetch('https://api.icpswap.com/info/global/protocol');
    const data = await response.json();
    console.log('Protocol statistics:', data);
  } catch (error) {
    console.error('Error fetching protocol statistics:', error);
  }
}

// Fetch daily protocol statistics
async function getDailyProtocolStatistics(page = 1, limit = 10) {
  try {
    const url = `https://api.icpswap.com/info/global/protocol/d1?page=${page}&limit=${limit}`;
    const response = await fetch(url);
    const data = await response.json();
    console.log('Daily protocol statistics:', data);
  } catch (error) {
    console.error('Error fetching daily protocol statistics:', error);
  }
}
```

##  Authentication

Currently, all public endpoints do not require authentication. Simply make HTTP requests to the API endpoints.

##  Response Format

All API responses follow a consistent JSON structure:

```json
{
  "code": 200,
  "message": null,
  "data": {
    // Response data here
  }
}
```

### Response Fields
- `code`: HTTP status code (200 for success)
- `message`: Error message (null for successful requests)
- `data`: The actual response data

##  Error Handling

### Common HTTP Status Codes
- `200`: Success
- `400`: Bad Request - Invalid parameters
- `404`: Not Found - Resource doesn't exist
- `429`: Too Many Requests - Rate limit exceeded
- `500`: Internal Server Error

### Error Response Example
```json
{
  "code": 400,
  "message": "Invalid token ledger ID",
  "data": null
}
```

##  Data Types

### Numeric Values
All numeric values are returned as strings to maintain precision:
- Prices: Decimal strings (e.g., "4.795472580794851000")
- Percentages: Decimal strings (e.g., "0.958253955536774600" = 95.83%)
- Timestamps: Unix timestamps in milliseconds

### Time Intervals
- `d1`: Daily data
- `h1`: Hourly data  
- `m1`: Minute data

##  Support

- **Documentation Issues**: Open an issue in this repository
- **API Questions**: Contact the ICPSwap development team
- **General Support**: Visit the ICPSwap community channels

---

**Last Updated**: April 2026  
**API Version**: v2  
**Base URL**: `https://api.icpswap.com/info/`
