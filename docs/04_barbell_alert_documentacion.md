---
title: "Documentación técnica del módulo Barbell Alert"
author: "efueyo"
date: "2026-05-27"
version: "1.0"
category: "tecnico"
tags:
  - barbell-alert
  - fondos
  - cartera
  - curva-de-tipos
  - automatizacion
license: "CC BY-NC-SA 4.0"
---

# Módulo `barbell_alert.py` — Documentación completa

> **Solo para fines educativos. No es asesoramiento financiero.**

---

## ¿Qué es y para qué sirve?

`barbell_alert.py` hace dos cosas complementarias:

**1. Mantiene la cartera actualizada** — dado un Excel con los datos básicos
de cada inversión (fondo, fecha, importe), calcula automáticamente las
participaciones, el valor actual, la plusvalía y los pesos reales de cada
posición usando los CSV históricos de cotizaciones.

**2. Genera la Alerta Barbell** — analiza si la distribución de la cartera
está bien posicionada para el entorno actual de tipos de interés, comparándola
con la estrategia Barbell óptima para ese entorno.

Funciona de forma independiente o integrado con `cri_fondos_v2.py`.

---

## Estructura del Excel de cartera

El Excel (`modelo_cartera_barbell.xlsx`, hoja `Sheet1`) tiene dos tipos
de columnas:

### Columnas que rellena el usuario (inputs)

| Columna | Tipo | Ejemplo | Descripción |
|---------|------|---------|-------------|
| `Valor` | Texto | RENTA 4 FONCUENTA AHORRO, F.I. | Nombre del fondo |
| `ISIN` | Texto | ES0173222003 | Código ISIN |
| `Ticker` | Texto | 0P00019MZZ.F | Ticker de cotización |
| `Fichero_csv` | Texto | ES0173222003.csv | Nombre del CSV en la carpeta de datos |
| `Categoria` | Texto | Fondo monetario | Categoría manual *(opcional)* |
| `Fecha_Inversion` | Fecha | 2025-09-19 | Fecha de la compra o aportación |
| `Cantidad_Invertida` | Número | 26446.63 | Importe invertido en EUR |

> Un mismo fondo puede aparecer en varias filas si tiene múltiples
> aportaciones en fechas distintas. El script lo gestiona correctamente.

### Columnas que calcula el script automáticamente (outputs)

| Columna | Cálculo | Descripción |
|---------|---------|-------------|
| `Num Partic.` | `Cantidad_Invertida ÷ NAV_en_Fecha_Inversion` | Participaciones compradas al precio del día de la inversión |
| `Fecha_actual` | Última fecha del CSV | Fecha del dato más reciente disponible |
| `Valor_actual` | `Num_Partic × NAV_actual` | Valor de mercado actual de la posición |
| `Benef.` | `Valor_actual − Cantidad_Invertida` | Ganancia o pérdida en EUR |
| `Plusv.%` | `Benef. ÷ Cantidad_Invertida × 100` | Rentabilidad de la posición en % |
| `Peso_Objetivo` | *(campo manual)* | Peso estratégico deseado — no se toca |
| `Peso_Actual` | `Valor_actual ÷ total_cartera × 100` | Peso real actual de la posición |

---

## Flujo completo del módulo

```
[0] (Opcional) Actualizar Excel desde CSV
      ↓ lee Fecha_Inversion y Cantidad_Invertida de cada fila
      ↓ busca el NAV en esa fecha en el CSV
      ↓ calcula Num_Partic, Valor_actual, Benef., Plusv.%, Peso_Actual
      ↓ hace backup del Excel y sobreescribe con los datos frescos

[1] Leer la cartera desde el Excel (ya actualizado)
      ↓ recalcula Peso% desde Valor_actual
        (ignora el Peso% del Excel línea a línea, que es por aportación)
      ↓ consolida fondos con múltiples filas

[2] Clasificar cada fondo en su bucket de duración
      ↓ lee el CSV histórico de cada fondo
      ↓ calcula volatilidad anualizada: std(retornos_diarios) × √252
      ↓ asigna bucket según umbrales de volatilidad
      ↓ usa caché por Fichero_csv (el mismo CSV no se lee dos veces)

[3] Detectar régimen de curva de tipos
      ↓ descarga T10Y2Y de FRED (bono 10Y menos bono 2Y, en %)
      ↓ clasifica el régimen: EMPINANDO / PLANA / INVERTIDA
      ↓ si FRED no está disponible → usa distribución conservadora

[4] Calcular alertas Barbell
      ↓ agrupa Valor_actual por bucket
      ↓ compara pesos reales vs distribución objetivo del régimen
      ↓ genera alerta si la desviación supera la tolerancia (±5pp por defecto)
      ↓ imprime informe con acciones sugeridas e importes orientativos en EUR
```

---

## Clasificación de fondos en buckets

La volatilidad anualizada es el proxy de la duración efectiva del fondo:

