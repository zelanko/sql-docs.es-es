---
title: ¿Qué&#39;Novedades de SQL Server Machine Learning Services | Microsoft Docs
description: Anuncios sobre nuevas características para cada versión de SQL Server 2016 R Services, R Server, SQL Server 2017 Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/28/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8d3dc4c730ea9c7c9ba0126a50ed4bb8129efc9c
ms.sourcegitcommit: fb269accc3786715c78f8b6e2ec38783a6eb63e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2018
ms.locfileid: "43152585"
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>Novedades de SQL Server Machine Learning Services 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Capacidades de aprendizaje automático se agregan a SQL Server en cada versión mientras seguimos expandir, ampliar, así como para ampliar la integración entre la plataforma de datos y la ciencia de datos, análisis y desea implementar a través de los datos de aprendizaje supervisión. 

## <a name="new-in-sql-server-2017"></a>Novedades de SQL Server 2017

Esta versión agrega [compatibilidad con Python y algoritmos de aprendizaje automático de líderes del sector](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/). Cambia para reflejar el nuevo ámbito, SQL Server 2017 marca la introducción de [SQL Server Machine Learning Services (In-Database)](what-is-sql-server-machine-learning.md), con compatibilidad con lenguaje Python y R. 

Esta versión también introducida [SQL Server Machine Learning Server (independiente)](r/r-server-standalone.md), totalmente independiente de SQL Server, para las cargas de trabajo de R y Python que se desean ejecutar en un sistema dedicado. Con el servidor independiente, puede distribuir y escalar soluciones de R o Python sin usar SQL Server.

### <a name="python-integration-for-in-database-analytics"></a>Integración de Python para realizar análisis en bases de datos

Ahora se admite la integración de T-SQL y Python a través de la [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) procedimiento almacenado del sistema. Puede llamar a cualquier código de Python mediante este procedimiento almacenado. Código que se ejecuta en una arquitectura segura dual que permite la implementación empresarial de los modelos de Python y secuencias de comandos, que se puede llamar desde una aplicación mediante un procedimiento almacenado simple. Mejoras adicionales del rendimiento se consiguen mediante transmisión por secuencias datos de SQL a procesos de Python y la paralelización de anillos de MPI.

Puede usar el T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) realice función [puntuación nativa](sql-native-scoring.md) en un modelo previamente entrenado que se ha guardado previamente en el formato binario necesario.

### <a name="python-libraries"></a>Bibliotecas de Python

| Paquete | Descripción |
|---------|-------------|
[**revoscalepy**](python/what-is-revoscalepy.md)| Equivalente de Python de RevoScaleR. Puede crear modelos de Python para regresiones logísticas y lineales, árboles de decisión, árboles impulsados y bosques aleatorios, todos los que se pueden paralelizar y es capaces de que se ejecuten en contextos de cálculo remoto. Este paquete es compatible con el uso de varios orígenes de datos y contextos de cálculo remoto. El desarrollador o científico de datos puede ejecutar código de Python en un servidor SQL remoto, para explorar datos o crear modelos sin mover datos. |
|[**microsoftml**](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) |Equivalente de Python del paquete MicrosoftML R. |

### <a name="r-libraries"></a>Bibliotecas de R

| Paquete | Descripción |
|---------|-------------|
| [**MicrosoftML (R)**](using-the-microsoftml-package.md) | Algoritmos de aprendizaje automático de última generación y transformación de datos que puede ser remoto ha escalado ni se ejecutarán en contextos de cálculo. Los algoritmos incluyen regresión logística, árboles de decisiones rápidos y bosques de decisión, regresión lineal y redes neurales profundas personalizables.  |
| [**Administración de paquetes de R**](r/install-additional-r-packages-on-sql-server.md) | Mejora en esta versión, destacan los siguientes aspectos: base de datos para administrar paquetes y asignar permisos para instalar paquetes, el DBA [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) instrucción T-SQL para ayudar a los DBA administrar los paquetes sin necesidad de conocer R y un amplio conjunto de funciones de R en [RevoScaleR](r/use-revoscaler-to-manage-r-packages.md) ayudar a instalar, quitar o enumerar los paquetes que pertenecen a los usuarios. |

### <a name="pre-trained-models"></a>Modelos entrenados previamente

