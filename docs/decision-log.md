DA-001

InvestAI será una aplicación web.

Razón:

Acceso desde cualquier dispositivo.
Mejor separación entre frontend y backend.
Arquitectura más profesional.
Compatible con futuras expansiones.

DA-002

PostgreSQL será la base de datos inicial.

Razón:

Los datos financieros son altamente relacionales y PostgreSQL ofrece un excelente equilibrio entre potencia, estabilidad y aprendizaje.

DA-003

El proyecto se desarrollará por versiones incrementales.

Nunca intentaremos construir el sistema completo de una sola vez.

DA-004

Cada sesión terminará con una bitácora y un commit.

DA-005

El Dashboard será el centro del sistema.

No mostrará estadísticas del usuario.

Mostrará la acción que se está analizando.

DA-006

InvestAI no trabajará con datos en tiempo real.

Las actualizaciones serán bajo demanda o mediante procesos ETL programados.

DA-007

InvestAI registrará operaciones de inversión, no administrará posiciones como un broker.

DA-008 

El desarrollo de InvestAI estará guiado por historias de usuario (User Stories), priorizando las necesidades del inversionista antes que la implementación técnica.

DA-009

El flujo del Dashboard seguirá el proceso natural de análisis de un inversionista.

DA-010

El Opportunity Score será configurable mediante reglas definidas por el usuario.

DA-011

InvestAI no mostrará información porque exista. Mostrará información porque ayuda al inversionista a tomar una decisión.

DA-012

La lista de seguimiento almacena empresas, no el historial del mercado. La lista de seguimiento solo almacenará el identificador de la empresa y el precio de referencia en el momento en que se añada la empresa. La información actual del mercado se obtendrá siempre de forma dinámica a partir de fuentes de datos externas.