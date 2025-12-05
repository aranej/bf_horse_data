# Datasets & Downloads

> Comprehensive guide to ready-to-use horse racing datasets for analysis and machine learning.

## Table of Contents

- [Free Official Data](#free-official-data)
- [Kaggle Datasets](#kaggle-datasets)
- [GitHub Datasets](#github-datasets)
- [Community Data Sources](#community-data-sources)
- [Academic Datasets](#academic-datasets)
- [Dataset Comparison](#dataset-comparison)
- [Data Field Reference](#data-field-reference)
- [Download Scripts & Tools](#download-scripts--tools)

---

## Free Official Data

### Betfair Starting Price (BSP) Data ⭐ HIGHLY RECOMMENDED

**URL:** https://promo.betfair.com/betfairsp/prices

The most accessible free dataset for horse racing analysis. Daily CSV files with comprehensive pricing data.

| Region | Coverage | Format | URL Pattern |
|--------|----------|--------|-------------|
| Great Britain | Daily | CSV | `dwbfpricesuk{DDMMYYYY}.csv` |
| Ireland | Daily | CSV | `dwbfpricesire{DDMMYYYY}.csv` |
| Australia | Daily | CSV | `dwbfpricesaus{DDMMYYYY}.csv` |
| USA | Daily | CSV | `dwbfpricesusa{DDMMYYYY}.csv` |
| South Africa | Daily | CSV | `dwbfpricessa{DDMMYYYY}.csv` |

**Historical Archive:** https://promo.betfair.com/betfairsp/SP_history.html

**Fields Available:**
```
EVENT_ID          - Unique event identifier
MENU_HINT         - Course name and time
EVENT_NAME        - Race name
EVENT_DT          - Event date/time
SELECTION_ID      - Runner identifier
SELECTION_NAME    - Horse name
WIN_LOSE          - Result (1=Won, 0=Lost)
BSP               - Betfair Starting Price
PPWAP             - Pre-play Weighted Average Price
MORNINGWAP        - Morning WAP
PPMAX/PPMIN       - Pre-play price range
IPMAX/IPMIN       - In-play price range
PPTRADEDVOL       - Pre-play traded volume
IPTRADEDVOL       - In-play traded volume
```

**Download Examples:**
```bash
# Yesterday's UK data
curl -O "https://promo.betfair.com/betfairsp/prices/dwbfpricesuk$(date -d 'yesterday' +%d%m%Y).csv"

# Specific date
curl -O https://promo.betfair.com/betfairsp/prices/dwbfpricesuk05122024.csv

# Historical archive (annual ZIP)
wget https://promo.betfair.com/betfairsp/prices/dwbfprices_gb_2023.zip
```

---

### Betfair Historical Data Service

**URL:** https://historicdata.betfair.com

| Tier | Interval | Volume Data | Price |
|------|----------|-------------|-------|
| **BASIC** | 1 minute | No | **Free** |
| ADVANCED | 1 second | Yes | Paid |
| PRO | 50 milliseconds | Yes | Paid |

**Coverage:**
- All Betfair Exchange markets since April 2015
- Australian/NZ data from October 2016
- Updates 5 days after event settlement

**Format:** TAR archives containing BZ2-compressed JSON (same as Stream API format)

**Access:** Requires verified Betfair account login

---

### Betfair Australia CSV Files ⭐ RECOMMENDED

**URL:** https://betfair-datascientists.github.io/data/dataListing/

**Cost:** FREE

**Contents:**
- Market snapshots at various timepoints
- Max/min matched prices
- Volume data (pre-play and in-play)
- Weighted average prices
- BSP values
- Winner information

**Coverage:** Australian and overseas races from Exchange inception

**Maintained by:** Betfair Data Scientists team (official)

---

### RacingFormBook.com ⭐ EXCELLENT VALUE

**URL:** https://www.racingformbook.com

**Cost:** £9/month (with FREE sample files available)

| Product | Format | Update Frequency |
|---------|--------|------------------|
| Daily Racecard CSV | CSV | Daily |
| Weekly Results CSV (Duo) | CSV | Weekly |
| Single File Format (SFF) Results | CSV | Weekly |
| Access Database | MDB | Since 2016 |

**Free Items:**
- Sample racecard data
- RaceHorseFormBuilder App (FREE)

**Fields in Results CSV:**
```
Race ID, Date, Course, Race Name
Horse name, Age, Weight, Draw
Trainer, Jockey, Owner
Starting Price (SP), Position
Lengths Beaten, Winning Time
Going, Distance, Class
```

**Download Sample:** https://www.racingformbook.com/basic-racing-results-csv-format/

---

## Kaggle Datasets

### UK/Ireland Racing ⭐ NEW

#### Horse Racing Results - UK/Ireland 2015-2025

**URL:** https://www.kaggle.com/datasets/deltaromeo/horse-racing-results-ukireland-2015-2025

**Format:** SQLite3 database + CSV files

**Coverage:** 10 years of UK & Ireland racing

**Updates:** Frequently updated (last: October 2025)

**Size:** ~20 upvotes, actively maintained

**Best For:** Comprehensive UK/IRE historical analysis

---

#### GB&IRE Horse Racing Form 2016-2024

**URL:** https://www.kaggle.com/datasets/billy8399/horses-for-courses

**Coverage:** 8+ years of form data

**Size:** 8 MB

**Format:** CSV

---

### Hong Kong Racing

#### Hong Kong Horse Racing 2014-17 ⭐ MOST POPULAR

**URL:** https://www.kaggle.com/datasets/lantanacamara/hong-kong-horse-racing

**Size:** 1,561 races

**Downloads:** 9,122+

**Notebooks:** 28 community notebooks using this data

**Files:**
- `race-result-horse.csv` - Horse-level results
- `race-result-race.csv` - Race-level information

**Why Popular:** Well-structured, clean data, widely referenced in ML projects

---

#### Horse Racing in HK

**URL:** https://www.kaggle.com/datasets/gdaley/hkracing

**Rating:** 7.6/10 usability

**Size:** 4 MB (2 CSV files)

**Best For:** Beginners starting with ML horse racing models

---

#### Horse Racing Dataset for Experts (Hong Kong)

**URL:** https://www.kaggle.com/datasets/hrosebaby/horse-racing-dataset-for-experts-hong-kong

**Contents (5 datasets):**
1. Barrier trials data
2. Horse information
3. Race results
4. Trackwork data
5. Comments about each horse

**Best For:** Advanced HK racing analysis

---

### Betfair-Specific Datasets

#### Betfair SP Collection

**URL:** https://www.kaggle.com/datasets/eonsky/betfair-sp

**Contents:**
- Current BSP files (auto-updated)
- Greyhound data (UK, Ireland, Australia)
- Horse Racing (USA, Ireland, UK, RSA, NZ, Australia)

**Best For:** Quick access to BSP without direct Betfair download

---

#### One Week of Betfair Data: Horses

**URL:** https://www.kaggle.com/datasets/zygmunt/betfair-horses

**Format:** BZ2 compressed JSON

**Contents:** Detailed tick-by-tick price history for one week

**Best For:** Understanding Betfair odds movement patterns

---

### Historical/Long-term Datasets

#### Horse Racing (1990-2020)

**URL:** https://www.kaggle.com/datasets/hwaitt/horse-racing

**Coverage:** 30 years of racing data

**Format:** Annual CSV files (Races + Horses per year)

**Best For:** Long-term trend analysis, historical research

---

#### Horse Racing

**URL:** https://www.kaggle.com/datasets/ahmedabdulhamid/horse-racing

**Focus:** Race conditions, course details, performance indicators

**Includes:** Trainer and jockey statistics

---

### Specialized Datasets

#### Horse Racing - Tipster Bets

**URL:** https://www.kaggle.com/datasets/gunner38/horseracing

**Size:** 39,000 bets from 31 tipsters

**Best For:** Analyzing tipster performance, betting patterns

---

#### Horse Racing - Big Data Derby

**URL:** https://www.kaggle.com/datasets/jpmiller/race-data

**Focus:** Equine health and performance metrics

**Unique:** Contains biometric/health data

**Source:** 2022 Big Data Derby competition

---

#### Horse Racing Dataset (thegodeye)

**URL:** https://www.kaggle.com/datasets/thegodeye/horse-racing-dataset/data

**Coverage:** Wide range of racing events

**Includes:** Results, odds, rankings

---

## GitHub Datasets

### Pre-packaged Datasets with Data

| Repository | Data Included | Format | Stars |
|------------|---------------|--------|-------|
| [AI_horse_prediction](https://github.com/StevenHo1394/AI_horse_prediction) | HK Jockey Club + pre-trained models | CSV | Active |
| [mvp-horse-racing-prediction](https://github.com/codeworks-data/mvp-horse-racing-prediction) | HK Racing ML ready | Jupyter | 62⭐ |
| [HorseRacingAnalysis](https://github.com/jimxx1995/HorseRacingAnalysis) | HK 2014-16, 1,561 races | CSV | - |
| [penguinnnnn/HKJCData](https://github.com/penguinnnnn/HKJCData) | HKJC crawled + analysis | CSV | - |

### AI_horse_prediction ⭐ INCLUDES MODELS

**Repository:** https://github.com/StevenHo1394/AI_horse_prediction

**Unique Features:**
- Pre-trained 50,000 epoch neural network models
- Ready-to-use CSV files
- Updated for 2021-2022 season

**File Naming:** `horse_data_yyyymmdd_racex.csv`

---

### Data Aggregation Tools

#### horse_racing_data_analyzer

**Repository:** https://github.com/adamcorren/horse_racing_data_analyzer

**Output:** Daily CSV files with 149 unique data points per horse

**Sources Combined:**
- Sporting Life prices
- Timeform prices
- Major bookmaker odds
- Betfair Exchange data

**Requirements:** Python + Chromedriver

---

### Hong Kong Scrapers with Data

#### HongKong-Horse-Racing-Results-Scraper

**Repository:** https://github.com/harrymings/HongKong-Horse-Racing-Results-Scraper

**Features:**
- Scrapes HKJC website
- User-specified date range
- CSV output per race

**Stars:** 5⭐ (recently created 2025)

---

#### sport-betting-data (HKJC)

**Repository:** https://github.com/rkwyu/sport-betting-data

**Coverage:** Horse Racing + Football from HKJC

**Features:**
- Horse racing odds
- Football betting data
- Regular updates

**Stars:** 6⭐

---

## Community Data Sources

### Bet Angel Forum Resources

**Forum:** https://forum.betangel.com

#### Key Threads for Data:

| Thread | Topic | URL |
|--------|-------|-----|
| Historical Data Discussion | General data sources | [Link](https://forum.betangel.com/viewtopic.php?t=3936) |
| Free Betfair Exchange Data | Free ADVANCED tier offer | [Link](https://forum.betangel.com/viewtopic.php?t=20776) |
| Power Query BF Downloader | Excel tool for bulk download | [Link](https://forum.betangel.com/viewtopic.php?t=28303) |
| Racecards CSV Download | Web Content Extractor method | [Link](https://forum.betangel.com/viewtopic.php?t=7257) |

**Community Templates:** Forum members share Excel/VBA templates for data processing

---

### UK Betting Forum

**URL:** https://www.theukbettingforum.co.uk

#### Scraping Section

**URL:** https://www.theukbettingforum.co.uk/XenForo/forums/scraping.80/

**Topics Covered:**
- Racing Post scraping methods
- RPR/Top Speed extraction
- Python scripts for data collection

**Notable Thread:** [Scraper for Top Speed and RPR](https://www.theukbettingforum.co.uk/XenForo/threads/scraper-method-to-obtain-top-speed-and-rpr-from-racing-post-website-into-excel.91586/)

---

### Punters Lounge Forum

**URL:** https://forum.punterslounge.com

**Database Comparison Thread:** [Which Database? Raceform/Dataform/Proform or Horse Race Base?](https://forum.punterslounge.com/topic/127184-which-database-raceformdataformproform-or-horse-race-base/)

---

### Horse Racing Datasets Directory ⭐ CURATED LIST

**Website:** https://horseracingdatasets.com/

**GitHub:** https://github.com/superterrific/horse-racing-datasets

**Features:**
- Curated directory of publicly available datasets
- Built with Airtable and Eleventy
- Regularly updated
- Filterable by region, type, format

---

## Academic Datasets

### Equibase Research Dataset ⭐ US RACING

**URL:** https://www.equibase.com/handicappersdata.cfm

**Announced:** March 2024

**Cost:** FREE for research/development

**Coverage:** Complete 2023 calendar year (US racing)

**Contents:**
- Complete past performance data
- Corresponding results charts
- Supporting documentation

**Use Cases:**
- Academic research
- Product testing
- Handicapping theory development

**Restrictions:** Research/non-commercial use only

---

### University Research Papers with Data

| Source | Coverage | Data Size | Link |
|--------|----------|-----------|------|
| Stanford CS230 | Hong Kong | ~200 races | [PDF](http://cs230.stanford.edu/projects_winter_2021/reports/70738477.pdf) |
| UC Berkeley | Kaggle data | Variable | [Link](https://saas.studentorg.berkeley.edu/rp/predicting-horse-races) |
| University of Louisville | Graph-based features | Variable | [PDF](https://ir.library.louisville.edu/cgi/viewcontent.cgi?article=4083&context=etd) |

---

## Dataset Comparison

### By Quality Tier

#### Tier 1: Production Ready (Best Quality)

| Dataset | Source | Size | Best For | Cost |
|---------|--------|------|----------|------|
| Betfair BSP | Official | 10+ years | Backtesting, BSP analysis | FREE |
| Betfair Historical BASIC | Official | Since 2015 | Tick data analysis | FREE |
| Kaggle UK/IRE 2015-2025 | Community | 10 years | UK/IRE ML | FREE |
| Equibase Research | Official | Full 2023 | US racing research | FREE |

#### Tier 2: High Quality

| Dataset | Source | Size | Best For | Cost |
|---------|--------|------|----------|------|
| Kaggle HK 2014-17 | Community | 1,561 races | ML training | FREE |
| RacingFormBook | Commercial | 2016-2025 | UK/IRE results | £9/mo |
| AI_horse_prediction | GitHub | Ongoing | Pre-trained models | FREE |
| Betfair AU CSV | Official | All-time | Australian racing | FREE |

#### Tier 3: Specialized

| Dataset | Source | Size | Best For | Cost |
|---------|--------|------|----------|------|
| HK Expert Dataset | Kaggle | 5 files | Comprehensive HK | FREE |
| Tipster Bets | Kaggle | 39,000 bets | Betting analysis | FREE |
| Big Data Derby | Kaggle | Variable | Health metrics | FREE |
| Horse Racing 1990+ | Kaggle | 30 years | Historical trends | FREE |

---

### By Region

| Region | Best Free Dataset | Alternative | Paid Option |
|--------|-------------------|-------------|-------------|
| **UK** | Betfair BSP | Kaggle UK/IRE 2015-2025 | RacingFormBook |
| **Ireland** | Betfair BSP | Kaggle UK/IRE 2015-2025 | RacingFormBook |
| **Hong Kong** | Kaggle HK 2014-17 | HK Expert Dataset | - |
| **Australia** | Betfair AU CSV | Betfair BSP | - |
| **USA** | Equibase Research | Betfair BSP | Equibase Full |

---

### By Use Case

| Use Case | Recommended Dataset | Why |
|----------|---------------------|-----|
| **ML Model Training** | Kaggle HK 2014-17 | Clean, well-structured, many examples |
| **Backtesting Strategies** | Betfair BSP History | 10+ years, daily granularity |
| **Tick Data Analysis** | Betfair Historical BASIC | 1-min intervals, official data |
| **UK Results Analysis** | RacingFormBook | Comprehensive fields, regular updates |
| **Academic Research** | Equibase Research | Official, documented, free |
| **Pre-trained Models** | AI_horse_prediction | Includes trained NN models |
| **Quick Prototyping** | Kaggle UK/IRE 2015-2025 | Ready SQLite + CSV |

---

## Data Field Reference

### Standard Race Fields

```
Race Information:
├── race_id          - Unique identifier
├── date             - Race date (YYYY-MM-DD)
├── time             - Off time (HH:MM)
├── course           - Racecourse name
├── distance         - Distance in furlongs/meters
├── class            - Race class (1-7)
├── type             - Flat/NH/AW, Handicap/Maiden/Conditions
├── going            - Track condition (Good, Soft, Heavy, etc.)
├── prize            - Prize money
├── runners          - Number of declared runners
└── non_runners      - Withdrawn horses

Horse Information:
├── horse_name       - Horse name (with country suffix)
├── horse_id         - Unique horse ID
├── age              - Age in years
├── sex              - C (colt), F (filly), G (gelding), M (mare), H (horse)
├── weight           - Weight carried (lbs or kg)
├── draw             - Starting stall number
├── trainer          - Trainer name
├── jockey           - Jockey name
├── owner            - Owner name
├── form             - Recent form string (e.g., "12-341")
├── days_since_run   - Days since last race
└── headgear         - Equipment (blinkers, visor, etc.)

Performance:
├── position         - Finishing position (1, 2, 3..., PU, F, UR)
├── lengths_beaten   - Distance behind winner
├── time             - Finish time (seconds)
├── sp               - Starting Price (decimal)
├── bsp              - Betfair Starting Price
└── comment          - In-running comment

Ratings (where available):
├── rpr              - Racing Post Rating
├── ts               - Top Speed (Timeform)
├── or               - Official Rating (BHA handicap)
├── tf_rating        - Timeform rating
└── speed_figure     - Speed rating
```

### Betfair-Specific Fields

```
Market Data:
├── event_id         - Betfair event ID
├── market_id        - Market identifier (e.g., 1.234567890)
├── selection_id     - Runner selection ID
├── win_lose         - Result flag (1/0)
├── bsp              - Betfair Starting Price
├── ppwap            - Pre-play weighted average price
├── morningwap       - Morning WAP (early price)
├── ppmax            - Pre-play maximum price traded
├── ppmin            - Pre-play minimum price traded
├── ipmax            - In-play maximum price
├── ipmin            - In-play minimum price
├── pptradedvol      - Pre-play traded volume (£)
└── iptradedvol      - In-play traded volume (£)

Tick Data (Historical files):
├── publish_time     - Timestamp (ms precision)
├── last_price       - Last traded price
├── total_matched    - Total matched volume
├── back_prices[]    - Array of back prices/sizes
├── lay_prices[]     - Array of lay prices/sizes
├── status           - ACTIVE, SUSPENDED, REMOVED
└── reduction_factor - Rule 4 deduction (if applicable)
```

---

## Download Scripts & Tools

### Python: Bulk BSP Download

```python
import requests
import pandas as pd
from datetime import datetime, timedelta
from pathlib import Path
from concurrent.futures import ThreadPoolExecutor

def download_bsp_data(date: datetime, region: str = "uk") -> pd.DataFrame:
    """Download BSP data for a single date."""
    date_str = date.strftime("%d%m%Y")
    url = f"https://promo.betfair.com/betfairsp/prices/dwbfprices{region}{date_str}.csv"
    
    try:
        df = pd.read_csv(url)
        df['download_date'] = date.strftime("%Y-%m-%d")
        return df
    except Exception as e:
        print(f"✗ {date.strftime('%Y-%m-%d')}: {e}")
        return pd.DataFrame()

def download_bsp_range(
    start_date: str,
    end_date: str,
    region: str = "uk",
    output_dir: str = "./data/bsp",
    parallel: bool = True
):
    """
    Download BSP data for date range.
    
    Args:
        start_date: Start date (YYYY-MM-DD)
        end_date: End date (YYYY-MM-DD)
        region: uk, ire, aus, usa, sa
        output_dir: Output directory
        parallel: Use parallel downloads
    """
    Path(output_dir).mkdir(parents=True, exist_ok=True)
    
    start = datetime.strptime(start_date, "%Y-%m-%d")
    end = datetime.strptime(end_date, "%Y-%m-%d")
    dates = [start + timedelta(days=x) for x in range((end - start).days + 1)]
    
    if parallel:
        with ThreadPoolExecutor(max_workers=5) as executor:
            results = list(executor.map(
                lambda d: download_bsp_data(d, region), 
                dates
            ))
    else:
        results = [download_bsp_data(d, region) for d in dates]
    
    # Combine non-empty results
    valid_dfs = [df for df in results if not df.empty]
    
    if valid_dfs:
        combined = pd.concat(valid_dfs, ignore_index=True)
        output_file = f"{output_dir}/bsp_{region}_{start_date}_{end_date}.csv"
        combined.to_csv(output_file, index=False)
        print(f"\n✓ Saved: {output_file}")
        print(f"  Total records: {len(combined):,}")
        print(f"  Date range: {combined['download_date'].min()} to {combined['download_date'].max()}")
        return combined
    
    return pd.DataFrame()

# Usage
if __name__ == "__main__":
    df = download_bsp_range("2024-01-01", "2024-01-31", region="uk")
```

### Bash: Download Kaggle Datasets

```bash
#!/bin/bash
# Requires: pip install kaggle
# Configure: ~/.kaggle/kaggle.json with your API credentials

DATA_DIR="./data"
mkdir -p "$DATA_DIR"

echo "=== Downloading Kaggle Horse Racing Datasets ==="

# Hong Kong Racing (Most Popular)
echo "Downloading Hong Kong 2014-17..."
kaggle datasets download -d lantanacamara/hong-kong-horse-racing -p "$DATA_DIR/hk_racing"
unzip -o "$DATA_DIR/hk_racing/hong-kong-horse-racing.zip" -d "$DATA_DIR/hk_racing"

# UK/Ireland 2015-2025
echo "Downloading UK/Ireland 2015-2025..."
kaggle datasets download -d deltaromeo/horse-racing-results-ukireland-2015-2025 -p "$DATA_DIR/uk_ire"
unzip -o "$DATA_DIR/uk_ire/horse-racing-results-ukireland-2015-2025.zip" -d "$DATA_DIR/uk_ire"

# Horse Racing 1990+
echo "Downloading Historical 1990+..."
kaggle datasets download -d hwaitt/horse-racing -p "$DATA_DIR/historical"
unzip -o "$DATA_DIR/historical/horse-racing.zip" -d "$DATA_DIR/historical"

# HK Expert Dataset
echo "Downloading HK Expert Dataset..."
kaggle datasets download -d hrosebaby/horse-racing-dataset-for-experts-hong-kong -p "$DATA_DIR/hk_expert"
unzip -o "$DATA_DIR/hk_expert/horse-racing-dataset-for-experts-hong-kong.zip" -d "$DATA_DIR/hk_expert"

# Betfair SP
echo "Downloading Betfair SP collection..."
kaggle datasets download -d eonsky/betfair-sp -p "$DATA_DIR/betfair_sp"
unzip -o "$DATA_DIR/betfair_sp/betfair-sp.zip" -d "$DATA_DIR/betfair_sp"

echo "=== Download Complete ==="
ls -la "$DATA_DIR"
```

### Python: rpscrape Historical Data

```python
#!/usr/bin/env python3
"""
Download historical Racing Post data using rpscrape.
Requires: git clone https://github.com/joenano/rpscrape.git
"""
import subprocess
import os
from pathlib import Path

def scrape_historical(
    region: str = "gb",
    year_start: int = 2020,
    year_end: int = 2024,
    race_type: str = "flat",
    output_dir: str = "./data/rpscrape"
):
    """
    Run rpscrape to download historical data.
    
    Args:
        region: gb, ire, fr, usa, aus
        year_start: Start year
        year_end: End year  
        race_type: flat or jumps
        output_dir: Output directory
    """
    rpscrape_path = Path("./rpscrape")  # Adjust path as needed
    
    if not rpscrape_path.exists():
        print("Installing rpscrape...")
        subprocess.run(["git", "clone", "https://github.com/joenano/rpscrape.git"])
        subprocess.run(["pip", "install", "-r", "rpscrape/requirements.txt"])
    
    os.makedirs(output_dir, exist_ok=True)
    
    # Run rpscrape
    cmd = [
        "python3", str(rpscrape_path / "rpscrape.py"),
        "-r", region,
        "-y", f"{year_start}-{year_end}",
        "-t", race_type
    ]
    
    print(f"Running: {' '.join(cmd)}")
    subprocess.run(cmd, cwd=str(rpscrape_path))
    
    print(f"\nData saved to: {rpscrape_path / 'data'}")

if __name__ == "__main__":
    scrape_historical(region="gb", year_start=2020, year_end=2024, race_type="flat")
```

---

## Data Quality Notes

### Known Issues

1. **Non-runners:** Historical BSP data may not account for Rule 4 deductions
2. **Missing data:** Some fields may be null for older races (especially ratings)
3. **Format changes:** Betfair CSV format has evolved over time
4. **Timezone:** Betfair data uses UK timezone (GMT/BST)
5. **Name variations:** Horse names may include country suffix (IRE, USA, FR)

### Data Validation Checklist

```python
def validate_racing_data(df):
    """Basic validation checks for racing data."""
    issues = []
    
    # Check for required fields
    required = ['date', 'horse_name', 'position']
    missing = [f for f in required if f not in df.columns]
    if missing:
        issues.append(f"Missing columns: {missing}")
    
    # Check for nulls in critical fields
    null_counts = df[required].isnull().sum()
    if null_counts.any():
        issues.append(f"Null values: {null_counts.to_dict()}")
    
    # Check position validity
    valid_positions = ['1','2','3','4','5','6','7','8','9','10','11','12','13',
                       '14','15','16','17','18','19','20','PU','F','UR','BD','RO']
    if 'position' in df.columns:
        invalid = df[~df['position'].astype(str).isin(valid_positions)]
        if len(invalid) > 0:
            issues.append(f"Invalid positions: {len(invalid)} rows")
    
    # Check SP validity (should be > 1.0)
    if 'sp' in df.columns:
        invalid_sp = df[(df['sp'] <= 1.0) & (df['sp'].notna())]
        if len(invalid_sp) > 0:
            issues.append(f"Invalid SP values: {len(invalid_sp)} rows")
    
    return issues

# Usage
issues = validate_racing_data(df)
if issues:
    print("Data quality issues found:")
    for issue in issues:
        print(f"  - {issue}")
else:
    print("✓ Data validation passed")
```

### Best Practices

1. **Validate data** before use - check for nulls, outliers, impossible values
2. **Handle non-runners** appropriately (exclude or mark separately)
3. **Normalize prices** when comparing across time periods (account for inflation)
4. **Document versions** of datasets used in research
5. **Backup raw data** before any transformations
6. **Use consistent naming** for horses (handle country suffixes)

---

## Next Steps

- [GitHub Tools & Scrapers](02-github-tools-scrapers.md) - Generate custom datasets
- [Python Libraries](03-python-libraries.md) - Process and analyze data
- [Community Resources](05-community-resources.md) - Get help from the community
- [Legal Considerations](06-legal-considerations.md) - Understand terms of service

---

**Last Updated:** December 2024
**Contributions:** Pull requests welcome for new datasets and corrections
