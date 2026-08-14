# Aplicación del Modelo de Fay-Herriot para la Estimación de Ingresos Reales Distritales

## Descripción

Proyecto desarrollado para la asignatura **Técnicas de Muestreo** de la **Universidad Nacional de Ingeniería (UNI)**, cuyo objetivo es estimar y analizar la evolución de los ingresos reales de los distritos de Lima Metropolitana durante el periodo **2019–2024**.

Debido a los reducidos tamaños muestrales en algunos distritos, las estimaciones directas presentan una elevada variabilidad o no pueden ser calculadas. Para solucionar este problema se aplica el **modelo de Fay-Herriot**, una metodología de estimación en áreas pequeñas que combina las estimaciones directas de la **ENAHO** con información auxiliar proveniente del **Censo Nacional 2017**.

![Clasificación socioeconómica de Lima](imagenes/7Z1pk2mdUa4IBlqetf1_iuFF1mLkHjBZIZPvbefXcTV0UNNgzc_VfNZ-Lc9Tb2AtcZI0HVlu13_T9Fp_gWRqGVUmvzJ0ThdjRTyMtd0qZhB3NsIzHSutA6Ir72Z2BPIXVBad-CQtjvR3vOquxDNhbHgNQ.jpg)

## 🔬 Metodología

### 1. Procesamiento de la ENAHO

El notebook `ENAHO2024.ipynb` contiene el procesamiento de la información de la **ENAHO** utilizada para el análisis de los ingresos distritales de Lima Metropolitana.

En esta etapa se realiza:

- Limpieza y preparación de la información de la ENAHO.
- Selección de los distritos de Lima Metropolitana mediante el código **UBIGEO**.
- Identificación del tamaño muestral por distrito.
- Cálculo de las **estimaciones directas del ingreso** utilizando los factores de expansión.
- Cálculo del error estándar y coeficiente de variación de las estimaciones.
- Identificación de distritos con tamaños muestrales reducidos.
- Integración de la información con las variables auxiliares provenientes del Censo.
- Preparación de los datos necesarios para la aplicación del **modelo Fay-Herriot**.

Los resultados obtenidos en esta etapa constituyen la información de entrada para la estimación EBLUP a nivel distrital.

### 2. Variables auxiliares

Se incorporaron variables provenientes del Censo, considerando:

- Semana de trabajo
- Conexión a internet
╒═══════════════════╤════════════╤══════════╤═══════════╤═══════════╕
│                   │       beta │       SE │   t_value │   p_value │
╞═══════════════════╪════════════╪══════════╪═══════════╪═══════════╡
│ Intercepto        │  1359.6668 │ 385.1500 │    3.5302 │    0.0004 │
├───────────────────┼────────────┼──────────┼───────────┼───────────┤
│ semana_trabajo    │ -3002.1281 │ 819.2374 │   -3.6645 │    0.0002 │
├───────────────────┼────────────┼──────────┼───────────┼───────────┤
│ conexion_internet │  3783.3707 │ 192.9179 │   19.6113 │    0.0000 │
╘═══════════════════╧════════════╧══════════╧═══════════╧═══════════╛

### 3. Modelo Fay-Herriot

Se estimaron los coeficientes mediante mínimos cuadrados ponderados
y la varianza del efecto aleatorio mediante REML.

**Resultado:**
Varianza del efecto aleatorio (σ²_u) estimada por REML: 1100350.201682

### 4. Estimación EBLUP

Se combinaron las estimaciones directas con las predicciones del modelo
mediante el factor de shrinkage (γ).