| Bucket | Volatilidad anual | Perfil típico |
|--------|:-----------------:|---------------|
| `MONETARIO` | < 3% | Fondos monetarios, ultra-corto plazo |
| `RF_CORTO` | 3% – 8% | Renta fija corto plazo, bonos flotantes |
| `RF_MEDIO` | 8% – 12% | Renta fija medio plazo, mixtos conservadores |
| `RF_LARGO` | 12% – 20% | Renta fija largo plazo, mixtos moderados |
| `RENTA_VARIABLE` | ≥ 20% | Acciones, mixtos agresivos |

---

## Régimen de curva y distribuciones Barbell óptimas

El diferencial T10Y2Y (bono americano 10Y − 2Y) clasifica el entorno:

| T10Y2Y | Régimen | Interpretación |
|:------:|---------|----------------|
| < −0,10% | `INVERTIDA` | Señal histórica de recesión. Aumentar RF largo |
| −0,10% a +0,50% | `PLANA` | Máxima incertidumbre. Barbell equilibrada |
| > +0,50% y subiendo | `EMPINANDO` | *Higher for Longer*. Priorizar carry de corto |

Distribución Barbell óptima según régimen:

| Bucket | EMPINANDO | PLANA | INVERTIDA | SIN DATOS |
|--------|:---------:|:-----:|:---------:|:---------:|
| MONETARIO | **50%** | 35% | 25% | 40% |
| RF_CORTO | **25%** | 20% | 15% | 25% |
| RF_MEDIO | 15% | 10% | 10% | 15% |
| RF_LARGO | 5% | **20%** | **35%** | 10% |
| RENTA_VARIABLE | 5% | 15% | 15% | 10% |

---

## Leer el informe

### Sección 1 — Régimen de curva

```
Valor T10Y2Y actual : +0.49%  [bajando]
Régimen detectado   : PLANA
Curva plana. Máxima incertidumbre. Aplicar Barbell clásica.
```

El valor actual de T10Y2Y y su tendencia (subiendo / bajando / plana en los
últimos ~3 meses) determinan qué distribución Barbell se usa como referencia.

### Sección 2 — Distribución por bucket

```
Bucket              Actual  Objetivo   Dif.pp  Estado
MONETARIO          ████████  80.0%     35.0%    +45.0pp  ▼ REDUCIR
RF_CORTO           █          7.4%     20.0%    -12.6pp  ▲ AUMENTAR
RF_LARGO                       0.0%    20.0%    -20.0pp  ▲ AUMENTAR
```

- La barra `████` es proporcional al peso actual.
- `Dif.pp` son los puntos porcentuales de desviación respecto al objetivo.
- `▼ REDUCIR` → exceso de peso en ese bucket.
- `▲ AUMENTAR` → déficit de peso.
- `⚠ DESCONOCIDO` → fondo sin CSV disponible; no se puede clasificar.

### Sección 3 — Resumen ejecutivo

```
▼ REDUCIR  MONETARIO
  Peso actual 80.0% → objetivo 35.0%  (exceso +45.0pp)
  Importe orientativo a reducir: ~357.419 EUR
  Fondos en este bucket:
    · RENTA 4 FONCUENTA AHORRO, F.I.      137.520€  (17.3%)
    · Plan De Pensiones Renta 4 Dedalo    168.968€  (21.3%)
```

El importe orientativo es `|diferencia_pp / 100| × valor_total_cartera`.
Es una estimación de cuánto capital habría que redirigir, no una orden de
venta. Los fondos se listan con su valor real en EUR calculado desde el CSV.

### Sección 4 — Detalle de fondos

```
Fondo                                    Valor EUR   Peso%  Bucket        Vol.
Plan De Pensiones Renta 4 Dedalo          168.968€   21.3%  MONETARIO    2.4%
RENTA 4 FONCUENTA AHORRO, F.I.           137.520€   17.3%  MONETARIO    1.3%
TOTAL                                     794.675€  100.0%
```

Una línea por fondo (todas las aportaciones consolidadas). El `TOTAL` debe
sumar 100%. Si no lo hace es porque algún fondo aparece como `DESCONOCIDO`
por falta de CSV.

---

## Uso desde Jupyter Lab

### Flujo completo en 2 celdas

```python
# Celda 1 — cargar el módulo (todo el código en esta celda)
%run barbell_alert.py

# Celda 2 — ejecutar
RUTA_EXCEL = '/home/enri/Py_CRI_6_fondos/Carteras/modelo_cartera_barbell.xlsx'
RUTA_CSVS  = '/home/enri/Py_CRI_6_fondos/Datos_fondos_csv'

ba = BarbellAlert(ruta_excel=RUTA_EXCEL, ruta_csvs=RUTA_CSVS)
ba.run()                         # solo análisis Barbell
```

### Actualizar Excel y analizar en un solo paso

