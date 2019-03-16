---
title: 'Escenarios de ciencia de datos y plantillas de solución: SQL Server Machine Learning'
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1c98f6110aa6cc0bbb86f04a685211d7dc58447a
ms.sourcegitcommit: 671370ec2d49ed0159a418b9c9ac56acf43249ad
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/15/2019
ms.locfileid: "58072159"
---
# <a name="data-science-scenarios-and-solution-templates"></a>Escenarios de ciencia de datos y plantillas de solución
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Las plantillas son soluciones de ejemplo que muestran los procedimientos recomendados y proporcionan los bloques de creación para ayudarle a implementar una solución rápida. Cada plantilla está diseñada para resolver un problema específico, para un específico vertical o del sector. Las tareas de cada plantilla permiten desde preparación de datos e ingeniería de características hasta el entrenamiento y la puntuación de modelos. Use estas plantillas para obtener información sobre cómo [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] funciona. A continuación, no dude en Personalizar la plantilla para ajustarse a su propio escenario y crear una solución personalizada. 

Cada solución incluye datos de ejemplo, código de R o código de Python y procedimientos almacenados de SQL si es aplicable. El código se puede ejecutar en el entorno de desarrollo de R o Python preferido, los cálculos que se realiza en SQL Server. En algunos casos, puede ejecutar código directamente mediante Transact-SQL y cualquier herramienta de cliente SQL, como SQL Server Management Studio.

> [!TIP]
> 
> La mayoría de las plantillas tienen varias versiones que admiten tanto en el entorno local y plataformas para el aprendizaje automático en la nube. Por ejemplo, puede compilar la solución con SQL Server sólo, o puede crear la solución en Microsoft R Server o en Azure Machine Learning.

+ Para obtener detalles y actualizaciones, consulte este anuncio: [Plantillas nuevas e interesantes en Azure Machine Learning](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)

