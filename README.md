Análisis de Evasión de Clientes (Churn) en Telecomunicaciones
🔹 Introducción
Este proyecto tiene como objetivo realizar un análisis exhaustivo del problema de evasión de clientes (Churn) en una empresa de telecomunicaciones. La evasión de clientes es un desafío crítico para las empresas, ya que la retención de clientes existentes suele ser más rentable que la adquisición de nuevos. Comprender y predecir el churn permite a la empresa tomar medidas proactivas para retener a sus clientes más valiosos y optimizar sus estrategias de negocio.

El análisis se centra en identificar los factores clave que influyen en la decisión de los clientes de cancelar sus servicios, proporcionando insights valiosos y recomendaciones estratégicas basadas en los datos.

🔹 Fuente de Datos
Los datos utilizados para este análisis provienen de un archivo JSON alojado en GitHub:
https://raw.githubusercontent.com/plotly/datasets/master/telecom_churn.json

Este dataset contiene información detallada sobre clientes de una compañía de telecomunicaciones, incluyendo datos demográficos, servicios contratados, información de cuenta y, crucialmente, si el cliente ha evadido el servicio (Churn).

🔹 Limpieza y Tratamiento de Datos
Se realizaron los siguientes pasos para importar, limpiar y procesar los datos, asegurando su calidad y consistencia para el análisis:

Carga de Datos: Los datos se importaron directamente desde la URL de GitHub utilizando la librería requests y se cargaron en un DataFrame de Pandas.

Manejo de Valores Ausentes: Se identificaron y eliminaron las filas donde la columna account.Charges.Total (renombrada a total_charges) contenía valores no numéricos o ausentes, ya que estos a menudo corresponden a clientes con tenure (antigüedad) de 0.

Eliminación de Duplicados: Se verificó y eliminó cualquier fila completamente duplicada en el dataset para evitar sesgos en el análisis.

Normalización de Categorías: Los valores en columnas categóricas se convirtieron a minúsculas y se eliminaron espacios en blanco (strip()) para estandarizar las entradas y asegurar consistencia (ej., "Yes" y "yes" se tratan como la misma categoría).

Renombrado de Columnas: Las columnas se renombraron a un formato más claro y consistente (snake_case) para facilitar su manipulación y comprensión, eliminando prefijos anidados (ej., customer.gender a gender, account.Charges.Monthly a monthly_charges).

Creación de la Columna cuentas_diarias: Se calculó una nueva característica, cuentas_diarias, dividiendo el monthly_charges (cargos mensuales) por 30 (asumiendo 30 días en un mes), para obtener una visión de la facturación diaria.

Estandarización Binaria: Columnas con valores 'Yes'/'No' (y sus variantes como 'no phone service', 'no internet service') se transformaron a un formato binario (1 para 'Yes'/presencia, 0 para 'No'/ausencia). La columna gender también se convirtió a binario (male: 0, female: 1).

🔹 Análisis Exploratorio de Datos (EDA)
El análisis exploratorio de datos (EDA) se llevó a cabo para comprender la distribución de las variables y su relación con la evasión de clientes.

Estadísticas Descriptivas: Se calcularon métricas como la media, mediana, desviación estándar, etc., para las columnas numéricas (tenure, monthly_charges, total_charges, cuentas_diarias) para entender su distribución central y dispersión.

Conteo de Valores Categóricos: Se analizaron las distribuciones de frecuencia de las variables categóricas para identificar la proporción de clientes en cada categoría.

Visualización de la Distribución de Churn: Un gráfico de barras mostró la proporción de clientes que evadieron (churn: 1) y los que permanecieron (churn: 0), revelando un desequilibrio de clases.




analitza.com
Churn por Variables Categóricas: Se generaron gráficos de barras (countplot) para visualizar la tasa de churn en relación con variables como gender, contract, payment_method, internet_service, y senior_citizen.




www.researchgate.net


mascolombia.com


www.ciat.org


www.incibe.es


www.eljaya.com
Churn por Variables Numéricas: Se utilizaron gráficos de densidad (histplot con KDE) para observar cómo se distribuyen las variables numéricas (tenure, monthly_charges, total_charges, cuentas_diarias) para los clientes que evadieron y los que no.




www.researchgate.net


www.researchgate.net


startupeable.com


fastercapital.com
Análisis de Correlación:

Una matriz de correlación (heatmap) mostró las relaciones lineales entre todas las variables numéricas, incluyendo churn.




nextscenario.com
Un boxplot exploró la relación entre cuentas_diarias y churn, mostrando si los clientes con mayor evasión tienen un patrón de gasto diario diferente.




investiga.banrep.gov.co
Un gráfico de barras analizó cómo el num_services (cantidad total de servicios contratados) influye en la probabilidad de churn.




www.redalyc.org
🔹 Conclusiones e Insights
A partir del análisis exploratorio de datos, se extraen los siguientes hallazgos clave:

Desequilibrio de Clases en Churn: La mayoría de los clientes no han evadido el servicio, lo que indica un desequilibrio en la variable objetivo. Esto es importante para la selección de modelos y métricas de evaluación.

