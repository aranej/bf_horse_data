# Betfair Horse Racing Data Sources

> Comprehensive reference documentation for accessing horse racing data for analytical processing and algorithmic trading.

## Overview

This repository serves as a curated reference guide for professionals, data scientists, and developers seeking to access horse racing data from Betfair Exchange and related sources. The documentation covers official APIs, community-built tools, datasets, and best practices for data collection.

## Table of Contents

### Core Documentation

| Document | Description |
|----------|-------------|
| [Official Data Sources](docs/01-official-data-sources.md) | Betfair Historical Data, APIs, and official provider services |
| [GitHub Tools & Scrapers](docs/02-github-tools-scrapers.md) | Community-built open source tools and scrapers |
| [Python Libraries](docs/03-python-libraries.md) | Python ecosystem for Betfair integration |
| [Datasets & Downloads](docs/04-datasets.md) | Ready-to-use datasets from Kaggle and other sources |
| [Community Resources](docs/05-community-resources.md) | Forums, Discord servers, and learning materials |
| [Legal Considerations](docs/06-legal-considerations.md) | Terms of service, rate limits, and compliance |

### Quick Reference

| Resource | Type | Cost | Best For |
|----------|------|------|----------|
| [Betfair SP History](https://promo.betfair.com/betfairsp/prices) | CSV | Free | BSP analysis, backtesting |
| [Betfair Historical Data](https://historicdata.betfair.com) | JSON/TAR | Free (Basic) | Tick data, market analysis |
| [betfairlightweight](https://github.com/betcode-org/betfair) | Python API | Free | Live trading, streaming |
| [rpscrape](https://github.com/joenano/rpscrape) | Scraper | Free | Racing Post historical data |
| [Kaggle HK Racing](https://www.kaggle.com/datasets/gdaley/hkracing) | Dataset | Free | ML model training |

## Data Access Tiers

### Free Tier
- Betfair SP (Starting Price) historical CSV files
- Betfair Historical Data BASIC (1-minute intervals)
- Kaggle datasets (Hong Kong, UK historical)
- Community scrapers (Racing Post via rpscrape)

### Professional Tier
- Betfair Historical Data PRO (50ms intervals) - Paid
- Betfair Live API Key - £299 one-time
- Total Performance Data (TPD) - £10/month
- Proform Racing Database - ~£1,200/year

## Technology Stack

```
Primary Language: Python 3.9+

Core Libraries:
├── betfairlightweight  - Betfair API wrapper
├── flumine             - Trading framework
├── pandas              - Data analysis
└── betfair_data        - Fast Rust-based parser

Scraping Tools:
├── selenium            - Browser automation
├── playwright          - Modern async scraping
├── beautifulsoup4      - HTML parsing
└── scrapy              - Web crawling framework
```

## Quick Start

### 1. Access Free BSP Data
```bash
# Download Betfair Starting Price data
curl -O https://promo.betfair.com/betfairsp/prices/dwbfpricesuk$(date +%d%m%Y).csv
```

### 2. Install Python Libraries
```bash
pip install betfairlightweight flumine pandas
```

### 3. Use Community Scraper
```bash
git clone https://github.com/joenano/rpscrape.git
cd rpscrape
pip install requests tomli orjson jarowinkler aiohttp lxml
python rpscrape.py
# In console: gb 2023 flat
```

## Repository Structure

```
bf_horse_data/
├── README.md                          # This file
├── docs/
│   ├── 01-official-data-sources.md    # Official APIs and data services
│   ├── 02-github-tools-scrapers.md    # Community tools catalog
│   ├── 03-python-libraries.md         # Python ecosystem guide
│   ├── 04-datasets.md                 # Available datasets
│   ├── 05-community-resources.md      # Forums and communities
│   └── 06-legal-considerations.md     # Legal and compliance
└── examples/                          # Code examples (future)
```

## Contributing

This is a living document. Contributions are welcome for:
- New data sources and tools
- Updated URLs and documentation
- Code examples and tutorials
- Corrections and improvements

## Disclaimer

This documentation is for educational and research purposes. Users are responsible for:
- Complying with terms of service of data providers
- Ensuring legal compliance in their jurisdiction
- Responsible use of scraping tools
- Proper licensing of commercial data

## License

MIT License - See LICENSE file for details.

---

**Last Updated:** December 2024
**Maintained by:** [Contributors]
