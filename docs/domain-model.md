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

# Core Entities

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

# Calculated Results

## Technical Indicator

...

## Financial Indicator

...

## Opportunity Evaluation

...

## Performance Analytics

...

## Investment Pattern

# Domain Services

## Market Data Collector

...

## AI Analysis Generator

...

## Performance Review Generator

...

## Opportunity Calculator

...

## Technical Indicator Calculator

...

## Financial Indicator Calculator

...

---

# Relationships