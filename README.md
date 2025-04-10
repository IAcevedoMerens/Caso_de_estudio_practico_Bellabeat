# Bellabeat Case Study

## Resumen ejecutivo

Este proyecto de análisis de datos se centra en **Bellabeat**, una empresa de tecnología del bienestar que fabrica dispositivos inteligentes enfocados en la salud femenina. El objetivo es descubrir patrones de uso y comportamiento a partir de datos de dispositivos inteligentes (*smart devices*), y así ofrecer recomendaciones basadas en datos que puedan guiar futuras estrategias de marketing.

Se utilizaron herramientas como **SQL (BigQuery)**, **R (ggplot2)** y **Excel**, aplicando el enfoque del proceso analítico propuesto en el curso profesional de Google:  *Google Data Analytics Professional Certificate*.

**Este proyecto fue desarrollado como parte del capstone project del programa oficial Google Data Analytics Professional Certificate dictado por Coursera. Se trabajó de manera práctica e individual aplicando todo el proceso de análisis de datos sobre un caso real, con el objetivo de comenzar a construir un portfolio profesional y técnico como analista de datos.**

## Introducción

**Bellabeat** busca entender cómo las personas utilizan sus productos y qué comportamientos saludables pueden promover mediante sus estrategias. Este estudio parte de un conjunto de datos recopilados a través de dispositivos Fitbit, con la idea de tomar decisiones basadas en datos. Se han utilizado un total de 5 datasets, recopilando las acciones y actividades de un total de 23 usuarios en común.

### Objetivo principal

Descubrir cómo los usuarios interactúan con los dispositivos y qué patrones de actividad física, sueño y consumo calórico se pueden identificar.

### Justificación de la elección de datasets

Se eligieron datasets de uso diario de dispositivos Fitbit disponibles públicamente en Kaggle, ya que estos representan comportamientos reales de usuarios durante un período de 31 días. Estas fuentes fueron seleccionadas por su nivel de detalle en variables como pasos diarios, calorías quemadas, minutos activos y duración del sueño.

Estos datos permiten:
- Analizar la correlación entre actividad física, sueño y consumo energético.
- Observar hábitos cotidianos a partir de registros horarios.
- Comprender mejor el perfil de usuario típico de dispositivos inteligentes de salud.

Al trabajar con datos reales y continuos, se pueden generar conclusiones más relevantes para diseñar estrategias de marketing basadas en evidencia.

## Metodología

El enfoque de este caso de estudio sigue las etapas del proceso de análisis de datos propuesto por Google:

1. **Ask**: Formulación de preguntas y comprensión del desafío de negocio.  
2. **Prepare**: Recolección y revisión de los datos de Fitbit.  
3. **Process**: Limpieza y unión de tablas mediante SQL (BigQuery).  
4. **Analyze**: Análisis exploratorio y segmentación en R.  
5. **Share**: Visualización y presentación de resultados mediante gráficos.  
6. **Act**: Generación de recomendaciones estratégicas para Bellabeat.

## Preguntas de investigación: orientación del trabajo

- **¿Cómo se comportan los usuarios en términos de pasos, sueño y calorías quemadas?**  
  Esta pregunta permitió conocer los niveles generales de actividad, descanso y gasto energético. Fue clave para identificar tendencias y perfiles de usuario.

- **¿Existen patrones horarios de mayor actividad?**  
  Ayudó a determinar en qué momentos del día las personas son más activas, lo que podría ser útil para estrategias de comunicación o recordatorios dentro de la app.

- **¿Se puede segmentar a los usuarios según sus niveles de actividad?**  
  Esta segmentación permitió clasificar a las usuarias en distintos grupos (sedentarias, activas, etc.), con el objetivo de proponer recomendaciones personalizadas.

- **¿Qué correlaciones existen entre sueño, pasos y calorías?**  
  Se buscó explorar si existía una relación directa entre la duración del sueño, el nivel de actividad y el consumo energético, para entender mejor los hábitos saludables.

- **¿Qué oportunidades de negocio puede aprovechar Bellabeat con estos datos?**  
  Esta pregunta guió las recomendaciones finales del proyecto, basadas en hallazgos previos, apuntando a cómo Bellabeat puede optimizar sus productos y su estrategia de marketing.

## Preparación de los datos

Se trabajó con diversos archivos CSV provenientes de la plataforma Fitbit, correspondientes a usuarios que usaron el dispositivo durante 31 días. Las tablas más relevantes para este análisis fueron:

- **`daily_activity_merged`**: contiene datos agregados por día y por usuario, como cantidad total de pasos (`TotalSteps`), calorías quemadas (`Calories`), distancia recorrida, y minutos en diferentes niveles de actividad (ligera, moderada, intensa). Es clave para analizar el comportamiento general de los usuarios en términos de actividad física y gasto calórico.

