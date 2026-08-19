# Aplicación del Modelo de Fay-Herriot para la Estimación de Ingresos Reales Distritales

## Descripción

Proyecto desarrollado para la asignatura **Técnicas de Muestreo** de la **Universidad Nacional de Ingeniería (UNI)**, cuyo objetivo es estimar y analizar la evolución de los ingresos reales de los distritos de Lima Metropolitana durante el periodo **2019–2024**.

Debido a los reducidos tamaños muestrales en algunos distritos, las estimaciones directas presentan una elevada variabilidad o no pueden ser calculadas. Para solucionar este problema se aplica el **modelo de Fay-Herriot**, una metodología de estimación en áreas pequeñas que combina las estimaciones directas de la **ENAHO** con información auxiliar proveniente del **Censo Nacional 2017**.

![Clasificación socioeconómica de Lima](imagenes/7Z1pk2mdUa4IBlqetf1_iuFF1mLkHjBZIZPvbefXcTV0UNNgzc_VfNZ-Lc9Tb2AtcZI0HVlu13_T9Fp_gWRqGVUmvzJ0ThdjRTyMtd0qZhB3NsIzHSutA6Ir72Z2BPIXVBad-CQtjvR3vOquxDNhbHgNQ.jpg)

## Metodología

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
<img width="784" height="484" alt="descarga (1)" src="https://github.com/user-attachments/assets/d7b9b53f-9258-452b-acd2-99902a58d98e" />

### 3. Modelo Fay-Herriot

Se estimaron los coeficientes mediante mínimos cuadrados ponderados
y la varianza del efecto aleatorio mediante REML.

**Resultado:**
Varianza del efecto aleatorio (σ²_u) estimada por REML: 1100350.201682

### 4. Estimación EBLUP

Se combinaron las estimaciones directas con las predicciones del modelo
mediante el factor de shrinkage (γ).

**Comparacion vs Estimacion Directa**
<img width="817" height="548" alt="descarga (2)" src="https://github.com/user-attachments/assets/c89bdaff-d05f-45ff-8c95-e9ba44e4a6df" />

### 5. Ajuste por inflación

Las estimaciones fueron deflactadas para obtener ingresos reales
comparables durante el periodo 2019–2024.

**Tasa de Inflacion:**
Tasa de inflación aplicada: 1.97%

### 6. Clasificación socioeconómica

Los distritos fueron clasificados según los rangos de ingreso utilizados
en el estudio.

## Resultados

### Clasificación socioeconómica
**Todos los Distritos según EBLUP (Clasificación por Nivel de Ingreso)**
<img width="1184" height="1277" alt="descarga (3)" src="https://github.com/user-attachments/assets/0258fee7-aae8-4bf0-b2db-4d70003bcd17" />

**Top 20 Distritos según EBLUP (Clasificación por Nivel de Ingreso)**
<img width="1180" height="684" alt="descarga (4)" src="https://github.com/user-attachments/assets/d191b6aa-2a48-4ca7-a043-332da83d6942" />

### Distritos con mayor crecimiento


<img width="357" height="235" alt="Captura de pantalla 2026-08-13 222545" src="https://github.com/user-attachments/assets/57edeb64-9c67-4142-a160-62796d310231" />

<img width="1184" height="584" alt="descarga (6)" src="https://github.com/user-attachments/assets/e1a4deb4-c979-4992-9214-2489dc381adc" />


### Distritos con mayor decrecimiento

<img width="1184" height="583" alt="descarga (5)" src="https://github.com/user-attachments/assets/e19d2706-1447-4419-ab79-2ae4b52e77c2" />

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
