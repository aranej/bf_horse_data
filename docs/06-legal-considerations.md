# Legal Considerations

> Terms of service, rate limits, and compliance guidelines for horse racing data collection.

## Table of Contents

- [Overview](#overview)
- [Terms of Service by Provider](#terms-of-service-by-provider)
- [API Rate Limits](#api-rate-limits)
- [Web Scraping Legality](#web-scraping-legality)
- [Anti-Bot Measures](#anti-bot-measures)
- [Best Practices](#best-practices)
- [Risk Assessment](#risk-assessment)

---

## Overview

### Key Principles

1. **Official APIs are always preferred** over web scraping
2. **Terms of Service** are legally binding agreements
3. **Rate limits** protect services and ensure fair access
4. **Commercial use** often requires explicit licensing
5. **Personal/research use** typically has more flexibility

### Risk Spectrum

```
Low Risk                                              High Risk
    │                                                      │
    ▼                                                      ▼
Official API → Free Data → ToS-Compliant → Scraping → Commercial
   (Betfair)    (BSP CSV)    Scraping      Public     Scraping
                                           Data
```

---

## Terms of Service by Provider

### Betfair Exchange

**Developer Terms:** https://developer.betfair.com

#### API Access

| Access Type | Cost | Restrictions |
|-------------|------|--------------|
| Delayed Key | Free | 1-60s delay, no betting |
| Live Key | £299 | Full access, real-time |

#### Data Rights

> "All data on Betfair website (including pricing data) is protected by copyright and database rights"

**Key Restrictions:**
- Data may not be used without license for business purposes
- "Business usage" includes:
  - Use by betting operators
  - Supplying data to betting operators
- Bots may be restricted if they:
  - Manipulate markets
  - Affect Exchange integrity

#### VPN Usage

> Using VPNs to access Betfair violates ToS and can result in:
> - Account suspension
> - Frozen withdrawals

#### BSP Data (promo.betfair.com)

The BSP data endpoint appears to be **publicly accessible** without explicit restrictions. However:
- Use for personal/research purposes is generally acceptable
- Commercial redistribution may require licensing
- High-volume automated access should respect server resources

---

### Racing Post

**Terms:** https://help.racingpost.com/hc/en-us/articles/208996085-Terms-and-conditions

#### License Grant

> "Non-exclusive and non-transferable licence for private and domestic use only"

#### Prohibitions

- Accessing services "by any means or for any purpose other than in accordance with these Terms"
- Copying, redistributing, or relaying content beyond copyright exceptions
- Causing system to be "interrupted, damaged, rendered less efficient or impaired"

#### Enforcement

> Racing Post reserves right to suspend/terminate access for ToS violations "with or without notice"

#### Practical Impact

- **Personal use scrapers** (like rpscrape) operate in gray area
- **Commercial use** explicitly prohibited without license
- **Official API** available for B2B licensing via Spotlight Sports Group

---

### British Horseracing Authority (BHA)

**Terms:** https://www.britishhorseracing.com/terms-conditions/

#### Position on Scraping

> BHA prohibits web scraping for commercial purposes and threatens legal action

#### API Access

- Limited API available
- Very strict throttling at IP address level
- Users report needing "random sleeps and multiple EC2 instances" for bulk access

---

### Bookmaker Sites (Bet365, William Hill, etc.)

#### Common Restrictions

Most UK bookmakers explicitly prohibit:
- Automated systems or bots
- Data extraction or scraping
- Screen scraping or data harvesting
- Any automated access to their services

#### Example: Bet365

> "Use of automated systems or software to copy and/or extract the whole or any part of, the Website, the information or data on the Website"

#### Consequences

- IP blocking
- Account closure
- Forfeiture of funds (disputed)
- Legal action (rare but possible)

---

### Oddschecker

#### Detection Measures

- Requires Selenium (not basic requests)
- Frequent layout changes
- User-agent verification
- Returns 403 Forbidden for obvious bots

#### Practical Status

- Scraping is common but technically against ToS
- Site is designed for human users
- Aggregates bookmaker odds (not original data)

---

## API Rate Limits

### Betfair Exchange API

#### Request Limits

| Operation | Limit |
|-----------|-------|
| listMarketBook | 5 calls/second per marketId |
| Order transactions | 1,000/second |
| Concurrent requests | 3 queued maximum |
| Login attempts | 100/minute (then 20-min lockout) |

#### Data Weight Limits

```
Market Data: Weight × Market IDs ≤ 200 points per request

Weights by operation:
├── listMarketBook (basic): Low
├── listMarketBook (with orders): Higher
└── Complex projections: Highest
```

#### Rate-Limited Operations

These operations share rate limits:
- `listMarketBook` (with OrderProjection or MatchProjection)
- `listCurrentOrders`
- `listMarketProfitAndLoss`

Note: `listClearedOrders` has separate rate limiting

#### Error Responses

| Error | Meaning |
|-------|---------|
| `TOO_MUCH_DATA` | Request exceeds data limits |
| `TOO_MANY_REQUESTS` | Exceeded request rate |
| HTTP 429 | Rate limit exceeded |

---

### Betfair Historical Data API

#### Rate Limits

**100 requests per 10 seconds**

All requests count toward limit, including:
- Successful requests
- Failed requests
- Error responses

---

### Best Practices for API Usage

```python
import time
from functools import wraps

def rate_limit(calls_per_second=5):
    """Decorator to enforce rate limiting."""
    min_interval = 1.0 / calls_per_second
    last_called = [0.0]

    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            elapsed = time.time() - last_called[0]
            if elapsed < min_interval:
                time.sleep(min_interval - elapsed)
            result = func(*args, **kwargs)
            last_called[0] = time.time()
            return result
        return wrapper
    return decorator

@rate_limit(calls_per_second=4)  # Leave margin
def get_market_book(trading, market_id):
    return trading.betting.list_market_book(market_ids=[market_id])
```

---

## Web Scraping Legality

### Legal Framework

#### United States

- No federal laws explicitly prohibiting scraping of public data
- **Computer Fraud and Abuse Act (CFAA)** can apply to unauthorized access
- **hiQ Labs v. LinkedIn (2022)**: Scraping public data not necessarily illegal
- Terms of Service violations may constitute breach of contract

#### United Kingdom / EU

- Terms of Service generally enforceable if agreed to
- **GDPR** applies to personal data
- **Database rights** protect structured data collections
- **Copyright** protects creative content

#### Key Legal Concepts

| Concept | Relevance |
|---------|-----------|
| **Clickwrap Agreement** | Explicit consent (clicking "I agree") creates binding contract |
| **Browsewrap Agreement** | Passive consent (just using site) - weaker enforcement |
| **robots.txt** | Technical indication of scraping policy (not legally binding) |
| **Public Data** | Generally more permissive for scraping |
| **Database Rights** | EU protection for structured data collections |

---

### Case-by-Case Assessment

#### Generally Acceptable

- Scraping public data for personal research
- Using official APIs within rate limits
- Downloading explicitly provided data files (BSP CSV)
- Academic research with proper attribution

#### Gray Area

- Personal scrapers for non-commercial use
- Small-scale data collection
- Data not explicitly protected
- No explicit prohibition in ToS

#### Generally Prohibited

- Commercial scraping without license
- Violating explicit ToS prohibitions
- Circumventing technical protections
- Redistributing scraped data
- High-volume automated access
- Scraping personal/private data

---

## Anti-Bot Measures

### Common Protections

| Protection | How It Works | Bypass Difficulty |
|------------|--------------|-------------------|
| **User-Agent Check** | Blocks non-browser user agents | Easy |
| **Rate Limiting** | Limits requests per time period | Medium |
| **JavaScript Challenge** | Requires JS execution | Medium |
| **CAPTCHA** | Human verification | Hard |
| **Cloudflare** | Multiple detection methods | Hard |
| **IP Blocking** | Blocks suspicious IPs | Medium |
| **Fingerprinting** | Browser/TLS fingerprinting | Very Hard |

### Cloudflare Protection

Many racing sites use Cloudflare, which employs:

- TLS fingerprint analysis
- HTTP header inspection
- Browser behavior analysis
- JavaScript challenges
- Rate limiting

**Error Codes:**
- Error 1015: "Your access rate has been limited"
- HTTP 403: Forbidden
- HTTP 429: Too Many Requests

### Bypass Tools (Use Responsibly)

| Tool | Purpose | Notes |
|------|---------|-------|
| cloudscraper | Cloudflare bypass | Python module |
| Selenium | Browser automation | Resource heavy |
| Playwright | Modern browser automation | Better async support |
| undetected-chromedriver | Stealth Chrome | Detection avoidance |
| Camoufox | Privacy browser | 2025 option |

**Warning:** Using bypass tools may violate ToS and could lead to:
- Permanent IP bans
- Account blacklisting
- Legal action

---

## Best Practices

### Technical Best Practices

```python
# 1. Respect robots.txt
import urllib.robotparser
rp = urllib.robotparser.RobotFileParser()
rp.set_url("https://example.com/robots.txt")
rp.read()
if rp.can_fetch("*", "/path/to/scrape"):
    # Proceed with scraping
    pass

# 2. Use appropriate delays
import time
import random

def polite_request(url, min_delay=1, max_delay=3):
    time.sleep(random.uniform(min_delay, max_delay))
    return requests.get(url, headers=headers)

# 3. Identify yourself
headers = {
    'User-Agent': 'ResearchBot/1.0 (contact@example.com; research purpose)',
}

# 4. Handle errors gracefully
def safe_request(url, max_retries=3):
    for attempt in range(max_retries):
        try:
            response = requests.get(url, headers=headers, timeout=10)
            if response.status_code == 429:
                time.sleep(60)  # Back off on rate limit
                continue
            response.raise_for_status()
            return response
        except requests.RequestException as e:
            if attempt == max_retries - 1:
                raise
            time.sleep(2 ** attempt)  # Exponential backoff
```

### Ethical Guidelines

1. **Use Official APIs** when available
2. **Respect Rate Limits** - don't overwhelm servers
3. **Honor robots.txt** - even if not legally binding
4. **Don't Redistribute** scraped data commercially
5. **Attribute Sources** in research/publications
6. **Minimize Impact** - cache data, avoid repeated requests
7. **Stop When Asked** - honor cease-and-desist requests

### Documentation Practices

```python
# Document data sources in your code
"""
Data Source: Betfair SP History
URL: https://promo.betfair.com/betfairsp/prices
Access Date: 2024-12-05
Terms: Public CSV files, used for personal research
License: Assumed permissive for non-commercial use
"""
```

---

## Risk Assessment

### Risk Matrix

| Activity | Legal Risk | Account Risk | Technical Risk |
|----------|------------|--------------|----------------|
| **Official API (within limits)** | None | None | None |
| **Free public data (BSP CSV)** | Very Low | None | Very Low |
| **Personal scraper (low volume)** | Low | Low | Medium |
| **High-volume scraping** | Medium | High | High |
| **Commercial scraping** | High | Very High | High |
| **Bypass anti-bot measures** | High | Very High | Very High |

### Decision Framework

```
Should I scrape this data?

1. Is there an official API?
   ├── Yes → Use the API
   └── No → Continue to 2

2. Is there a free download option?
   ├── Yes → Use the download
   └── No → Continue to 3

3. What do the ToS say?
   ├── Explicitly allowed → Proceed carefully
   ├── Silent on scraping → Gray area, assess risk
   └── Explicitly prohibited → Don't scrape

4. What's the purpose?
   ├── Personal research → Lower risk
   ├── Academic → Lower risk, cite properly
   └── Commercial → Seek license

5. Can I minimize impact?
   ├── Cache data
   ├── Limit request rate
   └── Avoid peak times
```

### Consequences Spectrum

| Consequence | Likelihood | Severity |
|-------------|------------|----------|
| IP temporarily blocked | Common | Low |
| IP permanently blocked | Occasional | Medium |
| Account suspended | Occasional | High |
| Cease-and-desist letter | Rare | Medium |
| Legal action | Very Rare | Very High |

---

## Specific Recommendations

### For Personal Research

✅ **Recommended:**
- Betfair API with free delayed key
- Betfair BSP CSV downloads
- Kaggle datasets
- GitHub datasets with permissive licenses
- rpscrape for personal analysis (accept ToS risk)

⚠️ **Use Caution:**
- Low-volume personal scrapers
- Oddschecker (common but against ToS)

❌ **Avoid:**
- High-volume automated scraping
- Bypassing anti-bot measures
- Redistributing scraped data

### For Commercial Projects

✅ **Recommended:**
- Betfair API with live key (£299)
- Official data licensing (Racing Post, Timeform)
- The Racing API (commercial)
- Equibase licensing (US)

❌ **Avoid:**
- Any scraping without explicit license
- Free data sources for commercial purposes
- Redistributing any third-party data

### For Academic Research

✅ **Recommended:**
- Equibase Research Dataset (free for research)
- Kaggle datasets (cite appropriately)
- Betfair data with acknowledgment
- Published academic datasets

⚠️ **Document:**
- Data sources and access methods
- Terms of use compliance
- Any limitations on redistribution

---

## Resources

### Legal References

- [Is Web Scraping Legal? (EWDCI)](https://ethicalwebdata.com/is-web-scraping-legal-navigating-terms-of-service-and-best-practices/)
- [Is Web Scraping Legal? (AIM Multiple)](https://research.aimultiple.com/is-web-scraping-legal/)
- [Web Scraping Legal Landscape (Browserless)](https://www.browserless.io/blog/is-web-scraping-legal)

### Terms of Service

- [Betfair Developer Terms](https://developer.betfair.com)
- [Racing Post Terms](https://help.racingpost.com/hc/en-us/articles/208996085-Terms-and-conditions)
- [BHA Terms](https://www.britishhorseracing.com/terms-conditions/)

### Rate Limit Documentation

- [Betfair API Limits](https://support.developer.betfair.com/hc/en-us/articles/115003864671-What-data-request-limits-exist-on-the-Exchange-API)
- [Historical Data API Limits](https://support.developer.betfair.com/hc/en-us/articles/10111059056669-What-are-the-request-rate-limits-on-the-Historical-Data-API)

---

## Disclaimer

This document provides general information about legal considerations for data collection. It is not legal advice. Users should:

1. Consult with qualified legal counsel for specific situations
2. Review current terms of service (they change frequently)
3. Assess their own risk tolerance
4. Take responsibility for their actions

The authors of this documentation assume no liability for actions taken based on this information.

---

## Next Steps

- [Official Data Sources](01-official-data-sources.md) - Legal data access
- [Python Libraries](03-python-libraries.md) - API integration
- [Datasets](04-datasets.md) - Pre-approved data sources
