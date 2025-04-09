# FastFoodProject
Este script realiza un proceso completo de ETL (Extracción, Transformación, Carga) y Modelado Predictivo
Configuración e Importaciones:

Carga las librerías necesarias (Pandas, NumPy, SQLAlchemy, PyMongo, Scikit-learn, etc.).
Define las credenciales para conectar a las bases de datos MySQL y MongoDB (recomendado usar variables de entorno por seguridad).
Extracción (E):

Define funciones para conectarse a MySQL y MongoDB.
Extrae todas las tablas de la base de datos MySQL FastFood.
Extrae las colecciones especificadas (Ubicacion_sensores, sensor_eventos) de MongoDB.
Guarda los datos extraídos en diccionarios de DataFrames de Pandas.
Transformación y Preparación (T y L):

Define una función (transform_and_clean_data) para:
Unir (merge) los DataFrames de MySQL (tickets, ventas, productos, tiendas, regiones, etc.) para crear una tabla detallada.
Limpiar los datos: convertir tipos (fechas, números), identificar nulos.
Crear nuevas características (feature engineering): extraer año, mes, día, día de la semana, etc., de la fecha de venta.
Define una función (aggregate_data_for_model) para:
Agregar los datos de ventas detallados a nivel diario por región (contando items vendidos).
Procesar y agregar los datos de eventos de sensores (asumiendo que son de lluvia) por día y región (calculando la intensidad promedio). ¡Importante: Requiere adaptar el filtro de sensores de lluvia!
Unir los datos agregados de ventas y lluvia para crear el DataFrame final listo para el modelado.
Entrenamiento y Evaluación de Modelos:

Define una función (train_and_evaluate_models) para:
Preparar los datos agregados: seleccionar características (X) y objetivo (y), tratar nulos finales.
Dividir los datos en conjuntos de entrenamiento y prueba.
Crear pipelines de preprocesamiento para manejar datos numéricos (imputar, escalar) y categóricos (imputar, codificar con One-Hot Encoding).
Entrenar dos modelos de regresión: Regresión Lineal y Random Forest Regressor.
Evaluar los modelos en el conjunto de prueba usando métricas como RMSE, MAE y R².
Devuelve un diccionario con los resultados de la evaluación.
Ejecución Principal (if __name__ == "__main__":)

Orquesta todo el proceso: llama a las funciones de extracción, transformación, agregación y modelado en secuencia.
Imprime el progreso y los resultados intermedios.
Muestra un resumen final de la evaluación de los modelos.
Imprime una marca de tiempo al finalizar.
Análisis de Resultados:

Compara el rendimiento de los modelos entrenados.
Visualiza las predicciones vs. los valores reales.
Analiza la importancia/influencia de las características (coeficientes de Regresión Lineal, importancia de Random Forest).
Explora patrones en los datos agregados (distribuciones, relaciones entre ventas, lluvia y tiempo) mediante gráficos.