- **`sleep_day_merged`**: incluye información diaria sobre el sueño por usuario, con columnas como `TotalMinutesAsleep` y `TotalTimeInBed`. Este dataset es esencial para explorar hábitos de descanso y su posible relación con otros comportamientos saludables.

- **`hourly_steps`**: contiene el número de pasos dados por usuario en intervalos horarios. Permite analizar patrones de actividad a lo largo del día, identificar las horas más activas, y cruzar esa información con otros indicadores de comportamiento.

La combinación de estos tres conjuntos de datos facilita un análisis completo e integrado sobre salud, actividad y bienestar.

## Limpieza de los datos

Durante la fase de limpieza se llevaron a cabo diversas acciones para asegurar la calidad y consistencia de los datos:

- **Eliminación de valores nulos**: se descartaron filas con registros faltantes en columnas clave como `TotalSteps`, `Calories` o `TotalMinutesAsleep`.
- **Formateo de fechas**: se estandarizó el formato de fecha y hora para permitir comparaciones entre tablas, por ejemplo entre `ActivityDate` y `SleepDay`.
- **Unificación de nombres de columnas**: se renombraron variables para facilitar un análisis coherente entre tablas que contienen información similar (`StepTotal` se convirtió en `TotalSteps`).
- **Filtrado por ID común**: se conservaron únicamente aquellos usuarios (`Id`) presentes en todos los datasets utilizados, para garantizar coherencia en el análisis cruzado.
- **Eliminación de duplicados**: se removieron registros repetidos por usuario y fecha u hora, cuando correspondiera.

A modo de ejemplo, la siguiente consulta en **BigQuery** se utilizó para identificar registros duplicados en los datos por hora:

Durante la fase de limpieza se llevaron a cabo diversas acciones para asegurar la calidad y consistencia de los datos:

- **Eliminación de valores nulos**: se descartaron filas con registros faltantes en columnas clave como `TotalSteps`, `Calories` o `TotalMinutesAsleep`.
- **Formateo de fechas**: se estandarizó el formato de fecha y hora para permitir comparaciones entre tablas, por ejemplo entre `ActivityDate` y `SleepDay`.
- **Unificación de nombres de columnas**: se renombraron variables para facilitar un análisis coherente entre tablas que contienen información similar (`StepTotal` se convirtió en `TotalSteps`).
- **Filtrado por ID común**: se conservaron únicamente aquellos usuarios (`Id`) presentes en todos los datasets utilizados, para garantizar coherencia en el análisis cruzado.
- **Eliminación de duplicados**: se removieron registros repetidos por usuario y fecha u hora, cuando correspondiera.

Una vez finalizado este proceso, se crearon versiones limpias y estandarizadas de cada tabla, y posteriormente se integraron mediante claves comunes (`Id`, `Date`) para formar una de las tablas finales de análisis: `daily_activity_final`, combinada con `sleep_day_merged_filtered`.

A continuación, se muestra un ejemplo de consulta SQL utilizada en BigQuery para realizar esta integración:

```sql
SELECT 
  a.Id,
  DATE(a.ActivityDate) AS Fecha,
  a.TotalSteps,
  a.Calories,
  b.TotalMinutesAsleep,
  b.TotalTimeInBed
FROM `capstonecaseofstudy.bellabeat_project.daily_activity_final` AS a
JOIN `capstonecaseofstudy.bellabeat_project.sleep_day_merged_filtered` AS b
ON a.Id = b.Id AND DATE(a.ActivityDate) = DATE(b.SleepDay);
```

Esta consulta permitió construir una tabla consolidada con datos clave sobre actividad, gasto calórico y sueño por usuario y por día.

## Análisis de datos

En esta sección se abordan las preguntas de investigación mediante consultas SQL realizadas en BigQuery, y se visualizan los resultados clave mediante gráficos generados en R utilizando `ggplot2`. El objetivo fue obtener hallazgos claros sobre la actividad física, el sueño, el gasto calórico y las oportunidades de segmentación entre usuarios.

### 1. ¿Existen usuarios con niveles de actividad significativamente distintos?

Se calcularon estadísticas descriptivas por usuario para observar la variación en el promedio de pasos y calorías diarias:

```sql
SELECT 
  Id,
  ROUND(AVG(TotalSteps), 2) AS promedio_pasos_diarios,
  ROUND(AVG(Calories), 2) AS promedio_calorias_diarias
FROM `capstonecaseofstudy.bellabeat_project.daily_activity_final`
GROUP BY Id
ORDER BY promedio_pasos_diarios DESC;
```

A continuación se muestran las primeras filas resultantes de esta consulta:

