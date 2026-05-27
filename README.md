 # Barbell‑Strategies  
### Gestión sistemática de carteras conservadoras basada en duración, curva de tipos y análisis cuantitativo

Barbell‑Strategies es un proyecto diseñado para ayudar a inversores conservadores y moderados a gestionar carteras de fondos de inversión de forma:

- sistemática  
- disciplinada  
- basada en datos  
- adaptada al ciclo económico  

El proyecto combina:

- reglas clásicas de gestión de duración,  
- señales macroeconómicas (curva de tipos),  
- principios de la estrategia Barbell,  
- un módulo cuantitativo para analizar carteras reales,  
- y una versión avanzada llamada **Barbell Alpha**.

El objetivo es ofrecer una metodología clara y reproducible para proteger el capital sin renunciar a oportunidades.

---

# 📌 Contenidos del proyecto

El repositorio incluye documentación completa, herramientas conceptuales y una presentación divulgativa.

## 📚 Documentación principal

| Documento | Descripción |
|----------|-------------|
| **[00_vision_general.md](docs/00_vision_general.md)** | Visión general del proyecto y sus objetivos. |
| **[01_reglas_barbell_fondos.md](docs/01_reglas_barbell_fondos.md)** | Reglas de la estrategia Barbell aplicadas a fondos UCITS. |
| **[02_estrategia_barbell_alpha.md](docs/02_estrategia_barbell_alpha.md)** | Versión avanzada y flexible de la Barbell clásica. |
| **[03_metricas_y_riesgos.md](docs/03_metricas_y_riesgos.md)** | Métricas cuantitativas para evaluar carteras de fondos. |
| **[04_barbell_alert_documentacion.md](docs/04_barbell_alert_documentacion.md)** | Documentación técnica del módulo Barbell Alert. |
| **[05_dinamica_seguimiento_inversor.md](docs/05_dinamica_seguimiento_inversor.md)** | Guía operativa para el seguimiento trimestral. |
| **[06_articulo_rankia.md](docs/06_articulo_rankia.md)** | Artículo editorial para Rankia. |
| **[07_presentacion_estrategia_barbell.md](docs/07_presentacion_estrategia_barbell.md)** | Presentación divulgativa de la estrategia Barbell. |

---

# 🧠 ¿Qué es la Estrategia Barbell?

La estrategia Barbell divide la cartera en dos extremos:

- **Muy corto plazo** → estabilidad, liquidez, protección ante subidas de tipos.  
- **Muy largo plazo** → convexidad, protección ante recesiones y bajadas de tipos.

Evita el tramo intermedio (5–7 años), que combina lo peor de ambos mundos.

La asignación se ajusta según el **semáforo de la curva de tipos**:

- 🟢 Empinándose → reducir duración  
- 🟡 Plana → Barbell equilibrada  
- 🔴 Invertida → aumentar duración larga  

---

# ⚙️ Barbell Alert — Motor cuantitativo

El módulo Barbell Alert permite:

- leer carteras reales desde Excel  
- cargar automáticamente los CSV de cada fondo  
- clasificar fondos por volatilidad (proxy de duración)  
- detectar el régimen de curva (T10Y2Y)  
- actualizar valores, pesos y plusvalías  
- simular tres estrategias:

  - Buy & Hold  
  - Barbell pasiva  
  - Barbell dinámica  

- calcular métricas clave (Sharpe, Calmar, MDD, volatilidad)  
- generar un informe claro con rebalanceos y recomendaciones  

---

# 🧩 Barbell Alpha — La evolución flexible

Barbell Alpha amplía la estrategia clásica con:

- duración flexible  
- crédito defensivo y oportunista  
- liquidez estratégica  
- señales macro ampliadas  
- gestión dinámica del riesgo  

Inspirada en fondos como DNCA Alpha Bonds, pero con reglas transparentes y reproducibles.

---

# 📁 Estructura del repositorio


```
Barbell-Strategies/
│
├── docs/
│   ├── 00_vision_general.md
│   ├── 01_reglas_barbell_fondos.md
│   ├── 02_estrategia_barbell_alpha.md
│   ├── 03_metricas_y_riesgos.md
│   ├── 04_barbell_alert_documentacion.md
│   ├── 05_dinamica_seguimiento_inversor.md
│   ├── 06_articulo_rankia.md
│   ├── 07_presentacion_estrategia_barbell.md
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
   - régimen de curva  
   - desviaciones respecto a la Barbell objetivo  
   - recomendaciones de rebalanceo  

4. Consulta la documentación en `/docs/` para interpretar resultados.  
5. Repite trimestralmente.

---

# 📄 Licencia

Este proyecto se distribuye bajo licencia:

**CC BY‑NC‑SA 4.0**  
Permite compartir y adaptar, siempre que:

- se cite al autor,  
- no haya uso comercial,  
- las obras derivadas mantengan la misma licencia.

---

# 🧭 Resumen para visitantes de GitHub

Barbell‑Strategies es una metodología moderna para gestionar carteras conservadoras en un entorno de tipos incierto.  
Combina análisis macro, reglas de duración y un motor cuantitativo para ofrecer una forma disciplinada y eficaz de proteger el capital sin renunciar a oportunidades.