**Resultado:**
╒════╤══════════╤═════════════════════════╤════════════╤═════════════╤═════════╤════════════╤════════════╕
│    │   UBIGEO │ NOMBRE DEL DISTRITO     │   Y_direct │   SD_direct │   EBLUP │   SE_EBLUP │   CV_EBLUP │
╞════╪══════════╪═════════════════════════╪════════════╪═════════════╪═════════╪════════════╪════════════╡
│  0 │   150101 │ Lima                    │    2219.29 │      222.20 │ 2187.19 │     217.38 │       9.94 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│  1 │   150102 │ Ancon                   │    1178.74 │      216.28 │ 1190.69 │     211.83 │      17.79 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│  2 │   150103 │ Ate                     │    1469.17 │      107.94 │ 1469.20 │     107.38 │       7.31 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│  3 │   150104 │ Barranco                │    2553.32 │      670.90 │ 2239.34 │     565.19 │      25.24 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│  4 │   150105 │ Breña                   │    2211.25 │      281.13 │ 2161.70 │     271.55 │      12.56 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│  5 │   150106 │ Carabayllo              │    1366.13 │      100.43 │ 1367.09 │      99.97 │       7.31 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│  6 │   150107 │ Chaclacayo              │    2600.26 │      415.62 │ 2447.15 │     386.40 │      15.79 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│  7 │   150108 │ Chorrillos              │    1992.27 │      199.83 │ 1974.04 │     196.30 │       9.94 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│  8 │   150109 │ Cieneguilla             │    1265.23 │      181.82 │ 1271.26 │     179.15 │      14.09 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│  9 │   150110 │ Comas                   │    1551.04 │      123.23 │ 1549.96 │     122.39 │       7.90 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 10 │   150111 │ El Agustino             │    1817.21 │      285.25 │ 1793.43 │     275.25 │      15.35 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 11 │   150112 │ Independencia           │    1725.36 │      179.43 │ 1718.15 │     176.86 │      10.29 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 12 │   150113 │ Jesus Maria             │    3570.01 │      288.82 │ 3422.16 │     278.45 │       8.14 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 13 │   150114 │ La Molina               │    4232.66 │      421.05 │ 3849.58 │     390.75 │      10.15 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 14 │   150115 │ La Victoria             │    1269.84 │      137.17 │ 1273.24 │     136.01 │      10.68 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 15 │   150116 │ Lince                   │    2025.93 │      258.23 │ 1994.28 │     250.74 │      12.57 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 16 │   150117 │ Los Olivos              │    1802.13 │      129.44 │ 1797.17 │     128.46 │       7.15 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 17 │   150118 │ Lurigancho              │    1144.55 │      110.96 │ 1148.17 │     110.34 │       9.61 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 18 │   150119 │ Lurin                   │    1743.01 │      192.93 │ 1734.14 │     189.75 │      10.94 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 19 │   150120 │ Magdalena del Mar       │    3898.11 │      408.45 │ 3578.69 │     380.61 │      10.64 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 20 │   150121 │ Pueblo Libre            │    3283.58 │      320.52 │ 3128.88 │     306.53 │       9.80 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 21 │   150122 │ Miraflores              │    4824.79 │      538.05 │ 4126.41 │     478.75 │      11.60 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 22 │   150123 │ Pachacamac              │     860.14 │      113.82 │  867.26 │     113.16 │      13.05 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 23 │   150124 │ Pucusana                │     nan    │      nan    │ 1471.98 │    1048.98 │      71.26 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 24 │   150125 │ Puente Piedra           │    1334.87 │      134.37 │ 1337.08 │     133.28 │       9.97 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 25 │   150126 │ Punta Hermosa           │     571.84 │      188.09 │  599.87 │     185.14 │      30.86 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 26 │   150127 │ Punta Negra             │     nan    │      nan    │ 1472.01 │    1048.98 │      71.26 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 27 │   150128 │ Rimac                   │    1186.89 │      222.17 │ 1199.13 │     217.35 │      18.13 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 28 │   150129 │ San Bartolo             │    1664.30 │      408.96 │ 1638.93 │     381.03 │      23.25 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 29 │   150130 │ San Borja               │    5817.17 │      949.29 │ 3860.82 │     703.86 │      18.23 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 30 │   150131 │ San Isidro              │    5509.16 │      584.05 │ 4553.79 │     510.29 │      11.21 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 31 │   150132 │ San Juan de Lurigancho  │    1140.06 │       57.18 │ 1141.04 │      57.09 │       5.00 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 32 │   150133 │ San Juan de Miraflores  │    1333.87 │      118.93 │ 1335.63 │     118.17 │       8.85 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 33 │   150134 │ San Luis                │    1724.44 │      311.29 │ 1704.02 │     298.43 │      17.51 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 34 │   150135 │ San Martin de Porres    │    1666.91 │      115.01 │ 1664.60 │     114.33 │       6.87 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 35 │   150136 │ San Miguel              │    3419.08 │      488.33 │ 3072.29 │     442.71 │      14.41 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 36 │   150137 │ Santa Anita             │    1741.42 │      179.13 │ 1733.79 │     176.57 │      10.18 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 37 │   150138 │ Santa Maria del Mar     │    1025.00 │        0.00 │ 1025.00 │       0.00 │       0.00 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 38 │   150139 │ Santa Rosa              │    1631.88 │      314.99 │ 1618.67 │     301.68 │      18.64 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 39 │   150140 │ Santiago de Surco       │    3363.01 │      227.83 │ 3277.83 │     222.64 │       6.79 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 40 │   150141 │ Surquillo               │    2736.95 │      467.47 │ 2527.38 │     426.99 │      16.89 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 41 │   150142 │ Villa el Salvador       │    1394.82 │      135.15 │ 1396.08 │     134.04 │       9.60 │
├────┼──────────┼─────────────────────────┼────────────┼─────────────┼─────────┼────────────┼────────────┤
│ 42 │   150143 │ Villa Maria del Triunfo │    1347.93 │       85.58 │ 1348.75 │      85.29 │       6.32 │
╘════╧══════════╧═════════════════════════╧════════════╧═════════════╧═════════╧════════════╧════════════╛