| Id         | promedio_pasos_diarios | promedio_calorias_diarias |
|------------|------------------------|---------------------------|
| 8053475328 | 14784.52               | 2932.02                   |
| 1503960366 | 11935.78               | 1808.74                   |
| 7007744171 | 11619.29               | 2570.24                   |
| 6962181067 | 10679.89               | 2015.38                   |
| 3977333714 | 10321.52               | 1480.64                   |



Estos valores se utilizaron para generar un gráfico de dispersión con línea de tendencia, observando que existen diferencias marcadas entre usuarias con respecto a su actividad física y su gasto energético. Esto evidencia la posibilidad de segmentar perfiles para estrategias personalizadas.

### 2. ¿En qué momento del día la gente camina más?

Se analizaron los pasos registrados por hora promedio entre todos los usuarios:

```sql
SELECT 
  EXTRACT(HOUR FROM ActivityHour) AS hora,
  ROUND(AVG(TotalSteps), 2) AS promedio_pasos
FROM `capstonecaseofstudy.bellabeat_project.hourly_steps_merged`
GROUP BY hora
ORDER BY promedio_pasos DESC;
```
A continuación se muestran las primeras filas resultantes de esta consulta:

| hora | promedio_pasos |
|------|----------------|
| 19   | 623.62         |
| 18   | 573.94         |
| 17   | 517.28         |
| 13   | 505.75         |
| 14   | 496.23         |


Los resultados se representaron mediante un gráfico de barras que muestra una mayor concentración de pasos entre las 17 y las 19 h. Esto puede ser aprovechado por Bellabeat para enviar recordatorios o motivaciones en momentos estratégicos del día.

### 3. ¿Existe una correlación entre pasos diarios, minutos de sueño y calorías quemadas?

Se integraron las tablas de actividad y sueño por usuario y día para calcular la correlación entre variables:

```sql
SELECT 
  CORR(a.TotalSteps, b.TotalMinutesAsleep) AS corr_pasos_sueno,
  CORR(a.TotalSteps, a.Calories) AS corr_pasos_calorias,
  CORR(b.TotalMinutesAsleep, a.Calories) AS corr_sueno_calorias
FROM `capstonecaseofstudy.bellabeat_project.daily_activity_final` a
JOIN `capstonecaseofstudy.bellabeat_project.sleep_day_merged_filtered` b
ON a.Id = b.Id AND DATE(a.ActivityDate) = DATE(b.SleepDay);
```

| corr_pasos_sueno     | corr_pasos_calorias | corr_sueno_calorias   |
|----------------------|---------------------|------------------------|
| -0.20007160349257597 | 0.44069190645277467 | -0.027815114588366056 |

Los valores de correlación fueron los siguientes:

- **Pasos y calorías**: 0.44 (moderada correlación positiva)  
- **Pasos y sueño**: -0.20 (correlación débil negativa)  
- **Sueño y calorías**: -0.03 (sin correlación)

#### Complemento: Consulta para visualizar la correlación por usuario

Para realizar las visualizaciones, fue necesario ejecutar una nueva consulta SQL que calcule los promedios por usuario:

```sql
SELECT 
  a.Id,
  AVG(a.TotalSteps) AS promedio_pasos,
  AVG(b.TotalMinutesAsleep) AS promedio_sueno,
  AVG(a.Calories) AS promedio_calorias
FROM `capstonecaseofstudy.bellabeat_project.daily_activity_final` a
JOIN `capstonecaseofstudy.bellabeat_project.sleep_day_merged` b
ON a.Id = b.Id AND DATE(a.ActivityDate) = DATE(b.SleepDay)
GROUP BY a.Id
```

Esta consulta devolvió un `dataframe` con tres variables por usuario: **promedio_pasos, promedio_sueno y promedio_calorias**, que se utilizaron para la visualización.

| Id         | promedio_pasos | promedio_sueno | promedio_calorias |
|------------|----------------|----------------|--------------------|
| 1503960366 | 11937.15       | 359.00         | 1802.19            |
| 8053475328 | 19078.67       | 297.00         | 3309.33            |
| 7086361926 | 9896.08        | 455.56         | 2576.32            |
| 1844505072 | 3477.00        | 652.00         | 1676.33            |
| 7007744171 | 5115.50        | 68.50          | 2150.50            |

### 4. ¿Se puede segmentar a los usuarios según sus niveles de actividad?

Se calculó el promedio de pasos diarios por usuario y se clasificaron en distintos niveles de actividad:

```sql
SELECT
  Id,
  ROUND(AVG(TotalSteps), 2) AS promedio_pasos,
  CASE
    WHEN AVG(TotalSteps) < 5000 THEN 'Sedentario'
    WHEN AVG(TotalSteps) BETWEEN 5000 AND 9999 THEN 'Moderadamente activo'
    WHEN AVG(TotalSteps) >= 10000 THEN 'Altamente activo'
  END AS nivel_actividad
FROM `capstonecaseofstudy.bellabeat_project.daily_activity_final`
GROUP BY Id;
```
A continuación se muestra una muestra representativa del resultado:

