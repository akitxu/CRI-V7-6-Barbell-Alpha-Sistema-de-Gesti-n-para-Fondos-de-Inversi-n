---
title: "Presentación de la Estrategia Barbell"
author: "efueyo"
date: "2026-05-27"
version: "1.0"
category: "presentacion"
tags:
  - barbell
  - renta-fija
  - fondos
  - curva-de-tipos
  - duracion
license: "CC BY-NC-SA 4.0"
---

# Estrategia Barbell  
## ¿Está mi cartera preparada para la realidad de los mercados de deuda?

Durante años, los fondos de renta fija fueron sinónimo de estabilidad.  
Pero desde 2021, los mercados de bonos han demostrado que también pueden generar pérdidas históricas cuando los tipos de interés cambian de dirección.

La pregunta clave para un inversor conservador es:

> **¿Mi cartera está realmente preparada para el entorno actual de tipos y para lo que pueda venir?**

Con ayuda de la IA, he desarrollado una metodología que combina:

- reglas clásicas de gestión de duración,  
- señales macroeconómicas (curva de tipos),  
- principios de la estrategia Barbell,  
- y un simulador cuantitativo para comparar estrategias.

El resultado es una herramienta práctica que cualquier inversor puede aplicar.

---

# 1. La regla de duración: evitar el “terreno de nadie”

En renta fija, la duración es el corazón del riesgo.

El tramo 5–7 años es el peor lugar para un inversor conservador:

- Si los tipos suben → cae, pero no lo suficiente para compensar.  
- Si los tipos bajan → sube, pero menos que los bonos largos.

Por eso la estrategia moderna polariza la duración:

- **Muy corto plazo** (monetarios, flotantes, RF < 2 años) → estabilidad.  
- **Muy largo plazo** (> 10 años) → convexidad y protección en recesiones.

Esta es la base de la Estrategia Barbell.

---

# 2. El semáforo de la curva de tipos: la brújula del mercado

La curva T10Y2Y es uno de los indicadores más fiables del ciclo económico.

### 🟢 Curva empinándose  
El largo paga más que el corto.  
→ Reducir duración, aumentar monetarios.

### 🟡 Curva plana  
Máxima incertidumbre.  
→ Aplicar Barbell clásica.

### 🔴 Curva invertida  
El corto paga más que el largo.  
→ Aumentar duración larga para capturar la futura caída de tipos.

El sistema descarga automáticamente T10Y2Y desde FRED y detecta el régimen actual.

---

# 3. La Estrategia Barbell: proteger capital sin renunciar a oportunidades

La Barbell divide la cartera en dos extremos:

- **50% Monetarios / RF muy corto** → base segura.  
- **25% Bonos flotantes** → seguro ante subidas de tipos.  
- **15% Renta fija intermedia** → algo de rentabilidad sin excesivo riesgo.  
- **10% Renta fija larga** → escudo ante recesiones.

Los pesos se ajustan según el semáforo de la curva.

---

# 4. El “colchón de tipos”: por qué hoy la renta fija es más segura que en 2021

En 2021 los tipos estaban al 0%.  
Hoy, con tipos en torno al 4%, el cupón actúa como airbag.

Ejemplo:

- Duración: 5  
- Cupón: 4%  

Los tipos tendrían que subir **0,8%** para que el fondo empiece a perder dinero.

---

# 5. Señal técnica de salida: cuándo protegerse

El sistema CRI identifica momentos de riesgo elevado:

- el precio deja de subir,  
- las medias se cruzan,  
- el precio rompe a la baja.

Cuando ocurre → **salir a liquidez**.

---

# 6. La liquidez como activo estratégico

Con monetarios pagando 3–4%, la liquidez ya no es “estar fuera del mercado”.  
Es una decisión activa y rentable en entornos inciertos.

---

# 7. El motor cuantitativo: cómo analizamos una cartera real

El sistema:

- lee la cartera desde Excel,  
- carga automáticamente los CSV de cada fondo,  
- clasifica fondos por volatilidad,  
- detecta el régimen de curva,  
- actualiza valores, pesos y plusvalías,  
- simula tres estrategias:

  - Buy & Hold  
  - Barbell pasiva  
  - Barbell dinámica  

- calcula métricas clave:

  - rentabilidad total  
  - anualizada  
  - drawdown  
  - Sharpe  
  - Calmar  
  - volatilidad  

- genera un informe claro con rebalanceos y recomendaciones.

---

# 8. ¿Qué obtiene un gestor conservador con este sistema?

- Una foto real y actualizada de su cartera.  
- Un diagnóstico objetivo del riesgo de duración.  
- Una recomendación basada en datos.  
- Una simulación histórica de estrategias.  
- Una guía clara para actuar según la curva.

---

# 9. ¿Qué son los buckets?

Un bucket es una categoría basada en **volatilidad anualizada**, que actúa como proxy de duración real.

### ¿Por qué volatilidad y no duración declarada?

Porque:

- la duración oficial no siempre es fiable,  
- la volatilidad se calcula directamente de los precios,  
- existe relación directa entre duración y volatilidad.

### Buckets

| Categoría     | Volatilidad | Ejemplos |
|---------------|-------------|----------|
| MONETARIO     | < 3%        | monetarios, letras |
| RF_CORTO      | 3–8%        | bonos 1–3 años |
| RF_MEDIO      | 8–12%       | bonos 3–7 años |
| RF_LARGO      | 12–20%      | bonos 10–30 años |
| RENTA_VARIABLE| > 20%       | acciones |

---

# 10. Cómo afectan los tipos a cada bucket

### Si los tipos suben:

- Monetario → casi sin impacto  
- RF corto → pequeña caída  
- RF medio → caída moderada  
- RF largo → caída fuerte  
- RV → impacto indirecto  

### Si los tipos bajan:

- RF largo sube con fuerza  
- RF medio sube moderado  
- RF corto sube poco  
- Monetario apenas se mueve  

---

# 11. Por qué la Barbell evita el tramo medio

RF_MEDIO (5–7 años) es la peor zona:

- no tiene la seguridad del corto,  
- no tiene la convexidad del largo.

Por eso la Barbell concentra en:

- **MONETARIO + RF_CORTO** → escudo  
- **RF_LARGO** → palanca  
- **RENTA_VARIABLE** → motor  

---

# 12. Resultado de aplicar la Estrategia Barbell a mi cartera

(Se mantiene tu tabla original, métricas y rebalanceos.)

---

# 13. Análisis de resultados

La cartera está **100% en MONETARIO**.  
Esto implica:

- ✔ extrema prudencia  
- ✔ protección ante subidas de tipos  
- ❌ no captura bajadas de tipos  
- ❌ no diversifica duración  
- ❌ no aplica Barbell equilibrada  

---

# 14. Conclusión final

La pregunta correcta no es:

> “¿Qué fondo compro?”

Sino:

> **“¿Qué estructura de duración necesito hoy?”**

La estrategia Barbell, combinada con análisis disciplinado de la curva y un sistema técnico de salida, ofrece una forma moderna, prudente y eficaz de gestionar una cartera conservadora.


