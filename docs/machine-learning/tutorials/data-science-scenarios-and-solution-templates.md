---
title: Plantillas de soluciones de ciencia de datos
description: En este artículo se describen las plantillas específicas del sector que muestran los procedimientos recomendados y proporcionan los bloques de creación para ayudarle a implementar una solución de aprendizaje automático.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 03/29/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b039af528200782d788394f49e0bd74ed2b54dd4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728638"
---
# <a name="data-science-scenarios-and-solution-templates"></a>Escenarios de ciencia de datos y plantillas de soluciones
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

En este artículo se describe una serie de plantillas de solución de aprendizaje automático de SQL Server. Estas plantillas demuestran procedimientos recomendados y proporcionan los bloques de creación para ayudarle a implementar una solución de aprendizaje automático rápidamente. Cada plantilla está diseñada para resolver un problema específico de ciencia de datos, para un segmento o un sector en concreto.
Las tareas de cada plantilla permiten desde preparación de datos e ingeniería de características hasta el entrenamiento y la puntuación de modelos. 

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Use estas plantillas para descubrir cómo funciona [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Después, no dude en personalizar la plantilla para que se adapte a su escenario y compilar una solución personalizada.
::: moniker-end

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Use estas plantillas para obtener información sobre el funcionamiento de SQL Server Machine Learning Services. Después, no dude en personalizar la plantilla para que se adapte a su escenario y compilar una solución personalizada.
::: moniker-end

Cada solución incluye datos de ejemplo, código de R o de Python y procedimientos almacenados de SQL, si procede. El código se puede ejecutar en el entorno de desarrollo de R o Python que prefiera, y los cálculos se realizan en SQL Server. En algunos casos, puede ejecutar código directamente mediante T-SQL y cualquier herramienta cliente de SQL, como SQL Server Management Studio.

> [!TIP]
> 
> La mayoría de las plantillas tienen varias versiones que admiten plataformas locales y en la nube para el aprendizaje automático. Por ejemplo, puede compilar la solución solo con SQL Server, o bien puede compilarla en Microsoft R Server o en Azure Machine Learning.

+ Para obtener instrucciones de descarga y configuración, vea [Procedimiento para usar las plantillas](#bkmk_HowTo).

## <a name="fraud-detection"></a>Detección de fraudes

[Plantilla de detección de fraude en línea (SQL Server R Services)](https://github.com/Microsoft/r-server-fraud-detection)

**Qué:** la capacidad de detectar transacciones fraudulentas es importante para los negocios en Internet. Para reducir las pérdidas de las devoluciones, estos negocios necesitan identificar rápidamente las transacciones que se han hecho mediante credenciales o instrumentos de pago robados. Cuando se detectan transacciones fraudulentas, las empresas suelen adoptar medidas para bloquear determinadas cuentas tan pronto como sea posible, para evitar pérdidas mayores. En este escenario, aprenderá a usar los datos de las transacciones de compras en línea para identificar posibles fraudes.

**Cómo:**  La detección de fraude se resuelve como un problema de clasificación binaria. La metodología empleada en esta plantilla se puede aplicar fácilmente a la detección de fraude en otros dominios.


## <a name="campaign-optimization"></a>Optimización de campañas

[Predecir cómo y cuándo ponerse en contacto con clientes potenciales](https://microsoft.github.io/r-server-campaign-optimization/)

**Qué:** esta solución usa datos del sector de las aseguradoras para predecir clientes potenciales en función de los datos demográficos, los datos históricos de respuesta y los detalles específicos de los productos.  También se generan recomendaciones para indicar el mejor canal y momento para dirigirse a los usuarios a fin de influir en el comportamiento de compra.

**Cómo:** la solución crea y compara varios modelos. La solución también muestra la integración de datos y la preparación de datos automatizadas mediante procedimientos almacenados. Se proporcionan ejemplos paralelos para SQL Server en base de datos, en Azure y en HDInsight Spark. 

## <a name="health-care-predict-length-of-stay-in-hospital"></a>Atención sanitaria: predicción de la duración de la hospitalización 

[Predicción de la duración de la hospitalización](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**Qué:** predecir con precisión qué pacientes podrían necesitar una hospitalización de larga duración es una parte importante tanto de la asistencia como de la planeación. Los administradores deben poder determinar qué instalaciones necesitan más recursos y los cuidadores quieren tener la garantía de que podrán atender a los pacientes.

**Cómo:** esta solución usa Data Science Virtual Machine e incluye una instancia de SQL Server con aprendizaje automático habilitado. También incluye un conjunto de informes de Power BI que sirve para interactuar con un modelo implementado.

## <a name="customer-churn"></a>Abandono de clientes

[Plantilla de predicción de abandono de clientes (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/README.md)

**Qué:** el análisis y la predicción del abandono de clientes es importante en cualquier sector donde debe administrarse y evitar la pérdida de clientes a los competidores: banca, telecomunicaciones y comercial, por nombrar algunos. El objetivo del análisis del abandono es identificar qué clientes tienen probabilidades de abandonar y después adoptar las acciones adecuadas para conservar a esos clientes y mantener su negocio.

**Cómo:** esta plantilla formula el problema del abandono como un problema de **clasificación binaria**. Usa datos de ejemplo de dos orígenes, datos demográficos y transacciones del cliente, para clasificar a los clientes como con probabilidad de abandono o poca probabilidad de abandono.
  
## <a name="predictive-maintenance"></a>Mantenimiento predictivo

[Plantilla de mantenimiento predictivo (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/README.md)

**Qué:** el mantenimiento predictivo aspira a aumentar la eficacia de las tareas de mantenimiento al capturar errores anteriores y usar esa información para predecir cuándo o dónde se puede producir un error en un dispositivo. La capacidad de predecir la obsolescencia de los dispositivos es especialmente útil para las aplicaciones que dependen de sensores o datos distribuidos. Este método también se puede aplicar para supervisar o predecir errores en dispositivos IoT (Internet de las cosas).

**Cómo:** esta solución se centra en responder a la pregunta "¿Cuándo se producirá un error en un equipo en activo?". Los datos de entrada representan medidas de sensor simuladas para motores de avión. Los datos obtenidos de la supervisión de las condiciones de funcionamiento actuales del motor, como el ciclo de trabajo actual, la configuración y las medidas del sensor, se usan para crear tres tipos de modelos de predicción:

-   **Modelos de regresión**, para predecir cuánto tiempo durará un motor antes de que se produzca un error. El modelo de ejemplo predice la métrica "Vida útil restante (RUL)", también denominada "Tiempo hasta el error (TTF)".
  
-   **Modelos de clasificación**, para predecir si un motor es propenso a errores.
  
    El **modelo de clasificación binaria** predice si se producirá un error en un motor en un determinado período de tiempo.

    El **modelo de clasificación de varias clases** predice si se puede producir un error en un motor concreto y proporciona un período de tiempo probable del error. Por ejemplo, para un día determinado, puede predecir si es probable que se produzca un error en un dispositivo en el día especificado o en un periodo de tiempo después de ese día.

## <a name="energy-demand-forecasting"></a>Previsión de demanda de energía

[Plantilla de previsión de demanda de energía con SQL Server R Services](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast-Template-with-SQL-Server-R-Services-1)

**Qué:** la previsión de la demanda es un problema importante en diversos dominios, como el energético, el minorista y el de servicios. Con una previsión exacta de la demanda, es más fácil para las empresas planear mejor la producción, la asignación de recursos y la toma de otras decisiones importantes para la empresa. En el sector energético, la previsión de la demanda es fundamental para reducir el costo de almacenamiento energético y equilibrar el suministro y la demanda.

**Cómo:** esta plantilla usa SQL Server R Services para predecir la demanda de electricidad. El modelo usado para la predicción es un modelo de regresión de bosque aleatorio basado en **rxDForest**, un algoritmo de aprendizaje automático de alto rendimiento incluido en Microsoft R Server. La solución incluye un simulador de demanda, todo el código de R y T-SQL necesario para entrenar un modelo y los procedimientos almacenados que puede usar para generar y presentar las predicciones. 


## <a name="how-to-use-the-templates"></a><a name="bkmk_HowTo"></a>Procedimiento para usar las plantillas

Para descargar los archivos incluidos en cada plantilla, puede usar los comandos de GitHub o puede abrir el vínculo y hacer clic en **Descargar Zip** para guardar todos los archivos en el equipo.  Una vez descargada, la solución suele contener estas carpetas:
  
-   **Data**: contiene los datos de ejemplo de cada aplicación.
  
-   **R**: contiene todo el código de desarrollo de R que necesita para la solución. La solución requiere las bibliotecas proporcionadas por Microsoft R Server, pero también se puede abrir y editar en cualquier IDE de R. El código de R se ha optimizado para que los cálculos se realicen "en la base de datos", al establecer el contexto de cálculo en una instancia de SQL Server.
  
-   **SQLR**: contiene varios archivos .sql que se pueden ejecutar en un entorno de SQL como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para crear los procedimientos almacenados que realizan tareas relacionadas, como el procesamiento de datos, la ingeniería de características y la implementación de modelos.
  
    La carpeta también contiene un script de PowerShell que puede ejecutar para invocar todos los scripts y crear el entorno integral. Asegúrese de editar el script para que se adapte a su entorno.

## <a name="next-steps"></a>Pasos siguientes

+ [Tutoriales de Python](sql-server-python-tutorials.md)
+ [Tutoriales de R](sql-server-r-tutorials.md)