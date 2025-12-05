# Python Libraries

> Complete guide to the Python ecosystem for Betfair horse racing integration.

## Table of Contents

- [Core Libraries](#core-libraries)
- [betfairlightweight](#betfairlightweight)
- [flumine](#flumine)
- [betfair_data](#betfair_data)
- [Supporting Libraries](#supporting-libraries)
- [Installation Guide](#installation-guide)
- [Quick Start Examples](#quick-start-examples)

---

## Core Libraries

### Overview

| Library | Purpose | PyPI | GitHub |
|---------|---------|------|--------|
| betfairlightweight | API wrapper | [PyPI](https://pypi.org/project/betfairlightweight/) | [betcode-org/betfair](https://github.com/betcode-org/betfair) |
| flumine | Trading framework | [PyPI](https://pypi.org/project/flumine/) | [betcode-org/flumine](https://github.com/betcode-org/flumine) |
| betfair_data | Fast data parser | [PyPI](https://pypi.org/project/betfair-data/) | [tarb/betfair_data](https://github.com/tarb/betfair_data) |

### Installation

```bash
# Core trading stack
pip install betfairlightweight flumine

# With speed optimizations (recommended)
pip install betfairlightweight[speed]

# Fast historical data parsing
pip install betfair-data

# Full stack
pip install betfairlightweight[speed] flumine betfair-data pandas
```

---

## betfairlightweight

**Repository:** https://github.com/betcode-org/betfair
**Documentation:** https://betcode-org.github.io/betfair/
**Stats:** 484 stars, 156 forks
**Python:** 3.9 - 3.14

### Features

- Full Betfair API-NG support
- Exchange Stream API integration
- Historical data streaming
- Race card endpoint (Timeform data)
- Uses C (ciso8601) and Rust (orjson) for speed

### Authentication

```python
import betfairlightweight as bflw

# Certificate-based login (recommended)
trading = bflw.APIClient(
    username="your_username",
    password="your_password",
    app_key="your_app_key",
    certs="/path/to/certs"
)
trading.login()

# Interactive login
trading = bflw.APIClient(
    username="your_username",
    password="your_password",
    app_key="your_app_key"
)
trading.login_interactive()
```

### Market Filtering

```python
from betfairlightweight import filters

# Horse racing markets
market_filter = filters.market_filter(
    event_type_ids=[7],           # 7 = Horse Racing
    market_countries=["GB", "IE"],
    market_type_codes=["WIN"]
)

# Get market catalogue
markets = trading.betting.list_market_catalogue(
    filter=market_filter,
    market_projection=["RUNNER_METADATA", "EVENT"],
    max_results=100
)

# Get prices
for market in markets:
    book = trading.betting.list_market_book(
        market_ids=[market.market_id],
        price_projection=filters.price_projection(
            price_data=["EX_BEST_OFFERS"]
        )
    )
```

### Streaming

```python
# Create streaming client
trading.streaming.start()

# Subscribe to market
market_subscription = trading.streaming.market_data_filter(
    market_ids=["1.123456789"],
    fields=["EX_BEST_OFFERS", "EX_TRADED"]
)

# Process updates
def process_market_book(market_book):
    for runner in market_book.runners:
        print(f"{runner.selection_id}: {runner.last_price_traded}")

trading.streaming.subscribe_to_markets(
    market_filter=market_subscription,
    market_data_callback=process_market_book
)
```

### Historical Data

```python
# Create historical stream
stream = trading.streaming.create_historical_stream(
    file_path="/path/to/historical/data",
    listener=StreamListener()
)

# Process historical data
generator = stream.get_generator()
for market_books in generator():
    for market_book in market_books:
        process_market_book(market_book)
```

### Race Card (Timeform Data)

```python
# No app key required
race_card = trading.race_card.get_race_card(
    market_ids=["1.123456789"]
)

for runner in race_card:
    print(f"Horse: {runner.horse_name}")
    print(f"Trainer: {runner.trainer_name}")
    print(f"Jockey: {runner.jockey_name}")
    print(f"Form: {runner.form}")
```

---

## flumine

**Repository:** https://github.com/betcode-org/flumine
**Documentation:** https://betcode-org.github.io/flumine/
**Stats:** 213 stars, 62 forks
**Python:** 3.9 - 3.12

### Features

- Event-driven trading framework
- Strategy-based architecture
- Paper trading mode
- Simulation/backtesting
- Multi-exchange support (Betfair, Betdaq, Betconnect)
- Risk management controls
- Data recording

### Architecture

```
flumine Framework:
├── Strategies          - Custom trading logic
├── Trading Controls    - Risk management
├── Workers             - Background processes
├── Execution           - Order management
└── Streams             - Market data feeds
```

### Basic Strategy

```python
from flumine import Flumine, clients
from flumine.strategy.strategy import BaseStrategy
from flumine.order.trade import Trade
from flumine.order.order import LimitOrder

class ExampleStrategy(BaseStrategy):
    def check_market_book(self, market, market_book):
        # Called on every market update
        return True

    def process_market_book(self, market, market_book):
        # Implement trading logic
        for runner in market_book.runners:
            if runner.selection_id == self.selection_id:
                if runner.last_price_traded < self.target_price:
                    # Place back bet
                    trade = Trade(
                        market_id=market.market_id,
                        selection_id=runner.selection_id,
                        handicap=runner.handicap,
                        strategy=self
                    )
                    order = trade.create_order(
                        side="BACK",
                        order_type=LimitOrder(
                            price=runner.last_price_traded,
                            size=2.00
                        )
                    )
                    market.place_order(order)
```

### Live Trading

```python
from flumine import Flumine, clients
from betfairlightweight import APIClient

# Setup
trading = APIClient(
    username="username",
    password="password",
    app_key="app_key",
    certs="/path/to/certs"
)

client = clients.BetfairClient(trading)
framework = Flumine(client=client)

# Add strategy
strategy = ExampleStrategy(
    market_filter={"eventTypeIds": ["7"]},  # Horse racing
    market_data_filter={"fields": ["EX_BEST_OFFERS"]}
)
framework.add_strategy(strategy)

# Run
framework.run()
```

### Paper Trading

```python
# Enable paper trading (no real bets)
client = clients.BetfairClient(trading, paper_trade=True)
```

### Simulation/Backtesting

```python
from flumine import FlumineSimulation
from flumine.strategy.strategy import BaseStrategy

# Create simulation framework
framework = FlumineSimulation()

# Add client
client = clients.SimulatedClient()
framework.add_client(client)

# Add strategy
framework.add_strategy(strategy)

# Add historical data
framework.add_market({
    "market_id": "1.123456789",
    "event_id": "123456789",
    "event_type_id": "7",
    "event_name": "Example Race",
    "market_start_time": "2024-01-01T14:00:00Z"
}, data_directory="/path/to/historical/data")

# Run simulation
framework.run()
```

### Trading Controls

```python
from flumine.controls.tradingcontrols import StrategyExposure

# Limit exposure per selection
framework.add_trading_control(
    StrategyExposure(
        strategy=strategy,
        max_selection_exposure=100.00,
        max_order_exposure=10.00
    )
)
```

---

## betfair_data

**Repository:** https://github.com/tarb/betfair_data
**Python:** >= 3.7

### Features

- **Very fast** (Rust implementation)
- Supports official Betfair data + self-recorded streams
- Drop-in replacement for betfairlightweight objects
- Multiple compression formats

### Supported Formats

- BZ2 compressed files
- GZIP compressed files
- TAR archives
- ZIP archives
- Uncompressed JSON

### Usage

```python
import betfair_data as bfd

# Parse single file
for market in bfd.parse_file("/path/to/data.bz2"):
    for market_book in market:
        for runner in market_book.runners:
            print(runner.selection_id, runner.last_price_traded)

# Parse directory
for market in bfd.parse_dir("/path/to/data/"):
    process_market(market)

# Parse TAR archive
for market in bfd.parse_tar("/path/to/data.tar"):
    process_market(market)
```

### Performance Comparison

```python
# betfairlightweight: ~60 seconds for large dataset
# betfair_data:       ~5 seconds for same dataset

# Tip: Remove simulation middleware for pure data collection
# framework._market_middleware = []
```

---

## Supporting Libraries

### Data Processing

```python
# Pandas - Data analysis
pip install pandas

import pandas as pd
df = pd.read_csv("bsp_data.csv")

# NumPy - Numerical computing
pip install numpy

# orjson - Fast JSON (included in betfairlightweight[speed])
pip install orjson
```

### Web Scraping

```python
# Selenium - Browser automation
pip install selenium

from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()
driver.get("https://www.racingpost.com/...")

# Playwright - Modern async scraping
pip install playwright
playwright install

from playwright.async_api import async_playwright

async with async_playwright() as p:
    browser = await p.chromium.launch()
    page = await browser.new_page()
    await page.goto("https://...")

# BeautifulSoup - HTML parsing
pip install beautifulsoup4 lxml

from bs4 import BeautifulSoup
soup = BeautifulSoup(html, 'lxml')

# Scrapy - Web crawling framework
pip install scrapy

# aiohttp - Async HTTP
pip install aiohttp

# cloudscraper - Cloudflare bypass
pip install cloudscraper
```

### Machine Learning

```python
# Scikit-learn
pip install scikit-learn

from sklearn.ensemble import RandomForestClassifier

# TensorFlow/Keras
pip install tensorflow

from tensorflow import keras

# LightGBM
pip install lightgbm

import lightgbm as lgb
```

---

## Installation Guide

### Full Development Environment

```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows

# Core libraries
pip install betfairlightweight[speed] flumine betfair-data

# Data processing
pip install pandas numpy

# Scraping (choose based on need)
pip install selenium beautifulsoup4 lxml
pip install playwright && playwright install

# ML (optional)
pip install scikit-learn lightgbm

# Development tools
pip install jupyter ipython pytest
```

### Requirements.txt

```text
# Core
betfairlightweight[speed]>=2.20.0
flumine>=2.6.0
betfair-data>=0.1.8

# Data
pandas>=2.0.0
numpy>=1.24.0

# Scraping
beautifulsoup4>=4.12.0
lxml>=4.9.0
requests>=2.31.0
aiohttp>=3.9.0

# Optional: Browser automation
selenium>=4.15.0
# playwright>=1.40.0

# Optional: ML
scikit-learn>=1.3.0
lightgbm>=4.0.0
```

---

## Quick Start Examples

### Example 1: Get Today's Horse Racing Markets

```python
import betfairlightweight as bflw
from betfairlightweight import filters

# Login
trading = bflw.APIClient(
    username="your_username",
    password="your_password",
    app_key="your_app_key"
)
trading.login_interactive()

# Get horse racing markets
market_filter = filters.market_filter(
    event_type_ids=[7],
    market_countries=["GB"],
    market_type_codes=["WIN"]
)

markets = trading.betting.list_market_catalogue(
    filter=market_filter,
    market_projection=["EVENT", "RUNNER_DESCRIPTION"],
    max_results=50
)

for market in markets:
    print(f"\n{market.event.name}")
    print(f"Start: {market.market_start_time}")
    for runner in market.runners:
        print(f"  - {runner.runner_name}")
```

### Example 2: Download BSP Data

```python
import requests
import pandas as pd
from datetime import datetime, timedelta

def download_bsp_data(days_back=7, region="uk"):
    """Download BSP data for the last N days."""

    base_url = "https://promo.betfair.com/betfairsp/prices"
    dfs = []

    for i in range(days_back):
        date = datetime.now() - timedelta(days=i+1)
        date_str = date.strftime("%d%m%Y")
        url = f"{base_url}/dwbfprices{region}{date_str}.csv"

        try:
            df = pd.read_csv(url)
            df['download_date'] = date
            dfs.append(df)
            print(f"Downloaded: {date.strftime('%Y-%m-%d')}")
        except Exception as e:
            print(f"Failed: {date.strftime('%Y-%m-%d')} - {e}")

    if dfs:
        return pd.concat(dfs, ignore_index=True)
    return pd.DataFrame()

# Download last 7 days UK BSP data
df = download_bsp_data(days_back=7, region="uk")
print(f"\nTotal records: {len(df)}")
print(df.head())
```

### Example 3: Parse Historical Data

```python
import betfair_data as bfd
import pandas as pd

def parse_historical_market(file_path):
    """Parse historical market data to DataFrame."""

    records = []

    for market in bfd.parse_file(file_path):
        for market_book in market:
            timestamp = market_book.publish_time

            for runner in market_book.runners:
                records.append({
                    'timestamp': timestamp,
                    'market_id': market_book.market_id,
                    'selection_id': runner.selection_id,
                    'status': runner.status,
                    'last_price_traded': runner.last_price_traded,
                    'total_matched': runner.total_matched
                })

    return pd.DataFrame(records)

# Parse and analyze
df = parse_historical_market("/path/to/1.123456789.bz2")
print(df.describe())
```

### Example 4: Simple Flumine Strategy

```python
from flumine import Flumine, clients
from flumine.strategy.strategy import BaseStrategy
from betfairlightweight import APIClient

class FavouriteBackStrategy(BaseStrategy):
    """Back the favourite if price > 2.0"""

    def check_market_book(self, market, market_book):
        # Only process if market is open
        return market_book.status == "OPEN"

    def process_market_book(self, market, market_book):
        # Find favourite (lowest price)
        runners = [(r, r.last_price_traded)
                   for r in market_book.runners
                   if r.last_price_traded]

        if not runners:
            return

        favourite = min(runners, key=lambda x: x[1])
        runner, price = favourite

        # Only back if price > 2.0
        if price and price > 2.0:
            print(f"Favourite: {runner.selection_id} @ {price}")

# Setup
trading = APIClient("user", "pass", app_key="key")
client = clients.BetfairClient(trading, paper_trade=True)
framework = Flumine(client=client)

# Add strategy
strategy = FavouriteBackStrategy(
    market_filter={"eventTypeIds": ["7"], "marketCountries": ["GB"]},
    market_data_filter={"fields": ["EX_BEST_OFFERS"]}
)
framework.add_strategy(strategy)

# Run (paper trading)
# framework.run()
```

---

## Resources

### Official Documentation

- [betfairlightweight Docs](https://betcode-org.github.io/betfair/)
- [flumine Docs](https://betcode-org.github.io/flumine/)
- [Betfair API Docs](https://docs.developer.betfair.com)

### Tutorials

- [Betfair API Python Tutorial](https://betfair-datascientists.github.io/api/apiPythontutorial/)
- [How to Automate Series](https://betfair-datascientists.github.io/tutorials/How_to_Automate_1/)
- [Flumine Simulations](https://betfair-datascientists.github.io/tutorials/flumineSimulations/)

### Community

- [Betcode Slack](https://betcode-org.github.io/) - 2,000+ members
- [Betfair Developer Forum](https://forum.developer.betfair.com)
- [Bet Angel Forum](https://forum.betangel.com)

---

## Next Steps

- [Datasets](04-datasets.md) - Ready-to-use data
- [Community Resources](05-community-resources.md) - Forums and help
- [Legal Considerations](06-legal-considerations.md) - Compliance
