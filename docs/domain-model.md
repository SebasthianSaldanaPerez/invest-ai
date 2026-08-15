# Domain Model

## Introduction

This document describes the core business concepts of InvestAI.
Its purpose is to define the entities, relationships, business rules and domain services before designing the software architecture or the database.

# Domain Candidates

## Market Intelligence

Company                    → Entity
Stock                      → Entity
Historical Price           → Entity
News                       → Entity
Analyst Consensus          → Entity
Financial Statement        → Entity
Technical Indicator        → Calculated Result
Financial Indicator        → Calculated Result

## Investment Decision Support

Strategy                   → Entity
Opportunity Evaluation     → Calculated Result
AI Analysis                → Entity

## Personal Investment Intelligence

Trade                      → Entity
Watchlist                  → Entity
Watchlist Item             → Entity
Performance Analytics      → Calculated Result
Investment Pattern         → Calculated Result
Performance Review         → Entity

## User Management

User                       → Entity
AI Preferences             → Value Object

# Entities

## Company

### Type
Entity

### Purpose
Represent a publicly traded company that can be analyzed within InvestAI.

### Main Attributes
-	Company ID
-	Name
-	Sector
-	Industry
-	Country
-	Employee Count
-	Description
-	Website

### Relationships
-	A Company can have one or more Stocks.
-	A Company can have multiple Financial Statements.
-	A Company can be related to multiple News items.
-	A Company can have multiple Analyst Consensus records.

### Business Rules
-	A Company must have a unique internal identifier.
-	A Company does not store historical market prices directly.
-	A Company must have at least one Stock to be analyzed in InvestAI.

## Stock

### Type
Entity

### Purpose
Represent a publicly traded company that can be analyzed within InvestAI.

### Main Attributes
-	Stock ID
-	Ticker
-	Exchange
-	Currency
-	Status

### Relationships
-	A Stock belongs to one Company.
-   A Stock can have multiple Historical Price records.
-   A Stock can be referenced by multiple Trades.
-   A Stock can be included in multiple Watchlist Items.
-   A Stock can have multiple Opportunity Evaluations.


### Business Rules
-	A Stock must have a unique internal identifier.
-	The combination of ticker and exchange must be unique.
-	A Stock must belong to a Company.
-   A Stock does not directly store its current price.

## Historical Price

### Type
Entity

### Purpose
Represent the market price of a Stock during a specific date and time period.

### Main Attributes
-	Historical Price ID
-   Date and Time
-   Open Price
-   High Price
-   Low Price
-   Close Price
-   Trading Volume


### Relationships
-	A Historical Price belongs to one Stock.
-   A Stock can have multiple Historical Price records.

### Business Rules
-	A Historical Price must belong to a Stock.
-   Each record must represent a specific date and time interval.
-   A Historical Price cannot exist without its associated Stock.
-   Calculated values such as averages, trends and period highs are not stored directly in this entity.

## Trade

### Type
Entity

### Purpose
Represent an investment decision registered by the User, beginning with a purchase and optionally ending with a sale.

### Main Attributes
-	Trade ID
-   Purchase Date
-   Purchase Price
-   Sell Date
-   Sell Price
-   Status
-   Investment Thesis
-   Opportunity Score at Purchase

### Relationships
-	A Trade belongs to one User.
-   A Trade references one Stock.
-   A Trade can reference an Opportunity Evaluation generated at the time of purchase.


### Business Rules
-	A Trade must have a unique internal identifier.
-   A Trade must have a purchase date and purchase price.
-   A newly created Trade must initially have an open status.
-   Sell Date and Sell Price are optional while the Trade remains open.
-   A closed Trade must have a Sell Date and Sell Price.
-   Sell Date cannot be earlier than Purchase Date.
-   Purchase Price and Sell Price must be greater than zero.
-   A Trade represents a decision record, not the management of invested capital or number of shares.

## User

### Type
Entity

### Purpose
Represent the person who uses InvestAI and owns the personalized investment information.

### Main Attributes
-	User ID
-   Name
-   Alias
-   Email Address
-   Created At


### Relationships
-	A User has one active Strategy.
-   A User has one Watchlist.
-   A User can have multiple Trades.
-   A User can have AI Preferences.
-   A User can generate multiple AI Analyses and Performance Reviews.


### Business Rules
-	A User must have a unique internal identifier.
-   A User can only have one active Strategy at a time.
-   The alias is used to personalize AI-generated responses.
-   Authentication information may be added when the system supports multiple users

## Strategy

### Type
Entity

### Purpose
Represent the criteria and preferences used by InvestAI to calculate Opportunity Evaluations for a User.

