# Database Design

## Purpose

This document describes the initial relational database design for InvestAI.

The database model translates the concepts defined in the Domain Model into persistent structures while preserving their relationships and business constraints.

PostgreSQL will be used as the initial relational database management system.

## Design Principles

- Domain entities do not automatically require their own database table.
- Calculated information should not be persisted unless there is a clear historical or performance requirement.
- Historical information must preserve the state known at the relevant point in time.
- Relationships between persistent entities should be enforced through appropriate foreign keys and constraints.
- The database design should avoid unnecessary duplication of information.

## Tables

### Companies

**Purpose**

Persist information about a publicly traded company.

**Columns**

- company_id
- name
- sector
- industry
- country
- employee_count
- description
- website

**Primary Key**

- company_id

**Foreign Keys**

- N/A

**Constraints**

- company_id must be unique and not null.
- name must not be null.

**Relationships**

- A Company can have one or more Stocks.
- A Company can have multiple Financial Statements.
- A Company can be related to multiple News items.

**Historical Considerations**

- A Company does not store historical market prices directly.


### Stocks

**Purpose**

Persist information about tradable financial instruments.

**Columns**

- stock_id
- company_id
- ticker
- exchange
- currency
- status

**Primary Key**

- stock_id

**Foreign Keys**

- company_id → companies.company_id

**Constraints**

- ticker + exchange must be unique.
- company_id must not be null.
- ticker must not be null.
- exchange must not be null.

**Relationships**

- A Stock belongs to one Company.
- A Stock can have multiple Historical Price records.
- A Stock can be referenced by multiple Trades.
- A Stock can be included in multiple Watchlist Items.
- A Stock can have multiple Opportunity Evaluations.

**Historical Considerations**

- Current price is not stored directly in this table.

### Historical Prices

**Purpose**

Persist historical market price information for a Stock.

**Columns**

- historical_price_id
- stock_id
- date_time
- open_price
- high_price
- low_price
- close_price
- trading_volume

**Primary Key**

- historical_price_id

**Foreign Keys**

- stock_id → stocks.stock_id

**Constraints**

- historical_price_id must be unique and not null.
- stock_id must not be null.
- date_time must not be null.
- stock_id + date_time must be unique.
- open_price must be greater than or equal to 0.
- high_price must be greater than or equal to 0.
- low_price must be greater than or equal to 0.
- close_price must be greater than or equal to 0.
- trading_volume must be greater than or equal to 0.

**Relationships**

- A Historical Price belongs to one Stock.
- A Stock can have multiple Historical Price records.

**Historical Considerations**

- Historical market prices are preserved as time-series records.
- Calculated values such as averages, trends and period highs are not stored directly in this table.

### Users

**Purpose**

Persist information about InvestAI users.

**Columns**

- user_id
- name
- alias
- email_address
- created_at

**Primary Key**

- user_id

**Foreign Keys**

- N/A

**Constraints**

- user_id must be unique and not null.
- name must not be null.
- email_address must be unique.
- email_address must not be null.
- created_at must not be null.

**Relationships**

- A User has one active Strategy.
- A User has one Watchlist.
- A User can have multiple Trades.
- A User can have AI Preferences.
- A User can have multiple Performance Reviews.

**Historical Considerations**

- created_at preserves the date when the User was created.
- Changes to User profile information do not modify historical Trade records.

### Trades

**Purpose**

Persist investment decisions made by a User for a specific Stock.

**Columns**

- trade_id
- user_id
- stock_id
- opportunity_evaluation_id
- purchase_date
- purchase_price
- sell_date
- sell_price
- status
- investment_thesis
- opportunity_score_at_purchase

**Primary Key**

- trade_id

**Foreign Keys**

- user_id → users.user_id
- stock_id → stocks.stock_id
- opportunity_evaluation_id → opportunity_evaluations.opportunity_evaluation_id

**Constraints**

- trade_id must be unique and not null.
- user_id must not be null.
- stock_id must not be null.
- purchase_date must not be null.
- purchase_price must be greater than 0.
- sell_date can be null while the Trade is open.
- sell_price can be null while the Trade is open.
- if present, sell_price must be greater than 0.
- if present, sell_date must be greater than or equal to purchase_date.
- status must be either OPEN or CLOSED.
- status must not be null.
- a CLOSED Trade must have a sell_date and sell_price.
- an OPEN Trade must not have a sell_date or sell_price.
- opportunity_evaluation_id can be null.

