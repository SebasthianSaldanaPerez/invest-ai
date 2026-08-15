# Architecture

## Purpose

This document describes the initial software architecture of InvestAI.

The architecture is designed to separate business rules, application logic, user interface, external data sources and persistence concerns.

The initial version will use a modular monolith architecture to keep development simple while allowing future evolution.

## Architectural Style

InvestAI will initially use a Modular Monolith architecture.

The system will remain a single deployable application while separating responsibilities into clearly defined internal layers and modules.

Microservices will not be introduced unless future scalability or operational requirements justify the additional complexity.

## Main Layers

### Presentation Layer

Responsible for interaction between the user and the application.

Initial responsibilities:

- Web interface
- API endpoints
- Request validation
- Response formatting

### Application Layer

Responsible for coordinating application use cases.

Examples:

- Analyze Stock
- Register Trade
- Close Trade
- Manage Watchlist
- Generate Opportunity Evaluation
- Generate AI Analysis

### Domain Layer

Contains the core business concepts and rules of InvestAI.

Includes:

- Entities
- Value Objects
- Calculated Results
- Domain Services
- Business Rules

The Domain Layer must remain independent from frameworks, databases and external APIs.

### Infrastructure Layer

Responsible for communication with external technologies and services.

Examples:

- PostgreSQL
- Financial market APIs
- News providers
- LLM providers
- Logging
- External storage

## Application Use Cases

The Application Layer coordinates the actions that InvestAI can perform.

Initial use cases include:

- Analyze Stock
- Add Stock to Watchlist
- Remove Stock from Watchlist
- Register Trade
- Close Trade
- Get Personal Analytics
- Generate Opportunity Evaluation
- Generate AI Analysis
- Generate Performance Review
- Update Strategy
- Update User Profile

Application use cases orchestrate Domain objects and Infrastructure interfaces without containing persistence or external-provider implementation details.

## Ports and Interfaces

The Application Layer depends on abstractions instead of concrete infrastructure implementations.

### Repositories

Initial repository interfaces include:

- CompanyRepository
- StockRepository
- TradeRepository
- WatchlistRepository
- StrategyRepository
- HistoricalPriceRepository
- NewsRepository
- FinancialStatementRepository
- OpportunityEvaluationRepository
- AIAnalysisRepository

Repositories define how application use cases access and persist domain information without depending directly on PostgreSQL or another storage technology.

### External Providers

External data sources are accessed through provider interfaces.

Initial providers include:

- MarketDataProvider
- NewsProvider
- AnalystDataProvider
- LLMProvider

Provider interfaces isolate external APIs and services from the Application and Domain layers.

## Main Application Flows

### Register Trade

User
→ Web Interface
→ FastAPI
→ RegisterTrade
→ Trade
→ TradeRepository
→ PostgreSQLTradeRepository
→ PostgreSQL

### Analyze Stock

User
→ Dashboard
→ FastAPI
→ AnalyzeStock
→ Repositories / External Providers
→ Domain Data
→ Dashboard Response

External information may be obtained through:

- MarketDataProvider
- NewsProvider
- AnalystDataProvider

### Generate Opportunity Evaluation

User
→ GenerateOpportunityEvaluation
→ Strategy
→ Financial Indicators
→ Technical Indicators
→ News Sentiment
→ Analyst Consensus
→ Opportunity Calculator
→ Opportunity Evaluation
→ OpportunityEvaluationRepository

### Generate AI Analysis

User
→ GenerateAIAnalysis
→ AIAnalysisGenerator
→ LLMProvider
→ External LLM
→ AI Analysis
→ AIAnalysisRepository

## Dependency Direction

InvestAI dependencies should point toward the Domain Layer.

Presentation depends on Application.

Application depends on Domain abstractions.

Infrastructure implements interfaces required by Application and Domain.

The Domain Layer must not depend directly on frameworks, databases or external APIs.