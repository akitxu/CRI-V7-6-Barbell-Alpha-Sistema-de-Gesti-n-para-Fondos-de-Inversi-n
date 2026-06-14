# Barbell‑Strategies  
### Gestión sistemática de carteras conservadoras basada en análisis cuantitativo y asignación dinámica

Barbell‑Strategies es un proyecto diseñado para ayudar a inversores conservadores y moderados a gestionar carteras de fondos de inversión de forma:

- sistemática  
- disciplinada  
- basada en datos  
- adaptada al entorno de mercado  

El proyecto combina:

- reglas clásicas de gestión Barbell,  
- clasificación de fondos por buckets de riesgo,  
- un motor técnico avanzado para detectar regímenes de mercado,  
- un módulo cuantitativo para analizar carteras reales,  
- y una versión evolucionada llamada **CRI V7‑6 Barbell_Alpha**.

El objetivo es ofrecer una metodología clara y reproducible para proteger el capital sin renunciar a oportunidades.

---

# 📌 Contenidos del proyecto

El repositorio incluye documentación completa, herramientas conceptuales y una presentación divulgativa.

## 📚 Documentación principal

| Documento / Celda | Descripción |
|-------------------|-------------|
| **[arquitectura_barbell_V7‑6.md](docs/arquitectura_barbell_V7‑6.md)** | Arquitectura general del sistema CRI V7‑6 Barbell_Alpha. |
| **[Barbell_Clásica_vs_Barbell_Alpha.md](docs/Barbell_Clásica_vs_Barbell_Alpha.md)** | Celda 0 — Comparativa conceptual entre Barbell Clásica y Barbell Alpha. |
| **Celda 1** | Carga de datos y estructura base del proyecto. |
| **Celda 2** | Definición de constantes, parámetros y configuración global. |
| **Celda 3** | Simuladores básicos y funciones auxiliares. |
| **Celda 4** | Comparativa Alpha inicial y métricas fundamentales. |
| **Celda 5** | Motor técnico avanzado basado en AnalizadorMercado. |
| **Celda 6** | Preparación de buckets y clasificación de fondos. |
| **Celda 7** | Pipeline PRO y depuración de la arquitectura. |
| **Celda 8** | Ejecución de simulaciones completas. |
| **Celda 9** | Cálculo de métricas cuantitativas (Sharpe, MDD, Calmar…). |
| **Celda 10** | Gráficos y visualización de resultados. |
| **Celda 11** | Diagnóstico estructural y análisis de riesgo. |
| **Celda 12** | Pipeline completo de la estrategia. |
| **Celda 13** | Automatización del flujo de trabajo. |
| **Celda 14** | Capítulo 14 — Documentación narrativa. |
| **Celda 15** | Capítulo 15 — Conclusiones y futuras extensiones. |
| **Celda 16** | Capítulo 16 — Cómo debe utilizar un inversor la estrategia. |
| **Celda 17** | Pipeline operativo (reglas del inversor). |
| **Celda 18** | Dashboard operativo y presentación de resultados. |
---

# 🧠 ¿Qué es la Estrategia Barbell?

La estrategia Barbell divide la cartera en dos extremos:

- **Muy corto plazo** → estabilidad, liquidez, baja volatilidad.  
- **Muy largo plazo** → convexidad, crecimiento y protección en crisis.

Evita el tramo intermedio, donde se concentra el riesgo menos compensado.

En esta versión, la asignación se supervisa mediante:

- **clasificación por buckets de riesgo**,  
- **desviaciones respecto a la Barbell Clásica**,  
- **régimen de mercado detectado por el motor técnico**.

---

# ⚙️ Barbell Alert — Motor cuantitativo

El módulo Barbell Alert permite:

- leer carteras reales desde Excel  
- cargar automáticamente los CSV de cada fondo  
- clasificar fondos por volatilidad (proxy de riesgo)  
- detectar el régimen de mercado mediante un motor técnico avanzado  
- actualizar valores, pesos y plusvalías  
- simular tres estrategias:

  - Buy & Hold  
  - Barbell pasiva  
  - Barbell Alpha (CRI V7‑6)

- calcular métricas clave (Sharpe, Calmar, MDD, volatilidad)  
- generar un informe claro con rebalanceos y recomendaciones  

---

# 🧩 CRI V7‑6 Barbell_Alpha — La evolución flexible

CRI V7‑6 Barbell_Alpha amplía la estrategia clásica con:

- asignación dinámica según régimen de mercado  
- sensibilidad táctica sin market timing agresivo  
- reglas transparentes y reproducibles  
- gestión disciplinada del riesgo  
- estructura modular y auditable  