| Id         | promedio_pasos | nivel_actividad       |
|------------|----------------|------------------------|
| 1503960366 | 11935.78       | Altamente activo       |
| 7007744171 | 11619.29       | Altamente activo       |
| 8053475328 | 14784.52       | Altamente activo       |
| 2026352035 | 4960.14        | Moderadamente activo   |
| 1844505072 | 2876.02        | Sedentario             |

Los resultados se visualizaron con un gráfico de barras para mostrar la distribución de usuarias por segmento. Esta segmentación puede ser útil para campañas dirigidas y recomendaciones personalizadas dentro de la app.

## Visualización de resultados

Los resultados obtenidos a través de consultas SQL en BigQuery fueron exportados como archivos `.csv`, que luego se importaron a R para realizar las visualizaciones utilizando `ggplot2`. Cada visualización fue diseñada con el objetivo de responder a las preguntas planteadas en la sección de análisis y mostrar de manera clara las tendencias más relevantes.

### 1. Dispersión entre pasos y calorías por usuario

Esta visualización parte del promedio de pasos y calorías diarios por usuaria. El objetivo es identificar visualmente la existencia de patrones o grupos diferenciados.

```r
ggplot(estadisticas_1, aes(x = promedio_pasos_diarios, y = promedio_calorias_diarias)) +
  geom_point(color = "#0072B2", size = 3) +
  geom_smooth(method = "lm", se = FALSE, color = "darkred", linetype = "dashed") +
  labs(
    title = "Relación entre pasos diarios y calorías por usuario",
    x = "Promedio de pasos diarios",
    y = "Promedio de calorías diarias"
  ) +
  theme_minimal()
```

[![Rplotpasosycalorias.png](https://i.postimg.cc/yNbdHWnc/Rplotpasosycalorias.png)](https://postimg.cc/94yVPm6Q)

### 2. Pasos promedio por hora

Este gráfico de barras muestra los pasos promedio agrupados por hora. Permite observar los momentos del día con mayor actividad.

```r
ggplot(estadisticas_2, aes(x = reorder(hora, -promedio_pasos), y = promedio_pasos)) +
  geom_col(fill = "#56B4E9") +
  labs(
    title = "Promedio de pasos por hora del día",
    x = "Hora del día",
    y = "Promedio de pasos"
  ) +
  theme_minimal()
```

[![Rplot-Pasos.png](https://i.postimg.cc/TYsf1Bnv/Rplot-Pasos.png)](https://postimg.cc/KRtdsq90)

### 3. Correlación entre pasos diarios y minutos de sueño

Esta visualización busca representar gráficamente las correlaciones estadísticas analizadas previamente, donde se integraron las variables en un solo gráfico utilizando `facet_wrap()` para compararlas de manera eficiente respecto a los pasos.

#### Visualización combinada con facet_wrap()

```r
# Transformación del dataframe para graficar con facet
df_long <- df_corr %>%
  pivot_longer(cols = c(promedio_sueno, promedio_calorias),
               names_to = "variable",
               values_to = "valor_y")

# Etiquetas más legibles
df_long$variable <- recode(df_long$variable,
                           "promedio_sueno" = "Minutos de Sueño",
                           "promedio_calorias" = "Calorías")

# Gráfico final
ggplot(df_long, aes(x = promedio_pasos, y = valor_y)) +
  geom_point(alpha = 0.6, color = "steelblue") +
  geom_smooth(method = "lm", se = FALSE, color = "black") +
  facet_wrap(~variable, scales = "free_y") +
  labs(
    title = "Relación entre pasos diarios y otras variables",
    x = "Promedio de pasos diarios",
    y = NULL
  ) +
  theme_minimal()
```

A continuación, el gráfico final que contempla las estadísticas de correlación de las distintas variables, visualizado en un gráfico de dispersión:

[![Rplot.png](https://i.postimg.cc/PxpcdQ1T/Rplot.png)](https://postimg.cc/hznMrxC5)

### 4. Distribución de niveles de actividad

A partir de la segmentación de usuarias según su nivel de pasos diarios, se generó un gráfico de barras para observar la distribución entre categorías.

```r
ggplot(segmentacion_usuarios, aes(x = nivel_actividad, fill = nivel_actividad)) +
  geom_bar() +
  labs(
    title = "Segmentación de usuarios según su nivel de actividad",
    x = "Nivel de actividad (según pasos promedio diarios)",
    y = "Cantidad de usuarios"
  ) +
  scale_fill_brewer(palette = "Set2") +
  theme_minimal()
```

[![segmentacionplot.png](https://i.postimg.cc/Vky8dQ2C/segmentacionplot.png)](https://postimg.cc/QHqPyP88)

