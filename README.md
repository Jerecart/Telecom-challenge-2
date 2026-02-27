Análisis Predictivo de Churn en la Industria de Telecomunicaciones
Este repositorio contiene un análisis exhaustivo de la evasión de clientes (Churn) en una base de datos simulada del sector de telecomunicaciones. El objetivo principal es identificar patrones, factores y comportamientos que contribuyen a que los clientes cancelen sus servicios, y desarrollar modelos predictivos para anticipar el churn.

1. Introducción
El presente informe tiene como fin analizar el fenómeno del Churn en telecomunicaciones, crucial para la retención de clientes y la rentabilidad. Se exploran los datos, se realizan análisis descriptivos y se buscan insights para desarrollar estrategias de prevención de la evasión.

2. Limpieza y Tratamiento de Datos
Los datos fueron obtenidos de una API externa (jsonplaceholder) y cargados en un DataFrame de Pandas. Los pasos de preprocesamiento incluyeron:

Eliminación de Columnas No Relevantes: userId e id fueron eliminadas al no aportar valor predictivo.
Verificación de Integridad: Se confirmó la ausencia de valores faltantes y filas duplicadas.
Simulación de Variables: Se añadieron columnas simuladas como churn, genero, tipo_contrato y metodo_pago para enriquecer el análisis.
Codificación de Variables Categóricas: Las variables categóricas fueron transformadas a formato numérico mediante One-Hot Encoding.
Evaluación del Desbalance de Clases: Se identificó un desbalance significativo en la variable churn (18% 'churn' vs. 82% 'no churn').
3. Análisis Exploratorio de Datos (EDA)
El EDA se centró en comprender la distribución de churn y su correlación con otras variables:

Distribución de Churn: Proporción del 18% de clientes que 'Se dieron de baja'.
Correlación con Churn:
tipo_contrato_Mensual mostró la correlación positiva más fuerte (0.21), indicando una mayor propensión a la cancelación.
metodo_pago_Transferencia Bancaria (0.10) también correlacionó positivamente.
metodo_pago_Efectivo (-0.17) y metodo_pago_Tarjeta de Crédito (-0.12) mostraron correlaciones negativas, asociándose con menor churn.
genero_Masculino tuvo una correlación muy débil (0.05).
4. Modelado Predictivo de Churn
División del Conjunto de Datos
El dataset se dividió en entrenamiento (80%) y prueba (20%) con estratificación por la variable churn.

Construcción y Evaluación de Modelos (Primera Iteración - Antes de SMOTE)
Se entrenaron dos modelos iniciales:

Regresión Logística (con Estandarización): Alta Accuracy (0.80) pero falló completamente en predecir la clase churn (Precision, Recall, F1-score de 0.00 para la clase 1).
Random Forest Classifier (sin Estandarización): Similar a la Regresión Logística, también mostró Accuracy de 0.80 y una incapacidad total para predecir la clase churn.
Ambos modelos estuvieron sesgados hacia la clase mayoritaria ('no churn') debido al desbalance de clases.

Manejo del Desbalance de Clases con SMOTE y Re-entrenamiento
Para abordar el desbalance, se aplicó SMOTE (Synthetic Minority Over-sampling Technique) al conjunto de entrenamiento, balanceando las clases (66 'no churn' vs. 66 'churn').

Se re-entrenaron ambos modelos con el conjunto de entrenamiento balanceado por SMOTE:

Regresión Logística con SMOTE y Estandarización:

Accuracy: 0.80
Classification Report (Clase 1 - Churn): Precision: 0.50, Recall: 0.50, F1-score: 0.50
Confusion Matrix: [[14 2], [2 2]]
Random Forest con SMOTE (sin Estandarización):

Accuracy: 0.80
Classification Report (Clase 1 - Churn): Precision: 0.50, Recall: 0.50, F1-score: 0.50
Confusion Matrix: [[14 2], [2 2]]
La aplicación de SMOTE mejoró significativamente la capacidad de ambos modelos para detectar la clase minoritaria (churn), permitiendo identificar a la mitad de los clientes que cancelan.

5. Conclusiones e Insights del Análisis de Churn
Distribución General de Churn: 18% de los clientes 'Se dieron de baja'.
Churn por Tipo de Contrato: Los contratos mensuales están fuertemente asociados con un mayor churn.
Churn por Método de Pago: Ciertos métodos como 'Transferencia Bancaria' y 'Cheque Electrónico' se asocian con mayor churn, mientras que 'Tarjeta de Crédito' y 'Efectivo' con menor churn.
Impacto del Desbalance de Clases: Fundamental manejarlo para que los modelos detecten la clase minoritaria.
Rendimiento del Modelo: Ambos modelos mejoraron notablemente en la predicción del churn después de SMOTE, alcanzando un 50% de Precision y Recall para la clase minoritaria.
6. Análisis de la Relevancia de las Variables
Regresión Logística (Coeficientes):
tipo_contrato_Mensual tuvo el coeficiente positivo más alto (0.556), siendo el mayor impulsor de churn.
Los metodo_pago como 'Efectivo' (-1.424) y 'Tarjeta de Crédito' (-1.034) mostraron los coeficientes negativos más fuertes, reduciendo la probabilidad de churn.
Random Forest (Importancia de Características):
metodo_pago_Tarjeta de Crédito (0.277) y metodo_pago_Efectivo (0.227) fueron las más importantes.
tipo_contrato_Mensual (0.211) también fue muy relevante.
Ambos modelos coinciden en la alta influencia del tipo de contrato y el método de pago en el churn.

7. Recomendaciones Estratégicas para la Mitigación del Churn
Incentivar Contratos a Largo Plazo: Ofrecer descuentos y beneficios para que clientes mensuales migren a planes anuales o bienales.
Optimización de la Experiencia de Pago: Mejorar la usabilidad de métodos de pago asociados a alto churn (ej. 'Cheque Electrónico', 'Transferencia Bancaria') y promocionar métodos de bajo churn.
Programas de Retención Personalizados: Utilizar los modelos predictivos para identificar clientes de alto riesgo y dirigirles ofertas o soporte proactivo.
Monitoreo Continuo y Análisis Predictivo: Implementar un sistema para seguir las tasas de churn por segmento y actualizar los modelos para una acción rápida.
La implementación de estas recomendaciones contribuirá a reducir el churn, fortalecer la relación con los clientes y asegurar un crecimiento sostenible.
