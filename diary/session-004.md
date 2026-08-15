# Session 004 - Domain Model and Initial Architecture

## Objetivo

Transformar el diseño funcional definido en sesiones anteriores en un primer modelo de dominio y una arquitectura conceptual para InvestAI.

El objetivo principal fue identificar los conceptos que existen dentro del dominio, definir sus responsabilidades y relaciones, y establecer una arquitectura inicial que permita implementar el sistema de forma modular y desacoplada.

## Temas trabajados

### Domain Model

Se identificaron y clasificaron los principales conceptos del dominio de InvestAI en diferentes categorías:

- Entities
- Value Objects
- Calculated Results
- Domain Services

También se organizaron los conceptos en diferentes áreas:

- Market Intelligence
- Investment Decision Support
- Personal Investment Intelligence
- User Management

Se documentaron para los principales conceptos:

- Purpose
- Main Attributes
- Relationships
- Business Rules

Entre los conceptos modelados se encuentran:

- Company
- Stock
- Historical Price
- News
- Analyst Consensus
- Financial Statement
- Trade
- User
- Strategy
- Watchlist
- Watchlist Item
- AI Analysis
- Performance Review
- Technical Indicator
- Financial Indicator
- Opportunity Evaluation
- Performance Analytics
- Investment Pattern

### Domain Relationships

Se creó un primer mapa conceptual de relaciones entre los diferentes elementos del dominio.

Esto permitió visualizar cómo la información fluye desde los datos de mercado hasta el análisis de decisiones personales.

De forma general:

Market Data
→ Analysis
→ Opportunity Evaluation
→ Investment Decision
→ Trade
→ Personal Analytics
→ Investment Patterns

### Initial Architecture

Se definió una arquitectura inicial basada en un Modular Monolith.

Se establecieron cuatro capas principales:

- Presentation
- Application
- Domain
- Infrastructure

Se definió la responsabilidad general de cada capa y se estableció que el Domain debe permanecer independiente de frameworks, bases de datos y proveedores externos.

### Application Use Cases

Se identificaron los principales casos de uso que serán coordinados por la Application Layer.

Entre ellos:

- Analyze Stock
- Register Trade
- Close Trade
- Add Stock to Watchlist
- Remove Stock from Watchlist
- Get Personal Analytics
- Configure Strategy
- Generate Opportunity Evaluation
- Generate AI Analysis
- Generate Performance Review
- Update User Profile

### Repositories and Providers

Se introdujo el concepto de Repository como una abstracción que define las operaciones necesarias para almacenar y recuperar información sin depender directamente de una tecnología de persistencia.

Ejemplo:

TradeRepository
→ PostgreSQLTradeRepository
→ PostgreSQL

También se diferenciaron los Repositories de los Providers.

Repositories:
Acceso y persistencia de información propia del sistema.

Providers:
Comunicación con servicios externos.

Ejemplos:

- MarketDataProvider
- NewsProvider
- AnalystDataProvider
- LLMProvider

### Application Flows

Se analizaron los flujos arquitectónicos de algunos de los principales casos de uso:

- Register Trade
- Analyze Stock
- Generate Opportunity Evaluation
- Generate AI Analysis

Esto permitió visualizar cómo una acción del usuario atraviesa las diferentes capas del sistema.

## Aprendizajes

- Comprendí que una Entity representa un concepto con identidad dentro del dominio y no una pantalla de la aplicación.
- Aprendí a diferenciar Entities, Value Objects, Calculated Results y Domain Services.
- Comprendí que las reglas relacionadas con la interfaz no deben formar parte de las Business Rules del dominio.
- Aprendí la diferencia entre Company y Stock.
- Comprendí la diferencia entre Technical Indicators y Financial Indicators.
- Aprendí que los datos calculados no necesariamente deben almacenarse como atributos de las entidades que los originan.
- Comprendí la función de las capas Presentation, Application, Domain e Infrastructure.
- Aprendí que la Application Layer coordina casos de uso, mientras que el Domain contiene las reglas y conceptos principales del negocio.
- Comprendí el propósito de los Repositories y cómo permiten desacoplar la lógica de negocio de la base de datos.
- Aprendí la diferencia entre una abstracción como TradeRepository y una implementación concreta como PostgreSQLTradeRepository.
- Comprendí el propósito de los Providers para desacoplar InvestAI de APIs y servicios externos.
- Comprendí de forma inicial el principio de Dependency Inversion.
- Aprendí que la arquitectura debe permitir cambiar tecnologías externas sin modificar las reglas principales del dominio.

## Resultado de la sesión

Se completó la primera versión del Domain Model de InvestAI y se definió la arquitectura conceptual inicial del sistema.

InvestAI cuenta ahora con una separación inicial entre:

- El dominio del negocio.
- Los casos de uso de la aplicación.
- La interacción con el usuario.
- La infraestructura y servicios externos.

Esta estructura servirá como base para diseñar posteriormente la persistencia de datos y comenzar la implementación técnica del sistema.

## Próxima sesión

Session 005 - Data Persistence and Database Design

El siguiente objetivo será determinar qué información del Domain Model debe persistirse, cómo se relacionará en PostgreSQL y cómo transformar el modelo conceptual en un primer modelo de datos.