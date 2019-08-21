---
title: Novedades
description: Nuevos anuncios de características para cada versión de SQL Server 2016 R Services, R Server SQL Server Machine Learning Services.
ms.date: 08/21/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f582088359c2878f5dfd84d4b353b1f9d8c369e5
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652293"
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>Novedades de SQL Server Machine Learning Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Las funcionalidades de machine learning se agregan a SQL Server en cada versión a medida que seguimos expandiendo, ampliando y profundizando la integración entre la plataforma de datos, el análisis avanzado y la ciencia de datos. 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2019-preview"></a>Novedades de SQL Server versión preliminar 2019

En esta versión se agregan las características más solicitadas para las operaciones de aprendizaje automático de R y Python en SQL Server. Para obtener más información acerca de todas las características de esta versión, consulte [novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md) y [notas de la versión de SQL Server 2019](../sql-server/sql-server-ver15-release-notes.md).

> [!NOTE]
> Para ver la documentación de novedades de Java en SQL Server 2019, consulte las novedades [de las extensiones de lenguaje de SQL Server](https://docs.microsoft.com/sql/language-extensions/language-extensions-whats-new) .

| Release | Actualización de características |
|---------|----------------|
| RC 1 | Ahora se admite [la conexión de bucle invertido a SQL Server desde un script de Python o R](connect/loopback-connection.md) para Windows y Linux. |
| CTP 3.2 | No hay cambios. |
| CTP 3.1 | No hay cambios. |
| CTP 3.0 | No hay cambios. |
| CTP 2,5 | No hay cambios. |
| CTP 2.4 | Compatibilidad con Linux para [crear biblioteca externa (Transact-SQL)](../t-sql/statements/create-external-library-transact-sql.md) para R y Python. |
| CTP 2.3 | Solo en Windows, se puede tener acceso al código de Python en una biblioteca externa mediante la instrucción [Create external library (Transact-SQL)](../t-sql/statements/create-external-library-transact-sql.md) . |
| CTP 2.2 | No hay cambios. |
| CTP 2.1 | No hay cambios. |
| CTP 2.0 | Compatibilidad con la plataforma Linux para el aprendizaje automático de R y Python. Introducción a la [instalación de SQL Server Machine Learning Services en Linux](../linux/sql-server-linux-setup-machine-learning.md). |
|  | [Sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) introduce dos nuevos parámetros que permiten generar fácilmente varios modelos a partir de datos con particiones. Obtenga más información en este tutorial, [crear modelos basados en particiones en R](tutorials/r-tutorial-create-models-per-partition.md). |
|   | Ahora se admite la compatibilidad con clústeres de conmutación por error en Windows y Linux, suponiendo que se ha iniciado SQL Server Launchpad servicio en todos los nodos. Para obtener más información, vea [SQL Server instalación de clúster de conmutación por error](../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md). |

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2017"></a>Novedad en SQL Server 2017

Esta versión agrega [compatibilidad con Python y algoritmos de aprendizaje automático líderes del sector](https://cloudblogs.microsoft.com/sqlserver/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/). Cuyo nombre se ha cambiado para reflejar el nuevo ámbito, SQL Server 2017 marca la introducción de [SQL Server Machine Learning Services (in-Database)](what-is-sql-server-machine-learning.md), con compatibilidad de idioma para Python y R. 

Para ver todos los anuncios de características, consulte [novedades de SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md).

### <a name="r-enhancements"></a>Mejoras de R

El componente R de SQL Server Machine Learning Services es la próxima generación de SQL Server 2016 R Services, con versiones actualizadas de R, RevoScaler y otros paquetes.

Las nuevas capacidades de R incluyen [**Administración de paquetes**](r/install-additional-r-packages-on-sql-server.md), con los siguientes aspectos destacados: 

+ Los roles de base de datos ayudan a los DBA a administrar paquetes y asignar permisos para la instalación de paquetes.
+ [Crear biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) ayuda a los DBA a administrar paquetes en el conocido lenguaje T-SQL.
+ Las funciones de [RevoScaleR](r/use-revoscaler-to-manage-r-packages.md) ayudan a instalar, quitar o enumerar los paquetes que pertenecen a los usuarios. Para obtener más información, vea [Cómo usar las funciones de RevoScaleR para buscar o instalar paquetes de R en SQL Server](r/use-revoscaler-to-manage-r-packages.md).

### <a name="r-libraries"></a>Bibliotecas de R

| Paquete | Descripción |
|---------|-------------|
| [**MicrosoftML**](r/ref-r-microsoftml.md) | En esta versión, MicrosoftML se incluye en una instalación predeterminada de R, lo que elimina el paso de actualización necesario en los servicios de SQL Server 2016 R anteriores. MicrosoftML proporciona algoritmos de aprendizaje automático de última generación y transformaciones de datos que se pueden escalar o ejecutar en contextos de cálculo remotos. Los algoritmos incluyen redes neuronal profundas personalizables, árboles de decisión rápidos y bosques de decisión, regresión lineal y regresión logística.  |

### <a name="python-integration-for-in-database-analytics"></a>Integración de Python para análisis en base de datos

Python es un lenguaje que ofrece una gran flexibilidad y capacidad para una variedad de tareas de aprendizaje automático. Las bibliotecas de código abierto para Python incluyen varias plataformas para redes neuronal personalizables, así como bibliotecas populares para el procesamiento de lenguaje natural. 

Dado que Python está integrado en el motor de base de datos, puede mantener el análisis cerca de los datos y eliminar los costos y riesgos de seguridad asociados al movimiento de datos. Puede implementar soluciones de machine learning basadas en Python mediante herramientas como Visual Studio. Las aplicaciones de producción pueden obtener predicciones, modelos u objetos visuales del tiempo de ejecución de Python 3,5 mediante métodos de acceso a datos de SQL Server.

La integración de T-SQL y Python se admite a través del procedimiento almacenado del sistema [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) . Puede llamar a cualquier código de Python mediante este procedimiento almacenado. El código se ejecuta en una arquitectura segura y dual que permite la implementación de nivel empresarial de modelos y scripts de Python, que se puede llamar desde una aplicación mediante un procedimiento almacenado simple. Se obtienen mejoras de rendimiento adicionales mediante la transmisión de datos de SQL a procesos de Python y la paralelización de anillo de MPI.

Puede usar la función de [predicción](../t-sql/queries/predict-transact-sql.md) de T-SQL para realizar una [puntuación nativa](sql-native-scoring.md) en un modelo preentrenado que se ha guardado previamente en el formato binario requerido.

### <a name="python-libraries"></a>Bibliotecas de Python

| Paquete | Descripción |
|---------|-------------|
|[**revoscalepy**](python/ref-py-revoscalepy.md)| Python: equivalente a RevoScaleR. Puede crear modelos de Python para regresiones lineales y logísticas, árboles de decisión, árboles mejorados y bosques aleatorios, todos los pueden paralelizar y capaces de ejecutarse en contextos de cálculo remotos. Este paquete admite el uso de varios orígenes de datos y contextos de cálculo remotos. El científico de datos o el desarrollador puede ejecutar código de Python en un SQL Server remoto para explorar datos o crear modelos sin mover datos. |
|[**microsoftml**](python/ref-py-microsoftml.md) |Python: equivalente al paquete MicrosoftML R. |

### <a name="pre-trained-models"></a>Modelos entrenados previamente

Los [**modelos previamente entrenados**](install/sql-pretrained-models-install.md) están disponibles para Python y R. Use estos modelos para el reconocimiento de imágenes y el análisis de opiniones positivos y negativos para generar predicciones en sus propios datos. 

### <a name="standalone-server-as-a-shared-feature-in-sql-server-setup"></a>Servidor independiente como una característica compartida en SQL Server instalación

Esta versión también agrega [SQL Server machine learning Server (independiente)](r/r-server-standalone.md), un servidor de ciencia de datos totalmente independiente, que admite análisis de predicción y estadísticos en R y Python. Al igual que con R Services, este servidor es la próxima versión de SQL Server 2016 R Server (independiente). Con el servidor independiente, puede distribuir y escalar soluciones de R o Python sin dependencias en SQL Server.
::: moniker-end

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2016"></a>Novedad en SQL Server 2016

En esta versión se introdujeron funciones de aprendizaje automático en SQL Server a través de **SQL Server 2016 R Services**, un motor de análisis de base de datos para procesar scripts de R en datos residentes dentro de una instancia del motor de base de datos.

Además, **SQL Server 2016 R Server (independiente)** se publicó como una manera de instalar R Server en un servidor de Windows. Inicialmente, SQL Server el programa de instalación proporcionó la única manera de instalar R Server para Windows. En versiones posteriores, los desarrolladores y científicos de datos que querían R Server en Windows podían usar otro instalador independiente para lograr el mismo objetivo. El servidor independiente en SQL Server es funcionalmente equivalente al producto de servidor independiente, [Microsoft R Server para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

Para ver todos los anuncios de características, consulte [novedades de SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md).

| Release |Actualización de características |
|---------|----------------|
| Adiciones de CU | [**La puntuación en tiempo real**](real-time-scoring.md) se basa en C++ las bibliotecas nativas para leer un modelo almacenado en un formato binario optimizado y, a continuación, generar predicciones sin tener que llamar al tiempo de ejecución de R. Esto hace que las operaciones de puntuación sean mucho más rápidas. Con la puntuación en tiempo real, puede ejecutar un procedimiento almacenado o realizar una puntuación en tiempo real desde el código de R. La puntuación en tiempo real también está disponible para SQL Server 2016, si la instancia se actualiza a la versión más reciente de [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]. |
| Versión inicial | [**Integración de R para el análisis en bases de datos**](r/sql-server-r-services.md). <br/><br/> Paquetes de r para llamar a funciones de R en T-SQL y viceversa. Las funciones de RevoScaleR proporcionan análisis de R a escala mediante la fragmentación de datos en partes componentes, la coordinación y la administración del procesamiento distribuido y la agregación de resultados. En SQL Server 2016 R Services (in-Database), el motor de RevoScaleR se integra con una instancia del motor de base de datos, donde se agrupan los datos y los análisis en el mismo contexto de procesamiento. <br/><br/>Integración de T-SQL y R a través de [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql). Puede llamar a cualquier código de R mediante este procedimiento almacenado. Esta infraestructura segura permite la implementación de nivel empresarial de modelos y scripts RN a los que se puede llamar desde una aplicación mediante un procedimiento almacenado simple. Se obtienen mejoras de rendimiento adicionales mediante la transmisión de datos de SQL a procesos de R y la paralelización de anillo de MPI. <br/><br/>Puede usar la función de [predicción](../t-sql/queries/predict-transact-sql.md) de T-SQL para realizar una [puntuación nativa](sql-native-scoring.md) en un modelo preentrenado que se ha guardado previamente en el formato binario requerido.|

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="linux-support"></a>Soporte técnico de Linux

SQL Server 2019 agrega compatibilidad con Linux para R y Python al instalar los paquetes de machine learning con una instancia del motor de base de datos. Para obtener más información, consulte [instalación de SQL Server Machine Learning Services en Linux](../linux/sql-server-linux-setup-machine-learning.md).

En Linux, SQL Server 2017 no tiene integración de R o Python, pero puede usar la [puntuación nativa](sql-native-scoring.md) en Linux porque esa funcionalidad está disponible a través de la [predicción](../t-sql/queries/predict-transact-sql.md)de T-SQL, que se ejecuta en Linux. La puntuación nativa habilita la puntuación de alto rendimiento de un modelo previamente entrenado, sin llamar a o incluso requerir un tiempo de ejecución de R.
::: moniker-end

<a name="azure-sql-database-roadmap"></a>

## <a name="machine-learning-services-in-azure-sql-database"></a>Machine Learning Services en Azure SQL Database

Machine Learning Services en Azure SQL Database está en versión preliminar pública. Para obtener más información, vea [Azure SQL Database Machine Learning Services (versión preliminar)](https://docs.microsoft.com/azure/sql-database/sql-database-machine-learning-services-overview).

## <a name="next-steps"></a>Pasos siguientes

+ [Instalación de Machine Learning Services de SQL Server (en bases de datos)](install/sql-machine-learning-services-windows-install.md)
+ [Tutoriales y ejemplos de machine learning](tutorials/machine-learning-services-tutorials.md)