### Main Attributes
-	Strategy ID
-   Profile
-   Risk Tolerance
-   Preferred Holding Period
-   Financial Weight
-   Technical Weight
-   News Sentiment Weight
-   Analyst Consensus Weight
-   Risk Metrics Weight
-   Opportunity Thresholds


### Relationships
-	A Strategy belongs to one User.
-   A Strategy is used to generate Opportunity Evaluations.


### Business Rules
-	A User can only have one active Strategy at a time.
-   The sum of the Opportunity Score weights must equal 100%.
-   Every weight must be within the permitted range.
-   A predefined profile can establish default weights.
-   A custom profile allows the User to modify the weights.
-   Changing a Strategy does not modify historical Opportunity Evaluations.

## Watchlist

### Type
Entity

### Purpose
Represent the collection of Stocks that a User wants to monitor or analyze later.

### Main Attributes
-	Watchlist ID
-   Created At
-   Updated At

### Relationships
-	A Watchlist belongs to one User.
-   A Watchlist contains multiple Watchlist Items.

### Business Rules
-	A User can have one main Watchlist in the initial version.
-   A Watchlist cannot contain the same Stock more than once.
-   Removing a Watchlist Item does not delete the associated Stock.
-   Opening a Stock in the Dashboard is an interface action and is not a business rule of the Watchlist.

## Watchlist Item

### Type
Entity

### Purpose
Represent a Stock saved by a User for future monitoring or analysis.
### Main Attributes

-	Watchlist Item ID
-   Added Date
-   Reference Price


### Relationships
-	A Watchlist Item belongs to one Watchlist.
-   A Watchlist Item references one Stock.


### Business Rules
-	A Watchlist Item must have a unique internal identifier.
-   A Watchlist Item must reference a Stock.
-   The same Stock cannot appear more than once in the same Watchlist.
-   Reference Price represents the market price when the Stock was added.
-   Current Price is not stored directly in the Watchlist Item.
-   A Watchlist Item can be removed without affecting the associated Stock or its market information.

## News

### Type
Entity

### Purpose
Represent a news article related to a Company or Stock that may provide relevant context for investment analysis.

### Main Attributes

-  News ID
-  Title
-  Publication Date
-  Source
-  URL
-  Summary
-  Sentiment


### Relationships
- A News item can be related to one Company.
- A Company can have multiple News items.


### Business Rules
- A News item must have a unique internal identifier.
- A News item must have a source and publication date.
- Sentiment can be Positive, Neutral or Negative.
- Duplicate News items should not be stored.

## Analyst Consensus

### Type
Entity

### Purpose
Represent the aggregated opinion of market analysts about a Company or Stock.

### Main Attributes
- Analyst Consensus ID
- Date
- Target Price
- Recommendation
- Number of Analysts

### Relationships
- An Analyst Consensus belongs to one Stock.
- A Stock can have multiple Analyst Consensus records over time.

### Business Rules
- Each Analyst Consensus must reference a Stock.
- Each record represents the consensus available at a specific point in time.
- Historical consensus records must not be overwritten when new consensus data becomes available.

## Financial Statement

### Type
Entity

### Purpose
Represent a financial report published by a Company for a specific accounting period.

### Main Attributes
- Financial Statement ID
- Statement Type
- Fiscal Period
- Publication Date
- Currency
- Financial Data

### Relationships
- A Financial Statement belongs to one Company.
- A Company can have multiple Financial Statements.

### Business Rules
- A Financial Statement must belong to a Company.
- Statement Type must identify whether it is an Income Statement, Balance Sheet or Cash Flow Statement.
- Each statement must correspond to a specific fiscal period.
- Historical Financial Statements must remain unchanged after being stored.

# Calculated Results

## Technical Indicator

### Type
Calculated Result

### Purpose
Represent a technical measurement calculated from historical market data to support stock analysis.

### Main Attributes
- Indicator Type
- Value
- Calculation Date
- Time Period

### Relationships
- A Technical Indicator is calculated for one Stock.
- Technical Indicators are calculated using Historical Price data.

### Business Rules
- A Technical Indicator must be derived from market data.
- Its calculation method must depend on the selected Indicator Type.
- Examples include RSI, MACD and Moving Averages.


## Financial Indicator

### Type
Calculated Result

### Purpose
Represent a financial measurement used to evaluate the financial condition, profitability or valuation of a Company.

### Main Attributes
- Indicator Type
- Value
- Calculation Date
- Fiscal Period

### Relationships
- A Financial Indicator is calculated for one Company.
- Financial Indicators can use Financial Statements and market information as input.

### Business Rules
- A Financial Indicator must be calculated from validated financial information.
- Its calculation method depends on the Indicator Type.
- Examples include P/E, ROE, ROA and Debt-to-Equity.