**Relationships**

- A Trade belongs to one User.
- A Trade references one Stock.
- A Trade can reference one Opportunity Evaluation generated at the time of purchase.

**Historical Considerations**

- A Trade preserves the information associated with the investment decision at the time it was made.
- opportunity_score_at_purchase preserves the Opportunity Score available at purchase time.
- Changes to later Opportunity Evaluations do not modify historical Trade information.
- A Trade represents a decision record, not the management of invested capital or number of shares.

### Strategies

**Purpose**

Persist investment analysis strategies configured by a User.

**Columns**

- strategy_id
- user_id
- profile
- risk_tolerance
- preferred_holding_period
- financial_weight
- technical_weight
- news_sentiment_weight
- analyst_consensus_weight
- risk_metrics_weight
- opportunity_thresholds
- is_active

**Primary Key**

- strategy_id

**Foreign Keys**

- user_id → users.user_id

**Constraints**

- strategy_id must be unique and not null.
- user_id must not be null.
- profile must be one of the supported Strategy profiles.
- each Opportunity Score weight must be within the permitted range.
- the sum of all Opportunity Score weights must equal 100%.
- a User can only have one active Strategy at a time.
- predefined profiles can establish default weights.
- a Custom profile allows the User to modify the weights.

**Relationships**

- A Strategy belongs to one User.
- A Strategy is used to generate Opportunity Evaluations.

**Historical Considerations**

- Changing a Strategy does not modify historical Opportunity Evaluations.
- Previous Strategy configurations may be preserved for historical traceability.

### Watchlists

**Purpose**

Persist a collection of Stocks monitored by a User.

**Columns**

- watchlist_id
- user_id
- created_at
- updated_at

**Primary Key**

- watchlist_id

**Foreign Keys**

- user_id → users.user_id

**Constraints**

- watchlist_id must be unique and not null.
- user_id must not be null.
- created_at must not be null.
- updated_at must be greater than or equal to created_at when present.
- a User can have one main Watchlist in the initial version

**Relationships**

- A Watchlist belongs to one User.
- A Watchlist contains multiple Watchlist Items.

**Historical Considerations**

- The Watchlist persists independently from changes in the market data of its Stocks.

### Watchlists items

**Purpose**

Persist Stocks saved within a User's Watchlist.

**Columns**

- watchlist_item_id
- watchlist_id
- stock_id
- added_date
- reference_price

**Primary Key**

- watchlist_item_id

**Foreign Keys**

- watchlist_id → watchlists.watchlist_id
- stock_id → stocks.stock_id

**Constraints**

- watchlist_item_id must be unique and not null.
- watchlist_id must not be null.
- stock_id must not be null.
- added_date must not be null.
- reference_price must be greater than 0.
- watchlist_id + stock_id must be unique.

**Relationships**

- A Watchlist Item belongs to one Watchlist.
- A Watchlist Item references one Stock.

**Historical Considerations**

- Reference Price represents the market price when the Stock was added.
- Removing a Watchlist Item does not affect the associated Stock or its market information.

### News

**Purpose**

Persist relevant News used by InvestAI for historical analysis and traceability.

**Columns**

- news_id
- company_id
- title
- publication_date
- retrieved_at
- source
- url
- summary
- sentiment

**Primary Key**

- news_id

**Foreign Keys**

- company_id → companies.company_id

**Constraints**

- news_id must be unique and not null.
- company_id must not be null.
- title must not be null.
- publication_date must not be null.
- retrieved_at must not be null.
- source must not be null.
- url must not be null.
- url must be unique.
- sentiment must be POSITIVE, NEUTRAL or NEGATIVE.
- summary can be null.

**Relationships**

- A News item belongs to one Company.
- A Company can have multiple News items.
- A News item can be associated with multiple Opportunity Evaluations.
- A News item can be associated with multiple AI Analyses.

**Historical Considerations**

- News is not automatically persisted every time a Stock is analyzed.
- Relevant News is persisted when required for historical traceability.
- publication_date represents when the News was published.
- retrieved_at represents when InvestAI obtained the News.
- Persisted News should remain unchanged to preserve historical context.
- Duplicate News items should not be stored.