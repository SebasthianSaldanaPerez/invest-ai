# UI Layouts

## Sitemap v0.1 InvestAI Modules

1. Dashboard
2. Investment Journal
3. Watchlist
4. Personal Analytics
5. Strategy Settings
6. User Profile (Future)

### Dashboard 

The Dashboard is the main workspace of InvestAI.

Its objective is to guide the investor through a logical investment analysis process, presenting information from basic market data to advanced AI-assisted insights.

The dashboard follows the analysis flow below:

1. Company Overview
2. Market Snapshot
3. Price Chart
4. News & Market Sentiment
5. Financial Overview
6. Key Indicators
7. Opportunity Score
8. AI Analysis

### Investment Journal 

Record every investment decision made by the user in order to build a historical dataset for future analysis.

1. Header
2. New Trade
3. Trade Table

### Watchlist 

Allow the investor to keep track of companies that may become future investment opportunities without recording an actual investment decision.

The Watchlist serves as a quick access point to monitor selected companies and continue their analysis over time.

1. Header
2. Actions
3. Displayed Information

### Personal Analytics

Provide Business Intelligence insights about the investor's historical performance by analyzing completed investment decisions.

The objective is to identify strengths, weaknesses and recurring investment patterns.

1. Header
2. Performance Evolution
3. Investment Patterns
4. Best & Worst Trades
5. AI Perfomance Review

### Strategy Settings

Allow the investor to personalize how InvestAI evaluates investment opportunities.

The configuration affects the Opportunity Score calculation while keeping the investor in full control of the decision-making process.

1. Investor Profile
2. Opportunity Score Weights
3. Analysis Preferences
4. Opportunity Score Thresholds
5. Future Enhancements

### User Profile

Allow the investor to manage personal account preferences and personalize the InvestAI experience.

1. Personal Information
2. Account Settings
3. AI Preferences

## Dashboard Sections

### 1. Company Overview

Displays the basic information of the selected company.

Contents:

- Logo
- Company Name
- Ticker
- Sector
- Industry
- Exchange
- Currency
- Short Description
- Add to Watchlist

**Future Enhancements**

- Headquarters
- CEO
- Employees
- IPO Date

Purpose

Allow the investor to immediately identify the company being analyzed.

### 2. Market Snapshot

Displays the current market situation.

Contents

- Current Price
- Daily Change
- Previous Close
- Daily High
- Daily Low
- Average Price (30 / 90 / 180 days)

Purpose

Provide a quick overview of the current market status.

### 3. Price Chart

**Purpose**

Visualize the historical price evolution of the selected stock.

**Displayed Information**

- Interactive line chart
- Time filters:
  - 1 Week
  - 1 Month
  - 3 Months
  - 6 Months
  - 1 Year
  - 5 Years

**Future Enhancements**

- Candlestick chart
- Volume overlay
- Benchmark comparison (S&P 500)

### 4. News & Market Sentiment

**Purpose**

Provide recent events and market sentiment that may influence the stock price.

**Displayed Information**

- Number of positive news
- Number of neutral news
- Number of negative news
- Latest news headlines
- Publication date

**Future Enhancements**

- News filtering
- Sentiment trend
- Source credibility score

### 5. Financial Overview

**Purpose**

Provide a quick overview of the company's financial health.

**Displayed Information**

- Revenue
- Net Income
- Cash Flow
- Debt
- Earnings Growth

Button

View Full Financial Statements

**Future Enhancements**

- Quarterly comparison
- Financial ratios
- Historical trends

### 6. Key Indicators

**Purpose**

Display the most relevant financial and technical indicators used during the investment analysis.

**Displayed Information**

Initial Version

- RSI
- SMA 50
- SMA 200
- Market Capitalization

**Future Enhancements**

- P/E Ratio
- EPS
- ROE
- ROA
- Beta
- Volatility

### 7. Opportunity Score

**Purpose**

Calculate the investment opportunity according to the user's personalized strategy.

Displayed Information

- Opportunity Score
- Confidence Level
- Main Factors

