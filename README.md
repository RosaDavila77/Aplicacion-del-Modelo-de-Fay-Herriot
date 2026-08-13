# Aplicación del Modelo de Fay-Herriot para la Estimación de Ingresos Reales Distritales

## Descripción

Proyecto desarrollado para la asignatura **Técnicas de Muestreo** de la **Universidad Nacional de Ingeniería (UNI)**, cuyo objetivo es estimar y analizar la evolución de los ingresos reales de los distritos de Lima Metropolitana durante el periodo **2019–2024**.

Debido a los reducidos tamaños muestrales en algunos distritos, las estimaciones directas presentan una elevada variabilidad o no pueden ser calculadas. Para solucionar este problema se aplica el **modelo de Fay-Herriot**, una metodología de estimación en áreas pequeñas que combina las estimaciones directas de la **ENAHO** con información auxiliar proveniente del **Censo Nacional 2017**.

## Metodología

* Obtención de información de ingresos familiares mediante la **ENAHO 2019–2024**.
* Cálculo de estimaciones directas de ingreso utilizando factores de expansión.
* Identificación de distritos con tamaños muestrales reducidos.
* Selección de variables auxiliares relacionadas con el ingreso:

  * Porcentaje de población con acceso a internet.
  * Porcentaje de población que trabajó durante la semana anterior.
* Ajuste del modelo de **Fay-Herriot** mediante mínimos cuadrados ponderados.
* Estimación de la varianza del efecto aleatorio mediante **REML**.
* Obtención de estimaciones **EBLUP** para los 43 distritos de Lima Metropolitana.
* Análisis del **factor de shrinkage (γ)** para evaluar el peso de la estimación directa frente a la predicción del modelo.
* Ajuste de los ingresos por inflación para obtener ingresos reales comparables entre años.
* Clasificación socioeconómica de los distritos utilizando los estratos de ingreso propuestos por el **INEI mediante el método de Dalenius**.

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
