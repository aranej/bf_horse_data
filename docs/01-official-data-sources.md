# Official Data Sources

> Comprehensive guide to official Betfair and industry data sources for horse racing.

## Table of Contents

- [Betfair Historical Data Service](#betfair-historical-data-service)
- [Betfair Starting Price (BSP) Data](#betfair-starting-price-bsp-data)
- [Betfair Exchange API](#betfair-exchange-api)
- [Betfair Stream API](#betfair-stream-api)
- [Total Performance Data (TPD)](#total-performance-data-tpd)
- [Timeform](#timeform)
- [Racing Post](#racing-post)
- [The Racing API](#the-racing-api)

---

## Betfair Historical Data Service

**URL:** https://historicdata.betfair.com

The official Betfair Exchange Historical Data service provides time-stamped Exchange data for purchase and download.

### Access Requirements

- Registered Betfair account with KYC verification
- Login: https://register.betfair.com/account/registration

### Data Tiers

| Tier | Interval | Volume Data | Price |
|------|----------|-------------|-------|
| **BASIC** | 1 minute | No | Free |
| **ADVANCED** | 1 second | Yes | Paid |
| **PRO** | 50 milliseconds | Yes | Paid |

### Data Coverage

- **Start Date:** April 2015 (most markets)
- **Australian/NZ:** October 2016 onwards
- **Update Frequency:** 5 days after event settlement
- **Database Size:** ~1.5TB raw and preprocessed data

### Data Format

- **Format:** JSON (same as Exchange Stream API)
- **Compression:** TAR archives containing BZ2 files
- **File Types:**
  - Event (E) files: All market changes across an event
  - Market (M) files: Individual files per market

### Fields Available

```
EVENT_ID, EVENT_NAME
SELECTION_ID, SELECTION_NAME
WIN_LOSE status
BSP (Betfair Starting Price)
PPWAP (Pre-play Weighted Average Price)
MORNINGWAP
PPMAX, PPMIN (Pre-play max/min prices)
IPMAX, IPMIN (In-play max/min prices)
Volume data (ADVANCED/PRO tiers only)
```

### API Access

**Documentation:** https://historicdata.betfair.com/#/apidocs

**Key Operations:**
- `GetMyData` - Returns purchased packages
- `GetCollectionOptions` - Returns filter options
- `DownloadListOfFiles` - Returns files based on filter

**Rate Limits:** 100 requests per 10 seconds

### Resources

- [Sample Code](https://docs.developer.betfair.com/display/1smk3cen4v3lu3yomq5qye0ni/Sample+Code)
- [Postman Collection](https://documenter.getpostman.com/view/2487254/RWaGVqZ9)
- [Excel Workbook](https://github.com/betfair/historic-data-workbook)

---

## Betfair Starting Price (BSP) Data

**URL:** https://promo.betfair.com/betfairsp/prices

Free daily CSV files containing Betfair Starting Prices for horse racing.

### Coverage

| Region | Data Available |
|--------|----------------|
| Great Britain | Yes |
| Ireland | Yes |
| Australia | Yes |
| USA | Yes |
| South Africa | Yes |

### File Format

Daily CSV files with naming convention: `dwbfprices[region][DDMMYYYY].csv`

### Fields

```csv
EVENT_ID        - Unique event identifier
MENU_HINT       - Course name and time
EVENT_NAME      - Race name
EVENT_DT        - Event date/time
SELECTION_ID    - Runner identifier
SELECTION_NAME  - Horse name
WIN_LOSE        - Result (1=Won, 0=Lost)
BSP             - Betfair Starting Price
PPWAP           - Pre-play Weighted Average Price
MORNINGWAP      - Morning WAP
PPMAX           - Pre-play maximum price
PPMIN           - Pre-play minimum price
IPMAX           - In-play maximum price
IPMIN           - In-play minimum price
PPTRADEDVOL     - Pre-play traded volume
IPTRADEDVOL     - In-play traded volume
```

### Download Example

```bash
# UK data for specific date
curl -O https://promo.betfair.com/betfairsp/prices/dwbfpricesuk05122024.csv

# Irish data
curl -O https://promo.betfair.com/betfairsp/prices/dwbfpricesire05122024.csv
```

### Historical Archive

- **URL:** https://promo.betfair.com/betfairsp/SP_history.html
- **Coverage:** 10+ years of historical BSP data
- **Format:** Downloadable ZIP archives by year

---

## Betfair Exchange API

**Portal:** https://developer.betfair.com

### API Types

| API | Purpose |
|-----|---------|
| **Betting API** | Market navigation, odds, bet placement |
| **Accounts API** | Balance, statements, vendor services |
| **Stream API** | Real-time market and order data |
| **Race Status API** | Race status (UK/IRE/SA only) |

### Authentication

- **App Key Types:**
  - Delayed: Free, 1-60 second data delay
  - Live: £299 one-time, real-time data

- **Requirements:**
  - Username and password
  - Application Key (App Key)
  - Session Token
  - SSL Certificate (recommended for non-interactive login)

### Key Endpoints

```
Betting API:
├── listMarketCatalogue  - Navigate markets
├── listMarketBook       - Get available prices
├── listRunnerBook       - Runner information
├── placeOrders          - Place bets
├── cancelOrders         - Cancel bets
└── listCurrentOrders    - Current order status

Accounts API:
├── getAccountFunds      - Account balance
└── listCurrencyRates    - Currency conversion
```

### Rate Limits

| Operation | Limit |
|-----------|-------|
| listMarketBook | 5 calls/second per marketId |
| Order transactions | 1000/second |
| Concurrent requests | 3 queued maximum |
| Market data weight | Weight × Market IDs ≤ 200 points |

### Horse Racing Metadata

Available via `listMarketCatalogue` with `RUNNER_METADATA`:

```
SIRE_NAME
TRAINER_NAME
FORM (recent race results)
JOCKEY_NAME
AGE
DAYS_SINCE_LAST_RUN
OFFICIAL_RATING
STALL_DRAW
```

### Resources

- [API Documentation](https://docs.developer.betfair.com)
- [Python Sample Code](https://github.com/betfair/API-NG-sample-code/tree/master/python)
- [Developer Forum](https://forum.developer.betfair.com)

---

## Betfair Stream API

**Documentation:** https://docs.developer.betfair.com/display/1smk3cen4v3lu3yomq5qye0ni/Exchange+Stream+API

Real-time streaming API for market and order data.

### Features

- Low latency market data streaming
- Real-time price and volume updates
- Order status streaming
- Market definition changes

### Protocol

- **Transport:** SSL sockets with CRLF JSON
- **Currency:** GBP only (use `listCurrencyRates` to convert)
- **Conflation:** Delayed keys receive data every 3 minutes

### Data Available

```
Market Data:
├── Price changes (back/lay)
├── Volume traded
├── Market status
└── Runner changes

Order Data:
├── Bet placement confirmation
├── Match notifications
└── Order status updates
```

### Sample Code

- [Java Sample](https://github.com/betfair/stream-api-sample-code)
- [C# Sample](https://github.com/betfair/stream-api-sample-code)
- [Node.js Sample](https://github.com/betfair/stream-api-sample-code)

---

## Total Performance Data (TPD)

**URL:** https://www.totalperformancedata.com

Real-time GPS/GNSS tracking data from racecourses.

### Coverage

| Region | Courses |
|--------|---------|
| UK | Royal Ascot, Doncaster, Royal Windsor, York, and more |
| US | Del Mar, Pimlico, Woodbine |
| International | Meydan (Dubai) |

### Data Points

```
Speed (current, par speed)
Velocity fluctuation
Stride frequency and length
Distance travelled
Distance to finish
Position tracking (sub-meter accuracy)
2 years historical metrics per horse
```

### Key Advantage

- Data arrives **5-6 seconds before TV broadcasts**
- Essential for in-play trading strategies

### Pricing

- **Starting:** £10/month via [TPD.Zone](https://www.tpd.zone/)
- **Integration:** Native support in Bet Angel and Gruss

### Integration Platforms

| Platform | Integration |
|----------|-------------|
| [Bet Angel](https://www.betangel.com/live-horse-racing-data/) | Native, included free |
| [Gruss](https://www.tpd.zone/gruss/) | Native, £10/month TPD subscription |

---

## Timeform

**API:** https://api.timeform.com/horseracingapi/

Premium horse racing ratings and analysis since 1948.

### Data Available

- Pre-race data and ratings
- Historical data from early 1990s
- Unique Timeform ratings
- Race analysis and predictions

### Access

- **Commercial only** - contact Timeform for licensing
- Available via Betfair's Timeform integration
- Not available for individual developers

### Betfair Integration

Timeform data accessible via betfairlightweight's race card endpoint:
```python
# No app key required
trading.race_card.get_race_card(market_ids)
```

---

## Racing Post

**URL:** https://www.racingpost.com

### Official API (B2B)

- **Provider:** Spotlight Sports Group
- **Access:** Commercial B2B only
- **Contact:** https://www.spotlightsportsgroup.com/

### Data Available

- Results and form
- RPR (Racing Post Rating)
- Top Speed figures
- Tipping and analysis
- Historical form books

### Terms of Service

> "Non-exclusive and non-transferable licence for private and domestic use only"

Commercial scraping is prohibited. See [Legal Considerations](06-legal-considerations.md).

---

## The Racing API

**URL:** https://www.theracingapi.com

Commercial racing data API service.

### Coverage

| Region | Data |
|--------|------|
| UK | Results, racecards, odds |
| Ireland | Results, racecards, odds |
| Australia | Results, racecards |
| USA | Results, racecards |

### Database

- 500,000+ results and racecards
- Live bookmaker odds
- REST API with JSON responses

### Features

- Real-time data feeds
- Historical data access
- Bookmaker odds comparison
- Horse/jockey/trainer statistics

### Pricing

Subscription-based - contact for pricing.

---

## Additional Official Sources

### Equibase (US/Canada)

**URL:** https://www.equibase.com

- Official data provider for US/Canadian Thoroughbred racing
- Charts, entries, results since early 1990s
- Research dataset available (2023 full year, free for research)

### British Horseracing Authority (BHA)

**URL:** https://www.britishhorseracing.com

- Official UK racing authority
- Limited API access with strict throttling
- Terms prohibit commercial web scraping

### Horse Racing Ireland

**URL:** https://www.goracing.ie

- Official Irish racing authority
- Race results and fixtures
- Limited data export options

---

## Comparison Matrix

| Source | Cost | Data Type | Best For |
|--------|------|-----------|----------|
| Betfair Historical | Free-Paid | Tick data | Backtesting |
| Betfair BSP | Free | Settlement prices | Simple analysis |
| Betfair API | £299 | Live data | Trading |
| TPD | £10/month | GPS tracking | In-play trading |
| Timeform | Commercial | Ratings | Professional analysis |
| The Racing API | Subscription | Comprehensive | Application development |

---

## Next Steps

- [GitHub Tools & Scrapers](02-github-tools-scrapers.md) - Community alternatives
- [Python Libraries](03-python-libraries.md) - Integration guides
- [Datasets](04-datasets.md) - Ready-to-use data
