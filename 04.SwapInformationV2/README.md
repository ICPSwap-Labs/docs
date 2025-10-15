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
- **Global Metrics**: Platform-wide statistics, trading volumes, and market insights

##  API Structure

The ICPSwap Data APIs are organized into three main categories:

```
icpswap-info-docs/
├── token/           # Token-related APIs
├── pool/            # Pool-related APIs
├── global/          # Global platform APIs (Coming Soon)
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

###  Global APIs (Coming Soon)
- Platform-wide trading statistics
- Market overview data
- Network metrics
- DEX performance indicators

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

**Last Updated**: October 2025  
**API Version**: v1  
**Base URL**: `https://api.icpswap.com/info/`