```python
ba.run(actualizar_excel=True)
# [0/4] Actualiza el Excel desde los CSV (con backup automático)
# [1/4] → [4/4] Análisis Barbell sobre los datos recién actualizados
```

### Solo actualizar el Excel (sin análisis Barbell)

```python
actualizar_excel_desde_csvs(
    ruta_excel = RUTA_EXCEL,
    ruta_csvs  = RUTA_CSVS,
)
```

Salida del actualizador:

```
  Fondo                                     Invertido   Valor act.    Benef.  Peso%  Fecha CSV
  ─────────────────────────────────────────────────────────────────────────────────────────────
  Plan De Pensiones Renta 4 Dedalo         168.000€    168.968€     +968€   21.3%  2026-05-15
  RENTA 4 FONCUENTA AHORRO, F.I.           135.000€    137.520€    +2520€   17.3%  2026-05-15
  ...
  TOTAL                                    780.000€    794.675€   +14675€  100.0%
```

### Integrado con el sistema CRI

```python
# Reutiliza los datos macro ya descargados por el pipe CRI
ba = barbell_desde_pipe(pipe, RUTA_EXCEL, RUTA_CSVS)
```

### Volver a ver el informe sin recalcular

```python
ba.informe()
```

### Acceder a los datos como DataFrame

```python
ba.tabla_resumen()   # alertas por bucket
ba.tabla_fondos()    # detalle por fondo
```

---

## Parámetros configurables

| Parámetro | Por defecto | Descripción |
|-----------|:-----------:|-------------|
| `tolerancia` | `5.0` pp | Desviación mínima para generar alerta |
| `ventana_dias` | `63` | Días para calcular la tendencia de T10Y2Y (~3 meses) |

```python
# Más estricto: alerta con cualquier desviación > 3pp
ba = BarbellAlert(ruta_excel=..., ruta_csvs=..., tolerancia=3.0)

# Ventana más larga para tendencia de curva (~6 meses)
ba = BarbellAlert(ruta_excel=..., ruta_csvs=..., ventana_dias=126)
```

---

## Cómo añadir un nuevo fondo a la cartera

1. Descarga el CSV histórico del fondo y guárdalo en `Datos_fondos_csv/`
   con el nombre `{ISIN}.csv` (ej: `ES0173222003.csv`).
2. Añade una fila al Excel con: `Valor`, `ISIN`, `Ticker`, `Fichero_csv`,
   `Categoria` *(opcional)*, `Fecha_Inversion`, `Cantidad_Invertida`.
3. Deja en blanco el resto de columnas — el script las calculará.
4. Ejecuta `ba.run(actualizar_excel=True)` o `actualizar_excel_desde_csvs(...)`.

---

## Gestión de fondos con múltiples aportaciones

Si has hecho varias aportaciones al mismo fondo en fechas distintas, añade
una fila por cada aportación. El script:

- Calcula las participaciones de cada aportación al NAV de su fecha.
- Consolida todas las filas del mismo fondo para calcular pesos y totales.
- No duplica el fondo en el análisis Barbell.

```
Fondo              Fecha        Invertido  Num Partic.  (calculado)
RENTA 4 FONCUENTA  2025-09-19   26.446 €     262.8 part.
RENTA 4 FONCUENTA  2025-12-05  100.189 €     996.1 part.
                   ─────────────────────────────────────
                   TOTAL       126.635 €    1.258,9 part. → Valor actual consolidado
```

---

## Preguntas frecuentes

**¿Qué pasa si FRED no está disponible?**
El análisis continúa usando la distribución `DESCONOCIDO` (conservadora).
El actualizador del Excel no depende de FRED, solo de los CSV locales.

**¿Qué pasa si falta el CSV de un fondo?**
Ese fondo aparece como `DESCONOCIDO` en el bucket y no se incluye en los
pesos por bucket. Su valor sí se suma al total de cartera. El aviso aparece
al final del informe con el nombre del fichero que falta.

**¿El Excel original se puede perder?**
No. Antes de cualquier escritura se crea un backup automático con timestamp:
`modelo_cartera_barbell_backup_20260515_143022.xlsx`.

**¿Puedo usar el módulo sin `cri_fondos_v2.py`?**
Sí, es completamente independiente. Solo necesita `numpy`, `pandas`,
`pandas-datareader` y `openpyxl`.

**¿La estrategia Barbell solo sirve para el entorno actual de tipos?**
**No**. Los principios son universales: la curva T10Y2Y y la gestión de duración
funcionan en cualquier ciclo de mercado. Lo que cambia es cuál régimen es
dominante y qué distribución óptima corresponde. En recesión manda la
duración larga; en expansión con inflación baja, el crédito y la RV; en
stagflación, los activos reales. El módulo se adapta automáticamente al
régimen detectado.

---

## Dependencias

```
pip install pandas numpy pandas-datareader openpyxl
```

---

*Módulo barbell_alert.py · Licencia CC BY-NC 4.0 · Solo para uso educativo*
