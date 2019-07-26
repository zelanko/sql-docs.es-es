---
title: Escenarios de ciencia de datos y plantillas de soluciones
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: cb144eb5c766b417884f6f1adb67dc0ac48504a5
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469777"
---
# <a name="data-science-scenarios-and-solution-templates"></a>Escenarios de ciencia de datos y plantillas de soluciones
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Las plantillas son soluciones de ejemplo que muestran los procedimientos recomendados y proporcionan los bloques de creación para ayudarle a implementar una solución rápida. Cada plantilla está diseñada para resolver un problema específico, para un sector o vertical específico. Las tareas de cada plantilla permiten desde preparación de datos e ingeniería de características hasta el entrenamiento y la puntuación de modelos. Use estas plantillas para obtener información [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] sobre cómo funciona. A continuación, no dude en personalizar la plantilla para que se adapte a su propio escenario y crear una solución personalizada. 

Cada solución incluye datos de ejemplo, código de R o código Python y procedimientos almacenados de SQL, si procede. El código se puede ejecutar en el entorno de desarrollo de R o Python preferido, con cálculos realizados en SQL Server. En algunos casos, puede ejecutar código directamente mediante T-SQL y cualquier herramienta de cliente SQL, como SQL Server Management Studio.

> [!TIP]
> 
> La mayoría de las plantillas tienen varias versiones que admiten plataformas locales y en la nube para el aprendizaje automático. Por ejemplo, puede compilar la solución usando solo SQL Server, o puede compilar la solución en Microsoft R Server o en Azure Machine Learning.

