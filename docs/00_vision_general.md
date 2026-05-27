---
title: "Visión general del proyecto Barbell‑Strategies"
author: "efueyo"
date: "2026-05-27"
version: "1.0"
category: "documentacion"
tags:
  - vision
  - barbell
  - fondos
  - gestion-patrimonial
  - curva-de-tipos
license: "CC BY-NC-SA 4.0"
---

# Visión general del proyecto Barbell‑Strategies

Barbell‑Strategies es un proyecto diseñado para ayudar al inversor a **gestionar carteras de fondos de inversión** de forma sistemática, disciplinada y adaptada al entorno macroeconómico. Su objetivo es ofrecer una metodología clara, reproducible y basada en datos para tomar decisiones de asignación de activos sin caer en el ruido del mercado ni en la intuición subjetiva.

El proyecto combina tres pilares:

1. **Reglas estratégicas basadas en la curva de tipos y la duración.**  
2. **Herramientas cuantitativas para analizar carteras reales de fondos.**  
3. **Una dinámica de seguimiento trimestral simple y accionable.**

---

## 1. ¿Qué problema resuelve?

Los inversores en fondos de inversión se enfrentan a tres dificultades recurrentes:

- **No saber si su cartera está alineada con el entorno de tipos.**  
- **No tener una metodología clara para decidir cuándo mover pesos.**  
- **No disponer de herramientas para actualizar y analizar su cartera de forma objetiva.**

Barbell‑Strategies resuelve estos problemas mediante:

- un **semáforo macro** basado en la curva T10Y2Y,  
- una **estrategia Barbell** adaptada a fondos UCITS,  
- un **módulo de análisis automático** que actualiza la cartera y genera alertas,  
- y una **guía operativa trimestral** para el inversor.

---

## 2. ¿Para quién está pensado?

Este proyecto está diseñado para:

- inversores conservadores o moderados,  
- que gestionan carteras de fondos de inversión,  
- que buscan una metodología clara y sistemática,  
- que quieren evitar el trading excesivo,  
- y que desean adaptar su cartera al ciclo económico sin complicaciones.

No es un sistema de trading, ni un modelo de predicción, ni un algoritmo de alta frecuencia.  
Es una **herramienta de gestión patrimonial**.

---

## 3. Componentes principales del proyecto

### **[1. Reglas Barbell para fondos](ca://s?q=Reglas_barbell_fondos)**  
Documento conceptual que explica:

- cómo asignar duración según el entorno de tipos,  
- cómo interpretar la curva 10Y–2Y,  
- cómo aplicar la estrategia Barbell a fondos UCITS,  
- cómo usar la liquidez como activo estratégico.

### **[2. Barbell Alert — documentación técnica](ca://s?q=Documentacion_barbell_alert)**  
El módulo que:

- actualiza automáticamente la cartera desde los CSV,  
- clasifica los fondos por volatilidad/duración,  
- detecta el régimen de curva,  
- calcula desviaciones respecto a la Barbell óptima,  
- genera alertas claras de “AUMENTAR / REDUCIR”.

### **[3. Dinámica de seguimiento del inversor](ca://s?q=Dinamica_seguimiento_inversor)**  
Guía operativa que explica:

- qué hacer cada trimestre,  
- cuándo actuar y cuándo esperar,  
- cómo registrar aportaciones y traspasos,  
- cómo interpretar el semáforo Barbell,  
- qué señales extraordinarias requieren acción inmediata.

### **[4. Estrategia Barbell Alpha](ca://s?q=Estrategia_Barbell_Alpha)** *(en desarrollo)*  
La evolución natural de la Barbell clásica:

- duración flexible,  
- crédito defensivo y oportunista,  
- liquidez estratégica,  
- reglas macro ampliadas,  
- enfoque similar a fondos flexibles tipo DNCA Alpha Bonds.

### **[5. Métricas y riesgos](ca://s?q=Metricas_y_riesgos)** *(en desarrollo)*  
Documento técnico que cubrirá:

- Sharpe, Sortino, Calmar,  
- drawdown, volatilidad, correlaciones,  
- riesgo de duración y riesgo de crédito,  
- sensibilidad a tipos y spreads.

### **[6. Artículo Rankia](ca://s?q=Articulo_Rankia)** *(en desarrollo)*  
Versión editorial y didáctica para publicación.

---

## 4. Filosofía del proyecto

Barbell‑Strategies se basa en tres principios:

### **1. Simplicidad operativa**  
El inversor solo necesita:

- actualizar datos,  
- ejecutar el análisis,  
- leer el semáforo,  
- decidir si actuar o esperar.

### **2. Adaptación al ciclo económico**  
La curva de tipos es el mejor indicador adelantado del régimen macro.  
El sistema ajusta la duración y los pesos según:

- curva empinándose,  
- curva plana,  
- curva invertida.

### **3. Protección + opcionalidad**  
La esencia Barbell:

- **protección** → monetarios y RF corta,  
- **convexidad** → RF larga,  
- **equilibrio** → RF media y flotantes.

---

## 5. ¿Cómo se usa el proyecto?

El flujo típico es:

1. Descargar los CSV actualizados de los fondos.  
2. Ejecutar `BarbellAlert` con `actualizar_excel=True`.  
3. Leer el informe:  
   - régimen de curva,  
   - pesos actuales vs objetivos,  
   - alertas por bucket.  
4. Decidir si actuar según la desviación.  
5. Registrar aportaciones o traspasos si procede.  
6. Repetir cada trimestre.

---

## 6. Estado actual del proyecto

| Componente | Estado |
|-----------|--------|
| Barbell clásica | ✔ Completa |
| Barbell Alert | ✔ Completo |
| Reglas Barbell | ✔ Completo |
| Dinámica de seguimiento | ✔ Completo |
| Barbell Alpha | ⏳ En desarrollo |
| Métricas y riesgos | ⏳ En desarrollo |
| Artículo Rankia | ⏳ En desarrollo |

---

## 7. Licencia

Este proyecto se distribuye bajo licencia **CC BY‑NC‑SA 4.0**, lo que permite:

- compartir,  
- adaptar,  
- reutilizar,  

siempre que:

- se cite al autor,  
- no haya uso comercial,  
- y las obras derivadas mantengan la misma licencia.

---

## 8. Conclusión

Barbell‑Strategies es una herramienta completa para gestionar carteras de fondos de inversión de forma sistemática, disciplinada y adaptada al ciclo económico.  
Combina reglas claras, análisis cuantitativo y una dinámica operativa simple que permite al inversor tomar decisiones informadas sin caer en el ruido del mercado.