**Comparacion vs Estimacion Directa**



### 5. Ajuste por inflación

Las estimaciones fueron deflactadas para obtener ingresos reales
comparables durante el periodo 2019–2024.

**Tasa de Inflacion:**
Tasa de inflación aplicada: 1.97%

### 6. Clasificación socioeconómica

Los distritos fueron clasificados según los rangos de ingreso utilizados
en el estudio.

## 📊 Resultados

### Clasificación socioeconómica

[IMAGEN]

### Evolución del ingreso real 2019–2024

[IMAGEN]

### Distritos con mayor crecimiento

[IMAGEN]

### Distritos con mayor decrecimiento

AÑO	NOMBRE_DEL_DISTRITO	CREC_ACUM
25	Punta Hermosa	-53.90
29	San Borja	-39.55
20	Miraflores	-34.15
30	San Isidro	-29.02
40	Surquillo	-17.35

## Principales resultados

El modelo Fay-Herriot permitió obtener estimaciones para distritos con poca información muestral y reducir la variabilidad de las estimaciones directas.

El análisis del factor de shrinkage mostró el grado en que cada distrito depende de la información directa de la encuesta o de la predicción proporcionada por el modelo.

Asimismo, se identificaron diferencias importantes en la evolución de los ingresos reales entre los distritos de Lima Metropolitana. Entre los distritos con mayor crecimiento durante el periodo analizado se encontraron **Chaclacayo, San Bartolo, Carabayllo, Punta Negra e Independencia**. Por otro lado, **Punta Hermosa, San Isidro, San Borja, Miraflores y Surquillo** presentaron los mayores decrecimientos.

## Herramientas y técnicas

* **Python**
* Pandas / NumPy
* Análisis estadístico
* Estimación en áreas pequeñas (SAE)
* Modelo de Fay-Herriot
* EBLUP
* REML
* Weighted Least Squares (WLS)
* Análisis de correlación
* Visualización de datos

## Autores

**Rosa Davila Ponce**

**Angelo De la Cruz Paucar**

**Mauricio Rico Peña**