## Opportunity Evaluation

### Type
Calculated Result

### Purpose
Represent the evaluation of an investment opportunity according to the User's active Strategy.

### Main Attributes
- Score
- Evaluation Date
- Financial Component Score
- Technical Component Score
- News Sentiment Component Score
- Analyst Consensus Component Score
- Risk Component Score
- Explanation

### Relationships
- An Opportunity Evaluation belongs to one Stock.
- An Opportunity Evaluation is generated using one Strategy.
- A Trade can reference the Opportunity Evaluation available at the time of purchase.

### Business Rules
- The Score must be calculated using the active Strategy.
- Each component must follow the weights defined by the Strategy.
- The final Score must remain within the defined scoring range.
- Historical evaluations must not change when the Strategy is modified later.


## Performance Analytics

### Type
Calculated Result

### Purpose
Represent statistical insights calculated from the User's completed Trades.

### Main Attributes
- Win Rate
- Loss Rate
- Average Return
- Average Holding Time
- Average Opportunity Score
- Best Performing Sector
- Worst Performing Sector

### Relationships
- Performance Analytics is calculated from a User's completed Trades.

### Business Rules
- Only completed Trades are included in realized performance calculations.
- Open Trades must not affect realized Win Rate or Loss Rate.
- Results are calculated dynamically from historical Trade data.


## Investment Pattern

### Type
Calculated Result

### Purpose
Represent recurring characteristics identified in the User's historical investment decisions.

### Main Attributes
- Pattern Type
- Description
- Supporting Metrics
- Confidence

### Relationships
- Investment Patterns are derived from a User's historical Trades.
- Patterns can incorporate Opportunity Evaluations and market context associated with those Trades.

### Business Rules
- Patterns must be derived from historical User data.
- A pattern should only be reported when sufficient supporting data exists.
- Investment Patterns do not automatically modify the User's Strategy.

# Domain Services


## AI Analysis

### Type
Entity

### Purpose
Represent an AI-generated analysis that summarizes and explains the available information about a Stock.

### Main Attributes
- AI Analysis ID
- Generated Date
- Summary
- Strengths
- Risks
- Relevant Questions
- Prompt Version
- Model

### Relationships
- An AI Analysis belongs to one Stock.
- An AI Analysis can use Opportunity Evaluations, News, Financial Indicators, Technical Indicators and Analyst Consensus as context.

### Business Rules
- An AI Analysis must have a generation date.
- The model and prompt version used to generate the analysis must be identifiable.
- A generated analysis must not automatically modify an Opportunity Evaluation or Strategy.


## Performance Review

### Type
Entity

### Purpose
Represent an AI-generated interpretation of the User's historical investment performance.

### Main Attributes
- Performance Review ID
- Generated Date
- Summary
- Strengths
- Weaknesses
- Identified Patterns
- Improvement Suggestions
- Model
- Prompt Version

### Relationships
- A Performance Review belongs to one User.
- A Performance Review can use Performance Analytics and Investment Patterns as input.

### Business Rules
- Only completed Trades are used for realized performance analysis.
- A Performance Review does not modify the User's Strategy automatically.
- The model and prompt version used to generate the review must be identifiable.


## Opportunity Calculator


## Technical Indicator Calculator


## Financial Indicator Calculator



# Relationships

User
├── has one active Strategy
├── has one Watchlist
├── has many Trades
├── has AI Preferences
└── has many Performance Reviews

Watchlist
└── contains many Watchlist Items

Watchlist Item
└── references one Stock

Trade
├── belongs to one User
├── references one Stock
└── can reference one Opportunity Evaluation

Company
├── has one or more Stocks
├── has many Financial Statements
└── has many News items

Stock
├── belongs to one Company
├── has many Historical Prices
├── has many Analyst Consensus records
├── has Technical Indicators
└── has many Opportunity Evaluations

Historical Prices
└── feed Technical Indicators

Financial Statements
└── feed Financial Indicators

Strategy
└── is used by Opportunity Evaluation

Technical Indicators ─────────┐
Financial Indicators ─────────┤
News Sentiment ────────────────┼──> Opportunity Evaluation
Analyst Consensus ─────────────┤
Strategy ──────────────────────┘

Trades
└── feed Performance Analytics

Performance Analytics
└── supports Investment Patterns

Performance Analytics ────────┐
Investment Patterns ──────────┼──> Performance Review
                              │
Opportunity Evaluation ───────┘

Opportunity Evaluation ───────┐
Technical Indicators ─────────┤
Financial Indicators ─────────┤
News ─────────────────────────┼──> AI Analysis
Analyst Consensus ─────────────┘