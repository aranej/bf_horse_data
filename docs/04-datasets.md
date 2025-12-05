# Datasets & Downloads

> Ready-to-use horse racing datasets for analysis and machine learning.

## Table of Contents

- [Free Official Data](#free-official-data)
- [Kaggle Datasets](#kaggle-datasets)
- [GitHub Datasets](#github-datasets)
- [Academic Datasets](#academic-datasets)
- [Dataset Comparison](#dataset-comparison)
- [Data Field Reference](#data-field-reference)

---

## Free Official Data

### Betfair Starting Price (BSP) Data

**URL:** https://promo.betfair.com/betfairsp/prices

| Region | Coverage | Format |
|--------|----------|--------|
| Great Britain | Daily | CSV |
| Ireland | Daily | CSV |
| Australia | Daily | CSV |
| USA | Daily | CSV |
| South Africa | Daily | CSV |

**Historical Archive:** https://promo.betfair.com/betfairsp/SP_history.html

**Fields:**
```
EVENT_ID, MENU_HINT, EVENT_NAME, EVENT_DT
SELECTION_ID, SELECTION_NAME, WIN_LOSE
BSP, PPWAP, MORNINGWAP
PPMAX, PPMIN, IPMAX, IPMIN
PPTRADEDVOL, IPTRADEDVOL
```

**Download Example:**
```bash
# Today's UK data
curl -O https://promo.betfair.com/betfairsp/prices/dwbfpricesuk$(date +%d%m%Y -d "yesterday").csv

# Historical archive
wget https://promo.betfair.com/betfairsp/prices/dwbfprices_gb_2023.zip
```

---

### Betfair Historical Data (BASIC Tier)

**URL:** https://historicdata.betfair.com

**Cost:** Free (BASIC tier)

**Coverage:**
- All Betfair Exchange markets since April 2015
- 1-minute interval data
- No volume data in BASIC tier

**Format:** TAR archives containing BZ2-compressed JSON

**Access:** Requires Betfair account login

---

### Betfair Australia CSV Files

**URL:** https://betfair-datascientists.github.io/data/dataListing/

**Cost:** Free

**Contents:**
- Market snapshots
- Max/min matched prices
- Volume (pre-play and in-play)
- Weighted average price
- BSP
- Winner information

**Coverage:** Australian and overseas races from beginning of Exchange

---

### RacingFormBook.com

**URL:** https://www.racingformbook.com/basic-racing-results-csv-format/

**Cost:** Free (requires registration)

**Coverage:** UK and Ireland

**Format:**
- Daily CSV files
- Bi-weekly downloads
- Access Database (2016-2025)

**Fields:**
```
Race ID, Date, Course
Horse name, Age
Starting Price (SP), Position
Trainer, Jockey
```

---

## Kaggle Datasets

### Hong Kong Horse Racing (Recommended)

#### Hong Kong Horse Racing 2014-17

**URL:** https://www.kaggle.com/datasets/lantanacamara/hong-kong-horse-racing

**Size:** 1,561 races

**Coverage:** Hong Kong seasons 2014-2017

**Files:**
- `race-result-horse.csv` - Horse-level results
- `race-result-race.csv` - Race-level information

**Most Used:** Referenced in multiple GitHub ML projects

---

#### Horse Racing in HK

**URL:** https://www.kaggle.com/datasets/gdaley/hkracing

**Purpose:** Thoroughbred racing ML projects

**Source:** Hong Kong Jockey Club website

**Quality:** Well-documented, good for beginners

---

#### Horse Racing Dataset for Experts (Hong Kong)

**URL:** https://www.kaggle.com/datasets/hrosebaby/horse-racing-dataset-for-experts-hong-kong

**Contents (5 datasets):**
1. Barrier trials data
2. Horse info
3. Race results
4. Trackwork
5. Comments about each horse

---

### UK/International Racing

#### Horse Racing (1990+)

**URL:** https://www.kaggle.com/datasets/hwaitt/horse-racing

**Coverage:** Data from 1990 onwards

**Quality:** Excellent for long-term historical analysis

---

#### Horse Racing Results 2017-2020

**URL:** https://www.kaggle.com/datasets/bogdandoicin/horse-racing-results-2017-2020

**Coverage:** 2017-2020 multi-region

---

#### One Week of Betfair Data: Horses

**URL:** https://www.kaggle.com/datasets/zygmunt/betfair-horses

**Published:** August 2017

**Format:** BZ2 compressed files

**Contents:** Detailed price history (odds) for one week

**Best For:** Understanding Betfair odds movement

---

### Other Racing Datasets

#### Horse Racing - Tipster Bets

**URL:** https://www.kaggle.com/datasets/gunner38/horseracing

**Size:** 39,000 bets from 31 tipsters

**Best For:** Analyzing betting patterns

---

#### Horse Racing - Big Data Derby

**URL:** https://www.kaggle.com/datasets/jpmiller/race-data

**Focus:** Equine health and performance metrics

**Unique:** Contains biometric/health data

---

## GitHub Datasets

### Pre-packaged Datasets

| Repository | Data Included | Format |
|------------|---------------|--------|
| [AI_horse_prediction](https://github.com/StevenHo1394/AI_horse_prediction) | HK Jockey Club + pre-trained models | CSV |
| [Horse-Racing](https://github.com/constancedongg/Horse-Racing) | race-result-horse.csv | CSV |
| [HorseRacingAnalysis](https://github.com/jimxx1995/HorseRacingAnalysis) | HK 2014-16, 1,561 races | CSV |

### AI_horse_prediction Dataset

**Repository:** https://github.com/StevenHo1394/AI_horse_prediction

**Unique Features:**
- Pre-trained 50,000 epoch neural network models
- Ready-to-use CSV files
- Updated for 2021-2022 season

**File Naming:** `horse_data_yyyymmdd_racex.csv`

---

### Data Aggregation Sites

#### Horse Racing Datasets

**URL:** https://horseracingdatasets.com/

**GitHub:** https://github.com/superterrific/horse-racing-datasets

**Features:**
- Curated directory of publicly shared datasets
- Built with Airtable and Eleventy
- Regularly updated

---

## Academic Datasets

### Equibase Research Dataset

**URL:** https://www.equibase.com/handicappersdata.cfm

**Announced:** March 2024

**Cost:** Free for research/development

**Coverage:** Complete 2023 calendar year (US racing)

**Contents:**
- Complete past performance data
- Corresponding results charts
- Supporting documentation

**Use Cases:**
- Academic research
- Product testing
- Handicapping theory development

---

### University Research Data

| Source | Coverage | Size |
|--------|----------|------|
| [Stanford CS230](http://cs230.stanford.edu/projects_winter_2021/reports/70738477.pdf) | Hong Kong | ~200 races |
| [UC Berkeley](https://saas.studentorg.berkeley.edu/rp/predicting-horse-races) | Kaggle data | Variable |
| [University of Louisville](https://ir.library.louisville.edu/cgi/viewcontent.cgi?article=4083&context=etd) | Graph-based features | Variable |

---

## Dataset Comparison

### By Quality Tier

#### Tier 1: Production Ready
| Dataset | Source | Size | Best For |
|---------|--------|------|----------|
| Betfair BSP | Official | 10+ years | Backtesting, BSP analysis |
| Betfair Historical | Official | Since 2015 | Tick data analysis |
| Equibase Research | Official | Full 2023 | US racing research |

#### Tier 2: High Quality
| Dataset | Source | Size | Best For |
|---------|--------|------|----------|
| Kaggle HK 2014-17 | Community | 1,561 races | ML training |
| RacingFormBook | Community | 2016-2025 | UK/IRE results |
| AI_horse_prediction | GitHub | Ongoing | Pre-trained models |

#### Tier 3: Specialized
| Dataset | Source | Size | Best For |
|---------|--------|------|----------|
| HK Expert Dataset | Kaggle | 5 files | Comprehensive HK data |
| Tipster Bets | Kaggle | 39,000 bets | Betting analysis |
| Big Data Derby | Kaggle | Variable | Health metrics |

---

### By Region

| Region | Best Free Dataset | Alternative |
|--------|-------------------|-------------|
| **UK** | Betfair BSP | RacingFormBook |
| **Ireland** | Betfair BSP | RacingFormBook |
| **Hong Kong** | Kaggle HK 2014-17 | HK Expert Dataset |
| **Australia** | Betfair AU CSV | Betfair BSP |
| **USA** | Equibase Research | Betfair BSP |

---

### By Use Case

| Use Case | Recommended Dataset |
|----------|---------------------|
| **ML Model Training** | Kaggle HK 2014-17 |
| **Backtesting Strategies** | Betfair BSP History |
| **Tick Data Analysis** | Betfair Historical BASIC |
| **UK Results Analysis** | RacingFormBook |
| **Academic Research** | Equibase Research |
| **Pre-trained Models** | AI_horse_prediction |

---

## Data Field Reference

### Standard Race Fields

```
Race Information:
├── race_id          - Unique identifier
├── date             - Race date
├── time             - Race time
├── course           - Racecourse name
├── distance         - Race distance
├── class            - Race class (1-7)
├── type             - Flat/NH, Handicap/Maiden
├── going            - Track condition
├── prize            - Prize money
└── runners          - Number of runners

Horse Information:
├── horse_name       - Horse name
├── horse_id         - Unique horse ID
├── age              - Horse age
├── sex              - Gender (C/F/G/M)
├── weight           - Weight carried
├── draw             - Starting position
├── trainer          - Trainer name
├── jockey           - Jockey name
├── owner            - Owner name
└── form             - Recent form string

Performance:
├── position         - Finishing position
├── lengths_beaten   - Distance behind winner
├── time             - Finish time
├── sp               - Starting price
├── bsp              - Betfair Starting Price
└── comment          - Race comment

Ratings (where available):
├── rpr              - Racing Post Rating
├── ts               - Top Speed
├── or               - Official Rating
└── tf_rating        - Timeform Rating
```

### Betfair-Specific Fields

```
Market Data:
├── event_id         - Betfair event ID
├── market_id        - Market identifier
├── selection_id     - Runner selection ID
├── win_lose         - Result flag
├── bsp              - Betfair Starting Price
├── ppwap            - Pre-play weighted average price
├── morningwap       - Morning WAP
├── ppmax/ppmin      - Pre-play price range
├── ipmax/ipmin      - In-play price range
├── pptradedvol      - Pre-play volume
└── iptradedvol      - In-play volume

Tick Data (Historical):
├── timestamp        - Update time
├── last_price       - Last traded price
├── total_matched    - Total matched volume
├── back_prices      - Available back prices
├── lay_prices       - Available lay prices
└── status           - Runner status
```

---

## Download Scripts

### Python: Bulk BSP Download

```python
import requests
import pandas as pd
from datetime import datetime, timedelta
from pathlib import Path

def download_bsp_history(
    start_date: str,
    end_date: str,
    region: str = "uk",
    output_dir: str = "./data/bsp"
):
    """
    Download BSP data for date range.

    Args:
        start_date: Start date (YYYY-MM-DD)
        end_date: End date (YYYY-MM-DD)
        region: uk, ire, aus, usa, sa
        output_dir: Output directory
    """
    Path(output_dir).mkdir(parents=True, exist_ok=True)

    base_url = "https://promo.betfair.com/betfairsp/prices"
    start = datetime.strptime(start_date, "%Y-%m-%d")
    end = datetime.strptime(end_date, "%Y-%m-%d")

    all_data = []
    current = start

    while current <= end:
        date_str = current.strftime("%d%m%Y")
        url = f"{base_url}/dwbfprices{region}{date_str}.csv"

        try:
            df = pd.read_csv(url)
            df['source_date'] = current.strftime("%Y-%m-%d")
            all_data.append(df)
            print(f"✓ {current.strftime('%Y-%m-%d')}")
        except:
            print(f"✗ {current.strftime('%Y-%m-%d')} - Not available")

        current += timedelta(days=1)

    if all_data:
        result = pd.concat(all_data, ignore_index=True)
        output_file = f"{output_dir}/bsp_{region}_{start_date}_{end_date}.csv"
        result.to_csv(output_file, index=False)
        print(f"\nSaved: {output_file}")
        print(f"Total records: {len(result)}")
        return result

    return pd.DataFrame()

# Usage
df = download_bsp_history("2024-01-01", "2024-01-31", region="uk")
```

### Bash: Download Kaggle Dataset

```bash
#!/bin/bash
# Requires: pip install kaggle
# Configure: ~/.kaggle/kaggle.json

# Hong Kong Racing
kaggle datasets download -d lantanacamara/hong-kong-horse-racing
unzip hong-kong-horse-racing.zip -d ./data/hk_racing

# Horse Racing 1990+
kaggle datasets download -d hwaitt/horse-racing
unzip horse-racing.zip -d ./data/historical

# HK Expert Dataset
kaggle datasets download -d hrosebaby/horse-racing-dataset-for-experts-hong-kong
unzip horse-racing-dataset-for-experts-hong-kong.zip -d ./data/hk_expert
```

---

## Data Quality Notes

### Known Issues

1. **Non-runners:** Historical prices may not account for Rule 4 deductions
2. **Missing data:** Some fields may be null for older races
3. **Format changes:** Betfair CSV format has changed over time
4. **Timezone:** Betfair data uses UK timezone

### Best Practices

1. **Validate data** before use (check for nulls, outliers)
2. **Handle non-runners** appropriately in analysis
3. **Normalize prices** when comparing across time periods
4. **Document versions** of datasets used in research

---

## Next Steps

- [GitHub Tools](02-github-tools-scrapers.md) - Generate custom datasets
- [Python Libraries](03-python-libraries.md) - Process data
- [Community Resources](05-community-resources.md) - Get help
