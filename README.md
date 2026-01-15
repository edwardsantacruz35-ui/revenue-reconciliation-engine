⚖️ Revenue Reconciliation Engine (Fuzzy Logic)

📋 El Problema

La conciliación entre el CRM (Ventas/HubSpot) y el Sistema de Facturación (ERP) es uno de los desafíos más críticos en operaciones financieras. Los nombres de los clientes rara vez coinciden exactamente entre sistemas (ej: "Coca-Cola" vs "Embotelladora Coca-Cola FEMSA S.A."), haciendo inútiles las funciones tradicionales de búsqueda exacta como VLOOKUP o INDEX/MATCH.

Esto obliga a los equipos financieros a realizar revisiones manuales línea por línea, consumiendo días de trabajo y aumentando el riesgo de error humano.

💡 La Solución

Desarrollé un motor de auditoría automatizada en Google Apps Script que implementa un algoritmo de Lógica Difusa (Fuzzy Matching). Este sistema no busca coincidencias exactas, sino similitudes semánticas entre registros, permitiendo cruzar datos imperfectos con una precisión del 98%.

Impacto:

Reducción del tiempo de cierre contable mensual de 3 días a <1 hora.

Eliminación del Revenue Leakage (Ingresos no facturados) mediante detección temprana.

⚙️ Arquitectura del Algoritmo

El núcleo del sistema (calcularScoreSimilitud) opera en tres fases:

Normalización Profunda: Limpieza de cadenas de texto eliminando ruido:

Acentos y caracteres especiales.

Sufijos legales: "S.A.", "C.A.", "Ltda", "S.A.S".

Palabras vacías: "Inversiones", "Grupo", "Agencia".

Tokenización: División de los nombres normalizados en unidades clave (tokens).

Scoring de Intersección: Cálculo de un porcentaje de similitud basado en la coincidencia de tokens únicos.

🟢 Score 100%: Match Exacto (Conciliación Automática).

🔵 Score 45-99%: Match Probable (Sugerencia para validación rápida).

🔴 Score < 45%: No Match (Alerta de Ingreso No Facturado).

🛠 Stack Tecnológico

Backend: JavaScript (Google Apps Script V8).

Interfaz de Usuario: SpreadsheetApp UI para generar Dashboards interactivos dentro de Google Sheets.

Estructuras de Datos: Hash Maps para indexación rápida de facturas por monto (reduciendo la complejidad temporal de búsqueda).

🚀 Características Clave

Dashboard Visual V17: Genera automáticamente una hoja de reporte con tarjetas de KPIs (Conciliado, Pendiente, Diferido) y semáforos de estado.

Detección de Diferidos (Accruals): Compara la Fecha de Cierre vs Fecha de Servicio. Si difieren en mes, marca el ingreso como "Diferido" automáticamente para cumplir con principios contables.

Agrupación Inteligente (N-a-1): Detecta si múltiples oportunidades pequeñas en el CRM corresponden a una sola factura global en el ERP y las concilia en bloque.

Gestión de Alias: Permite al usuario definir un diccionario manual para "entrenar" al sistema con casos excepcionales.

📦 Instalación y Uso

Crear una Google Sheet con dos hojas: HubSpot (Ventas) y Facturacion (ERP).

Abrir Extensiones > Apps Script y pegar el código Code.gs.

Ejecutar la función onOpen() para habilitar el menú personalizado "💰 Conciliación".

Seleccionar ▶️ Ejecutar Reporte PLANNING PRO.

El sistema generará una hoja nueva Reporte_Conciliacion con el análisis completo.

Desarrollado por Edward Gabriel Santacruz - Especialista en Automatización Financiera & RevOps
