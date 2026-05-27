---
title: "Métricas y riesgos en carteras de fondos"
author: "efueyo"
date: "2026-05-27"
version: "1.0"
category: "tecnico"
tags:
  - metricas
  - riesgo
  - sharpe
  - drawdown
  - volatilidad
  - correlaciones
license: "CC BY-NC-SA 4.0"
---

---
title: "Métricas y riesgos en carteras de fondos"
author: "efueyo"
date: "2026-05-27"
version: "1.0"
category: "tecnico"
tags:
  - metricas
  - riesgo
  - sharpe
  - drawdown
  - volatilidad
  - correlaciones
  - fondos
license: "CC BY-NC-SA 4.0"
---

# Métricas y riesgos en carteras de fondos

Este documento resume las métricas cuantitativas más relevantes para evaluar carteras de fondos de inversión.  
Su objetivo es complementar la estrategia Barbell y Barbell Alpha con un marco técnico que permita:

- comparar fondos entre sí,  
- evaluar el riesgo real de la cartera,  
- entender la sensibilidad a tipos y spreads,  
- y tomar decisiones informadas de asignación.

---

## 1. Volatilidad anualizada

La volatilidad es la métrica base para clasificar fondos en buckets Barbell.



\[
\sigma_{anual} = \text{std}(r_{diarios}) \times \sqrt{252}
\]



Interpretación:

- **< 3%** → monetarios / ultracorto  
- **3–8%** → RF corto  
- **8–12%** → RF medio  
- **12–20%** → RF largo  
- **> 20%** → renta variable  

La volatilidad no mide pérdidas, sino **variabilidad**.

---

## 2. Drawdown y drawdown máximo

El drawdown mide la caída desde un máximo histórico:



\[
DD_t = \frac{V_t - \max(V_{0..t})}{\max(V_{0..t})}
\]



El **máximo drawdown (MDD)** es la peor caída registrada.

Interpretación:

- MDD bajo → fondo estable  
- MDD alto → fondo con riesgo estructural  

En fondos de renta fija, un MDD > 10% suele indicar:

- duración elevada,  
- riesgo de crédito,  
- o ambos.

---

## 3. Ratio Sharpe

Mide la rentabilidad ajustada por riesgo:



\[
Sharpe = \frac{R_p - R_f}{\sigma_p}
\]



Donde:

- \(R_p\) = rentabilidad del fondo  
- \(R_f\) = tipo libre de riesgo  
- \(\sigma_p\) = volatilidad  

Interpretación:

- **> 1.0** → excelente  
- **0.5–1.0** → aceptable  
- **< 0.5** → pobre  

En fondos de renta fija, un Sharpe alto suele indicar:

- buena gestión de duración,  
- carry estable,  
- baja volatilidad.

---

## 4. Ratio Sortino

Similar al Sharpe, pero penaliza solo la volatilidad negativa:



\[
Sortino = \frac{R_p - R_f}{\sigma_{downside}}
\]



Es más útil en fondos conservadores, donde la volatilidad al alza no es un problema.

---

## 5. Ratio Calmar

Relaciona rentabilidad con drawdown máximo:



\[
Calmar = \frac{R_{anual}}{|MDD|}
\]



Interpretación:

- **> 0.5** → robusto  
- **> 1.0** → excelente  

Muy útil para comparar fondos flexibles o mixtos.

---

## 6. Correlaciones

La correlación entre fondos permite:

- detectar redundancias,  
- evitar concentraciones ocultas,  
- construir carteras más diversificadas.

Interpretación:

- **> 0.8** → fondos casi idénticos  
- **0.4–0.7** → diversificación moderada  
- **< 0.3** → diversificación real  

En renta fija, correlaciones altas suelen indicar:

- duración similar,  
- exposición al mismo tipo de crédito.

---

## 7. Sensibilidad a tipos (duración)

La duración mide la sensibilidad del fondo a movimientos de tipos:



\[
\Delta P \approx -Duración \times \Delta Tipos
\]



Ejemplo:

- duración 5  
- subida de tipos +1%  

→ caída aproximada del **5%**.

La duración es clave en:

- Barbell clásica (corto vs largo),  
- Barbell Alpha (duración flexible).

---

## 8. Sensibilidad a spreads (crédito)

Los fondos de crédito no solo dependen de los tipos, sino también de los **spreads corporativos**.

Regla práctica:

- **Spreads estrechos (< 100 pb)** → poco margen, riesgo alto  
- **Spreads amplios (> 200 pb)** → oportunidad, riesgo controlado  

Los fondos con alta sensibilidad a spreads:

- high yield,  
- subordinados,  
- crédito oportunista,  
- fondos flexibles de renta fija.

---

## 9. Tracking error

Mide cuánto se desvía un fondo respecto a su índice de referencia:



\[
TE = \text{std}(R_p - R_{benchmark})
\]



Útil para:

- fondos indexados,  
- fondos de RF euro vs índice agregado,  
- comparar fondos similares.

---

## 10. Beta y volatilidad relativa

La beta mide la sensibilidad del fondo respecto al mercado:



\[
\beta = \frac{\text{Cov}(R_p, R_m)}{\sigma_m^2}
\]



Interpretación:

- **β < 0.5** → fondo defensivo  
- **β ≈ 1** → fondo direccional  
- **β > 1** → fondo agresivo  

En renta fija, la beta suele ser baja, salvo en:

- high yield,  
- fondos mixtos agresivos.

---

## 11. Colchón de tipos (regla práctica)

Del artículo de Antonio Dávila:



\[
\text{Pérdida máxima tolerable} \approx \frac{Yield}{Duración}
\]



Ejemplo:

- Yield 4%  
- Duración 5  

→ colchón ≈ 0.8% de subida de tipos antes de entrar en pérdidas.

---

## 12. Cómo usar estas métricas en Barbell‑Strategies

### **Barbell clásica**
- Volatilidad → clasificación en buckets  
- Duración → sensibilidad a tipos  
- Drawdown → estabilidad del fondo  
- Correlaciones → evitar duplicidades  

### **Barbell Alpha**
- Sharpe / Sortino → calidad del gestor  
- Calmar → robustez en crisis  
- Spreads → oportunidad en crédito  
- Beta → sensibilidad al mercado  
- Tracking error → consistencia  

---

## 13. Conclusión

Las métricas cuantitativas permiten evaluar la calidad y el riesgo real de una cartera de fondos.  
Combinadas con la estrategia Barbell y el análisis de curva de tipos, proporcionan un marco sólido para tomar decisiones informadas y gestionar el riesgo de forma disciplinada.

