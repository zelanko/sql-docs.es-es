---
title: ¿Qué&#39;s nuevo en servicios de aprendizaje de máquina de SQL Server | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/02/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 405e4636525898268c54f1a3d603c9e5da3dc14d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>Novedades en servicios de aprendizaje de máquina de SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Capacidades de aprendizaje de máquina se agregan a SQL Server en cada versión mientras seguimos expandir, ampliar y profundizar en la integración entre la plataforma de datos y la ciencia de datos, análisis y supervisados de aprendizaje que se va a implementar a través de los datos. 

## <a name="new-in-sql-server-2017"></a>Novedades en SQL Server de 2017

Esta versión agrega compatibilidad con Python y algoritmos de aprendizaje automático de líderes en la industria. Cambiar el nombre para reflejar el nuevo ámbito, SQL Server 2017 marca la introducción de **servicios de aprendizaje de máquina de SQL Server (In-Database)**, con compatibilidad con idiomas de Python y R. 

Esta versión también introducida **aprendizaje de máquina SQL Server (independiente)**, totalmente independiente de SQL Server, para las cargas de trabajo de R y Python que desea ejecutar en un sistema dedicado. Con el servidor independiente, puede distribuir y escalar las soluciones de R o Python sin usar SQL Server.

| Versión | Actualización de la función |
|---------|----------------|
| CU 6 | Correcciones de errores y actualización de paquetes, pero no características nuevas de anuncios. Correcciones incluyen compatibilidad con tipos de datos de fecha y hora de consulta SPEES para Python y mensajes de error mejorados en microsoftml cuando faltan modelos previamente entrenados. |
| CU 5 | Correcciones de errores y actualización de paquetes, pero no características nuevas de anuncios. Revisiones incluyen mejoras para transformar las funciones y variables en revoscalepy, corregir los errores de tiempo basadas en la ruta de acceso en rxInstallPackages, corregir las conexiones en un bucle invertido para RxExec y las funciones de rx_exec y las revisiones de mensajes de advertencia. |
| CU 4 | Correcciones de errores y actualización de paquetes, pero no características nuevas de anuncios. |
| CU 3 | Serialización en revoscalepy, de modelo de Python mediante la [rx_serialize_model función](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model).<br/><br/>[Puntuación nativo](sql-native-scoring.md) además de mejoras en [en tiempo real de puntuación](real-time-scoring.md). Con la puntuación en bases de datos, el rendimiento es un millón de filas por segundo a través de modelos de R. En esta actualización, la puntuación en tiempo real y la puntuación nativo ofrecen un mejor rendimiento en varias filas y la puntuación del lote. Nativo de puntuación utiliza una función de T-SQL para puntuar rápida puede ejecutar en cualquier edición de SQL Server, incluso en Linux. La función no requiere ninguna instalación de R o una configuración adicional. Esto significa que puede entrenar un modelo en otra parte, guárdela en SQL Server y, a continuación, realizar puntuaciones sin llamar nunca a R. Para obtener más información sobre las metodologías de puntuación, vea [cómo llevar a cabo en tiempo real de puntuación de puntuación nativo](r/how-to-do-realtime-scoring.md). |
| CU 2 | Correcciones de errores y actualización de paquetes, pero no características nuevas de anuncios. |
| CU 1 | En revoscalepy, agrega rx_create_col_info para devolver información de esquema desde un origen de datos de SQL Server, similar a [rxCreateColInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcreatecolinfo) para R. <br/><br/>Mejoras en [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec) para admitir escenarios paralelos usando el `RxLocalParallel` contexto de proceso.|
| Versión inicial |[**Integración de Python para análisis en bases de datos**](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/) <br/><br/>El [revoscalepy](python/what-is-revoscalepy.md) paquete es el equivalente de Python de RevoScaleR. Puede crear modelos de Python para las regresiones lineales y logísticas, árboles de decisión, los árboles impulsados y bosques aleatorios, paralelizar todas y puede que se ejecutan en contextos de proceso remoto. Este paquete admite el uso de varios orígenes de datos y contextos de proceso remoto. El científico de datos o el desarrollador puede ejecutar código Python en un servidor SQL Server remoto, para explorar datos o crear modelos sin mover los datos. <br/><br/>El [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) paquete es el equivalente de Python del paquete MicrosoftML R.<br/><br/>Integración de T-SQL y Python a través de [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql). Puede llamar a cualquier código Python con este procedimiento almacenado. Esta infraestructura segura permite la implementación de nivel empresarial de los modelos de Python y las secuencias de comandos que se pueda llamar desde una aplicación mediante un procedimiento almacenado simple. Se obtienen mejoras de rendimiento adicionales mediante transmisión por secuencias de datos de SQL a procesos de Python y la paralelización de anillo MPI. <br/><br/>Puede usar el código T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) función para realizar [puntuación nativo](sql-native-scoring.md) en un modelo previamente entrenado que se ha guardado previamente en el formato binario requerido.|
| Versión inicial | [**MicrosoftML (R)** ](using-the-microsoftml-package.md) contiene algoritmos y transformaciones de datos que pueden ser contextos de escalado y se ejecutarán en proceso remoto de aprendizaje de automático de la innovadora. Los algoritmos incluyen redes neurales profundas personalizables, árboles de decisión rápida y bosques de decisión, regresión lineal y regresión logística. |
| Versión inicial | [**Modelos previamente entrenados** ](r/install-pretrained-models-sql-server.md) para reconocimiento de imágenes y análisis de opiniones positivas y negativas. Use estos modelos para generar las predicciones en sus propios datos. |
| Versión inicial | [**Administración del paquete**](r/r-package-management-for-sql-server-r-services.md), incluido el destacan los siguientes aspectos: roles para ayudar a lo DBA administrar paquetes y asignar permisos para instalar paquetes, la base de datos [crear biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) instrucción T-SQL para Ayuda de los DBA administrar los paquetes sin necesidad de conocer R y un amplio conjunto de R las funciones de [RevoScaleR](r/use-revoscaler-to-manage-r-packages.md) como ayuda instalar, quitar o enumerar los paquetes que pertenecen a los usuarios. |
| Versión inicial | [**Puesta en marcha a través de mrsdeploy** ](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package) para implementar y script de R como un servicio web de hospedaje. Se aplica a solo un script de R (ningún equivalente de Python). Diseñado para que la opción de servidor (independiente) evitar la competencia de recursos con otras operaciones de SQL Server. |


