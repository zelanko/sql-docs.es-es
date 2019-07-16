---
title: Tutoriales de SQL Server R y Python, SQL Server Machine Learning
description: Ejemplos y tutoriales de R y Python, secuencias de comandos en SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 8c8e8ad13ddc34148f1718b7843e00545cd758c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962095"
---
# <a name="sql-server-machine-learning-tutorials-in-r-and-python"></a>Tutoriales de SQL Server Machine Learning en R y Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo proporciona una lista completa de los tutoriales y ejemplos de código que muestran las características de aprendizaje automático [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) o [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md). 

+ Guías de inicio rápido use datos integrados o no hay datos para la exploración rápida con mínimo esfuerzo.
+ Tutoriales profundización más tareas, conjuntos de datos mayores y más explicaciones.
+ Ejemplos y soluciones son para los programadores que prefieran para comenzar con el código, trabajando hacia atrás a los conceptos y las lecciones para rellenar los huecos de conocimiento.

Obtendrá información sobre cómo usar las bibliotecas de R y Python con datos relacionales residentes en el mismo contexto operativo, cómo usar procedimientos almacenados de SQL Server para ejecutar e implementar código personalizado y cómo llamar a Microsoft R y bibliotecas de Python para datos de alto rendimiento ciencia y tareas de aprendizaje automático.

Como primer paso, revise los conceptos fundamentales de seguridad de Microsoft R y Python integración con SQL Server.

## <a name="concepts"></a>Conceptos

Análisis en bases de datos hace referencia a la compatibilidad nativa para R y Python en SQL Server al instalar SQL Server Machine Learning Services o SQL Server 2016 R Services (solo para R) como un complemento para el motor de base de datos. Integración de R y Python incluye distribuciones base de código abierto, además de las bibliotecas específicas de Microsoft para el análisis de alto rendimiento.

Desde un punto de vista de arquitectura, el código se ejecuta como un proceso externo en el cuadro para mantener la integridad del motor de base de datos. Sin embargo, tener acceso todos los datos y la seguridad es a través de roles de base de datos de SQL Server y permisos, lo que significa que cualquier aplicación con acceso a SQL Server pueden tener acceso a la secuencia de comandos de R y Python al implementarlo como un procedimiento almacenado, o serializar y guardar un modelo entrenado en una instancia de SQL Base de datos del servidor.

Diferencias clave entre R y Python que se admiten en SQL Server en comparación con la compatibilidad con idiomas equivalente en otros productos de Microsoft y los servicios incluyen:

+ Capacidad de código de "paquete" en los procedimientos almacenados o como modelos binarios.
+ Escribir código que llama a las bibliotecas de Microsoft R y Python instaladas localmente con los archivos de programa de SQL Server.
+ Arquitectura de seguridad de base de datos de SQL Server se aplican a las soluciones de R y Python.
+ Aprovechar la infraestructura de SQL Server y soporte administrativo para sus soluciones personalizadas.

## <a name="quickstarts"></a>Tutoriales rápidos

Comience aquí para obtener información sobre cómo ejecutar R o Python desde T-SQL y cómo instrumentar el código de R y Python para un entorno de producción de SQL.

+ [Python: Ejecución de Python mediante T-SQL](run-python-using-t-sql.md)
+ [R: Hello World en R y SQL](rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [R: Controlar las entradas y salidas](rtsql-working-with-inputs-and-outputs.md)
+ [R: Administrar tipos de datos y objetos](rtsql-r-and-sql-data-types-and-data-objects.md)
+ [R: Uso de funciones de R](rtsql-using-r-functions-with-sql-server-data.md)
+ [R: Crear un modelo predictivo](rtsql-create-a-predictive-model-r.md)
+ [R: Predecir y trazar desde el modelo](rtsql-predict-and-plot-from-model.md)

## <a name="tutorials"></a>Tutoriales

Compilar en su primera experiencia con R y Python y T-SQL echar un vistazo más de cerca a los paquetes de Microsoft y las operaciones más especializadas, como cuando se desplaza desde local a los contextos de cálculo remoto.

+ [Tutoriales de Python](sql-server-python-tutorials.md)
+ [Tutoriales de R](sql-server-r-tutorials.md)

<a name ="bkmk_samples"></a>

## <a name="samples"></a>Muestras

Estos ejemplos y demostraciones proporcionadas por el equipo de desarrollo de SQL Server y R Server resaltan formas en que puede usar análisis insertados en aplicaciones del mundo real.

| Vínculo | Descripción | 
|------|-------------|
| [Realizar el cliente clústeres que usan R y SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | Usar aprendizaje no supervisado para segmentar los clientes en función de los datos de ventas. En este ejemplo se usa el algoritmo de rxKmeans escalable de Microsoft R para generar el modelo de agrupación en clústeres. |
| [Realizar el cliente agrupación en clústeres con Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | Obtenga información sobre cómo usar el algoritmo de Kmeans para realizar una agrupación en clústeres no supervisado de los clientes. En este ejemplo utiliza el lenguaje Python en database.| SQL Server 2017 |
| [Crear un modelo predictivo con R y SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | Obtenga información sobre cómo una empresa de alquiler de esquís puede usar el aprendizaje automático para predecir alquileres futuros, que permite el plan de negocio y personal para satisfacer la demanda futura. Este ejemplo utiliza los algoritmos de Microsoft para compilar la regresión logística y los modelos de árboles de decisión. | 
| [Crear un modelo predictivo con Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | Compile la aplicación de análisis de alquiler de esquí mediante Python, para ayudar a planear la demanda futura. Este ejemplo usa la nueva biblioteca de Python, **revoscalepy**, para crear un modelo de regresión lineal. | 

<a name="bkmk_solutions"></a>

## <a name="solution-templates"></a>Plantillas de solución

El equipo de ciencia de datos de Microsoft ha proporcionado plantillas personalizables que pueden usarse para impulsar soluciones para escenarios comunes. Cada solución se adapta a un problema específico de la tarea o del sector. La mayoría de las soluciones está diseñada para ejecutarse en SQL Server, o en un entorno de nube como Azure Machine Learning. Otras soluciones pueden ejecutar en Linux o en los clústeres de Spark o Hadoop, mediante el uso de Microsoft R Server o Machine Learning Server.

Se proporciona todo el código, así como instrucciones sobre cómo entrenar e implementar un modelo de puntuación mediante procedimientos almacenados de SQL Server.

+ [Detección de fraude](https://gallery.cortanaanalytics.com/Tutorial/Online-Fraud-Detection-Template-with-SQL-Server-R-Services-1)
+ [Predicción personalizada de abandono](https://gallery.cortanaanalytics.com/Tutorial/Customer-Churn-Prediction-Template-with-SQL-Server-R-Services-1)
+ [Mantenimiento predictivo](https://gallery.cortanaanalytics.com/Tutorial/Predictive-Maintenance-Template-with-SQL-Server-R-Services-1)
+ [Predecir la duración del hospital de la estancia](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

