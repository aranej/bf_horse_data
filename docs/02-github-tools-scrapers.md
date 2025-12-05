# GitHub Tools & Scrapers

> Comprehensive catalog of community-built open source tools for horse racing data collection.

## Table of Contents

- [Top Recommended Tools](#top-recommended-tools)
- [Racing Post Scrapers](#racing-post-scrapers)
- [Betfair Tools](#betfair-tools)
- [Odds & Bookmaker Scrapers](#odds--bookmaker-scrapers)
- [Timeform & Form Data](#timeform--form-data)
- [Sectional Times](#sectional-times)
- [Regional Scrapers](#regional-scrapers)
- [ML & Prediction Projects](#ml--prediction-projects)
- [Utility Libraries](#utility-libraries)

---

## Top Recommended Tools

### Tier 1: Production Ready

| Tool | Stars | Purpose | Language |
|------|-------|---------|----------|
| [rpscrape](https://github.com/joenano/rpscrape) | 187⭐ | Racing Post scraper | Python 3.13+ |
| [betfairlightweight](https://github.com/betcode-org/betfair) | 484⭐ | Betfair API wrapper | Python |
| [flumine](https://github.com/betcode-org/flumine) | 213⭐ | Trading framework | Python |
| [betfair_data](https://github.com/tarb/betfair_data) | - | Fast Rust parser | Python/Rust |

### Tier 2: Specialized Use

| Tool | Purpose | Best For |
|------|---------|----------|
| [horse_racing_data_analyzer](https://github.com/adamcorren/horse_racing_data_analyzer) | Multi-source aggregation | 149 features per horse |
| [betfair-horse-racing](https://github.com/dickreuter/betfair-horse-racing) | Automated trading | Neural network strategies |
| [Attheraces-Scraper](https://github.com/AiRacing1/Attheraces-Scraper) | Sectional times | UK race analysis |
| [bfsp_scraper](https://github.com/qemtek/bfsp_scraper) | BSP data | Historical SP analysis |

---

## Racing Post Scrapers

### rpscrape (Recommended)

**Repository:** https://github.com/joenano/rpscrape

The most comprehensive and actively maintained Racing Post scraper.

**Features:**
- Historical results data
- Current racecards (JSON)
- Configurable data fields
- CSV output with gzip compression

**Requirements:**
```bash
Python 3.13+
pip install requests tomli orjson jarowinkler aiohttp lxml
```

**Data Fields Available:**
```
Race: date, course, distance, class, going, prize money
Horse: name, age, sex, weight, draw, form
Performance: position, lengths beaten, time
Ratings: RPR, Top Speed (TS), Official Rating (OR)
Connections: jockey, trainer, owner
Odds: SP, forecast
```

**Usage:**
```bash
# Clone and run
git clone https://github.com/joenano/rpscrape.git
cd rpscrape
python rpscrape.py

# Commands (in console):
gb 2023 flat              # GB flat 2023
ire 2020-2023 jumps       # Irish jumps 2020-2023
2 1999-2018 jumps         # Ascot (code 2) jumps
```

**Configuration:** `user_settings.toml`
```toml
# Toggle fields on/off
rpr = true
ts = true
or = true
trainer_rtf = true
```

---

### Horse-Racing-Data-Extraction

**Repository:** https://github.com/hyattsaleh15/Horse-Racing-Data-Extraction

**Features:**
- 6 months historical data
- Two-script approach (URL harvester + extractor)

**Data Extracted:**
- Horse demographics
- Jockey names
- Venue details
- Finishing positions
- Going conditions

---

### horse_racing_data_analyzer

**Repository:** https://github.com/adamcorren/horse_racing_data_analyzer

**Features:**
- Combines bookmaker + exchange + hourly pre-race data
- Produces **149 unique data points** per horse
- Daily CSV exports

**Data Sources:**
- Sporting Life prices
- Timeform prices
- Major bookmakers
- Betfair Exchange

**Requirements:**
- Python
- Chromedriver (matching Chrome version)

---

## Betfair Tools

### BSP Scrapers

#### bfsp_scraper

**Repository:** https://github.com/qemtek/bfsp_scraper

**Features:**
- Scrapes Betfair SP website
- S3 bucket storage
- 10+ years historical data

**Scripts:**
```python
# Latest data (yesterday)
python get_latest.py

# Historical (10 years)
python get_historical.py
```

#### betfairsp-scraper

**Repository:** https://github.com/buyAndFree/betfairsp-scraper

**Features:**
- Async downloads (multiple files)
- CLI interface
- Multi-region support

**Coverage:** UK, Ireland, Australia, USA, South Africa

---

#### Betfair-Data-Scraper

**Repository:** https://github.com/Deruzala/Betfair-Data-Scraper

**Features:**
- SQL Server integration
- Win and place markets
- UK, IRE, AUS data

---

### Historical Data Parsers

#### betfair_data (Rust-based)

**Repository:** https://github.com/tarb/betfair_data

**Features:**
- **Very fast** (Rust implementation)
- Supports official + self-recorded streams
- Drop-in replacement for betfairlightweight objects

**Supported Formats:**
- BZ2 compressed
- GZIP compressed
- TAR archives
- ZIP archives
- Uncompressed JSON

**Installation:**
```bash
pip install betfair_data
```

#### betfairhistorystreamextractor

**Repository:** https://github.com/saeh/betfairhistorystreamextractor

**Features:**
- Extract prices at specific times before start
- Tested on AU Horse Racing
- Uses betfairlightweight

---

### Website Scrapers

#### betfair-scraper

**Repository:** https://github.com/meister245/betfair-scraper

**Features:**
- Hybrid: browser simulation + API calls
- Sportsbook odds scraping

**Installation:**
```bash
pip install -U betfair-scraper
```

#### betfair.com

**Repository:** https://github.com/michalskop/betfair.com

**Features:**
- Last Price Traded data
- Tabular datapackage format
- Automated GitHub updates
- Tested on politics markets

---

### Automated Trading Systems

#### betfair-horse-racing

**Repository:** https://github.com/dickreuter/betfair-horse-racing

**Features:**
- **Fully functional automated trading system**
- Neural network analysis (Keras/TensorFlow)
- Flask web interface
- PnL tracking and statistics

**Data Collection:**
- 60 minutes before race: prices every minute
- During race: prices every 10 seconds
- Post-race: winner collection

**Architecture:**
```
├── neural_network_base.py      # Base NN implementation
├── neural_networks_nicolas.py  # Strategy implementations
├── historic_data_processor.py  # Backtesting
├── custom_optimization.py      # Optimization routines
└── backbets.py                 # Backtesting module
```

---

## Odds & Bookmaker Scrapers

### Multi-Bookmaker Tools

#### betScrapeR

**Repository:** https://github.com/dashee87/betScrapeR

**Language:** R

**Features:**
- Betfair Exchange API integration
- Web scraping from Oddschecker
- Dataframe output
- Arbitrage detection examples

**Bookmakers:** All available on Oddschecker for each race

**Requirements:**
- Betfair API app key
- R environment

---

#### Oddschecker-Scraper

**Repository:** https://github.com/ChamRoshi/Oddschecker-Scraper

**Features:**
- Simple interface
- Pandas DataFrame output
- Search function

**Usage:**
```python
from oddschecker import page_stats, search

# Get odds table
odds_dict = page_stats("https://www.oddschecker.com/...")
title = odds_dict["title"]
df = odds_dict["df"]

# Search for event
url = search("cheltenham gold cup")
```

---

#### Odds-Tracker

**Repository:** https://github.com/zxch91/Odds-Tracker

**Features:**
- Tracks odds at 2 time intervals
- Compares changes over time
- Horse racing specific

**Technology:** Selenium, Pandas, BeautifulSoup

---

#### gto76/bets

**Repository:** https://github.com/gto76/bets

**Bookmakers:**
- Betfair, Marathonbet, Favbet
- LSbet, Betsafe, William Hill
- Meridianbet, Bet1128

**Storage:** MySQL database

**Modes:**
- Test mode (print without saving)
- Save mode (store HTML pages)
- Parse stored pages

---

### Single Bookmaker Scrapers

| Bookmaker | Repository | Notes |
|-----------|------------|-------|
| Bet365 | [bet365-scraper](https://github.com/billyb2/bet365-scraper) | Live odds, Selenium |
| Bet365 | [PyBet365](https://github.com/F4doraOfDoom/PyBet365) | Proxy support |
| Paddy Power | [PaddyPowerScraper](https://github.com/paulc160/PaddyPowerScraper) | Jupyter notebook |
| Unibet | [unibet](https://github.com/BowTiedBettor/unibet) | Odds plotting |
| William Hill | [sports-scraping](https://github.com/andrrew-c/sports-scraping) | Live scores/odds |

---

### Arbitrage Tools

#### each-way-matcher

**Repository:** https://github.com/tom-pollak/each-way-matcher

**Features:**
- **Horse racing specific**
- Scrapes OddsMonkey
- Auto-places bets on Sporting Index
- Lays on Betfair

#### Bet-arbitrage-finder

**Repository:** https://github.com/mgirkins/Bet-arbitrage-finder

**Features:**
- Scrapes Oddschecker
- Finds arbitrage opportunities

**Formula:** `1/Odds_A + 1/Odds_B < 1`

---

## Timeform & Form Data

### starform

**Repository:** https://github.com/hullboy73/starform

**Features:**
- Lifetime performance summaries
- Recent 10 runs for tomorrow's runners
- Historical results
- Tomorrow's racecards

**Note:** Timeform recently updated website, breaking some functionality. Links and results work, but cards/form may not.

---

### tfraces

**Repository:** https://github.com/ms5/tfraces

**Features:**
- Scrapy framework
- Basic results data
- Timeform as source

---

## Sectional Times

### Attheraces-Scraper

**Repository:** https://github.com/AiRacing1/Attheraces-Scraper

**Features:**
- **All 59 UK racecourses** (since July 2024)
- Sectional/split times
- Selenium WebDriver

**Data Available:**
- Sectional times through race
- Optimum figures (Simon Rowlands)
- ~48 hours post-race publication

**Courses Include:**
- Cheltenham, Epsom, Newmarket
- Goodwood, York, Ascot
- All UK courses via ARC/TPD/RMG collaboration

---

## Regional Scrapers

### Hong Kong

| Repository | Description |
|------------|-------------|
| [HK-Horse-Racing-Data-Scraper](https://github.com/j-csc/HK-Horse-Racing-Data-Scraper) | HKJC scheduled scraper |
| [ML-horseracing](https://github.com/1alex2lee/ML-horseracing) | 7 years, 12K data points |
| [AI_horse_prediction](https://github.com/StevenHo1394/AI_horse_prediction) | Pre-trained models included |

**HK-Horse-Racing-Data-Scraper** extracts:
- Horse veterinary records
- Penetrometer readings
- Horse info and roarers
- Racecards

---

### Australia

| Repository | Description |
|------------|-------------|
| [horse_racing_web_scraper](https://github.com/dan-abu/horse_racing_web_scraper) | Playwright, async |
| [bfscraper](https://github.com/apapadimitriou/bfscraper) | AU BSP/WAP |

---

### US / Equibase

| Repository | Description |
|------------|-------------|
| [horse_racing_data_scraper](https://github.com/natewillis/horse_racing_data_scraper) | PDF chart parser |
| [equibase-python](https://github.com/mainaanthony/equibase-python) | Selenium scraper |
| [handycapper](https://github.com/ccmd00d/handycapper) | REST API + SDK |

---

## ML & Prediction Projects

### With Data Pipelines

| Repository | Data Source | ML Model |
|------------|-------------|----------|
| [betfair-horse-racing](https://github.com/dickreuter/betfair-horse-racing) | Betfair API | Neural Network |
| [HorseRacePrediction](https://github.com/ethan-eplee/HorseRacePrediction) | Kaggle | Classification/Regression |
| [HorseRacingPrediction](https://github.com/dominicplouffe/HorseRacingPrediction) | Custom (5 years) | SVR |
| [AI_horse_prediction](https://github.com/StevenHo1394/AI_horse_prediction) | HKJC | 3-layer NN |

### With Included Datasets

| Repository | Dataset | Format |
|------------|---------|--------|
| [AI_horse_prediction](https://github.com/StevenHo1394/AI_horse_prediction) | HK Jockey Club | CSV + models |
| [Horse-Racing](https://github.com/constancedongg/Horse-Racing) | race-result-horse.csv | CSV |
| [HorseRacingAnalysis](https://github.com/jimxx1995/HorseRacingAnalysis) | HK 2014-16 | CSV |

---

## Utility Libraries

### racing_data

**Repository:** https://github.com/predictive-punter/racing_data

**Features:**
- Python class library
- Object-oriented (Runners, Horses, Jockeys, Trainers)
- Provider-based architecture

**PyPI:** `pip install racing-data`

---

### horse-racing-datasets

**Repository:** https://github.com/superterrific/horse-racing-datasets

**Features:**
- Curated directory
- Airtable + Eleventy
- Website: https://horseracingdatasets.com/

---

### AwesomeBetfair

**Repository:** https://github.com/betfair-down-under/AwesomeBetfair

**Features:**
- **Curated list of all Betfair tools**
- Links to scrapers, parsers, tutorials
- Best starting point for discovery

---

## Tool Selection Guide

### By Use Case

| Use Case | Recommended Tool |
|----------|------------------|
| Racing Post data | rpscrape |
| Betfair BSP | bfsp_scraper |
| Live trading | betfairlightweight + flumine |
| Historical analysis | betfair_data |
| Sectional times | Attheraces-Scraper |
| Multi-bookmaker odds | betScrapeR / Oddschecker-Scraper |
| HK data | HK-Horse-Racing-Data-Scraper |
| US data | handycapper |
| ML pipeline | horse_racing_data_analyzer |

### By Skill Level

| Level | Tools |
|-------|-------|
| Beginner | rpscrape, bfsp_scraper |
| Intermediate | betfairlightweight, Oddschecker-Scraper |
| Advanced | flumine, betfair-horse-racing |

---

## Next Steps

- [Python Libraries](03-python-libraries.md) - Detailed library guides
- [Datasets](04-datasets.md) - Ready-to-use data
- [Legal Considerations](06-legal-considerations.md) - Compliance guidelines