+ Para obtener instrucciones de descarga y configuración, consulte [Cómo usar las plantillas](#bkmk_HowTo).

## <a name="fraud-detection"></a>Detección de fraude

[Plantilla de detección de fraudes en línea (SQL Server R Services)](https://github.com/Microsoft/r-server-fraud-detection)

**Elemento** La capacidad de detectar transacciones fraudulentas es importante para las empresas en línea. Para reducir las pérdidas de cobros, las empresas necesitan identificar rápidamente las transacciones que se realizaron usando instrumentos o credenciales de pago robados. Cuando se detectan transacciones fraudulentas, las empresas suelen adoptar medidas para bloquear determinadas cuentas tan pronto como sea posible, para evitar pérdidas mayores. En este escenario, aprenderá a usar los datos de las transacciones de compra en línea para identificar posibles fraudes.

**Qué**  La detección de fraude se resuelve como un problema de clasificación binaria. La metodología empleada en esta plantilla se puede aplicar fácilmente a la detección de fraude en otros dominios.


## <a name="campaign-optimization"></a>Optimización de campañas

[Predecir cómo y cuándo ponerse en contacto con clientes potenciales](https://microsoft.github.io/r-server-campaign-optimization/)

**Elemento** Esta solución utiliza datos del sector de seguros para predecir clientes potenciales en función de los datos demográficos, los datos de respuesta histórica y los detalles específicos del producto.  También se generan recomendaciones para indicar el mejor canal y el mejor tiempo para que los usuarios puedan influir en el comportamiento de compra.

**Qué** La solución crea y compara varios modelos. La solución también muestra la integración de datos automatizada y la preparación de datos mediante procedimientos almacenados. Se proporcionan ejemplos paralelos para SQL Server en la base de datos, en Azure y en HDInsight Spark. 

## <a name="health-care-predict-length-of-stay-in-hospital"></a>Atención sanitaria: predicción de la duración de la estancia en el hospital 

[Predicción de la duración de la estancia en hospitales](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**Elemento** Predecir con precisión qué pacientes pueden requerir hospital a largo plazo es una parte importante del cuidado y el planeamiento. Los administradores deben tener la capacidad de determinar qué instalaciones requieren más recursos y los cuidadosles desean garantizar que puedan satisfacer las necesidades de los pacientes.

**Qué** Esta solución utiliza el Data Science Virtual Machine e incluye una instancia de SQL Server con machine learning habilitado. También incluye un conjunto de informes de Power BI que puede usar para interactuar con un modelo implementado.

## <a name="customer-churn"></a>Renovación de clientes

[Plantilla de predicción de renovación de clientes (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/README.md)

**Elemento** El análisis y la predicción de la renovación de los clientes es importante en cualquier sector en el que se debe administrar y evitar la pérdida de clientes a los competidores: Banca, telecomunicaciones y minorista, por nombrar algunas. El objetivo del análisis del abandono es identificar qué clientes tienen probabilidades de abandonar y después adoptar las acciones adecuadas para conservar a esos clientes y mantener su negocio.

**Qué** Esta plantilla formula el problema de renovación como un problema de **clasificación binaria** . Usa datos de ejemplo de dos orígenes, datos demográficos y transacciones del cliente, para clasificar a los clientes como con probabilidad de abandono o poca probabilidad de abandono.
  
## <a name="predictive-maintenance"></a>Mantenimiento predictivo

[Plantilla de mantenimiento predictivo (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/README.md)

**Elemento** El mantenimiento predictivo pretende aumentar la eficacia de las tareas de mantenimiento mediante la captura de errores pasados y el uso de esa información para predecir cuándo o dónde puede producirse un error en un dispositivo. La capacidad de predecir la obsolescencia del dispositivo es especialmente útil para las aplicaciones que se basan en sensores o datos distribuidos. Este método también se puede aplicar para supervisar o predecir errores en dispositivos IoT (Internet de las cosas).

**Qué** Esta solución se centra en responder a la pregunta "¿Cuándo se producirá un error en un equipo en servicio?" Los datos de entrada representan medidas de sensor simuladas para motores de avión. Los datos obtenidos de la supervisión de las condiciones de funcionamiento actuales del motor, como el ciclo de trabajo actual, la configuración y las medidas del sensor, se usan para crear tres tipos de modelos predictivos:

-   **Modelos de regresión**, para predecir cuánto tiempo durará un motor antes de que se produzca un error. El modelo de ejemplo predice la métrica "vida útil restante" (RUL), también denominada "tiempo para el error" (TTF).
  
-   **Modelos de clasificación**, para predecir si un motor es propenso a errores.
  
    El **modelo de clasificación binaria** predice si un motor producirá un error dentro de un período de tiempo determinado.

    El **modelo de clasificación multiclase** predice si un motor determinado puede producir un error y proporciona un período de tiempo probable de error. Por ejemplo, para un día determinado, puede predecir si es probable que se produzca un error en un dispositivo en el día especificado o en un periodo de tiempo después de ese día.

## <a name="energy-demand-forecasting"></a>Previsión de la demanda de energía

[Plantilla de previsión de la demanda de energía con SQL Server R Services](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast-Template-with-SQL-Server-R-Services-1)

**Qué:** : La previsión de la demanda es un problema importante en diversos dominios, como la energía, el minorista y los servicios. La previsión de la demanda precisa ayuda a las empresas a llevar a cabo una mejor planeación de producción, la asignación de recursos y tomar otras decisiones empresariales importantes. En el sector energético, la previsión de la demanda es fundamental para reducir el costo de almacenamiento energético y equilibrar el suministro y la demanda.

**Qué** Esta plantilla usa SQL Server R Services para predecir la demanda de electricidad. El modelo usado para la predicción es un modelo de regresión de bosque aleatorio basado en **rxDForest**, un algoritmo de aprendizaje automático de alto rendimiento incluido en Microsoft R Server. La solución incluye un simulador de demanda, todo el código de R y T-SQL necesario para entrenar un modelo y los procedimientos almacenados que puede usar para generar y presentar las predicciones. 


## <a name="bkmk_HowTo"></a>Cómo usar las plantillas

Para descargar los archivos incluidos en cada plantilla, puede usar los comandos de GitHub o puede abrir el vínculo y hacer clic en **Descargar Zip** para guardar todos los archivos en el equipo.  Una vez descargada, la solución suele contener estas carpetas:
  
-   **Datos**: Contiene los datos de ejemplo de cada aplicación.
  
-   **R**: Contiene todo el código de desarrollo de R que necesita para la solución. La solución requiere las bibliotecas proporcionadas por Microsoft R Server, pero también se puede abrir y editar en cualquier IDE de R. El código de R se ha optimizado para que los cálculos se realicen "en la base de datos", al establecer el contexto de cálculo en una instancia de SQL Server.
  
-   **SQLR**: Contiene varios archivos. SQL que se pueden ejecutar en un entorno de SQL como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , por ejemplo, para crear los procedimientos almacenados que realizan tareas relacionadas, como el procesamiento de datos, la ingeniería de características y la implementación de modelos.
  
    La carpeta también contiene un script de PowerShell que puede ejecutar para invocar todos los scripts y crear el entorno integral. Asegúrese de editar el script para que se adapte a su entorno.

## <a name="next-steps"></a>Pasos siguientes

+ [Tutoriales de SQL Server machine learning](machine-learning-services-tutorials.md)




