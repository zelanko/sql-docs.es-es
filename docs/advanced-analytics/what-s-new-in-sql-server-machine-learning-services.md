---
title: Novedades - servicios de SQL Server Machine Learning | Microsoft Docs
description: Anuncios sobre nuevas características para cada versión de SQL Server 2016 R Services, R Server, SQL Server 2017 Machine Learning Services.
ms.date: 05/22/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 7c5871c6e33947f744dde571c329e8025b4a0813
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2019
ms.locfileid: "65993445"
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>Novedades de SQL Server Machine Learning Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Capacidades de aprendizaje automático se agregan a SQL Server en cada versión mientras seguimos expandir, ampliar, así como para ampliar la integración entre la plataforma de datos, análisis avanzado y ciencia de datos. 

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2019-preview"></a>Novedades de la versión preliminar de SQL Server 2019

Esta versión agrega las características más solicitadas para las operaciones de aprendizaje de máquinas R y Python en SQL Server. Para obtener más información acerca de todas las características de esta versión, consulte [What ' s New in SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md) y [Release Notes for SQL Server 2019](../sql-server/sql-server-ver15-release-notes.md).

> [!NOTE]
> ¿Para lo que es nueva documentación de Java en SQL Server 2019, consulte el [Novedades de extensiones de lenguaje de SQL Server?](https://docs.microsoft.com/sql/language-extensions/language-extensions-whats-new)

| Versión | Actualización de características |
|---------|----------------|
| CTP 2.5 | No hay cambios. |
| CTP 2.4 | Linux support para [CREATE EXTERNAL LIBRARY (Transact-SQL)](../t-sql/statements/create-external-library-transact-sql.md) R y Python. |
| CTP 2.3 | En Windows solo, código de Python puede obtenerse en una biblioteca externa con la [CREATE EXTERNAL LIBRARY (Transact-SQL)](../t-sql/statements/create-external-library-transact-sql.md) instrucción. |
| CTP 2.2 | No hay cambios. |
| CTP 2.1 | No hay cambios. |
| CTP 2.0 | Compatibilidad con la plataforma de Linux para el aprendizaje automático R y Python. Introducción a [instalar SQL Server Machine Learning Services en Linux](../linux/sql-server-linux-setup-machine-learning.md). |
|  | El [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) introduce dos nuevos parámetros que permiten generar fácilmente varios modelos de datos con particiones. Obtenga más información en este tutorial, [crear modelos basados en la partición en R](tutorials/r-tutorial-create-models-per-partition.md). |
|   | Compatibilidad con clústeres de conmutación por error ahora se admite en Windows y Linux, suponiendo que se inicia el servicio Launchpad de SQL Server en todos los nodos. Para obtener más información, consulte [instalación de clúster de conmutación por error de SQL Server](../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md). |

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2017"></a>Novedades de SQL Server 2017

Esta versión agrega [compatibilidad con Python y algoritmos de aprendizaje automático de líderes del sector](https://cloudblogs.microsoft.com/sqlserver/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/). Cambia para reflejar el nuevo ámbito, SQL Server 2017 marca la introducción de [SQL Server Machine Learning Services (In-Database)](what-is-sql-server-machine-learning.md), con compatibilidad con lenguaje Python y R. 

Para todos los anuncios de características de seguridad, consulte [What ' s New in SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md).

### <a name="r-enhancements"></a>Mejoras de R

El componente de R de Machine Learning Services de SQL Server 2017 es la próxima generación de SQL Server 2016 R Services, con las versiones actualizadas de R base, RevoScaler y otros paquetes.

Las nuevas capacidades para R incluyen [ **administración de paquetes**](r/install-additional-r-packages-on-sql-server.md), destacan los siguientes aspectos: 

+ Roles de base de datos ayudan a los DBA administrar paquetes y asignar permisos para la instalación del paquete.
+ [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) ayuda a los DBA administrar paquetes en el lenguaje T-SQL que ya conoce.
+ [RevoScaleR](r/use-revoscaler-to-manage-r-packages.md) funciones ayudará a instalar, quitar o enumerar los paquetes que pertenecen a los usuarios. Para obtener más información, consulte [paquetes de cómo usar las funciones de RevoScaleR para buscar o instalar R en SQL Server](r/use-revoscaler-to-manage-r-packages.md).

### <a name="r-libraries"></a>Bibliotecas de R

| Paquete | Descripción |
|---------|-------------|
| [**MicrosoftML**](r/ref-r-microsoftml.md) | En esta versión, MicrosoftML se incluye en una instalación de R de forma predeterminada, lo que elimina el paso de actualización necesario en SQL Server 2016 R Services anterior. MicrosoftML proporciona transformaciones de datos que se pueden escalar o ejecutar en contextos de cálculo remotos y los algoritmos de aprendizaje de automático de última generación. Los algoritmos incluyen regresión logística, árboles de decisiones rápidos y bosques de decisión, regresión lineal y redes neurales profundas personalizables.  |

### <a name="python-integration-for-in-database-analytics"></a>Integración de Python para realizar análisis en bases de datos

Python es un lenguaje que proporciona gran flexibilidad y capacidad para una variedad de tareas de aprendizaje automático. Bibliotecas de código abierto para Python incluyen varias plataformas para redes neurales personalizables, así como bibliotecas comunes para el procesamiento de lenguaje natural. Ahora, se admite este idioma utilizado en el aprendizaje automático de SQL Server 2017.

Dado que Python está integrado con el motor de base de datos, puede mantener análisis cerca de los datos y eliminar los costos y riesgos de seguridad asociados con el movimiento de datos. Puede implementar soluciones de aprendizaje automático basadas en Python con herramientas como Visual Studio. Las aplicaciones de producción pueden obtener predicciones, modelos, o métodos de acceso de los objetos visuales del tiempo de ejecución de Python 3.5 con datos de SQL Server.

Se admite la integración de T-SQL y Python a través de la [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) procedimiento almacenado del sistema. Puede llamar a cualquier código de Python mediante este procedimiento almacenado. Código que se ejecuta en una arquitectura segura dual que permite la implementación empresarial de los modelos de Python y secuencias de comandos, que se puede llamar desde una aplicación mediante un procedimiento almacenado simple. Mejoras adicionales del rendimiento se consiguen mediante transmisión por secuencias datos de SQL a procesos de Python y la paralelización de anillos de MPI.

Puede usar el T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) realice función [puntuación nativa](sql-native-scoring.md) en un modelo previamente entrenado que se ha guardado previamente en el formato binario necesario.

### <a name="python-libraries"></a>Bibliotecas de Python

| Paquete | Descripción |
|---------|-------------|
|[**revoscalepy**](python/ref-py-revoscalepy.md)| Equivalente de Python de RevoScaleR. Puede crear modelos de Python para regresiones logísticas y lineales, árboles de decisión, árboles impulsados y bosques aleatorios, todos los que se pueden paralelizar y es capaces de que se ejecuten en contextos de cálculo remoto. Este paquete es compatible con el uso de varios orígenes de datos y contextos de cálculo remoto. El desarrollador o científico de datos puede ejecutar código de Python en un servidor SQL remoto, para explorar datos o crear modelos sin mover datos. |
|[**microsoftml**](python/ref-py-microsoftml.md) |Equivalente de Python del paquete MicrosoftML R. |

### <a name="pre-trained-models"></a>Modelos entrenados previamente

[**Modelos previamente entrenados** ](install/sql-pretrained-models-install.md) están disponibles para Python y R. usan estos modelos de reconocimiento de imágenes y análisis de opiniones positivas y negativas, para generar las predicciones con sus propios datos. 

### <a name="standalone-server-as-a-shared-feature-in-sql-server-setup"></a>Servidor independiente como una característica compartida en el programa de instalación de SQL Server

Esta versión también agrega [SQL Server Machine Learning Server (independiente)](r/r-server-standalone.md), un servidor de ciencia de datos totalmente independiente, que admiten el análisis predictivo y estadística en R y Python. Como con R Services, este servidor es la próxima versión de SQL Server 2016 R Server (independiente). Con el servidor independiente, puede distribuir y escalar soluciones de R o Python sin dependencias en SQL Server.
::: moniker-end

## <a name="new-in-sql-server-2016"></a>Novedades de SQL Server 2016

Esta funcionalidad en SQL Server a través de aprendizaje de automático de versión introducida **SQL Server 2016 R Services**, un motor de análisis en bases de datos para la secuencia de comandos de R de procesamiento de datos residentes en una instancia del motor de base de datos.

Además, **SQL Server 2016 R Server (independiente)** se publicó como una manera de instalar R Server en un servidor de Windows. Inicialmente, el programa de instalación de SQL Server proporciona la única manera de instalar R Server para Windows. En versiones posteriores, los desarrolladores y científicos de datos que deseaban R Server en Windows podrían usar a otro instalador independiente para lograr el mismo objetivo. El servidor independiente de SQL Server es funcionalmente equivalente al producto de servidor independiente, [Microsoft R Server para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

Para todos los anuncios de características de seguridad, consulte [What ' s New in SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md).

| Versión |Actualización de características |
|---------|----------------|
| CU adiciones | [**Puntuación en tiempo real** ](real-time-scoring.md) se basa en las bibliotecas de C++ nativas para leer un modelo almacenado en un formato binario optimizado y, a continuación, generar predicciones sin tener que llamar al runtime de R. Esto hace que las operaciones de puntuación mucho más rápidas. Con la puntuación en tiempo real, puede ejecutar un procedimiento almacenado o realizar la puntuación en tiempo real desde el código de R. También está disponible para SQL Server 2016, si la instancia se actualiza a la versión más reciente de puntuación en tiempo real [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]. |
| Versión inicial | [**Integración de R para realizar análisis en bases de datos**](r/sql-server-r-services.md). <br/><br/> Paquetes de R para R que realiza la llamada funciones Transact-SQL y viceversa. Funciones de RevoScaleR proporcionan análisis de R a escala mediante la fragmentación de los datos en distintos componentes, coordinación y administración de procesamiento distribuido y agregación de resultados. En SQL Server 2016 R Services (In-Database), el motor de RevoScaleR se integra con una instancia del motor de base de datos, ella juntos en el mismo contexto de procesamiento de análisis y datos. <br/><br/>La integración a través de Transact-SQL y R [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql). Puede llamar a cualquier código de R mediante este procedimiento almacenado. Esta infraestructura segura permite la implementación de nivel empresarial de modelos Rn y secuencias de comandos que se pueden llamar desde una aplicación mediante un procedimiento almacenado simple. Mejoras adicionales del rendimiento se consiguen mediante transmisión por secuencias datos de SQL a los procesos de R y la paralelización de anillos de MPI. <br/><br/>Puede usar el T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) realice función [puntuación nativa](sql-native-scoring.md) en un modelo previamente entrenado que se ha guardado previamente en el formato binario necesario.|

## <a name="linux-support-roadmap"></a>Plan de soporte técnico de Linux

SQL Server 2019 CTP 2.3 agrega compatibilidad con Linux R y Python, al instalar los paquetes con una instancia del motor de base de datos de aprendizaje automático. Para obtener más información, consulte [instalar SQL Server Machine Learning Services en Linux](../linux/sql-server-linux-setup-machine-learning.md).

En Linux, SQL Server 2017 no tiene la integración de R o Python, pero puede usar [puntuación nativa](sql-native-scoring.md) en Linux porque esta funcionalidad está disponible a través de Transact-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md), que se ejecuta en Linux. Puntuación nativa permite puntuar alto rendimiento desde un modelo previamente entrenado, sin llamar a, o incluso un runtime de R.

<a name="azure-sql-database-roadmap"></a>

## <a name="machine-learning-services-in-azure-sql-database"></a>Servicios en la base de datos SQL de Azure Machine Learning

Machine Learning Services (con R) en Azure SQL Database está en versión preliminar pública. Para obtener más información, consulte [Machine Learning Services de Azure SQL Database con R (versión preliminar)](https://docs.microsoft.com/azure/sql-database/sql-database-machine-learning-services-overview).

## <a name="next-steps"></a>Pasos siguientes

+ [Instalar SQL Server 2017 Machine Learning Services (en bases de datos)](install/sql-machine-learning-services-windows-install.md)
+ [Ejemplos y tutoriales sobre aprendizaje automático](tutorials/machine-learning-services-tutorials.md)