+ Para su descarga e instrucciones de configuración, consulte [cómo usar las plantillas de](#bkmk_HowTo).

## <a name="fraud-detection"></a>Detección de fraude

[Plantilla de detección de fraudes en línea (SQL Server R Services)](https://github.com/Microsoft/r-server-fraud-detection)

**Qué:** La capacidad para detectar transacciones fraudulentas es importante para las empresas en línea. Para reducir las pérdidas de cargo al usuario, las empresas necesitan identificar rápidamente las transacciones que se realizaron con instrumentos de pago robados o credenciales. Cuando se detectan transacciones fraudulentas, las empresas suelen adoptar medidas para bloquear determinadas cuentas tan pronto como sea posible, para evitar pérdidas mayores. En este escenario, aprenderá a usar los datos de las transacciones de compra en línea para identificar posibles fraudes.

**Cómo:**  La detección de fraude se resuelve como un problema de clasificación binaria. La metodología empleada en esta plantilla se puede aplicar fácilmente a la detección de fraude en otros dominios.


## <a name="campaign-optimization"></a>Optimización de campañas

[Predecir cómo y cuándo ponerse en contacto con clientes potenciales](https://microsoft.github.io/r-server-campaign-optimization/)

**Qué:** Esta solución utiliza datos de sector de seguros para predecir clientes potenciales basadas en datos demográficos, datos históricos de respuesta y detalles específicos del producto.  También se generaron las recomendaciones para indicar el mejor canal y hora a los usuarios de enfoque para influir en el comportamiento de compra.

**Cómo:** La solución se crea y compara varios modelos. La solución también muestra la integración de datos automatizada y preparación de datos mediante procedimientos almacenados. Se proporcionan ejemplos en paralelo de SQL Server en bases de datos, en Azure y HDInsight Spark. 

## <a name="health-care-predict-length-of-stay-in-hospital"></a>Atención médica: predecir la duración de la estancia en hospitales 

[Predicción de la duración de la estancia en hospitales](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**Qué:** Predecir con precisión que los pacientes pueden requerir hospitalización a largo plazo es una parte importante de atención y planeación. Los administradores necesitan poder determinar qué instalaciones requieren más recursos y proveedores de atención médica desean garantizar que pueden satisfacer las necesidades de los pacientes.

**Cómo:** Esta solución usa la máquina Virtual de ciencia de datos e incluye una instancia de SQL Server con el aprendizaje automático habilitado. También incluye un conjunto de informes de Power BI que puede usar para interactuar con un modelo implementado.

## <a name="customer-churn"></a>Abandono de clientes

[Plantilla de predicción de abandono de clientes (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/README.md)

**Qué:** Analizar y predecir el abandono de clientes es importante en cualquier sector donde debe administrarse y evitar la pérdida de clientes a los competidores: banca, telecomunicaciones y comercial, por nombrar algunos. El objetivo del análisis del abandono es identificar qué clientes tienen probabilidades de abandonar y después adoptar las acciones adecuadas para conservar a esos clientes y mantener su negocio.

**Cómo:** Esta plantilla Formula del problema como un **clasificación binaria** problema. Usa datos de ejemplo de dos orígenes, datos demográficos y transacciones del cliente, para clasificar a los clientes como con probabilidad de abandono o poca probabilidad de abandono.
  
## <a name="predictive-maintenance"></a>Mantenimiento predictivo

[Plantilla de mantenimiento predictivo (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/README.md)

**Qué:** Mantenimiento predictivo pretende aumentar la eficacia de las tareas de mantenimiento mediante la captura de errores del pasado y usar esa información para predecir cuándo o dónde se puede producir un error en un dispositivo. La capacidad de previsión de obsolescencia de los dispositivos es especialmente valiosa para aquellas aplicaciones que se basan en datos distribuidos o sensores. Este método también se pueden aplicar para supervisar o predecir errores en los dispositivos de IoT (Internet de las cosas).

Vea este anuncio para obtener más información: [Nueva plantilla de mantenimiento predictivo](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)

**Cómo:** Esta solución se centra en responder a la pregunta, "Cuando en un equipo producirá un error?" Los datos de entrada representan medidas de sensor simuladas para motores de avión. Los datos obtenidos de la supervisión de condiciones de funcionamiento actuales del motor, como el ciclo de trabajo actual, la configuración y las medidas de sensor, se usan para crear tres tipos de modelos de predicción:

-   **Modelos de regresión**, para predecir cuánto tiempo durará un motor antes de que se produzca un error. El modelo de ejemplo predice la métrica "Vida útil restante" (RUL), también se denomina "Tiempo a Failure" (THF).
  
-   **Modelos de clasificación**, para predecir si un motor es propenso a errores.
  
    El **modelo de clasificación binaria** predice si se producirá un error en un motor de un período de tiempo determinado.

    El **modelo de clasificación multiclase** predice si un motor concreto podría producir un error y proporciona una ventana de tiempo probable del error. Por ejemplo, para un día determinado, puede predecir si es probable que se produzca un error en un dispositivo en el día especificado o en un periodo de tiempo después de ese día.

## <a name="energy-demand-forecasting"></a>Previsión de demanda de energía

[La plantilla con SQL Server R Services de previsión de demanda de energía](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast-Template-with-SQL-Server-R-Services-1)

**Qué:**: Previsión de demanda es un problema importante en diversos dominios incluidos energía, venta directa y servicios. Previsión de demanda precisa ayuda a las empresas realizar producción mejor planeación, asignación de recursos y tomar otras decisiones empresariales importantes. En el sector energético, la previsión de demanda es fundamental para reducir el costo de almacenamiento de energía y equilibrio de suministro y demanda.

**Cómo:** Esta plantilla usa SQL Server R Services para predecir la demanda de electricidad. El modelo utilizado para la predicción es un modelo de regresión de bosque aleatorio basado en **rxDForest**, un algoritmo que se incluyen en Microsoft R Server de aprendizaje de automático de alto rendimiento. La solución incluye un simulador de demanda, todo el código de R y T-SQL necesario para entrenar un modelo y los procedimientos almacenados que puede usar para generar y presentar las predicciones. 


## <a name="bkmk_HowTo"></a>Cómo usar las plantillas

Para descargar los archivos incluidos en cada plantilla, puede usar los comandos de GitHub o puede abrir el vínculo y hacer clic en **Descargar Zip** para guardar todos los archivos en el equipo.  Una vez descargada, la solución suele contener estas carpetas:
  
-   **Datos**: Contiene los datos de ejemplo para cada aplicación.
  
-   **R**: Contiene todo el código de desarrollo de R que necesita para la solución. La solución requiere las bibliotecas proporcionadas por Microsoft R Server, pero también se puede abrir y editar en cualquier IDE de R. El código de R se ha optimizado para que los cálculos se realicen "en la base de datos", al establecer el contexto de cálculo en una instancia de SQL Server.
  
-   **SQLR**: Contiene varios archivos .sql que se pueden ejecutar en un entorno de SQL como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para crear los procedimientos almacenados que realizan tareas relacionadas como procesamiento de datos, ingeniería de características e implementación de modelos.
  
    La carpeta también contiene un script de PowerShell que puede ejecutar para invocar todos los scripts y crear el entorno integral. Asegúrese de editar el script para que se adapte a su entorno.

## <a name="next-steps"></a>Pasos siguientes

+ [Tutoriales sobre aprendizaje automático de SQL Server](machine-learning-services-tutorials.md)




