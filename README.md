Este script es un proceso automatizado para el análisis de datos de qMSP (quantitative Methylation-Specific PCR). El objetivo principal es importar, procesar, y analizar múltiples archivos de datos relacionados con la cuantificación de genes a partir de datos de qMSP. El flujo principal del script implica la limpieza de datos, el cálculo de medidas como el CT y la eficiencia, la normalización frente a un gen control (bactin), y la visualización de resultados en gráficos.

Descripción de las principales secciones:

1. Configuración del Script

	•	El encabezado del script incluye metadatos como el título, el autor y la fecha de ejecución.
	•	Configuración del formato de salida en HTML con tabla de contenido flotante y subtítulos para las figuras.

2. Carga de Bibliotecas

	•	Se cargan varias bibliotecas de R necesarias para la manipulación de datos, visualización y lectura de archivos Excel (tidyverse, ggpubr, plotly, readxl, etc.).

3. Función de Preprocesamiento

	•	PreProcessing: Set_Names_and_Qty: Identifica automáticamente los archivos .xls en el directorio, asigna nuevos nombres y carga los datos en el entorno de R, organizando los archivos para su procesamiento posterior.

4. Función check_NA

	•	Filtra los valores NA en las columnas de interés (CT, Quantity, Efficiency) y registra las muestras eliminadas en un archivo CSV. También limpia la memoria después de la operación.

5. Función check_efficiency

	•	Verifica si la eficiencia de los datos está dentro de un rango definido (por defecto 85-105). Si la eficiencia está fuera del rango, detiene el proceso y advierte sobre la curva estándar incorrecta.

6. Funciones relacionadas con el control de bactin y otros genes

	•	check_bactin_in_dataframes: Verifica si el gen control bactin está presente en los datos y filtra las columnas relevantes.
	•	check_genes_into_df: Realiza transformaciones si el gen bactin no está presente, ajustando las columnas de los genes de interés.

7. Función Calculate_Mean_Quantity

	•	Calcula la media de CT y Quantity para muestras duplicadas y las combina en un solo data frame.

8. Función Calculate_Ratio

	•	Calcula las relaciones entre los genes de interés y el gen control bactin, creando una nueva columna con la relación de CT y la cantidad entre el gen y bactin.

9. Función Calculate_Quantile

	•	Filtra los datos eliminando los valores atípicos utilizando el rango intercuartílico (IQR) y devuelve un subconjunto de datos sin los valores extremos.

10. Funciones Write_Metadata_Mean y Write_Metadata_Ratios

	•	Fusionan y renombran los data frames generados para diferentes genes y sus relaciones con bactin. Estas funciones crean un gran data frame unificado que contiene los datos combinados de todas las muestras.

11. Carga de Datos y Manipulación

	•	Carga los archivos Excel de qMSP y convierte las columnas CT, Efficiency, y Quantity a formato numérico para su procesamiento posterior. También elimina las filas que contengan valores nulos en estas columnas.

12. Cálculo de Media, Relación y Quartiles

	•	Aplica las funciones de cálculo de media y ratios sobre las muestras, concatenando los resultados en un data frame final para análisis posterior.

13. Gráficos y Visualización

	•	Se crean gráficos de caja (boxplot) para visualizar las relaciones entre los genes de interés y el gen control bactin. También se calculan y grafican las medias de cantidad y los logaritmos base 2 de esas cantidades.
	•	Los gráficos se guardan como archivos TIFF y se muestran en el documento HTML generado.

Flujo general del script:

	1.	Carga y preprocesamiento de datos: Se importan y limpian los datos de varios archivos Excel.
	2.	Validación de calidad: Se verifican condiciones como la eficiencia de las curvas estándar y la presencia del gen bactin.
	3.	Cálculo de métricas: Se calculan las medias de las variables relevantes y las relaciones entre los genes de interés y bactin.
	4.	Visualización: Se generan gráficos para representar los datos, incluidos boxplots y sus transformaciones logarítmicas.
	5.	Salida de resultados: Se exportan los resultados a archivos CSV y gráficos en formato TIFF.

Este script automatiza el análisis de datos de qMSP, desde la importación hasta la visualización y la exportación de resultados, asegurando que los datos estén correctamente procesados y normalizados antes de su análisis.