## <a name="new-in-sql-server-2016"></a>Novedades en SQL Server 2016

Esta máquina versión introducida las capacidades en SQL Server a través de aprendizaje **SQL Server 2016 R Services**, un motor de análisis de bases de datos para el script de R de procesamiento de datos residentes en una instancia del motor de base de datos.

Además, **R Server (independiente) de SQL Server 2016** se publicó como una manera de instalar R Server en un servidor de Windows. Inicialmente, el programa de instalación de SQL Server proporciona la única manera de instalar R Server para Windows. En versiones posteriores, los desarrolladores y científicos de datos que deseaban R Server en Windows pudieron usar a otro instalador independiente para lograr el mismo objetivo. El servidor independiente de SQL Server es funcionalmente equivalente al producto de servidor independiente, [Microsoft R Server para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

| Versión |Actualización de la función |
|---------|----------------|
| CU | [**En tiempo real de puntuación** ](real-time-scoring.md) se basa en las bibliotecas de C++ nativo para leer un modelo que se almacenan en un formato binario optimizado y, a continuación, generar predicciones sin tener que llamar al runtime de R. Esto hace que las operaciones de puntuación mucho más rápidas. Con la puntuación en tiempo real, puede ejecutar un procedimiento almacenado o realizar en tiempo real desde el código de R de puntuación. En tiempo real de puntuación también está disponible para SQL Server 2016, si la instancia se actualiza a la versión más reciente de [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]. |
| Versión inicial | [**Integración de R para el análisis en bases de datos**](r/sql-server-r-services.md). <br/><br/> Paquetes de R para R llamada funciona en T-SQL y viceversa. Funciones de RevoScaleR proporcionan análisis de R a escala por fragmentación de datos en componentes, coordinar y administrar el procesamiento distribuido y agregar los resultados. En SQL Server 2016 R Services (In-Database), el motor de RevoScaleR se integra con una instancia del motor de base de datos, ella datos y análisis juntos en el mismo contexto de procesamiento. <br/><br/>Integración de T-SQL y R a través de [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql). Puede llamar a cualquier código de R mediante este procedimiento almacenado. Esta infraestructura segura permite la implementación de nivel empresarial de los modelos de Rn y secuencias de comandos que se pueda llamar desde una aplicación mediante un procedimiento almacenado simple. Se obtienen mejoras de rendimiento adicionales mediante transmisión por secuencias de datos de SQL a procesos de R y la paralelización de anillo MPI. <br/><br/>Puede usar el código T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) función para realizar [puntuación nativo](sql-native-scoring.md) en un modelo previamente entrenado que se ha guardado previamente en el formato binario requerido.|

## <a name="linux-support-roadmap"></a>Guía básica de compatibilidad con Linux

Aprendizaje automático que usan R o Python en bases de datos no se admite actualmente en SQL Server en Linux. Busque anuncios en una versión posterior.

Sin embargo, en Linux puede realizar [puntuación nativo](sql-native-scoring.md) mediante la función de PREDICCIÓN de T-SQL. Puntuación nativo permite puntuar desde un modelo previamente entrenado muy rápido, sin llamar a, o incluso un tiempo de ejecución de R. Esto significa que puede usar SQL Server en Linux para generar predicciones muy rápidas, para atender a las aplicaciones cliente.

## <a name="next-steps"></a>Pasos siguientes

+ [Instalar servicios de aprendizaje automático SQL Server de 2017 (en bases de datos)](install/sql-machine-learning-services-windows-install.md)
+ [Ejemplos y tutoriales de aprendizaje de máquina](tutorials/machine-learning-services-tutorials.md)
