---
title: DBCC (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC
- DBCC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transactional consistency
- Database Console Command statements
- status information [SQL Server], DBCC statements
- snapshots [SQL Server database snapshots], DBCC statements
- emergency database state [SQL Server]
- TABLOCK
- internal database snapshots [SQL Server]
- reporting DBCC statement progress
- logical consistency of data [SQL Server]
- DBCC statements
- validation statements [SQL Server]
- miscellaneous statements [SQL Server]
- statements [SQL Server], DBCC statements
- DBCC commands [SQL Server]
- result sets [SQL Server], DBCC statements
- maintenance statements [SQL Server]
- physical consistency of data [SQL Server]
- current DBCC statement status
- progress reporting [DBCC statements]
- informational statements [SQL Server]
ms.assetid: c6da8c04-5b6b-459a-9f76-110c92ca8b29
author: pmasl
ms.author: umajay
ms.openlocfilehash: 7f0d3d07f6f4a0ef3a35991c4805c478ed702bdf
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "73982443"
---
# <a name="dbcc-transact-sql"></a>DBCC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

El lenguaje de programación [!INCLUDE[tsql](../../includes/tsql-md.md)] proporciona instrucciones DBCC que actúan como comandos de consola de base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
Las instrucciones de comandos de consola de base de datos se dividen en las siguientes categorías.
  
|Categoría de comando|Acciones|  
|---|---|
|Mantenimiento|Tareas de mantenimiento en las bases de datos, los índices o los grupos de archivos.|  
|Varios|Tareas varias como habilitar marcas de seguimiento o quitar una DLL de la memoria.|  
|Informativo|Tareas que recopilan y muestran diversos tipos de información.|  
|Validación|Operaciones de validación en una base de datos, tabla, índice, catálogo, grupo de archivos o asignación de páginas de base de datos.|  
  
Los comandos DBCC reciben parámetros de entrada y devuelven valores. Todos los parámetros de los comandos DBCC pueden aceptar literales Unicode y DBCS.
  
## <a name="dbcc-internal-database-snapshot-usage"></a>Uso de comandos DBCC en instantáneas internas de la base de datos  
Los siguientes comandos DBCC operan en una instantánea de la base de datos interna de solo lectura que crea el [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Así se evitan problemas de bloqueo y simultaneidad cuando se ejecutan estos comandos. Para más información, vea [Instantáneas de base de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).
- DBCC CHECKALLOC
- DBCC CHECKCATALOG
- DBCC CHECKDB
- DBCC CHECKFILEGROUP
- DBCC CHECKTABLE

Cuando se ejecuta uno de estos comandos DBCC, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] crea una instantánea de la base de datos y la pone en un estado coherente desde el punto de vista transaccional. El comando DBCC ejecuta entonces las comprobaciones de esta instantánea. Una vez completado el comando DBCC, la instantánea se quita.
  
Algunas veces no es necesaria una instantánea de la base de datos interna o no se puede crear. Cuando esto ocurre, el comando DBCC se ejecuta de nuevo en la base de datos real. Si la base de datos está en línea, el comando DBCC utiliza el bloqueo de tabla para asegurar la coherencia de los objetos que está comprobando. Este comportamiento es el mismo que si se especificara la opción WITH TABLOCK.
  
No se crea ninguna instantánea de la base de datos interna al ejecutar un comando DBCC:
-   En **master** y cuando la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se está ejecutando en el modo de usuario único.  
-   En una base de datos distinta de **master**, pero cuando la base de datos se haya puesto en el modo de usuario único mediante la instrucción ALTER DATABASE.  
-   En una base de datos de solo lectura.  
-   En una base de datos que se ha establecido en modo de emergencia mediante la instrucción ALTER DATABASE.  
-   En **tempdb**. En este caso, no se puede crear una instantánea de la base de datos debido a restricciones internas.  
-   Utilizando la opción WITH TABLOCK. En este caso, DBCC respeta la solicitud no creando ninguna instantánea de la base de datos.  
  
Los comandos DBCC utilizan bloqueos de tabla en lugar de instantáneas internas de la base de datos cuando el comando se ejecuta en:
-   Un grupo de archivos de solo lectura  
-   Un sistema de archivos FAT  
-   Un volumen que no admite "flujos con nombre"  
-   Un volumen que no admite "flujos alternativos"  
  
> [!NOTE]  
>  Intentar ejecutar DBCC CHECKALLOC, o la parte equivalente de DBCC CHECKDB, utilizando la opción WITH TABLOCK requiere un bloqueo X de base de datos. Este bloqueo de base de datos no se puede definir ni en **tempdb** ni en **master** y probablemente produzca error en todas las demás bases de datos.  
  
> [!NOTE]  
>  DBCC CHECKDB produce un error cuando se ejecuta en **master** si no se puede crear una instantánea de base de datos interna.  
  
## <a name="progress-reporting-for-dbcc-commands"></a>Generación de informes de progreso para comandos DBCC  
La vista de catálogo **sys.dm_exec_requests** contiene información sobre el progreso y la fase actual de ejecución de los comandos DBCC CHECKDB, CHECKFILEGROUP y CHECKTABLE. La columna **percent_complete** indica el porcentaje del comando que se ha completado, mientras que la columna **command** informa de la fase actual de ejecución de este.
  
La definición de una unidad de progreso depende de la fase actual de ejecución del comando DBCC. En ocasiones, se informa del progreso con la granularidad de una página de base de datos; en otras fases, se informa del mismo con la granularidad de una sola base de datos o reparación de asignaciones. En la siguiente tabla se describe cada una de las fases de ejecución y la granularidad con la que el comando informa del progreso.
  
|Fase de ejecución|Descripción|Granularidad de informe de progreso|  
|---------------------|-----------------|------------------------------------|  
|DBCC TABLE CHECK|Durante esta fase se comprueba la coherencia lógica y física de los objetos de la base de datos.|Informe de progreso en el nivel de página de la base de datos.<br /><br /> El valor del informe de progreso se actualiza para cada 1.000 páginas de base de datos comprobadas.|  
|DBCC TABLE REPAIR|Durante esta fase de realizan reparaciones de base de datos si se especifican REPAIR_FAST, REPAIR_REBUILD o REPAIR_ALLOW_DATA_LOSS y existen errores de objeto que necesiten ser reparados.|Informe de progreso para cada reparación individual.<br /><br /> El contador se actualiza para cada reparación finalizada.|  
|DBCC ALLOC CHECK|Durante esta fase se comprueban las estructuras de asignación de la base de datos.<br /><br /> Nota: DBCC CHECKALLOC realiza las mismas comprobaciones.|No se informa del progreso.|  
|DBCC ALLOC REPAIR|Durante esta fase de realizan reparaciones de base de datos si se especifican REPAIR_FAST, REPAIR_REBUILD o REPAIR_ALLOW_DATA_LOSS y existen errores de asignación que necesiten ser reparados.|No se informa del progreso.|  
|DBCC SYS CHECK|Durante esta fase se comprueban las tablas de sistema de la base de datos.|Informe de progreso en el nivel de página de la base de datos.<br /><br /> El valor del informe del progreso se actualiza para cada 1000 páginas de base de datos comprobadas.|  
|DBCC SYS REPAIR|Durante esta fase de realizan reparaciones de base de datos si se especifican REPAIR_FAST, REPAIR_REBUILD o REPAIR_ALLOW_DATA_LOSS y existen errores de tabla del sistema que necesiten ser reparados.|Informe de progreso para cada reparación individual.<br /><br /> El contador se actualiza para cada reparación finalizada.|  
|DBCC SSB CHECK|Durante esta fase se comprueban los objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Broker.<br /><br /> Nota: Esta fase no se ejecuta cuando DBCC CHECKTABLE se ejecuta.|No se informa del progreso.|  
|DBCC CHECKCATALOG|Durante esta fase se comprueba la coherencia de los catálogos de la base de datos.<br /><br /> Nota: Esta fase no se ejecuta cuando DBCC CHECKTABLE se ejecuta.|No se informa del progreso.|  
|DBCC IVIEW CHECK|Durante esta fase se comprueba la coherencia lógica de cualquier vista indizada presente en la base de datos.|Informe de progreso en el nivel de la vista de base de datos individual que se está comprobando.|  
  
## <a name="informational-statements"></a>Instrucciones informativas  
  
|||  
|-|-|  
|[DBCC INPUTBUFFER](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)|[DBCC SHOWCONTIG](../../t-sql/database-console-commands/dbcc-showcontig-transact-sql.md)|  
|[DBCC OPENTRAN](../../t-sql/database-console-commands/dbcc-opentran-transact-sql.md)|[DBCC SQLPERF](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)|  
|[DBCC OUTPUTBUFFER](../../t-sql/database-console-commands/dbcc-outputbuffer-transact-sql.md)|[DBCC TRACESTATUS](../../t-sql/database-console-commands/dbcc-tracestatus-transact-sql.md)|  
|[DBCC PROCCACHE](../../t-sql/database-console-commands/dbcc-proccache-transact-sql.md)|[DBCC USEROPTIONS](../../t-sql/database-console-commands/dbcc-useroptions-transact-sql.md)|  
|[DBCC SHOW_STATISTICS](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)||  
  
## <a name="validation-statements"></a>Instrucciones de validación  
  
|||  
|-|-|  
|[DBCC CHECKALLOC](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)|[DBCC CHECKFILEGROUP](../../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md)|  
|[DBCC CHECKCATALOG](../../t-sql/database-console-commands/dbcc-checkcatalog-transact-sql.md)|[DBCC CHECKIDENT](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)|  
|[DBCC CHECKCONSTRAINTS](../../t-sql/database-console-commands/dbcc-checkconstraints-transact-sql.md)|[DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)|  
|[DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)||  
  
## <a name="maintenance-statements"></a>Instrucciones de mantenimiento  
  
|||  
|-|-|  
|[DBCC CLEANTABLE](../../t-sql/database-console-commands/dbcc-cleantable-transact-sql.md)|[DBCC INDEXDEFRAG](../../t-sql/database-console-commands/dbcc-indexdefrag-transact-sql.md)|  
|[DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md)|[DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)|  
|[DBCC DROPCLEANBUFFERS](../../t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql.md)|[DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)|  
|[DBCC FREEPROCCACHE](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)|[DBCC UPDATEUSAGE](../../t-sql/database-console-commands/dbcc-updateusage-transact-sql.md)|  
  
## <a name="miscellaneous-statements"></a>Instrucciones varias  
  
|||  
|-|-|  
|[DBCC dllname (FREE)](../../t-sql/database-console-commands/dbcc-dllname-free-transact-sql.md)|[DBCC HELP](../../t-sql/database-console-commands/dbcc-help-transact-sql.md)|  
|[DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)|[DBCC TRACEOFF](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)|  
|[DBCC FREESESSIONCACHE](../../t-sql/database-console-commands/dbcc-freesessioncache-transact-sql.md)|[DBCC TRACEON](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)|  
|[DBCC FREESYSTEMCACHE](../../t-sql/database-console-commands/dbcc-freesystemcache-transact-sql.md)|[DBCC CLONEDATABASE](../../t-sql/database-console-commands/dbcc-clonedatabase-transact-sql.md) <br /><br /> **Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 y versiones posteriores|  
  
  
