---
title: SQL Server Machine Learning Services tutoriales | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b692b9660c3caec18c689f56ba382f8df194a9cc
ms.sourcegitcommit: b1990ec4491b5a8097c3675334009cb2876673ef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/17/2018
ms.locfileid: "49384130"
---
# <a name="tutorials-for-sql-server-machine-learning-services"></a>Tutoriales de SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se proporciona una lista completa de los tutoriales, demostraciones y aplicaciones de ejemplo que usan características de aprendizaje automático en SQL Server 2016 o SQL Server 2017. Comience aquí para obtener información sobre cómo ejecutar R o Python desde T-SQL, cómo usar contextos de cálculo local y remota y cómo optimizar el código de R y Python para un entorno de producción de SQL.

+ [Tutoriales de Python](../tutorials/sql-server-python-tutorials.md)

+ [Tutoriales de R](../tutorials/sql-server-r-tutorials.md)

Para obtener más información sobre los requisitos y cómo configurar la aplicación, consulte [requisitos previos](#bkmk_prerequisites).

## <a name="samples-and-solutions"></a>Ejemplos y soluciones

+ [Ejemplos](#bkmk_samples) 

    Estos escenarios del mundo real del equipo de desarrollo de SQL Server muestran cómo incrustar el aprendizaje automático en las aplicaciones. Todas las muestras incluyen código que puede descargar, modificar y utilizar en producción.

+ [Soluciones](#bkmk_solutions) 

    Las plantillas desde el equipo de ciencia de datos de Microsoft son personalizables, para empezar a trabajar rápidamente con aprendizaje automático. Cada solución se adapta a un problema específico de la tarea o del sector. La mayoría de las soluciones está diseñada para ejecutarse en SQL Server, o en un entorno de nube como Azure Machine Learning. Otras soluciones pueden ejecutar en Linux o en los clústeres de Spark o Hadoop, mediante el uso de Microsoft R Server o Machine Learning Server.

### <a name ="bkmk_samples"></a>Muestras de productos de SQL Server

Estos ejemplos y demostraciones proporcionadas por el equipo de desarrollo de SQL Server y R Server resaltan formas en que puede usar análisis insertados en aplicaciones del mundo real.

| Vínculo | Descripción | Se aplica a |
|------|-------------|------------|
| [Realizar el cliente clústeres que usan R y SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | Usar aprendizaje no supervisado para segmentar los clientes en función de los datos de ventas. En este ejemplo se usa el algoritmo de rxKmeans escalable de Microsoft R para generar el modelo de agrupación en clústeres. | SQL Server 2016 o SQL Server 2017 |
| [Realizar el cliente agrupación en clústeres con Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | Obtenga información sobre cómo usar el algoritmo de Kmeans para realizar una agrupación en clústeres no supervisado de los clientes. En este ejemplo utiliza el lenguaje Python en database.| SQL Server 2017 |
| [Crear un modelo predictivo con R y SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | Obtenga información sobre cómo una empresa de alquiler de esquís puede usar el aprendizaje automático para predecir alquileres futuros, que permite el plan de negocio y personal para satisfacer la demanda futura. Este ejemplo utiliza los algoritmos de Microsoft para compilar la regresión logística y los modelos de árboles de decisión. | SQL Server 2016 o SQL Server 2017 |
| [Crear un modelo predictivo con Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | Compile la aplicación de análisis de alquiler de esquí mediante Python, para ayudar a planear la demanda futura. Este ejemplo usa la nueva biblioteca de Python, **revoscalepy**, para crear un modelo de regresión lineal. | SQL Server 2017 |
| [Uso de Tableau con SQL Server Machine Learning Services](https://blogs.msdn.microsoft.com/mlserver/2017/12/14/how-to-use-tableau-with-sql-server-machine-learning-services-with-r-and-python/) | Analizar los medios sociales y crear gráficos de una plantilla, con SQL Server y R. | SQL Server 2016 o SQL Server 2017 |

### <a name="bkmk_solutions"></a>Plantillas de solución

El equipo de ciencia de datos de Microsoft ha proporcionado plantillas de solución que pueden usarse para impulsar soluciones para escenarios comunes. Se proporciona todo el código, así como instrucciones sobre cómo entrenar e implementar un modelo de puntuación mediante procedimientos almacenados de SQL Server.

+ [Detección de fraude](https://gallery.cortanaanalytics.com/Tutorial/Online-Fraud-Detection-Template-with-SQL-Server-R-Services-1)
+ [Predicción personalizada de abandono](https://gallery.cortanaanalytics.com/Tutorial/Customer-Churn-Prediction-Template-with-SQL-Server-R-Services-1)
+ [Mantenimiento predictivo](https://gallery.cortanaanalytics.com/Tutorial/Predictive-Maintenance-Template-with-SQL-Server-R-Services-1)
+ [Predecir la duración del hospital de la estancia](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

Para obtener más información, consulte [Plantillas de aprendizaje automático con SQL Server 2016 R Services](https://blogs.technet.microsoft.com/machinelearning/2016/03/23/machine-learning-templates-with-sql-server-2016-r-services/).

## <a name="more-resources-and-reading"></a>Más recursos y lectura

+ [¿Por qué genérelo?](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/01/10/sql-server-r-services-why-did-we-build-it/)

    ¿Quiere conocer la verdadera historia tras R Services? Lea este artículo desde el equipo de desarrollo y P.M. que explica los objetivos de SQL Server R Services y el origen.

+ [Tutoriales y los datos de ejemplo para Microsoft R](https://docs.microsoft.com/machine-learning-server/r/tutorial-introduction)

    Obtenga información sobre Microsoft R y lo que el paquete RevoScaleR que ofrece en esta colección de tutoriales rápidos. Obtenga información sobre cómo escribir código de R una vez e implementar en cualquier lugar, con orígenes de datos de RevoScaleR y contextos de cálculo remoto.

+ [Introducción a MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package)

  Obtenga información sobre cómo usar los nuevos algoritmos en el paquete MicrosoftML para el modelado avanzado y las transformaciones de datos escalable, optimizadas para varios contextos de cálculo.
