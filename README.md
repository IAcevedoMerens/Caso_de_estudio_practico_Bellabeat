# Bellabeat Case Study

## Resumen ejecutivo

Este proyecto de análisis de datos se centra en **Bellabeat**, una empresa de tecnología del bienestar que fabrica dispositivos inteligentes enfocados en la salud femenina. El objetivo es descubrir patrones de uso y comportamiento a partir de datos de dispositivos inteligentes (*smart devices*), y así ofrecer recomendaciones basadas en datos que puedan guiar futuras estrategias de marketing.

Se utilizaron herramientas como **SQL (BigQuery)**, **R (ggplot2)** y **Excel**, aplicando el enfoque del proceso analítico propuesto en el curso profesional de Google:  
*Google Data Analytics Professional Certificate*.

**A modo de aclaración, este proyecto forma parte de una de las opciones de *"capstone projects"* de Coursera en el ya mencionado *Google Data Analytics Professional Certificate*, donde se ha elegido trabajar de manera práctica e individualmente en la exploración del análisis de los datos para comenzar un portfolio profesional y técnico**

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
  Esta pregunta permitió conocer los niveles generales de actividad, descanso y gasto energético. Fue clave para identificar tendencias, extremos y perfiles de usuario.

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

urante la fase de limpieza se llevaron a cabo diversas acciones para asegurar la calidad y consistencia de los datos:

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
