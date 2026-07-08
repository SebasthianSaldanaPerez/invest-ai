Sesión 003 — Diseño de la Experiencia de Usuario (UX) y Wireframes
Fecha: 07 de Julio de 2026

Objetivo: Definir la experiencia de usuario (UX) y el diseño funcional de la primera versión de InvestAI mediante la creación de los layouts de cada módulo principal. El objetivo fue establecer el flujo de navegación, la responsabilidad de cada pantalla y la información que mostrará cada una antes de comenzar el diseño del dominio y el desarrollo técnico.

Aprendizajes
-Comprendí la importancia de diseñar primero el producto antes de escribir código.
-Aprendí que cada pantalla debe responder una necesidad específica del usuario y evitar responsabilidades innecesarias.
-Entendí que la información mostrada en un dashboard debe justificar su existencia aportando valor para la toma de decisiones.
-Descubrí la diferencia entre información almacenada e información calculada dinámicamente.
-Aprendí que muchas variables pueden persistirse en la base de datos sin necesidad de mostrarlas en la interfaz.
-Comprendí que el sistema debe crecer junto con mi conocimiento sobre inversiones, incorporando nuevos indicadores conforme los vaya aprendiendo.
-Confirmé la importancia de documentar las decisiones de diseño desde el inicio del proyecto.

Temas resueltos
-Dashboard
    Se definió la estructura principal del Dashboard.
    Se organizó la información siguiendo el flujo natural de análisis de un inversionista.
    Se establecieron ocho secciones principales:
        Company Overview
        Market Snapshot
        Price Chart
        News & Market Sentiment
        Financial Overview
        Key Indicators
        Opportunity Score
        AI Analysis
-Investment Journal
    Se redefinió el propósito del Journal como un registro de decisiones de inversión y no como un control de portafolio.
    Se simplificó el formulario de registro de operaciones.
    Se estableció el flujo para abrir y cerrar operaciones.
    Se definieron los datos calculados automáticamente (P&L y Holding Time).
    Se acordó almacenar información adicional (sector, industria, etc.) aunque no sea visible para el usuario.
-Watchlist
    Se decidió que las empresas se agregan desde el Dashboard mediante un botón de favoritos.
    Se estableció que la Watchlist únicamente almacenará la empresa y un precio de referencia.
    Se definió que la información de mercado siempre será obtenida dinámicamente mediante la API.
    Se simplificó la pantalla eliminando información innecesaria.
-Personal Analytics
    Se diseñó un módulo enfocado en Business Intelligence personal.
    Se definieron indicadores generales del rendimiento histórico.
    Se incorporó una gráfica de evolución del rendimiento.
    Se añadieron rankings de mejores y peores operaciones.
    Se incorporó un módulo de análisis generado por IA sobre el desempeño del inversionista.
-Strategy Settings
    Se definió la pantalla para personalizar la estrategia de inversión.
    Se propuso el uso de perfiles de inversionista (Conservative, Balanced, Aggressive y Custom).
    Se decidió configurar pesos para los factores del Opportunity Score en lugar de reglas rígidas.
    Se identificó esta pantalla como el punto de personalización principal del sistema.
-User Profile
    Se diseñó la pantalla para administrar la información del usuario.
    Se separó la configuración personal de la configuración estratégica.
    Se definieron preferencias relacionadas con la interacción con la IA.
-Documentación
    Se estableció la estructura definitiva del documento ui-layouts.md.
    Se documentó cada módulo utilizando una estructura uniforme basada en:
        Purpose
        Displayed Information
        Future Enhancements
    Se reforzó el uso del Decision Log para registrar decisiones arquitectónicas y funcionales importantes.

Conclusión

Durante esta sesión se completó el diseño funcional de la primera versión de InvestAI. Antes de iniciar el desarrollo técnico, el proyecto ya cuenta con una estructura clara de módulos, flujos de navegación y responsabilidades, reduciendo significativamente la incertidumbre en las siguientes etapas del desarrollo.