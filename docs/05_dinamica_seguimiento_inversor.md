---
title: "Dinámica de seguimiento para el inversor"
author: "efueyo"
date: "2026-05-27"
version: "1.0"
category: "operativo"
tags:
  - seguimiento
  - inversion
  - barbell
  - fondos
  - rebalanceo
license: "CC BY-NC-SA 4.0"
---

# Dinámica de seguimiento para el inversor.
La idea es convertir el análisis en una rutina periódica simple, no en un sistema de trading activo. Los fondos de inversión tienen costes de traspaso bajos (en España los traspasos entre fondos son gratuitos fiscalmente), pero tampoco conviene moverse en exceso.El ciclo de seguimiento

| Dinámica de seguimiento para el inversor | Explicación                                                                                                      |
|------------------------------------------|------------------------------------------------------------------------------------------------------------------|
| La idea                                  | Convertir el análisis en una rutina periódica simple, no en un sistema de trading activo                         |
| Costes                                   | Los fondos tienen costes de traspaso bajos; en España los traspasos son fiscalmente gratuitos                    |
| Recomendación general                    | No conviene moverse en exceso; el objetivo es estabilidad y disciplina                                           |
| El ciclo de seguimiento                  | —                                                                                                                |

Paso a paso cada trimestre
## 1. Actualizar los datos (5 minutos)
Descargar los CSV actualizados de tus fondos y guardarlos en la carpeta Datos_fondos_csv. La mayoría de plataformas (Renta 4, Morningstar, Yahoo Finance) permiten exportar el histórico de cotizaciones.
## 2. Ejecutar el análisis (2 minutos)
```
python# Celda 1
%run barbell_alert.py
%run barbell_comparativa.py

# Celda 2 — Análisis Barbell
RUTA_EXCEL = Path('/home/enri/Py_CRI_6_fondos/Carteras/mi_cartera_barbell_0.xlsx')
RUTA_CSVS  = Path('/home/enri/Py_CRI_6_fondos/Datos_fondos_csv')

ba = BarbellAlert(ruta_excel=RUTA_EXCEL, ruta_csvs=RUTA_CSVS)
ba.run(actualizar_excel=True);
```
## 3. Leer el semáforo de la Alerta Barbell
El informe te da directamente la acción a tomar:
```
▼ REDUCIR  MONETARIO    (+44pp de exceso)  → tengo demasiado monetario
▲ AUMENTAR RF_LARGO     (-20pp de déficit) → me falta exposición a largo plazo
▲ AUMENTAR RF_CORTO     (-12pp de déficit) → me falta renta fija corta
'''

4. Decidir si actuar o esperar
No hay que actuar en cada trimestre. La regla es sencilla:

| Desviación detectada | Acción                                               |
|-----------------------|------------------------------------------------------|
| < 5 pp               | No hacer nada. Dentro de tolerancia                  |
| 5–15 pp              | Vigilar. Considerar en la próxima aportación         |
| > 15 pp              | Actuar. Planificar traspaso con el gestor            |
| Cambio de régimen    | Revisar aunque no haya desviación grande             |

## 5. Registrar en el Excel y en el tracker

Si haces algún movimiento, registrarlo:
Python
```
### Si haces una aportación nueva
pipe.tracker.registrar_aportacion("2026-07-01", 5000.0, "aportacion trimestral Q3")
```
Si haces un traspaso (venta de un fondo + compra de otro)
Python
```
### Registrar una acción (compra/venta)
pipe.tracker.registrar_accion("2026-07-01", "TRASPASO", "R4 Foncuenta → fondo RF_LARGO nuevo")
```
Para actualizar el Excel 
Python
```
### Actualizar el Excel con el nuevo fondo
ba.run(actualizar_excel=True);
```
## El árbol de decisión trimestral
![Árbol de decisión](./img/arbol%20de%20decision.png)

```
![imagen.png](attachment:d6484f6f-7dab-490a-a747-c0b349114e55.png)
```
## Los tres momentos clave del año.

### Enero — Revisión anual completa.  

Actualizar todos los CSV: Ejecutar ba.run() y comp.run().  
Ver la comparativa Buy&Hold vs Barbell del año anterior.  
Decidir si la estructura de la cartera sigue siendo válida.
Reunión con el gestor si hay cambios importantes.

### Cada trimestre — Revisión rápida

Actualizar CSV y ejecutar ba.run().  
Ver el semáforo: ¿hay algún REDUCIR o AUMENTAR > 15pp?.  
Si hay nueva aportación prevista, dirigirla al bucket deficitario.  

### Cuando ocurre algo extraordinario.

Cambio brusco del T10Y2Y (más de 0.5pp en un mes).  
Caída del mercado > 10% en poco tiempo.  
Cambio de política de la Fed o el BCE.  
En estos casos ejecutar el análisis aunque no sea trimestre.


## Cómo gestionar las nuevas aportaciones.

Las aportaciones periódicas son la herramienta más eficiente para rebalancear sin costes:
En lugar de vender el fondo con exceso y comprar el deficitario
(lo que puede tener coste fiscal en planes de pensiones o EPSVs),

→ dirige la nueva aportación directamente al bucket deficitario.  
Por ejemplo, si tienes exceso en MONETARIO y déficit en RF_CORTO, y vas a aportar 1.000€ este trimestre:

No aportes a Foncuenta (MONETARIO, ya con exceso).  
.  Aporta a Epsv Renta 4 Dédalo (RF_CORTO, deficitario).
Python
```
pipe.tracker.registrar_aportacion("2026-07-01", 1000.0, "aportacion dirigida a RF_CORTO")
```
## Señales de alerta que requieren acción inmediata.  
Fuera del ciclo trimestral, hay tres situaciones que justifican revisar en cualquier momento:
1. El T10Y2Y cruza −0.10% → la curva se invierte. Señal histórica de recesión en 12-18 meses. Aumentar RF_LARGO como cobertura.
2. El T10Y2Y supera +1.5% y sube → curva muy empinada. Reducir duración, aumentar monetario y flotantes para capturar el carry sin riesgo de precio.
3. Caída de la cartera > 8% en un trimestre → revisar si el régimen ha cambiado o si algún fondo ha roto su patrón histórico de volatilidad (puede que haya cambiado de categoría real).

## En resumen
La dinámica ideal es:
- Trimestralmente:   15 minutos · actualizar datos · leer semáforo · decidir
- Anualmente:        1-2 horas  · revisión completa · reunión con gestor
- Extraordinario:    cuando el mercado te lo pida · sin agenda fija
Y la regla de oro:

No actuar por debajo de 15pp de desviación. El rebalanceo frecuente genera costes (operativos, fiscales, de tiempo) que superan el beneficio. La paciencia y la consistencia valen más que la precisión milimétrica en los pesos.