[**Modelos previamente entrenados** ](install/sql-pretrained-models-install.md) están disponibles para Python y R. usan estos modelos de reconocimiento de imágenes y análisis de opiniones positivas y negativas, para generar las predicciones con sus propios datos. 


## <a name="new-in-sql-server-2016"></a>Novedades de SQL Server 2016

Esta funcionalidad en SQL Server a través de aprendizaje de automático de versión introducida **SQL Server 2016 R Services**, un motor de análisis en bases de datos para la secuencia de comandos de R de procesamiento de datos residentes en una instancia del motor de base de datos.

Además, **SQL Server 2016 R Server (independiente)** se publicó como una manera de instalar R Server en un servidor de Windows. Inicialmente, el programa de instalación de SQL Server proporciona la única manera de instalar R Server para Windows. En versiones posteriores, los desarrolladores y científicos de datos que deseaban R Server en Windows podrían usar a otro instalador independiente para lograr el mismo objetivo. El servidor independiente de SQL Server es funcionalmente equivalente al producto de servidor independiente, [Microsoft R Server para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

| Versión |Actualización de características |
|---------|----------------|
| CU adiciones | [**Puntuación en tiempo real** ](real-time-scoring.md) se basa en las bibliotecas de C++ nativas para leer un modelo almacenado en un formato binario optimizado y, a continuación, generar predicciones sin tener que llamar al runtime de R. Esto hace que las operaciones de puntuación mucho más rápidas. Con la puntuación en tiempo real, puede ejecutar un procedimiento almacenado o realizar la puntuación en tiempo real desde el código de R. También está disponible para SQL Server 2016, si la instancia se actualiza a la versión más reciente de puntuación en tiempo real [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]. |
| Versión inicial | [**Integración de R para realizar análisis en bases de datos**](r/sql-server-r-services.md). <br/><br/> Paquetes de R para R que realiza la llamada funciones Transact-SQL y viceversa. Funciones de RevoScaleR proporcionan análisis de R a escala mediante la fragmentación de los datos en distintos componentes, coordinación y administración de procesamiento distribuido y agregación de resultados. En SQL Server 2016 R Services (In-Database), el motor de RevoScaleR se integra con una instancia del motor de base de datos, ella juntos en el mismo contexto de procesamiento de análisis y datos. <br/><br/>La integración a través de Transact-SQL y R [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql). Puede llamar a cualquier código de R mediante este procedimiento almacenado. Esta infraestructura segura permite la implementación de nivel empresarial de modelos Rn y secuencias de comandos que se pueden llamar desde una aplicación mediante un procedimiento almacenado simple. Mejoras adicionales del rendimiento se consiguen mediante transmisión por secuencias datos de SQL a los procesos de R y la paralelización de anillos de MPI. <br/><br/>Puede usar el T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) realice función [puntuación nativa](sql-native-scoring.md) en un modelo previamente entrenado que se ha guardado previamente en el formato binario necesario.|

## <a name="linux-support-roadmap"></a>Plan de soporte técnico de Linux

Aprendizaje automático mediante R o Python en bases de datos no se admite actualmente en SQL Server en Linux. Busque anuncios en una versión posterior.

Sin embargo, en Linux puede realizar [puntuación nativa](sql-native-scoring.md) mediante la función PREDICT de Transact-SQL. Puntuación nativa permite puntuar desde un modelo previamente entrenado muy rápido, sin llamar a, o incluso un runtime de R. Esto significa que puede usar SQL Server en Linux para generar predicciones a gran velocidad, para atender a aplicaciones cliente.

<a name="azure-sql-database-roadmap"></a>

## <a name="azure-sql-database-roadmap"></a>Guía básica de la base de datos de SQL Azure

No hay compatibilidad limitada con R en Azure SQL Database: disponible únicamente en Centro occidental de Ee.uu., en los servicios creados en el nivel Premium. Cobertura ampliada, incluida la compatibilidad con Python, es probable que siga en una versión futura. Sin embargo, no hay ninguna fecha de lanzamiento prevista en este momento.  

## <a name="next-steps"></a>Pasos siguientes

+ [Instalar SQL Server 2017 Machine Learning Services (en bases de datos)](install/sql-machine-learning-services-windows-install.md)
+ [Ejemplos y tutoriales sobre aprendizaje automático](tutorials/machine-learning-services-tutorials.md)