Inspirada en la filosofía Barbell, pero adaptada a carteras reales de fondos de inversión.

---

# 📁 Estructura del repositorio

```
Barbell-Strategies/
│
├── docs/
│   ├── Introducción. Arquitectura general.
│   ├── 00_Barbell Clásica versus Barbell Alpha
│   ├── 01_Constantes globales
│   ├── 02_CLASIFICADORES (Clásico + Alpha + Mixta SAFE/RISK)
│   ├── 03_Carga de datos + asignación de buckets
│   ├── 04_SIMULADOR CLÁSICO PRO (Buy&Hold + Barbell Clásica)
│   ├── 05_SIMULADOR ALPHA (con MacroAlpha híbrido)
│   ├── 06_MÉTRICAS Y TABLA FINAL (SIN ComparativaAlpha)
│   ├── 07_PIPELINE PRO (EJECUCIÓN COMPLETA Y DEPURACIÓN) 
│   ├── 08_ GRÁFICOS + TABLA FINAL + REBALANCEOS 
│   ├── 09_EXPORTACIÓN A EXCEL Y CSV 
│   ├── 10_INFORME PDF AUTOMÁTICO 
│   ├── 11_DASHBOARD INTERACTIVO PLOTLY 
│   ├── 12_CELDA 12 — PIPELINE COMPLETO PRO (ONE-SHOT LIMPIO) 
│   ├── 13_ALERTA BARBELL ALPHA (motor técnico) 
│   ├── 14_ALERTA BARBELL CLÁSICA (PRO FINAL)¶ 
│   ├── 15_Conclusiones y Futuras Extensiones 
│   ├── 16_CÓMO DEBE UTILIZAR UN INVERSOR LA ESTRATEGIA BARBELL CRI V7‑6 
│   ├── 17_PIPELINE OPERATIVO (REGLAS DEL INVERSOR) 
│   ├── 18_Automatizar las 5 reglas operativas del inversor 
│   └── img/
│
├── src/                # Código fuente del motor cuantitativo
├── data/               # CSV de fondos
├── notebooks/          # Jupyter Notebooks de análisis
└── README.md
```
---

# 🚀 Guía rápida de uso

1. Actualiza los CSV de tus fondos en `/data/`.  
2. Ejecuta el módulo Barbell Alert.  
3. Revisa:

   - clasificación por buckets  
   - régimen de mercado  
   - desviaciones respecto a la Barbell objetivo  
   - recomendaciones de rebalanceo  

4. Consulta la documentación en `/docs/` para interpretar resultados.  
5. Repite periódicamente.

---

# 📄 Licencia

Este proyecto se distribuye bajo licencia:

**CC BY‑NC‑SA 4.0**  
Permite compartir y adaptar, siempre que:

- se cite al autor,  
- no haya uso comercial,  
- las obras derivadas mantengan la misma licencia.

---

# Disclaimer  
Este proyecto es experimental y se ofrece únicamente con fines educativos y de investigación.  
No constituye asesoramiento financiero ni una recomendación de inversión.  
El autor no garantiza la exactitud, integridad o idoneidad del contenido y no asume ninguna responsabilidad por pérdidas derivadas de su uso.

---

# 🧭 Resumen para visitantes de GitHub

Barbell‑Strategies es una metodología moderna para gestionar carteras conservadoras en un entorno incierto.  
Combina análisis cuantitativo, reglas Barbell y un motor técnico de regímenes para ofrecer una forma disciplinada y eficaz de proteger el capital sin renunciar a oportunidades.

---

# 📄 Licencia

Este proyecto se distribuye bajo licencia:

**CC BY‑NC‑SA 4.0**  
Permite compartir y adaptar, siempre que:

- se cite al autor,  
- no haya uso comercial,  
- las obras derivadas mantengan la misma licencia.

---
# Disclaimer  
Este proyecto es experimental y se ofrece únicamente con fines educativos y de investigación.
No constituye asesoramiento financiero ni una recomendación de inversión.
El autor no garantiza la exactitud, integridad o idoneidad del contenido y no asume ninguna responsabilidad por pérdidas derivadas de su uso.
# 🧭 Resumen para visitantes de GitHub

Barbell‑Strategies es una metodología moderna para gestionar carteras conservadoras en un entorno de tipos incierto.  
Combina análisis macro, reglas de duración y un motor cuantitativo para ofrecer una forma disciplinada y eficaz de proteger el capital sin renunciar a oportunidades.