Button

Calculate Opportunity Score

**Future Enhancements**

- Historical score evolution
- Strategy comparison

### 8. AI Analysis

**Purpose**

Provide an AI-generated summary to complement the investor's own analysis.

Displayed Information

- Executive Summary
- Risks
- Strengths
- Questions to investigate

Button

Generate AI Analysis

**Future Enhancements**

- Earnings call summary
- Company comparison
- Analyst consensus explanation

## Investement Journal Sections

### New Trade

The "New Trade" action opens a modal window.

Fields:

- Purchase Date
- Ticker
- Purchase Price
- Opportunity Score
- Investment Thesis (Optional)

### Trade Table

Displayed Information

- Purchase Date
- Ticker
- Purchase Price
- Status
- Sell Date
- Sell Price
- Profit & Loss (Calculated)
- Holding Time (Calculated)
- Investment Thesis

## Watchlist Sections

### Header

- Total Watchlist
- Search Bar

### Main Actions

- Add to Watchlist (from the Dashboard using the Favorite button)
- Open Company Dashboard
- Remove from Watchlist

### Displayed Information

- Ticker
- Company Name
- Sector
- Added Price
- Current Price
- Change Since Added
- Actions

### User Flow

1. The investor searches and analyzes a company in the Dashboard.
2. If the company is interesting but no investment decision is made, the investor clicks the Favorite button.
3. The company is automatically added to the Watchlist.
4. The Watchlist displays updated market information whenever it is opened.
5. The investor can reopen the Dashboard directly from the Watchlist to continue the analysis.

### Notes

The Watchlist is not intended to store historical market data.

Only the company identifier (ticker) and the reference price at the time it was added are stored. Current market information is retrieved dynamically from the data provider.

### Future Enhancements

- Tags (Long-term, Dividend, Growth, Speculative, etc.)
- Price alerts
- Custom sorting
- Filters by sector
- Automatic Opportunity Score preview

## Personal Analytics Sections

### Header

- Win Rate
- Lose Rate
- Average Return
- Average Holding Time
- Average Opportunity Score

### Performance Evolution

Displays the historical performance of completed trades over time.

Displayed Information

- Performance chart
- Return percentage
- Time axis

### Investment Patterns

Displays statistics calculated from completed trades.

Displayed Information

- Best Performing Sector
- Worst Performing Sector
- Best Holding Time
- Average Profit
- Average Loss
- Average Opportunity Score

### Best & Worst Trades

Displays two rankings.

Best Trades

- Top 5 highest returns

Worst Trades

- Bottom 5 returns

### AI Performance Review

Purpose

Generate an AI-assisted review of the investor's historical performance.

Button

Generate Performance Review

Generated Information

- Performance summary
- Recurring strengths
- Common mistakes
- Investment habits
- Improvement suggestions

### Future Enhancements

- Monthly performance comparison
- Sector heatmap
- Interactive filters
- Benchmark comparison (S&P 500)
- ML-based behavioral insights

## Strategy Settings Sections

#### Investor Profile

Available Profiles

- Conservative
- Balanced
- Aggressive
- Custom

#### Opportunity Score Weights

Configurable Factors

- Financial Health
- Technical Indicators
- News Sentiment
- Analyst Consensus
- Risk Metrics

#### Analysis Preferences

- Preferred Holding Period
- Risk Tolerance
- Preferred Sectors
- Preferred Exchanges

#### Opportunity Score Thresholds

- High Opportunity
- Watch
- Neutral
- High Risk

### Future Enhancements

- Multiple investment strategies
- AI optimization suggestions
- Strategy import/export
- Backtesting

## User Profile Sections

### Personal Information

Displayed Information

- Profile Picture
- Display Name
- Email Address
- Preferred Alias

### Account Settings

- Change Password
- Language
- Time Zone

### AI Preferences

- Preferred Response Language
- Response Style
- Preferred Alias

### Future Enhancements

- Two-Factor Authentication
- Notification Preferences
- LLM Provider Selection
- Data Export