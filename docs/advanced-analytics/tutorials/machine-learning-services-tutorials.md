---
title: Tutoriales de SQL Server R y Python
description: Ejemplos y tutoriales de scripting de R y Python en SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 9a212160c17e4cc3c8322af6026c9e2e4df97254
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343610"
---
# <a name="sql-server-machine-learning-tutorials-in-r-and-python"></a>SQL Server Machine Learning tutoriales en R y Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se proporciona una lista completa de los tutoriales y ejemplos de código que muestran las características de aprendizaje automático de [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) o [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md). 

+ Los inicios rápidos usan datos integrados o no tienen datos para una exploración rápida con menos esfuerzo.
+ Los tutoriales profundizan más en las tareas, los conjuntos de valores más grandes y las explicaciones más largas.
+ Los ejemplos y las soluciones están destinados a los desarrolladores que prefieren empezar con código, trabajando hacia atrás en conceptos y lecciones para rellenar los huecos de conocimiento.

Aprenderá a usar las bibliotecas de R y Python con datos relacionales residentes en el mismo contexto operativo, cómo usar SQL Server procedimientos almacenados para ejecutar e implementar código personalizado, y cómo llamar a las bibliotecas de Microsoft R y Python para datos de alto rendimiento. tareas de ciencia y aprendizaje automático.

Como primer paso, revise los conceptos básicos respaldados por la integración de R y Python de Microsoft con SQL Server.

## <a name="concepts"></a>Conceptos

El análisis en base de datos hace referencia a la compatibilidad nativa con R y Python en SQL Server cuando se instala SQL Server Machine Learning Services o 2016 SQL Server R Services (R Only) como un complemento al motor de base de datos. La integración de R y Python incluye distribuciones base de código abierto, además de bibliotecas específicas de Microsoft para el análisis de alto rendimiento.

Desde un punto de la arquitectura, el código se ejecuta como un proceso externo en el cuadro para conservar la integridad del motor de base de datos. Sin embargo, toda la seguridad y el acceso a los datos se realiza a través de SQL Server roles y permisos de la base de datos, lo que significa que cualquier aplicación con acceso a SQL Server puede acceder a su script de R y Python al implementarlo como un procedimiento almacenado, o serializar y guardar un modelo entrenado en un SQL. Base de datos de servidor.

Las principales diferencias entre la compatibilidad con R y Python en SQL Server frente a la compatibilidad con lenguajes equivalentes en otros productos y servicios de Microsoft incluyen:

+ Capacidad para "empaquetar" código en procedimientos almacenados o como modelos binarios.
+ Escriba código que llame a las bibliotecas de Microsoft R y Python instaladas localmente con los archivos de programa de SQL Server.
+ Aplique la arquitectura de seguridad de base de datos de SQL Server a sus soluciones de R y Python.
+ Aproveche la infraestructura de SQL Server y la compatibilidad administrativa con sus soluciones personalizadas.

## <a name="quickstarts"></a>Tutoriales rápidos

Comience aquí para obtener información sobre cómo ejecutar R o Python desde T-SQL y cómo poner en funcionamiento el código de R y Python para un entorno de producción de SQL.

+ [Python Ejecución de Python con T-SQL](run-python-using-t-sql.md)
+ [R: Hola mundo en R y SQL](rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [R: Controlar entradas y salidas](rtsql-working-with-inputs-and-outputs.md)
+ [R: Controlar tipos de datos y objetos](rtsql-r-and-sql-data-types-and-data-objects.md)
+ [R: Uso de funciones de R](rtsql-using-r-functions-with-sql-server-data.md)
+ [R: Crear un modelo predictivo](rtsql-create-a-predictive-model-r.md)
+ [R: Predecir y trazar desde el modelo](rtsql-predict-and-plot-from-model.md)

## <a name="tutorials"></a>Tutoriales

Cree su primera experiencia con R y Python y T-SQL examinando más de cerca los paquetes de Microsoft y las operaciones más especializadas, como el cambio de los contextos de cálculo locales a remotos.

+ [Tutoriales de Python](sql-server-python-tutorials.md)
+ [Tutoriales de R](sql-server-r-tutorials.md)

<a name ="bkmk_samples"></a>

## <a name="samples"></a>Muestras

Estos ejemplos y demostraciones proporcionados por el equipo de desarrollo de SQL Server y R Server resaltan las formas en que puede usar análisis insertados en aplicaciones reales.

| Vínculo | Descripción | 
|------|-------------|
| [Realice la agrupación en clústeres de clientes con R y SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | Use el aprendizaje sin supervisión para segmentar a los clientes en función de los datos de ventas. En este ejemplo se usa el algoritmo rxKmeans escalable de Microsoft R para generar el modelo de agrupación en clústeres. |
| [Realice la agrupación en clústeres de clientes con Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | Obtenga información acerca de cómo usar el algoritmo Kmeans para realizar clústeres sin supervisión de clientes. En este ejemplo se usa el lenguaje Python en la base de datos.| SQL Server 2017 |
| [Crear un modelo predictivo con R y SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | Obtenga información sobre cómo una empresa de alquiler de esquí podría usar el aprendizaje automático para predecir alquileres futuros, lo que ayuda al plan empresarial y al personal a satisfacer la demanda futura. En este ejemplo se usan los algoritmos de Microsoft para crear modelos de regresión logística y árboles de decisión. | 
| [Creación de un modelo predictivo con Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | Cree la aplicación de análisis de alquiler de esquí con Python, que le ayudará a planear la demanda futura. En este ejemplo se usa la nueva biblioteca de Python, **revoscalepy**, para crear un modelo de regresión lineal. | 

<a name="bkmk_solutions"></a>

## <a name="solution-templates"></a>Plantillas de soluciones

El equipo de ciencia de datos de Microsoft ha proporcionado plantillas de solución personalizables que se pueden usar para iniciar soluciones para escenarios comunes. Cada solución se adapta a una tarea concreta o a un problema del sector. La mayoría de las soluciones están diseñadas para ejecutarse en SQL Server, o en un entorno de nube como Azure Machine Learning. Otras soluciones pueden ejecutarse en Linux o en clústeres de Spark o Hadoop mediante el uso de Microsoft R Server o Machine Learning Server.

Se proporciona todo el código, junto con instrucciones sobre cómo entrenar e implementar un modelo para la puntuación mediante SQL Server procedimientos almacenados.

+ [Detección de fraude](https://gallery.cortanaanalytics.com/Tutorial/Online-Fraud-Detection-Template-with-SQL-Server-R-Services-1)
+ [Predicción personalizada de abandono](https://gallery.cortanaanalytics.com/Tutorial/Customer-Churn-Prediction-Template-with-SQL-Server-R-Services-1)
+ [Mantenimiento predictivo](https://gallery.cortanaanalytics.com/Tutorial/Predictive-Maintenance-Template-with-SQL-Server-R-Services-1)
+ [Predecir la duración de la estancia del hospital](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