Antigüedad (tenure): Los clientes con menor antigüedad (pocos meses) tienen una tasa de evasión significativamente más alta. Esto sugiere que los primeros meses son críticos para la retención.

Tipo de Contrato (contract): Los clientes con contratos mes a mes presentan una tasa de evasión mucho mayor en comparación con aquellos con contratos de uno o dos años. Los contratos a largo plazo fomentan la lealtad.

Servicio de Internet (internet_service - Fibra Óptica): Los clientes con servicio de fibra óptica muestran una tendencia más alta a evadir el servicio en comparación con DSL o sin servicio de internet. Esto podría indicar problemas de calidad o expectativas no cumplidas con la fibra óptica.

Cargos Mensuales y Totales (monthly_charges, total_charges): Los clientes con cargos mensuales más altos, especialmente aquellos que usan fibra óptica, tienen una mayor probabilidad de evadir. Los cargos totales bajos también se asocian con mayor churn, lo que se alinea con la menor antigüedad.

Servicios Adicionales: La ausencia de servicios como seguridad en línea (online_security), respaldo en línea (online_backup), protección de dispositivos (device_protection) y soporte técnico (tech_support) está asociada con una mayor tasa de evasión. Estos servicios parecen ser factores de retención.

Método de Pago (payment_method - Cheque Electrónico): Los clientes que utilizan el cheque electrónico como método de pago tienen una tasa de evasión notablemente más alta. Esto podría estar relacionado con la facilidad de cancelación o con un perfil de cliente más propenso a cambiar.

Facturación sin Papel (paperless_billing): Los clientes con facturación sin papel muestran una tasa de evasión ligeramente más alta. Esto podría ser un indicador de un perfil de cliente más digital y propenso a buscar alternativas en línea.

Género y Ciudadano Senior (gender, senior_citizen): Estas variables no parecen tener un impacto significativo en la tasa de evasión, lo que sugiere que el churn no está fuertemente influenciado por estos factores demográficos en este dataset.

Correlación de Cargos y Antigüedad con Churn: Existe una correlación positiva moderada entre monthly_charges y churn, y una correlación negativa fuerte entre tenure y churn. Esto refuerza que los clientes nuevos y con cargos mensuales altos son más propensos a evadir.

Cuentas Diarias y Churn: La distribución de cuentas_diarias muestra que los clientes con mayor evasión tienden a tener cuentas_diarias más altas, lo que es coherente con monthly_charges.

Número de Servicios y Churn: Los clientes con menos servicios contratados (especialmente 1 o 2) tienen una mayor tasa de evasión, lo que sugiere que la diversificación de servicios aumenta la lealtad.

🔹 Recomendaciones
Basado en los hallazgos anteriores, se proponen las siguientes recomendaciones estratégicas para reducir la evasión de clientes:

Programas de Retención para Nuevos Clientes: Implementar programas de bienvenida y seguimiento intensivo durante los primeros 6 meses de servicio para clientes nuevos, ofreciendo soporte proactivo y resolviendo cualquier inquietud rápidamente.

Incentivar Contratos a Largo Plazo: Ofrecer descuentos atractivos o beneficios adicionales a los clientes que opten por contratos de uno o dos años, desincentivando los contratos mes a mes.

Mejorar la Experiencia de Fibra Óptica: Investigar y abordar las posibles causas de insatisfacción entre los clientes de fibra óptica (ej., velocidad inconsistente, problemas de conexión, soporte técnico). Mejorar la calidad del servicio y la comunicación sobre el mismo.

Promover Servicios de Valor Añadido: Educar a los clientes sobre los beneficios de la seguridad en línea, respaldo, protección de dispositivos y soporte técnico. Considerar ofrecer paquetes atractivos que incluyan estos servicios.

Optimizar Métodos de Pago: Analizar por qué los clientes que usan cheque electrónico tienen mayor churn. Podría implicar ofrecer incentivos para cambiar a métodos de pago más estables (ej., domiciliación bancaria) o mejorar la experiencia de pago con cheque electrónico.

Segmentación y Ofertas Personalizadas: Utilizar los insights sobre los perfiles de alto riesgo (ej., contratos mes a mes, fibra óptica, sin servicios adicionales) para crear campañas de retención personalizadas.

Monitoreo Continuo: Establecer un sistema de monitoreo continuo de las métricas de churn y los factores influyentes para adaptar las estrategias en tiempo real.

Feedback del Cliente: Implementar encuestas de satisfacción y canales de feedback para identificar problemas antes de que el cliente decida irse.

Paquetes de Servicios: Diseñar paquetes de servicios que incluyan múltiples ofertas (ej., internet, teléfono, seguridad) para aumentar el número de servicios por cliente y, por ende, su lealtad.

🔹 Cómo Ejecutar el Proyecto
Para ejecutar este análisis, necesitarás un entorno Python con las siguientes librerías instaladas:

pandas

requests

matplotlib

seaborn

Puedes instalar estas librerías usando pip:
pip install pandas requests matplotlib seaborn

Luego, puedes ejecutar el script de Python (el contenido del Canvas) en tu entorno. Asegúrate de que la json_url en el script apunte a la ubicación correcta del archivo JSON.
