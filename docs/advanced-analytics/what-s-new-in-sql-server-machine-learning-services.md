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
ms.openlocfilehash: f01177114dd175767652a9bbd28e15afc3ce812e
ms.sourcegitcommit: c86335a432e109322d718a13c37ff4b948c39d2d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2018
ms.locfileid: "43193031"
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>Novedades de SQL Server Machine Learning Services 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Capacidades de aprendizaje automático se agregan a SQL Server en cada versión mientras seguimos expandir, ampliar, así como para ampliar la integración entre la plataforma de datos y la ciencia de datos, análisis y desea implementar a través de los datos de aprendizaje supervisión. 

## <a name="new-in-sql-server-2017"></a>Novedades de SQL Server 2017

Esta versión agrega [compatibilidad con Python y algoritmos de aprendizaje automático de líderes del sector](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/). Cambia para reflejar el nuevo ámbito, SQL Server 2017 marca la introducción de [SQL Server Machine Learning Services (In-Database)](what-is-sql-server-machine-learning.md), con compatibilidad con lenguaje Python y R. 

### <a name="r-enhancements"></a>Mejoras de R

El componente de R de Machine Learning Services de SQL Server 2017 es la próxima generación de SQL Server 2016 R Services, con las versiones actualizadas de R base, RevoScaler y otros paquetes.

Las nuevas capacidades para R incluyen [ **administración de paquetes**](r/install-additional-r-packages-on-sql-server.md), destacan los siguientes aspectos: 

+ Roles de base de datos ayudan a los DBA administrar paquetes y asignar permisos para la instalación del paquete.
+ [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) ayuda a los DBA administrar paquetes en el lenguaje T-SQL que ya conoce.
+ [RevoScaleR](r/use-revoscaler-to-manage-r-packages.md) funciones ayudará a instalar, quitar o enumerar los paquetes que pertenecen a los usuarios. Para obtener más información, consulte [paquetes de cómo usar las funciones de RevoScaleR para buscar o instalar R en SQL Server](r/use-revoscaler-to-manage-r-packages.md).

### <a name="r-libraries"></a>Bibliotecas de R

| Paquete | Descripción |
|---------|-------------|
| [**MicrosoftML**](using-the-microsoftml-package.md) | En esta versión, MicrosoftML se incluye en una instalación de R de forma predeterminada, lo que elimina el paso de actualización necesario en SQL Server 2016 R Services anterior. MicrosoftML proporciona transformaciones de datos que se pueden escalar o ejecutar en contextos de cálculo remotos y los algoritmos de aprendizaje de automático de última generación. Los algoritmos incluyen regresión logística, árboles de decisiones rápidos y bosques de decisión, regresión lineal y redes neurales profundas personalizables.  |

### <a name="python-integration-for-in-database-analytics"></a>Integración de Python para realizar análisis en bases de datos

Ahora se admite la integración de T-SQL y Python a través de la [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) procedimiento almacenado del sistema. Puede llamar a cualquier código de Python mediante este procedimiento almacenado. Código que se ejecuta en una arquitectura segura dual que permite la implementación empresarial de los modelos de Python y secuencias de comandos, que se puede llamar desde una aplicación mediante un procedimiento almacenado simple. Mejoras adicionales del rendimiento se consiguen mediante transmisión por secuencias datos de SQL a procesos de Python y la paralelización de anillos de MPI.

Puede usar el T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) realice función [puntuación nativa](sql-native-scoring.md) en un modelo previamente entrenado que se ha guardado previamente en el formato binario necesario.

### <a name="python-libraries"></a>Bibliotecas de Python

| Paquete | Descripción |
|---------|-------------|
[**revoscalepy**](python/what-is-revoscalepy.md)| Equivalente de Python de RevoScaleR. Puede crear modelos de Python para regresiones logísticas y lineales, árboles de decisión, árboles impulsados y bosques aleatorios, todos los que se pueden paralelizar y es capaces de que se ejecuten en contextos de cálculo remoto. Este paquete es compatible con el uso de varios orígenes de datos y contextos de cálculo remoto. El desarrollador o científico de datos puede ejecutar código de Python en un servidor SQL remoto, para explorar datos o crear modelos sin mover datos. |
|[**microsoftml**](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) |Equivalente de Python del paquete MicrosoftML R. |

### <a name="pre-trained-models"></a>Modelos entrenados previamente

[**Modelos previamente entrenados** ](install/sql-pretrained-models-install.md) están disponibles para Python y R. usan estos modelos de reconocimiento de imágenes y análisis de opiniones positivas y negativas, para generar las predicciones con sus propios datos. 

### <a name="standalone-server-as-a-shared-feature-in-sql-server-setup"></a>Servidor independiente como una característica compartida en el programa de instalación de SQL Server

Esta versión también agrega [SQL Server Machine Learning Server (independiente)](r/r-server-standalone.md), un servidor de ciencia de datos totalmente independiente, que admiten el análisis predictivo y estadística en R y Python. Como con R Services, este servidor es la próxima versión de SQL Server 2016 R Server (independiente). Con el servidor independiente, puede distribuir y escalar soluciones de R o Python sin dependencias en SQL Server.


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
