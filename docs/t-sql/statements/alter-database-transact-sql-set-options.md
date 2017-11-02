---
title: MODIFICAR opciones de SET de base de datos (Transact-SQL) | Documentos de Microsoft
description: "Obtenga información acerca de cómo establecer opciones de base de datos como el cifrado de optimización, automática, el almacén de consultas en un SQL Server y la base de datos de SQL Azure"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- online database state [SQL Server]
- database options [SQL Server]
- emergency database state [SQL Server]
- databases [SQL Server], options
- read-only databases
- recovery models [SQL Server], switching
- ALTER DATABASE statement, SET options
- offline database state [SQL Server]
- snapshot isolation framework option
- checksums [SQL Server]
- automatic tuning
- SQL plan regression correction
ms.assetid: f76fbd84-df59-4404-806b-8ecb4497c9cc
caps.latest.revision: 159
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 5dbb93a69c6f8194c2d17eb982fae1ba15d4a522
ms.contentlocale: es-es
ms.lasthandoff: 09/27/2017

---
# <a name="alter-database-set-options-transact-sql"></a>Opciones de ALTER DATABASE SET (Transact-SQL) 
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  En este tema se describe la sintaxis de ALTER DATABASE, relacionada con la configuración de las opciones de las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para otros elementos de sintaxis ALTER DATABASE, vea los temas siguientes.  
  
-   [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  

-   [ALTER DATABASE &#40; Base de datos SQL Azure &#41;](alter-database-azure-sql-database.md) 

-   [ALTER DATABASE &#40; Almacenamiento de datos SQL de Azure &#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md)  
  
-   [ALTER DATABASE &#40; Almacenamiento de datos en paralelo &#41;](../../t-sql/statements/alter-database-parallel-data-warehouse.md)  
  
Creación de reflejo de base de datos, [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], y niveles de compatibilidad son `SET` opciones pero se describen en otros temas debido a su extensión. Para obtener más información, vea [ALTER creación de reflejo de base de datos de base de datos &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md), [ALTER HADR de conjunto de base de datos &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-hadr.md), y [modificar el nivel de compatibilidad de base de datos &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
> [!NOTE]  
>  Muchas opciones de set de base de datos pueden configurarse para la sesión actual mediante el uso de [instrucciones SET &#40; Transact-SQL &#41; ](../../t-sql/statements/set-statements-transact-sql.md) y a menudo se configuran las aplicaciones cuando se conectan. Las opciones SET de nivel de sesión reemplazan a los valores **ALTER DATABASE SET** . Las opciones de base de datos descritas a continuación son valores que se pueden establecer en las sesiones que no proporcionan explícitamente otros valores de opciones SET.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
ALTER DATABASE { database_name  | CURRENT }  
SET   
{  
    <optionspec> [ ,...n ] [ WITH <termination> ]   
}  
  
<optionspec> ::=   
{  
    <auto_option>   
  | <automatic_tuning_option>   
  | <change_tracking_option>   
  | <containment_option>   
  | <cursor_option>   
  | <database_mirroring_option>  
  | <date_correlation_optimization_option>  
  | <db_encryption_option>  
  | <db_state_option>  
  | <db_update_option>   
  | <db_user_access_option>   
  | <delayed_durability_option>  
  | <external_access_option>  
  | FILESTREAM ( <FILESTREAM_option> )  
  | <HADR_options>  
  | <mixed_page_allocation_option>  
  | <parameterization_option>  
  | <query_store_options>  
  | <recovery_option>  
  | <remote_data_archive_option>  
  | <service_broker_option>  
  | <snapshot_option>  
  | <sql_option>   
  | <target_recovery_time_option>   
  | <termination>  
}  
  
<auto_option> ::=   
{  
    AUTO_CLOSE { ON | OFF }   
  | AUTO_CREATE_STATISTICS { OFF | ON [ ( INCREMENTAL = { ON | OFF } ) ] }   
  | AUTO_SHRINK { ON | OFF }   
  | AUTO_UPDATE_STATISTICS { ON | OFF }   
  | AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }  
}  
  
<automatic_tuning_option> ::=  
{  
  AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = { ON | OFF } )
}  

<change_tracking_option> ::=  
{  
  CHANGE_TRACKING   
   {   
       = OFF  
     | = ON [ ( <change_tracking_option_list > [,...n] ) ]   
     | ( <change_tracking_option_list> [,...n] )  
   }  
}  
  
   <change_tracking_option_list> ::=  
   {  
       AUTO_CLEANUP = { ON | OFF }   
     | CHANGE_RETENTION = retention_period { DAYS | HOURS | MINUTES }  
   }  
  
<containment_option> ::=   
   CONTAINMENT = { NONE | PARTIAL }  
  
<cursor_option> ::=   
{  
    CURSOR_CLOSE_ON_COMMIT { ON | OFF }   
  | CURSOR_DEFAULT { LOCAL | GLOBAL }   
}  
  
<database_mirroring_option>  
  ALTER DATABASE Database Mirroring  
  
<date_correlation_optimization_option> ::=  
    DATE_CORRELATION_OPTIMIZATION { ON | OFF }  
  
<db_encryption_option> ::=  
    ENCRYPTION { ON | OFF }  
  
<db_state_option> ::=  
    { ONLINE | OFFLINE | EMERGENCY }  
  
<db_update_option> ::=  
    { READ_ONLY | READ_WRITE }  
  
<db_user_access_option> ::=  
    { SINGLE_USER | RESTRICTED_USER | MULTI_USER }  
  
<delayed_durability_option> ::=  
    DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }  
  
<external_access_option> ::=  
{  
    DB_CHAINING { ON | OFF }  
  | TRUSTWORTHY { ON | OFF }  
  | DEFAULT_FULLTEXT_LANGUAGE = { <lcid> | <language name> | <language alias> }  
  | DEFAULT_LANGUAGE = { <lcid> | <language name> | <language alias> }  
  | NESTED_TRIGGERS = { OFF | ON }  
  | TRANSFORM_NOISE_WORDS = { OFF | ON }  
  | TWO_DIGIT_YEAR_CUTOFF = { 1753, ..., 2049, ..., 9999 }  
}  
<FILESTREAM_option> ::=  
{  
    NON_TRANSACTED_ACCESS = { OFF | READ_ONLY | FULL   
  | DIRECTORY_NAME = <directory_name>  
}  
<HADR_options> ::=  
    ALTER DATABASE SET HADR  
  
<mixed_page_allocation_option> ::=  
    MIXED_PAGE_ALLOCATION { OFF | ON }  
  
<parameterization_option> ::=  
    PARAMETERIZATION { SIMPLE | FORCED }  
  
<query_store_options> ::=  
{  
    QUERY_STORE   
    {  
          = OFF   
        | = ON [ ( <query_store_option_list> [,...n] ) ]  
        | ( < query_store_option_list> [,...n] )  
        | CLEAR [ ALL ]  
    }  
}   
  
<query_store_option_list> ::=  
{  
      OPERATION_MODE = { READ_WRITE | READ_ONLY }   
    | CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = number )  
    | DATA_FLUSH_INTERVAL_SECONDS = number   
    | MAX_STORAGE_SIZE_MB = number   
    | INTERVAL_LENGTH_MINUTES = number   
    | SIZE_BASED_CLEANUP_MODE = [ AUTO | OFF ]  
    | QUERY_CAPTURE_MODE = [ ALL | AUTO | NONE ]  
    | MAX_PLANS_PER_QUERY = number
    | WAIT_STATS_CAPTURE_MODE = [ ON | OFF ]
}  
  
<recovery_option> ::=   
{  
    RECOVERY { FULL | BULK_LOGGED | SIMPLE }   
  | TORN_PAGE_DETECTION { ON | OFF }  
  | PAGE_VERIFY { CHECKSUM | TORN_PAGE_DETECTION | NONE }  
}  
  
<remote_data_archive_option> ::=  
{  
    REMOTE_DATA_ARCHIVE =  
    {  
        ON ( SERVER = <server_name> ,   
                  {   CREDENTIAL = <db_scoped_credential_name>  
                     | FEDERATED_SERVICE_ACCOUNT =  ON | OFF   
                  }  
               )  
      | OFF  
    }  
}  
  
<service_broker_option> ::=  
{  
    ENABLE_BROKER  
  | DISABLE_BROKER  
  | NEW_BROKER  
  | ERROR_BROKER_CONVERSATIONS  
  | HONOR_BROKER_PRIORITY { ON | OFF}  
}  
  
<snapshot_option> ::=  
{  
    ALLOW_SNAPSHOT_ISOLATION { ON | OFF }  
  | READ_COMMITTED_SNAPSHOT {ON | OFF }  
  | MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = {ON | OFF }  
}  
<sql_option> ::=   
{  
    ANSI_NULL_DEFAULT { ON | OFF }   
  | ANSI_NULLS { ON | OFF }   
  | ANSI_PADDING { ON | OFF }   
  | ANSI_WARNINGS { ON | OFF }   
  | ARITHABORT { ON | OFF }   
  | COMPATIBILITY_LEVEL = { 90 | 100 | 110 | 120}  
  | CONCAT_NULL_YIELDS_NULL { ON | OFF }   
  | NUMERIC_ROUNDABORT { ON | OFF }   
  | QUOTED_IDENTIFIER { ON | OFF }   
  | RECURSIVE_TRIGGERS { ON | OFF }   
}  
  
<target_recovery_time_option> ::=  
    TARGET_RECOVERY_TIME = target_recovery_time { SECONDS | MINUTES }  
  
<termination>  ::=   
{  
    ROLLBACK AFTER integer [ SECONDS ]   
  | ROLLBACK IMMEDIATE   
  | NO_WAIT  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Es el nombre de la base de datos que se va a modificar.  
  
 CURRENT  
 **Se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 `CURRENT`realiza la acción en la base de datos actual. `CURRENT`no se admite para todas las opciones en todos los contextos. Si `CURRENT` se produce un error, proporcione el nombre de la base de datos.  
  
 **\<auto_option >:: =**  
  
 Controla las opciones automáticas.  
  
 AUTO_CLOSE { ON | OFF }  
 ON  
 La base de datos se cierra correctamente y se liberan sus recursos después de que salga el último usuario.  
  
 La base de datos se vuelve a abrir automáticamente cuando un usuario intenta utilizarla de nuevo. Por ejemplo, mediante la emisión de un `USE database_name` instrucción. Si la base de datos se cierra correctamente mientras AUTO_CLOSE está establecido en ON, la base de datos no se volverá a abrir hasta que un usuario intente utilizar la base de datos la próxima vez que se reinicie el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 OFF  
 La base de datos permanece abierta después de que haya salido el último usuario.  
  
 La opción AUTO_CLOSE es útil para las bases de datos de escritorio porque permite administrar los archivos de la base de datos como archivos normales. Se pueden mover, copiar para realizar copias de seguridad e incluso enviar por correo electrónico a otros usuarios. El proceso AUTO_CLOSE es asincrónico. La apertura y cierre repetidos de la base de datos no reduce el rendimiento.  
  
> [!NOTE]  
>  La opción AUTO_CLOSE no está disponible en una base de datos independiente o en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 El estado de esta opción se puede determinar mediante el examen de la columna is_auto_close_on de la vista de catálogo sys.databases o la propiedad IsAutoClose de la función DATABASEPROPERTYEX.  
  
> [!NOTE]  
>  Si AUTO_CLOSE es ON, algunas columnas de la vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) y de la función DATABASEPROPERTYEX devuelven NULL porque la base de datos no está disponible para recuperar los datos. Para resolver este problema, ejecute la instrucción USE para abrir la base de datos.  
  
> [!NOTE]  
>  La creación de reflejo de la base de datos requiere AUTO_CLOSE OFF.  
  
 Cuando la base de datos se establece en AUTOCLOSE = ON, una operación que inicia el cierre automático de la base de datos borra la memoria caché de planes para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Al borrar la memoria caché de planes, se provoca una nueva compilación de todos los planes de ejecución posteriores y puede ocasionar una disminución repentina y temporal del rendimiento de las consultas. En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 y posterior, para cada almacén de caché borrado de la memoria caché de planes, el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contendrá el siguiente mensaje informativo: "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha detectado %d instancias de vaciado del almacén de caché '%s' (parte de la memoria caché de planes) debido a determinadas operaciones de mantenimiento de base de datos o reconfiguración". Este mensaje se registra cada cinco minutos siempre que se vacíe la memoria caché dentro de ese intervalo de tiempo.  
  
 AUTO_CREATE_STATISTICS { ON | OFF }  
 ON  
 El optimizador de consultas crea las estadísticas en columnas únicas de los predicados de consulta, según sea necesario, para mejorar los planes de consulta y el rendimiento de las consultas. Estas estadísticas de columna única se crean cuando el optimizador de consultas las compila. Las estadísticas de columna única solamente se crean en las columnas que ya no son la primera columna de un objeto de estadísticas existente.  
  
 El valor predeterminado es ON. Recomendamos utilizar la configuración predeterminada para la mayoría de las bases de datos.  
  
 OFF  
 El optimizador de consultas no crea las estadísticas en columnas únicas de los predicados de consulta cuando está compilando consultas. Establecer esta opción en OFF puede producir planes de consulta poco óptimos y un rendimiento degradado de las consultas.  
  
 El estado de esta opción se puede determinar mediante el examen de la columna is_auto_create_stats_on de la vista de catálogo sys.databases o la propiedad IsAutoCreateStatistics de la función DATABASEPROPERTYEX.  
  
 Para obtener más información, vea la sección "Usar las opciones de estadísticas de toda la base de datos" en [estadísticas](../../relational-databases/statistics/statistics.md).  
  
 INCREMENTAL = ON | OFF  
 Cuando AUTO_CREATE_STATISTICS está establecido en ON e INCREMENTAL está establecido en ON, las estadísticas creadas automáticamente se crean como incrementales cuando se admitan las estadísticas incrementales. El valor predeterminado es OFF. Para obtener más información, vea [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md).  
  
 **Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 AUTO_SHRINK { ON | OFF }  
 ON  
 Los archivos de la base de datos se pueden reducir periódicamente.  
  
 Pueden reducirse automáticamente los archivos de datos y los archivos de registro. AUTO_SHRINK reduce el tamaño del registro de transacciones solo si el modelo de recuperación de la base de datos se establece en SIMPLE o si se realiza una copia de seguridad del registro. Cuando el valor es OFF, los archivos de la base de datos no se reducen de forma automática durante las comprobaciones periódicas del espacio no utilizado.  
  
 La opción AUTO_SHRINK reduce los archivos cuando no se utiliza más de un 25% del espacio del archivo. El tamaño del archivo se reduce hasta un tamaño en el que el 25% del archivo corresponde al espacio sin utilizar o hasta el tamaño que tenía el archivo cuando se creó (el tamaño mayor de los dos).  
  
 No puede reducir una base de datos de solo lectura.  
  
 OFF  
 Los archivos de la base de datos no se reducen automáticamente durante las comprobaciones periódicas del espacio no utilizado.  
  
 El estado de esta opción se puede determinar mediante el examen de la columna is_auto_shrink_on de la vista de catálogo sys.databases o de la propiedad IsAutoShrink de la función DATABASEPROPERTYEX.  
  
> [!NOTE]  
>  La opción AUTO_SHRINK no está disponible en una base de datos independiente.  
  
 AUTO_UPDATE_STATISTICS { ON | OFF }  
 ON  
 Especifica que el optimizador de consultas actualiza las estadísticas cuando son usadas por una consulta y pudieran estar obsoletas. Las estadísticas se vuelven obsoletas después de que operaciones de inserción, actualización, eliminación o combinación cambien la distribución de los datos en la tabla o la vista indizada. El optimizador de consultas determina cuándo han podido quedar obsoletas las estadísticas contando el número de modificaciones de datos desde la actualización más reciente de las estadísticas, comparando el número de modificaciones con respecto a un umbral. El umbral se basa en el número de filas de la tabla o la vista indizada.  
  
 El optimizador de consultas comprueba que hay estadísticas obsoletas antes de compilar una consulta y antes de ejecutar un plan de consulta almacenado en la memoria caché. Antes de compilar una consulta, el optimizador de consultas utiliza las columnas, tablas y vistas indizadas en el predicado de consulta, para determinar qué estadísticas podrían estar obsoletas. Antes de ejecutar un plan de consulta almacenado en la memoria caché, [!INCLUDE[ssDE](../../includes/ssde-md.md)] comprueba que el plan de consulta hace referencia a las estadísticas actualizadas.  
  
 La opción AUTO_UPDATE_STATISTICS se aplica a las estadísticas creadas para índices y columnas únicas de los predicados de consulta, así como a las estadísticas creadas con la instrucción CREATE STATISTICS. Esta opción también se aplica a las estadísticas filtradas.  
  
 El valor predeterminado es ON. Recomendamos utilizar la configuración predeterminada para la mayoría de las bases de datos.  
  
 Utilice la opción AUTO_UPDATE_STATISTICS_ASYNC para especificar si las estadísticas se actualizan sincrónica o asincrónicamente.  
  
 OFF  
 Especifica que el optimizador de consultas no actualiza las estadísticas cuando son usadas por una consulta y parece que puedan estar obsoletas. Establecer esta opción en OFF puede producir planes de consulta poco óptimos y un rendimiento degradado de las consultas.  
  
 El estado de esta opción se puede determinar mediante el examen de la columna is_auto_update_stats_on de la vista de catálogo sys.databases o la propiedad IsAutoUpdateStatistics de la función DATABASEPROPERTYEX.  
  
 Para obtener más información, vea la sección "Usar las opciones de estadísticas de toda la base de datos" en [estadísticas](../../relational-databases/statistics/statistics.md).  
  
 AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }  
 ON  
 Especifica que las actualizaciones de las estadísticas para la opción AUTO_UPDATE_STATISTICS son asincrónicas. El optimizador de consultas no espera a que finalicen las actualizaciones de las estadísticas para compilar las consultas.  
  
 La configuración de esta opción en ON no surte efecto a menos que AUTO_UPDATE_STATISTICS se establezca en ON.  
  
 De forma predeterminada, la opción AUTO_UPDATE_STATISTICS_ASYNC está configurada en OFF y el optimizador de consultas actualiza las estadísticas sincrónicamente.  
  
 OFF  
 Especifica que las actualizaciones de las estadísticas para la opción AUTO_UPDATE_STATISTICS son sincrónicas. El optimizador de consultas espera a que finalicen las actualizaciones de las estadísticas para compilar las consultas.  
  
 La configuración de esta opción en OFF no surte efecto a menos que AUTO_UPDATE_STATISTICS esté configurado en ON.  
  
 El estado de esta opción se puede determinar mediante el examen de la columna is_auto_update_stats_async_on de la vista de catálogo sys.databases.  
  
 Para obtener más información que describe cuándo utilizar las actualizaciones de estadísticas sincrónicas o asincrónicas, vea la sección "Usar las opciones de estadísticas de toda la base de datos" en [estadísticas](../../relational-databases/statistics/statistics.md).  
  
 **\<automatic_tuning_option >:: =**  
 **Se aplica a**: [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].  

 Habilita o deshabilita `FORCE_LAST_GOOD_PLAN` [el ajuste automático](../../relational-databases/automatic-tuning/automatic-tuning.md) opción.  
  
 FORCE_LAST_GOOD_PLAN = {ON | {OFF}  
 ON  
 El [!INCLUDE[ssde_md](../../includes/ssde_md.md)] fuerza automáticamente el último plan buena conocido en el [!INCLUDE[tsql_md](../../includes/tsql_md.md)] donde nuevo plan SQL hace que las regresiones de rendimiento de las consultas. El [!INCLUDE[ssde_md](../../includes/ssde_md.md)] continuas supervisa el rendimiento de las consultas de la [!INCLUDE[tsql_md](../../includes/tsql_md.md)] consulta con el plan forzado. Si no hay mejoras de rendimiento, el [!INCLUDE[ssde_md](../../includes/ssde_md.md)] seguirá utilizando último plan buena conocida. Si no se detectan mejoras de rendimiento, la [!INCLUDE[ssde_md](../../includes/ssde_md.md)] generará un nuevo plan SQL. La instrucción se producirá un error si el almacén de consultas no está habilitado o si no está en *lectura y escritura* modo.   

 OFF  
 El [!INCLUDE[ssde_md](../../includes/ssde_md.md)] informa de posibles regresiones de rendimiento de consultas provocadas por cambios de plan SQL en [sys.dm_db_tuning_recommendations](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md) vista. Sin embargo, estas recomendaciones no se aplican automáticamente. Usuario puede supervisar corregir identifican los problemas y recomendaciones activas aplicando [!INCLUDE[tsql_md](../../includes/tsql_md.md)] secuencias de comandos que se muestran en la vista. Es el valor predeterminado.

 **\<change_tracking_option >:: =**  
  
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  No está disponible en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Controla las opciones de seguimiento de cambios. Puede habilitar el seguimiento de cambios, establecer y cambiar opciones, y deshabilitar el seguimiento de cambios. Para ver ejemplos, consulte la sección de ejemplos más adelante en este tema.  
  
 ON  
 Habilita el seguimiento de cambios para la base de datos. Si habilita el seguimiento de cambios, también puede establecer las opciones AUTO CLEANUP y CHANGE RETENTION.  
  
 AUTO_CLEANUP = { ON | OFF }  
 ON  
 La información sobre el seguimiento de cambios se quita de forma automática después del período de retención especificado.  
  
 OFF  
 Los datos del seguimiento de cambios no se quitan de la base de datos.  
  
 CHANGE_RETENTION =*retention_period* {días | HORAS | MINUTOS}  
 Especifica el período mínimo para mantener la información del seguimiento de cambios en la base de datos. Los datos solamente se quitan cuando el valor AUTO_CLEANUP es ON.  
  
 *retention_period* es un entero que especifica el componente numérico del período de retención.  
  
 El período de retención predeterminado es de 2 días. El período de retención mínimo es de 1 minuto. El tipo de retención predeterminado es días.  
  
 OFF  
 Deshabilita el seguimiento de cambios para la base de datos. Debe deshabilitar el seguimiento de cambios en todas las tablas para poder deshabilitarlo en la base de datos.  
  
 **\<containment_option >:: =**  
  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. No está disponible en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Controla las opciones de contención de la base de datos.  
  
 CONTENCIÓN = {NONE | PARCIAL}  
 Ninguno  
 La base de datos no es una base de datos independiente.  
  
 PARTIAL  
 La base de datos es una base de datos independiente. El establecimiento de la contención de la base de datos en parcial producirá un error si la base de datos tiene habilitados la replicación, la captura de datos modificados o el seguimiento de cambios. La comprobación de errores se detiene después de un error. Para obtener más información acerca de las bases de datos independientes, vea [Contained Databases](../../relational-databases/databases/contained-databases.md).  
  
> [!NOTE]  
>  No se puede configurar la contención en [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]. Contención no se designa explícitamente, pero [!INCLUDE[ssSDS](../../includes/sssds-md.md)] puede usar usuarios de base de datos de características independientes como contenidos.  
  
 **\<cursor_option >:: =**  
  
 Controla las opciones del cursor.  
  
 CURSOR_CLOSE_ON_COMMIT { ON | OFF }  
 ON  
 Todos los cursores abiertos al confirmar o revertir una transacción se cierran.  
  
 OFF  
 Los cursores permanecen abiertos cuando se confirma una transacción. Cuando se revierte se cierran todos los cursores, excepto los que están definidos como INSENSITIVE o STATIC.  
  
 La configuración del nivel de conexión, establecida mediante la instrucción SET, invalida la configuración predeterminada de la base de datos para CURSOR_CLOSE_ON_COMMIT. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión y establecen CURSOR_CLOSE_ON_COMMIT en OFF para la sesión al establecer la conexión con una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [SET CURSOR_CLOSE_ON_COMMIT &#40;Transact-SQL&#41;](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md).  
  
 El estado de esta opción se puede determinar mediante el examen de la columna is_cursor_close_on_commit_on de la vista de catálogo sys.databases o la propiedad IsCloseCursorsOnCommitEnabled de la función DATABASEPROPERTYEX.  
  
 CURSOR_DEFAULT { LOCAL | GLOBAL }  
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  No está disponible en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Controla si el ámbito del cursor utiliza LOCAL o GLOBAL.  
  
 LOCAL  
 Cuando se especifica LOCAL y no se define ningún cursor como GLOBAL al crearlo, el ámbito del cursor es local para el lote, procedimiento almacenado o desencadenador en el que se creó el cursor. El nombre del cursor solamente es válido dentro de este ámbito. Es posible hacer referencia al cursor mediante variables de cursor locales del lote, procedimiento almacenado, desencadenador o parámetro OUTPUT del procedimiento almacenado. La asignación del cursor se desasigna implícitamente cuando el lote, el procedimiento almacenado o el desencadenador finaliza, a menos que se haya pasado en un parámetro OUTPUT. Si el cursor se pasa en un parámetro OUTPUT, el cursor se desasigna cuando se cancela la asignación de la última variable que hace referencia a él o se sale del ámbito.  
  
 GLOBAL  
 Si se especifica GLOBAL y no se define ningún cursor como LOCAL al crearlo, el ámbito del cursor es global para la conexión. Se puede hacer referencia al nombre del cursor en cualquier procedimiento almacenado o lote que se ejecute durante la conexión.  
  
 El cursor se desasigna implícitamente solamente cuando se realiza la desconexión. Para obtener más información, vea [DECLARE CURSOR &#40; Transact-SQL &#41; ](../../t-sql/language-elements/declare-cursor-transact-sql.md).  
  
 El estado de esta opción se puede determinar mediante el examen de la columna is_local_cursor_default de la vista de catálogo sys.databases o la propiedad IsLocalCursorsDefault de la función DATABASEPROPERTYEX.  
  
 **\<database_mirroring >**  
  
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  No está disponible en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Para las descripciones del argumento, vea [ALTER creación de reflejo de base de datos de base de datos &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md).  
  
 **\<date_correlation_optimization_option >:: =**  
  
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  No está disponible en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Controla la opción date_correlation_optimization.  
  
 DATE_CORRELATION_OPTIMIZATION { ON | OFF }  
 ON  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]mantiene estadísticas de correlación entre dos tablas cualesquiera de la base de datos que estén vinculadas mediante una restricción FOREIGN KEY y tengan **datetime** columnas.  
  
 OFF  
 No se mantiene ninguna estadística de correlación.  
  
 Para establecer DATE_CORRELATION_OPTIMIZATION en ON, no debe haber ninguna conexión activa con la base de datos, salvo la conexión que está ejecutando la instrucción ALTER DATABASE. Después se admitirán múltiples conexiones.  
  
 La configuración actual de esta opción se puede determinar mediante el examen de la columna is_date_correlation_on de la vista de catálogo sys.databases.  
  
 **\<db_encryption_option >:: =**  
  
 Controla el estado del cifrado de la base de datos.  
  
 ENCRYPTION {ON | OFF}  
 Establece que se cifre (ON) o no se cifre (OFF) la base de datos. Para obtener más información acerca del cifrado de base de datos, vea [cifrado de datos transparente &#40; TDE &#41; ](../../relational-databases/security/encryption/transparent-data-encryption.md), y [cifrado de datos transparente con base de datos SQL Azure](../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md).  
  
 Cuando el cifrado está habilitado en el nivel de la base de datos, se cifrarán todos los grupos de archivos. Todos los grupos de archivos nuevos heredarán la propiedad de cifrado. Si en la base de datos hay grupos de archivos establecidos en **READ ONLY**, se producirá un error en la operación de cifrado de la base de datos.  
  
 Puede ver el estado de cifrado de la base de datos mediante el uso de la [sys.dm_database_encryption_keys](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) vista de administración dinámica.  
  
 **\<db_state_option >:: =**  
  
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  No está disponible en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Controla el estado de la base de datos.  
  
 OFFLINE  
 La base de datos está cerrada, se ha cerrado correctamente y se ha marcado como sin conexión. La base de datos no se puede modificar mientras está desconectada.  
  
 ONLINE  
 La base de datos está abierta y disponible para su uso.  
  
 EMERGENCY  
 La base de datos está marcada como READ_ONLY, el registro está deshabilitado y el acceso está limitado a miembros del rol fijo de servidor sysadmin. EMERGENCY se utiliza principalmente para la solución de problemas. Por ejemplo, una base de datos marcada como sospechosa debido a un archivo de registro dañado se puede establecer en el estado EMERGENCY. Esto puede habilitar el acceso de solo lectura del administrador del sistema a la base de datos. Solamente los miembros del rol fijo de servidor sysadmin pueden establecer una base de datos en el estado EMERGENCY.  
  
> [!NOTE]  
>  **Permisos:** se requiere el permiso ALTER DATABASE para la base de datos para cambiar una base de datos al estado sin conexión o emergencia. Se requiere el permiso ALTER ANY DATABASE de nivel de servidor para mover una base de datos de Sin conexión a En línea.  
  
 El estado de esta opción se puede determinar mediante el examen de las columnas state y state_desc en la [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) vista de catálogo o la propiedad Status de la [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) función. Para más información, consulte [Database States](../../relational-databases/databases/database-states.md).  
  
 Una base de datos marcada como RESTORING no se puede establecer como OFFLINE, ONLINE o EMERGENCY. Es posible que una base de datos se encuentre en estado RESTORING durante una operación de restauración activa o cuando se produce un error en una operación de restauración de una base de datos o de un archivo de registro, debido a un archivo de copia de seguridad dañado.  
  
 **\<db_update_option >:: =**  
  
 Controla si se permiten las actualizaciones en la base de datos.  
  
 READ_ONLY  
 Los usuarios pueden leer datos de la base de datos, pero no pueden modificarlos.  
  
> [!NOTE]  
>  Para mejorar el rendimiento de las consultas, actualice las estadísticas antes de establecer una base de datos en READ_ONLY. Si se necesitan estadísticas adicionales después de establecer una base de datos en READ_ONLY, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] creará las estadísticas en tempdb. Para obtener más información acerca de las estadísticas para una base de datos de solo lectura, vea [estadísticas](../../relational-databases/statistics/statistics.md).  
  
 READ_WRITE  
 La base de datos está disponible para operaciones de lectura y escritura.  
  
 Para cambiar este estado, debe tener acceso exclusivo a la base de datos. Para obtener más información, vea la cláusula SINGLE_USER.  
  
> [!NOTE]  
>  En las bases de datos federadas de [!INCLUDE[ssSDS](../../includes/sssds-md.md)], SET { READ_ONLY | READ_WRITE } está deshabilitado.  
  
 **\<db_user_access_option >:: =**  
  
 Controla el acceso del usuario a la base de datos.  
  
 SINGLE_USER  
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  No está disponible en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Especifica que solamente puede tener acceso a la base de datos un usuario cada vez. Si se especifica SINGLE_USER y hay otros usuarios conectados a la base de datos, la instrucción ALTER DATABASE se bloquea hasta que todos los usuarios se desconecten de la base de datos especificada. Para invalidar este comportamiento, vea WITH \<terminación > cláusula.  
  
 La base de datos permanece en modo SINGLE_USER incluso si es el propio usuario que estableció la opción el que cierra la sesión. A partir de ese momento, un usuario distinto, pero solo uno, puede conectarse a la base de datos.  
  
 Antes de establecer la base de datos como SINGLE_USER, compruebe que la opción AUTO_UPDATE_STATISTICS_ASYNC está establecida en OFF. Cuando se establece en ON, el subproceso en segundo plano usado para actualizar las estadísticas realiza una conexión con la base de datos y no se podrá tener acceso a la base de datos en modo de usuario único. Para ver el estado de esta opción, consulte la columna is_auto_update_stats_async_on en la [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) vista de catálogo. Si la opción está establecida en ON, realice las tareas siguientes:  
  
1.  Establezca AUTO_UPDATE_STATISTICS_ASYNC en OFF.  
  
2.  Comprobar para trabajos de estadísticas asincrónicos consultando la [sys.dm_exec_background_job_queue](../../relational-databases/system-dynamic-management-views/sys-dm-exec-background-job-queue-transact-sql.md) vista de administración dinámica.  
  
 Si hay trabajos activos, permitir que los trabajos completar o termínelos utilizando [KILL STATS JOB](../../t-sql/language-elements/kill-stats-job-transact-sql.md).  
  
RESTRICTED_USER  
 RESTRICTED_USER permite que solamente se conecten a la base de datos los miembros del rol fijo de base de datos db_owner y de los roles fijos de servidor dbcreator y sysadmin, aunque no limita su número. Todas las conexiones a la base de datos se desconectan en el margen de tiempo especificado por la cláusula de terminación de la instrucción ALTER DATABASE. Una vez que la base de datos ha cambiado al estado RESTRICTED_USER, se rechazan los intentos de conexión por parte de usuarios no cualificados.  
  
MULTI_USER  
 Todos los usuarios que tengan los permisos correspondientes pueden conectarse a la base de datos.  
  
 El estado de esta opción se puede determinar mediante el examen de la columna user_access de la vista de catálogo sys.databases o la propiedad UserAccess de la función DATABASEPROPERTYEX.  
  
 **\<delayed_durability_option >:: =**  
  
 **Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Controla si las transacciones se confirman con perdurabilidad total o diferida.  
  
 DISABLED  
 Todas las transacciones tras SET DISABLED son totalmente perdurables. Se omiten las opciones de perdurabilidad que se establecen en un bloque ATOMIC o en una instrucción de confirmación.  
  
 ALLOWED  
 Todas las transacciones tras SET ALLOWED son totalmente perdurables o de perdurabilidad diferida, dependiendo de la opción de perdurabilidad establecida en el bloque ATOMIC o instrucción de confirmación.  
  
 FORCED  
 Todas las transacciones tras SET FORCED son totalmente perdurables. Se omiten las opciones de perdurabilidad que se establecen en un bloque ATOMIC o en una instrucción de confirmación.  
  
 **\<external_access_option >:: =**  
  
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  No está disponible en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Controla si recursos externos como los objetos de otra base de datos pueden tener acceso a la base de datos.  
  
 DB_CHAINING { ON | OFF }  
 ON  
 La base de datos puede ser el origen o el destino de un encadenamiento de propiedad entre bases de datos.  
  
 OFF  
 La base de datos no puede participar en el encadenamiento de propiedad entre bases de datos.  
  
> [!IMPORTANT]  
>  La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reconoce esta configuración si la opción del servidor cross db ownership chaining server es 0 (OFF). Si cross db ownership chaining es 1 (ON), todas las bases de datos de usuario pueden participar en cadenas de propiedad entre bases de datos, independientemente del valor de esta opción. Esta opción se establece mediante [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
 Para establecer esta opción requiere el permiso CONTROL SERVER en la base de datos.  
  
 La opción DB_CHAINING no se puede establecer en estas bases de datos del sistema: maestra, modelo y tempdb.  
  
 El estado de esta opción se puede determinar mediante el examen de la columna is_db_chaining_on de la vista de catálogo sys.databases.  
  
 TRUSTWORTHY { ON | OFF }  
 ON  
 Los módulos de base de datos (por ejemplo, las funciones definidas por el usuario o los procedimientos almacenados) que utilizan un contexto de suplantación pueden tener acceso a recursos externos a la base de datos.  
  
 OFF  
 Los módulos de base de datos en un contexto de suplantación no pueden tener acceso a recursos externos a la base de datos.  
  
 TRUSTWORTHY se establece en OFF siempre que la base de datos se adjunta.  
  
 De forma predeterminada, el valor TRUSTWORTHY se establece en OFF en todas las bases de datos de sistema, excepto msdb. El valor no se puede cambiar en las bases de datos model ni tempdb. Se recomienda no establecer la opción TRUSTWORTHY en ON en la base de datos maestra.  
  
 Para establecer esta opción requiere el permiso CONTROL SERVER en la base de datos.  
  
 El estado de esta opción se puede determinar mediante el examen de la columna is_trustworthy_on de la vista de catálogo sys.databases.  
  
 DEFAULT_FULLTEXT_LANGUAGE  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica el valor de idioma predeterminado para las columnas indizadas de texto completo.  
  
> [!IMPORTANT]  
>  Esta opción solo se permite cuando CONTAINMENT se ha establecido en PARTIAL. Si CONTAINMENT se establece en NONE, se producirán errores.  
  
 DEFAULT_LANGUAGE  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica el idioma predeterminado de los nuevos inicios de sesión creados. El idioma se puede especificar proporcionando el identificador local (LCID), el nombre de idioma o el alias de idioma. Para obtener una lista de alias y nombres de idioma aceptables, vea [sys.syslanguages &#40; Transact-SQL &#41; ](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md). Esta opción solo se permite cuando CONTAINMENT se ha establecido en PARTIAL. Si CONTAINMENT se establece en NONE, se producirán errores.  
  
 NESTED_TRIGGERS  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica si un desencadenador AFTER puede actuar en cascada; es decir, realizar una acción que inicia otro desencadenador que, a su vez, inicia otro desencadenador, etc. Esta opción solo se permite cuando CONTAINMENT se ha establecido en PARTIAL. Si CONTAINMENT se establece en NONE, se producirán errores.  
  
 TRANSFORM_NOISE_WORDS  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Se utiliza para suprimir un mensaje de error si las palabras irrelevantes producen un error en una operación booleana en una consulta de texto completo. Esta opción solo se permite cuando CONTAINMENT se ha establecido en PARTIAL. Si CONTAINMENT se establece en NONE, se producirán errores.  
  
 TWO_DIGIT_YEAR_CUTOFF  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica un número entero comprendido entre 1753 y 9999 que representa el año límite para interpretar años de dos dígitos como años de cuatro dígitos. Esta opción solo se permite cuando CONTAINMENT se ha establecido en PARTIAL. Si CONTAINMENT se establece en NONE, se producirán errores.  
  
 **\<FILESTREAM_option >:: =**  
  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Controla los valores de objetos FileTable.  
  
 NON_TRANSACTED_ACCESS = { OFF | READ_ONLY | FULL }  
 OFF  
 El acceso no transaccional a los datos de FileTable está deshabilitado.  
  
 READ_ONLY  
 Los procesos no transaccionales pueden leer datos FILESTREAM en los objetos FileTable de esta base de datos.  
  
 FULL  
 El acceso no transaccional total a datos FILESTREAM en objetos FileTable está habilitado.  
  
 DIRECTORY_NAME =  *\<directory_name >*  
 Un nombre de directorio compatible con Windows. Este nombre debe ser único entre todos los nombres de directorio de nivel de base de datos en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La comparación de unicidad no distingue mayúsculas de minúsculas, independientemente de la configuración de intercalación. Esta opción se debe establecer antes de crear un objeto FileTable en esta base de datos.  
  
 **\<HADR_options >:: =**  
  
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  No está disponible en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Vea [ALTER HADR de conjunto de base de datos &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-hadr.md).  
  
 **\<mixed_page_allocation_option >:: =**  
  
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)). No está disponible en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 MIXED_PAGE_ALLOCATION {DESACTIVADO | EN} controles si la base de datos puede crear páginas iniciales con una extensión mixta para las primeras ocho páginas de una tabla o índice.  
  
 OFF  
 La base de datos siempre crea páginas iniciales usar extensiones uniformes. Es el valor predeterminado.  
  
 ON  
 La base de datos puede crear páginas iniciales con extensiones mixtas.  
  
 Esta opción es ON para todas las bases de datos del sistema. **tempdb** es la base de datos de sistema solo admite OFF.  
  
 **\<PARAMETERIZATION_option >:: =**  
  
 Controla la opción de parametrización.  
  
 PARAMETERIZATION { SIMPLE | FORCED }  
 SIMPLE  
 Las consultas incluyen parámetros en función del comportamiento predeterminado de la base de datos.  
  
 FORCED  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye parámetros para todas las consultas de la base de datos.  
  
 La configuración actual de esta opción se puede determinar mediante el examen de la columna is_parameterization_forced de la vista de catálogo sys.databases.  
  
 **\<query_store_options >:: =**  
  
 **Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 ON | OFF | CLEAR [ ALL ]  
 Controla si el almacén de consultas está habilitado en esta base de datos y también controla la eliminación del contenido del almacén de consultas.  
  
ON  
 Habilita el almacén de consultas.  
  
OFF  
 Deshabilita el almacén de consultas.  Es el valor predeterminado.   
  
CLEAR  
 Quite el contenido del almacén de consultas.  
  
OPERATION_MODE  
 Describe el modo de operación del almacén de consultas. Los valores válidos son READ_ONLY y READ_WRITE. En el modo READ_WRITE, el almacén de consultas recopila y continúa el plan de consultas y la información de estadística del tiempo de ejecución. En el modo READ_ONLY, la información se puede leer del almacén de consultas, pero no se agrega información nueva. Si se ha agotado el espacio máximo del almacén de consultas, el almacén de consultas cambiará el modo de operación a READ_ONLY.  
  
 CLEANUP_POLICY  
 Describe la directiva de retención de datos del almacén de consultas. STALE_QUERY_THRESHOLD_DAYS determina el número de días de retención de la información de una consulta en el almacén de consultas. STALE_QUERY_THRESHOLD_DAYS es del tipo **bigint**.  
  
 DATA_FLUSH_INTERVAL_SECONDS  
 Determina la frecuencia con la que los datos escritos en el almacén de consultas se conservan en el disco. Para optimizar el rendimiento, los datos recopilados por el almacén de consultas se escriben de manera asincrónica en el disco. La frecuencia con la que se produce esta transferencia asincrónica se configura mediante el argumento DATA_FLUSH_INTERVAL_SECONDS. DATA_FLUSH_INTERVAL_SECONDS es de tipo **bigint**.  
  
 MAX_STORAGE_SIZE_MB  
 Determina el espacio asignado al almacén de consultas. MAX_STORAGE_SIZE_MB es de tipo **bigint**.  
  
 INTERVAL_LENGTH_MINUTES  
 Determina el intervalo de tiempo en el que se agregan los datos de estadísticas de ejecución en tiempo de ejecución al almacén de consultas. Para optimizar el uso del espacio, se agregan las estadísticas de ejecución en tiempo de ejecución en el almacén de estadísticas de tiempo de ejecución en una ventana de tiempo fijo. Esta ventana de tiempo fijo se configura con el argumento INTERVAL_LENGTH_MINUTES. INTERVAL_LENGTH_MINUTES es de tipo **bigint**.  
  
 SIZE_BASED_CLEANUP_MODE  
 Controla si la limpieza se activará automáticamente cuando la cantidad total de datos se acerque al tamaño máximo:  
  
 OFF  
 Limpieza de tamaño en función no se activa automáticamente. 
  
 AUTO  
 Tamaño en función de limpieza se activará automáticamente al tamaño en disco alcanza el 90% de **max_storage_size_mb**. Limpieza de tamaño según quita las consultas menos costosas y más antiguas en primer lugar. Se detiene en aproximadamente el 80% de **max_storage_size_mb**.  Este es el valor de configuración predeterminado.  
  
 SIZE_BASED_CLEANUP_MODE es de tipo **nvarchar**.  
  
 QUERY_CAPTURE_MODE  
 Designa el modo de captura de consulta activa:  
  
 Se capturan todas las todas las consultas. Este es el valor de configuración predeterminado.  Este es el valor de la configuración predeterminada para[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]
  
 AUTO captura consultas pertinentes en función del consumo de recursos y el número de ejecución.  Este es el valor de la configuración predeterminada para[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]
  
 Ninguno dejar de capturar nuevas consultas. Almacén de consultas continuará recopilar las estadísticas de compilación y en tiempo de ejecución para las consultas que se capturaron ya. Utilice esta configuración con precaución ya que se pueden perder para capturar consultas importantes.  
  
 QUERY_CAPTURE_MODE es de tipo **nvarchar**.  
  
 max_plans_per_query  
 Entero que representa el número máximo de planes que se tienen para cada consulta. Valor predeterminado es 200.  
  
 **\<recovery_option >:: =**  
  
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  No está disponible en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Controla las opciones de recuperación de base de datos y la comprobación de errores de E/S de disco.  
  
 FULL  
 Proporciona una restauración completa tras un error del medio, utilizando copias de seguridad del registro de transacciones. Si un archivo de datos está dañado, la recuperación del medio puede restaurar todas las transacciones confirmadas. Para obtener más información, vea [Modelos de recuperación &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
 BULK_LOGGED  
 Proporciona una recuperación tras un error del medio mediante la combinación del rendimiento óptimo y el uso del espacio de registro mínimo para determinadas operaciones a gran escala o masivas. Para obtener información acerca de las operaciones que pueden registrar mínimamente, vea [el registro de transacciones &#40; SQL Server &#41; ](../../relational-databases/logs/the-transaction-log-sql-server.md). En el modelo de recuperación BULK_LOGGED, el registro de estas operaciones es mínimo. Para obtener más información, vea [Modelos de recuperación &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
 SIMPLE  
 Se proporciona una estrategia de copia de seguridad sencilla que utiliza un espacio de registro mínimo. Se puede volver a utilizar el espacio de registro de forma automática cuando ya no se necesite para la recuperación tras errores del servidor. Para obtener más información, vea [Modelos de recuperación &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
> [!IMPORTANT]  
>  El modelo de recuperación simple es más fácil de administrar que los otros dos modelos, pero a costa de un mayor riesgo de perder los datos si se daña un archivo de datos. Todos los cambios se pierden, desde la copia de seguridad de base de datos más reciente o desde la copia de seguridad diferencial de la base de datos, y se deben volver a incluir de forma manual.  
  
 El modelo de recuperación predeterminado se determina mediante el modelo de recuperación de la base de datos **model** . Para obtener más información acerca de cómo seleccionar el modelo de recuperación adecuado, consulte [modelos de recuperación &#40; SQL Server &#41; ](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
 El estado de esta opción se puede determinar examinando la **recovery_model** y **recovery_model_desc** columnas en la vista de catálogo sys.databases o la propiedad de recuperación de la DATABASEPROPERTYEX función.  
  
 TORN_PAGE_DETECTION { ON | OFF }  
 ON  
 Las páginas incompletas se pueden detectar mediante el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 OFF  
 Las páginas incompletas no se pueden detectar mediante [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
> [!IMPORTANT]  
>  La estructura de sintaxis TORN_PAGE_DETECTION ON | OFF se quitará en una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite utilizar esta estructura de sintaxis en nuevos trabajos de desarrollo y prevea modificar las aplicaciones que actualmente la utilizan. Utilice la opción PAGE_VERIFY en su lugar.  
  
 PAGE_VERIFY { CHECKSUM | TORN_PAGE_DETECTION | NONE }   
 Detecta páginas de bases de datos dañadas por errores de ruta de E/S de disco. Los errores de ruta de E/S de disco pueden producir daños en la base de datos debidos por lo general a problemas con el suministro eléctrico o a errores del hardware del disco que ocurren en el momento en que se está escribiendo en el disco.  
  
 CHECKSUM  
 Calcula una suma de comprobación del contenido de toda la página y almacena el valor en el encabezado de página si se escribe una página en el disco. Si la página se lee desde el disco, la suma de comprobación se vuelve a calcular y se compara con el valor de suma de comprobación almacenado en el encabezado de página. Si el valor no coincide, se genera el mensaje de error 824 (indica un error de la suma de comprobación) para el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], así como para el registro de eventos de Windows. Un error de la suma de comprobación indica un problema de ruta de E/S. Para determinar la causa, es necesario investigar el hardware, los controladores de firmware, el BIOS, los controladores de filtro (por ejemplo, software antivirus) y otros componentes de ruta de E/S.  
  
 TORN_PAGE_DETECTION  
 Guarda una pauta específica de 2 bits por cada sector de 512 bytes en la página de base de datos de 8 kilobytes (KB) y la almacena en el encabezado de página de la base de datos al escribir la página en el disco. Si la página se lee desde el disco, los bits rasgados almacenados en el encabezado de página se comparan con la información del sector de la página real. Los valores no coincidentes indican que solamente se ha escrito en el disco una parte de la página. En esta situación, se genera el mensaje de error 824 (indica un error de página rasgada) tanto para el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como para el registro de eventos de Windows. Las páginas rasgadas se suelen detectar mediante la recuperación de la base de datos si se trata realmente de la escritura incompleta de una página. No obstante, otros errores de ruta de E/S pueden generar una página rasgada en cualquier momento.  
  
 Ninguno  
 Las escrituras de páginas de bases de datos no generan un valor CHECKSUM o TORN_PAGE_DETECTION. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no comprobará ninguna suma de comprobación o página rasgada durante una lectura aunque haya un valor CHECKSUM o TORN_PAGE_DETECTION en el encabezado de página.  
  
 Tenga en cuenta los siguientes puntos importantes cuando utilice la opción PAGE_VERIFY:  
  
-   El valor predeterminado es CHECKSUM.  
  
-   Si una base de datos de usuario o del sistema se actualiza a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versión posterior, se conserva el valor de PAGE_VERIFY (NONE o TORN_PAGE_DETECTION). Se recomienda utilizar CHECKSUM.  
  
    > [!NOTE]  
    >  En las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la opción de base de datos PAGE_VERIFY está establecida en NONE para la base de datos tempdb y no se puede modificar. En [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores, el valor predeterminado de la base de datos tempdb es CHECKSUM para las nuevas instalaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Al actualizar una instalación [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el valor predeterminado sigue siendo NONE. La opción se puede modificar. Se recomienda usar CHECKSUM para la base de datos tempdb.  
  
-   Es posible que TORN_PAGE_DETECTION utilice menos recursos, pero proporciona en cambio un subconjunto mínimo de la protección de CHECKSUM.  
  
-   PAGE_VERIFY se puede configurar sin dejar la base de datos sin conexión, ni bloquearla ni impedir la simultaneidad en ella.  
  
-   CHECKSUM y TORN_PAGE_DETECTION se excluyen mutuamente. No se pueden habilitar ambas opciones al mismo tiempo.  
  
 Si se detecta un error de suma de comprobación o de página rasgada, puede realizar una recuperación mediante la restauración de los datos o una regeneración del índice, si el error se limita únicamente a las páginas de índice. Si detecta un error de suma de comprobación, ejecute DBCC CHECKDB para determinar el tipo de página o páginas de base de datos afectadas. Para obtener más información acerca de las opciones de restauración, vea [argumentos RESTORE &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md). Aunque la restauración de los datos resolverá el problema de los datos dañados, es necesario diagnosticar y corregir la causa (por ejemplo, un error del hardware de disco) lo antes posible, para evitar errores continuos.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vuelve a intentar cualquier lectura que genere un error con una suma de comprobación, una página rasgada u otros errores de E/S, en cuatro ocasiones. Si la lectura se desarrolla correctamente en uno de los reintentos, se escribe un mensaje en el registro de errores y el comando que ha desencadenado la lectura continúa. Si los reintentos no se realizan correctamente, el comando genera el mensaje de error 824.  
  
 Para obtener más información acerca de la suma de comprobación, página rasgada, reintento de lectura, mensajes de error 823 y 824 y otros [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] características de auditoría de E/S, vea este [sitio Web de Microsoft](http://go.microsoft.com/fwlink/?LinkId=47160).  
  
 La configuración actual de esta opción se puede determinar mediante el examen de la columna page_verify_option de la [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) vista de catálogo o la propiedad IsTornPageDetectionEnabled de la [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)(función).  
  
**\<remote_data_archive_option >:: =**  
  
 **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. No está disponible en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Habilita o deshabilita Stretch Database para la base de datos. Para obtener más información, vea [Stretch Database](../../sql-server/stretch-database/stretch-database.md).  
  
REMOTE_DATA_ARCHIVE = {ON (servidor = \<nombre_servidor >, {CREDENCIAL = \<db_scoped_credential_name > | FEDERATED_SERVICE_ACCOUNT = ON | {OFF}) | DESACTIVADO ACTIVADO  
 Habilita Stretch Database para la base de datos. Para obtener más información, incluidos los requisitos previos adicionales, consulte [Enable Stretch Database para una base de datos](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md).  
  
 **Permisos**. Para habilitar Stretch Database para una base de datos o una tabla, requiere permisos db_owner. Para habilitar Stretch Database para una base de datos, también requiere permisos CONTROL DATABASE.  
  
SERVER = \<nombre_servidor >  
 Especifica la dirección del servidor de Azure. Incluir la `.database.windows.net` parte del nombre. Por ejemplo, `MyStretchDatabaseServer.database.windows.net`.  
  
CREDENCIAL = \<db_scoped_credential_name >  
 Especifica el ámbito de la base de datos de credencial que la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza para conectar con el servidor de Azure. Asegúrese de que la credencial existe antes de ejecutar este comando. Para obtener más información, consulte [CREATE DATABASE SCOPED CREDENTIAL &#40; Transact-SQL &#41; ](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).  
  
FEDERATED_SERVICE_ACCOUNT = ON | DESACTIVAR  
 Puede usar una cuenta de servicio federado para las instalaciones de SQL Server para comunicarse con el servidor remoto de Azure cuando se cumplen las condiciones siguientes.  
  
-   La cuenta de servicio con la que se está ejecutando la instancia de SQL Server es una cuenta de dominio.  
  
-   La cuenta de dominio pertenece a un dominio cuyo Active Directory está federado con Azure Active Directory.  
  
-   El servidor remoto de Azure está configurado para admitir la autenticación de Azure Active Directory.  
  
-   La cuenta de servicio con la que se ejecuta la instancia de SQL Server debe configurarse como una cuenta dbmanager o sysadmin en el servidor remoto de Azure.  
  
 Si se especifica ON, no se puede especificar el argumento de la CREDENCIAL. Si se especifica OFF, tendrá que proporcionar el argumento de la CREDENCIAL.  
  
 OFF  
 Deshabilita la base de datos de Stretch para la base de datos. Para obtener más información, vea [Deshabilitar Stretch Database y recuperar datos remotos](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md).  
  
 Solo puede deshabilitar Stretch Database para una base de datos después de la base de datos ya no contiene todas las tablas que están habilitadas para Stretch Database. Después de deshabilitar Stretch Database, se detiene la migración de datos y resultados de la consulta ya no se incluyen los resultados de las tablas remotas.  
  
 Deshabilitar Stretch no quita la base de datos remota. Si quiere eliminar la base de datos remota, tiene que quitarla mediante el Portal de administración de Azure.  
  
**\<service_broker_option >:: =**  
  
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  No está disponible en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Controla las siguientes [!INCLUDE[ssSB](../../includes/sssb-md.md)] opciones: habilita o deshabilita la entrega de mensajes, establece un nuevo [!INCLUDE[ssSB](../../includes/sssb-md.md)] identificador o establece prioridades de conversación en ON u OFF.  
  
 ENABLE_BROKER  
 Indica que se habilite [!INCLUDE[ssSB](../../includes/sssb-md.md)] para la base de datos especificada. Se inicia la entrega de mensajes y la marca is_broker_enabled se establece en TRUE en la vista de catálogo sys.databases. La base de datos conserva el identificador de [!INCLUDE[ssSB](../../includes/sssb-md.md)] existente. Service Broker no puede habilitarse mientras la base de datos sea la entidad de seguridad en una configuración de creación de reflejo de la base de datos.  
  
> [!NOTE]  
>  ENABLE_BROKER requiere un bloqueo exclusivo de base de datos. Si otras sesiones tienen recursos bloqueados en la base de datos, ENABLE_BROKER esperará hasta que las demás sesiones liberen sus bloqueos. Para habilitar [!INCLUDE[ssSB](../../includes/sssb-md.md)] en una base de datos de usuario, asegúrese de que ninguna otra sesión esté utilizando la base de datos antes de ejecutar la instrucción ALTER DATABASE SET ENABLE_BROKER, por ejemplo, colocando la base de datos en modo de usuario único. Para habilitar [!INCLUDE[ssSB](../../includes/sssb-md.md)] en la base de datos msdb, detenga en primer lugar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que [!INCLUDE[ssSB](../../includes/sssb-md.md)] pueda obtener el bloqueo necesario.  
  
 DISABLE_BROKER  
 Indica que se deshabilite [!INCLUDE[ssSB](../../includes/sssb-md.md)] para la base de datos especificada. Se detiene la entrega de mensajes y la marca is_broker_enabled se establece en FALSE en la vista de catálogo sys.databases. La base de datos conserva el identificador de [!INCLUDE[ssSB](../../includes/sssb-md.md)] existente.  
  
 NEW_BROKER  
 Especifica que la base de datos debe recibir un identificador de agente nuevo. Dado que la base de datos se considera como un Service Broker nuevo, todas las conversaciones existentes en la base de datos se quitan inmediatamente sin generar mensajes de finalización de diálogo. Cualquier ruta que haga referencia al identificador de [!INCLUDE[ssSB](../../includes/sssb-md.md)] anterior se debe volver a crear con el nuevo identificador.  
  
 ERROR_BROKER_CONVERSATIONS  
 Especifica que la entrega de mensajes de [!INCLUDE[ssSB](../../includes/sssb-md.md)] está habilitada. Esto conserva existente [!INCLUDE[ssSB](../../includes/sssb-md.md)] identificador de la base de datos. [!INCLUDE[ssSB](../../includes/sssb-md.md)] finaliza todas las conversaciones de la base de datos con un error. Esto permite que las aplicaciones realicen una limpieza regular de las conversaciones existentes.  
  
 HONOR_BROKER_PRIORITY {ON | OFF}  
 ON  
 Las operaciones de envío tienen en cuenta los niveles de prioridad asignados a las conversaciones. Los mensajes de las conversaciones que tienen niveles de prioridad altos se envían antes que los que tienen asignados niveles de prioridad bajos.  
  
 OFF  
 Las operaciones de envío se ejecutan como si todas las conversaciones tuvieran el nivel de prioridad predeterminado.  
  
 Los cambios de la opción HONOR_BROKER_PRIORITY tienen efecto inmediato para los diálogos nuevos o los que no tiene ningún mensaje en espera de ser enviado. Los diálogos que tienen mensajes en espera de ser enviados cuando se ejecuta ALTER DATABASE no adoptarán el nuevo valor hasta que se haya enviado alguno de los mensajes del diálogo. La cantidad de tiempo que transcurre hasta que se inicien todos los diálogos con el nuevo valor puede variar considerablemente.  
  
 El valor actual de esta propiedad se notifica en la columna is_broker_priority_honored de la [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) vista de catálogo.  
  
 **\<snapshot_option >:: =**  
  
 Determina el nivel de aislamiento de transacción.  
  
 ALLOW_SNAPSHOT_ISOLATION { ON | OFF }  
 ON  
 Habilita la opción de instantánea en el nivel de base de datos. Cuando se habilita, las instrucciones DML inician la generación de versiones de fila aunque ninguna transacción utilice el aislamiento de instantánea. Una vez habilitada esta opción, las transacciones pueden especificar el nivel de aislamiento de transacción SNAPSHOT. Si se ejecuta una transacción en el nivel de aislamiento SNAPSHOT, todas las instrucciones verán una instantánea de los datos tal como estaban al inicio de la transacción. Si una transacción ejecutada en el nivel de aislamiento SNAPSHOT tiene acceso a los datos de varias bases de datos, ALLOW_SNAPSHOT_ISOLATION debe establecerse en ON en todas las bases de datos o cada instrucción de la transacción debe utilizar sugerencias de bloqueo en cualquier referencia de una cláusula FROM a una tabla de una base de datos donde ALLOW_SNAPSHOT_ISOLATION sea OFF.  
  
 OFF  
 Desactiva la opción de instantánea en el nivel de base de datos. Las transacciones no pueden especificar el nivel de aislamiento de transacción SNAPSHOT.  
  
 Si se establece ALLOW_SNAPSHOT_ISOLATION en un estado nuevo (de ON a OFF o de OFF a ON), ALTER DATABASE no devuelve el control al autor de la llamada hasta confirmar todas las transacciones existentes de la base de datos. Si la base de datos ya se encuentra en el estado especificado en la instrucción ALTER DATABASE, se devuelve de inmediato el control al autor de la llamada. Si la instrucción ALTER DATABASE no devuelve rápidamente, utilice [sys.dm_tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md) para determinar si hay transacciones de larga ejecución. Si se cancela la instrucción ALTER DATABASE, la base de datos permanece en el estado en que estaba al iniciar ALTER DATABASE. El [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) vista de catálogo indica el estado de las transacciones de aislamiento de instantánea en la base de datos. Si **snapshot_isolation_state_desc** = IN_TRANSITION_TO_ON, ALTER DATABASE ALLOW_SNAPSHOT_ISOLATION OFF se pause seis segundos y vuelva a intentar la operación.  
  
 No puede cambiar el estado de ALLOW_SNAPSHOT_ISOLATION si la base de datos está establecida en OFFLINE.  
  
 Si establece ALLOW_SNAPSHOT_ISOLATION en una base de datos READ_ONLY, la configuración se mantendrá si la base de datos se establece posteriormente en READ_WRITE.  
  
 Puede cambiar la configuración de ALLOW_SNAPSHOT_ISOLATION para las bases de datos maestra, model, msdb y tempdb. Si cambia la configuración para tempdb, dicha configuración se mantiene cada vez que la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] se detiene y se reinicia. Si cambia la configuración para la base de datos model, dicha configuración se convierte en la configuración predeterminada para todas las bases de datos nuevas que se crean, excepto para tempdb.  
  
 La opción es ON de forma predeterminada para las bases de datos maestra y msdb.  
  
 La configuración actual de esta opción se puede determinar mediante el examen de la columna snapshot_isolation_state de la vista de catálogo sys.databases.  
  
 READ_COMMITTED_SNAPSHOT { ON | OFF }  
 ON  
 Habilita la opción de instantánea de lectura confirmada en el nivel de base de datos. Cuando se habilita, las instrucciones DML inician la generación de versiones de fila aunque ninguna transacción utilice el aislamiento de instantánea. Una vez habilitada esta opción, las transacciones que especifican el nivel de aislamiento de lectura confirmada usan versiones de fila en lugar de bloqueos. Si una transacción se ejecuta en el nivel de aislamiento de lectura confirmada, todas las instrucciones ven una instantánea de los datos tal como estaban al inicio de la instrucción.  
  
 OFF  
 Desactiva la opción de instantánea de lectura confirmada en el nivel de base de datos. Las transacciones que especifican el nivel de aislamiento READ COMMITTED utilizan el bloqueo.  
  
 Para establecer READ_COMMITTED_SNAPSHOT en ON u OFF, no puede haber ninguna conexión activa a la base de datos, excepto la que ejecuta el comando ALTER DATABASE. Sin embargo, no es necesario que la base de datos esté en modo de usuario único. No puede cambiar el estado de esta opción si la base de datos está establecida en OFFLINE.  
  
 Si establece READ_COMMITTED_SNAPSHOT en una base de datos READ_ONLY, la configuración se mantiene si la base de datos se establece después en READ_WRITE.  
  
 READ_COMMITTED_SNAPSHOT no se puede cambiar a ON para las bases de datos maestra, tempdb o msdb. Si cambia la configuración para model, dicha configuración se convierte en predeterminada para todas las bases de datos creadas, excepto para tempdb.  
  
 La configuración actual de esta opción se puede determinar mediante el examen de la columna is_read_committed_snapshot_on de la vista de catálogo sys.databases.  
  
> [!WARNING]  
>  Cuando se crea una tabla con **DURABILITY = SCHEMA_ONLY**, y **READ_COMMITTED_SNAPSHOT** se cambia posteriormente mediante **ALTER DATABASE**, se perderán los datos de la tabla.  
  
 MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT { ON | OFF }  
 **Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 ON  
 Cuando el nivel de aislamiento de transacción se establece en uno inferior a SNAPSHOT (por ejemplo, READ COMMITTED o READ UNCOMMITTED), todas las operaciones interpretadas de [!INCLUDE[tsql](../../includes/tsql-md.md)] en las tablas con optimización para memoria se realizan con aislamiento SNAPSHOT. Esto se hace independientemente de si el nivel de aislamiento de transacción se establece explícitamente en el nivel de sesión o el valor predeterminado se utiliza de forma implícita.  
  
 OFF  
 No eleva el nivel de aislamiento de transacción para las operaciones interpretadas de [!INCLUDE[tsql](../../includes/tsql-md.md)] en las tablas con optimización para memoria.  
  
 No puede cambiar el estado de MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT si la base de datos está establecida en OFFLINE.  
  
 De forma predeterminada, la opción está desactivada.  
  
 La configuración actual de esta opción se puede determinar examinando la **is_memory_optimized_elevate_to_snapshot_on** columna en el [sys.databases &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) vista de catálogo.  
  
 **\<sql_option >:: =**  
  
 Controla las opciones de cumplimiento con ANSI en el nivel de base de datos.  
  
 ANSI_NULL_DEFAULT { ON | OFF }  
 Determina el valor predeterminado, NULL o NOT NULL de una columna o [tipo CLR definido por el usuario](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md) para que la nulabilidad no está explícitamente definida en las instrucciones CREATE TABLE o ALTER TABLE. Las columnas para las que se hayan definido restricciones siguen las reglas de las restricciones, independientemente de esta configuración.  
  
 ON  
 El valor predeterminado es NULL.  
  
 OFF  
 El valor predeterminado es NOT NULL.  
  
 La configuración del nivel de conexión, establecida mediante la instrucción SET, invalida la configuración predeterminada del nivel de base de datos para ANSI_NULL_DEFAULT. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión y establecen ANSI_NULL_DEFAULT en ON para la sesión cuando se realiza la conexión con una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [SET ANSI_NULL_DFLT_ON &#40; Transact-SQL &#41; ](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md).  
  
 Para la compatibilidad con ANSI, si se establece la opción de base de datos ANSI_NULL_DEFAULT en ON, el valor predeterminado cambia a NULL.  
  
 El estado de esta opción se puede determinar mediante el examen de la columna is_ansi_null_default_on de la vista de catálogo sys.databases o la propiedad IsAnsiNullDefault de la función DATABASEPROPERTYEX.  
  
 ANSI_NULLS { ON | OFF }  
 ON  
 Todas las comparaciones con un valor NULL se evalúan como UNKNOWN.  
  
 OFF  
 Las comparaciones de valores no UNICODE con un valor NULL se evalúan como TRUE si ambos valores son NULL.  
  
> [!IMPORTANT]  
>  En una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ANSI_NULLS siempre estará ON y cualquier aplicación que establezca explícitamente la opción en OFF producirá un error. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan.  
  
 La configuración del nivel de conexión establecida mediante la instrucción SET invalida la configuración predeterminada de la base de datos para ANSI_NULLS. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión y establecen ANSI_NULLS en ON para la sesión al realizar la conexión con una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md).  
  
 El valor de SET ANSI_NULLS también debe estar en ON al crear o realizar cambios en los índices en columnas calculadas o vistas indizadas.  
  
 El estado de esta opción se puede determinar mediante el examen de la columna is_ansi_nulls_on de la vista de catálogo sys.databases o la propiedad IsAnsiNullsEnabled de la función DATABASEPROPERTYEX.  
  
 ANSI_PADDING { ON | OFF }  
 ON  
 Las cadenas se rellenan a la misma longitud antes de la conversión o inserción en un **varchar** o **nvarchar** tipo de datos.  
  
 Los espacios en blanco finales de los valores de caracteres insertados en las columnas **varchar** o **nvarchar** y los ceros finales de los valores binarios insertados en las columnas **varbinary** no se recortan. Los valores no se rellenan hasta completar la longitud de la columna.  
  
 OFF  
 Espacios en blanco para finales **varchar** o **nvarchar** y los ceros finales para **varbinary** se recortan.  
  
 Si se especifica OFF, esta opción solamente afecta a la definición de las columnas nuevas.  
  
> [!IMPORTANT]  
>  En una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ANSI_PADDING siempre estará en ON y cualquier aplicación que establezca explícitamente la opción en OFF producirá un error. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Se recomienda establecer siempre ANSI_PADDING en ON. ANSI_PADDING también debe estar en ON al crear o tratar índices en columnas calculadas o vistas indizadas.  
  
 **Char(*n*)** y **binario(*n*)** columnas que permiten valores NULL se rellenan hasta completar la longitud de la columna Si ANSI_PADDING se establece en ON, pero los espacios en blanco y los ceros finales se recortan Si ANSI_PADDING es OFF. **Char(*n*)** y **binario(*n*)** columnas que no permiten valores NULL siempre se rellenan a la longitud de la columna.  
  
 La configuración del nivel de conexión establecida mediante la instrucción SET invalida la configuración predeterminada del nivel de base de datos para ANSI_PADDING. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión y establecen ANSI_PADDING en ON para la sesión al realizar la conexión con una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md).  
  
 El estado de esta opción se puede determinar mediante el examen de la columna is_ansi_padding_on de la vista de catálogo sys.databases o la propiedad IsAnsiPaddingEnabled de la función DATABASEPROPERTYEX.  
  
 ANSI_WARNINGS { ON | OFF }  
 ON  
 Se emiten los mensajes de error o advertencias cuando se producen condiciones como la división por cero o cuando aparecen valores NULL en funciones de agregación.  
  
 OFF  
 No se genera ninguna advertencia ni se devuelven valores NULL si se producen condiciones como la división por cero.  
  
 El valor de SET ANSI_WARNINGS debe ser ON al crear o realizar cambios en los índices en columnas calculadas o vistas indizadas.  
  
 La configuración del nivel de conexión establecida mediante la instrucción SET invalida la configuración predeterminada de la base de datos para ANSI_WARNINGS. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión y establecen ANSI_WARNINGS en ON para la sesión al realizar la conexión con una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md).  
  
 El estado de esta opción se puede determinar mediante el examen de la columna is_ansi_warnings_on de la vista de catálogo sys.databases o la propiedad IsAnsiWarningsEnabled de la función DATABASEPROPERTYEX.  
  
 ARITHABORT { ON | OFF }  
 ON  
 Se finaliza una consulta cuando se produce un error de desbordamiento o de división por cero durante su ejecución.  
  
 OFF  
 Se muestra un mensaje de advertencia si se produce uno de estos errores, pero la consulta, lote o transacción continúa procesándose como si no se hubiera producido ningún error.  
  
 El valor de SET ARITHABORT debe ser ON al crear o realizar cambios en los índices en columnas calculadas o vistas indizadas.  
  
 El estado de esta opción se puede determinar mediante el examen de la columna is_arithabort_on de la vista de catálogo sys.databases o la propiedad IsArithmeticAbortEnabled de la función DATABASEPROPERTYEX.  
  
 COMPATIBILITY_LEVEL { 90 | 100 | 110 | 120}  
 Para obtener más información, vea [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
 CONCAT_NULL_YIELDS_NULL { ON | OFF }  
 ON  
 El resultado de una operación de concatenación es NULL si alguno de los operandos es NULL. Por ejemplo, la concatenación de la cadena de caracteres "Esto es" y NULL da como resultado el valor NULL, y no el valor "Esto es".  
  
 OFF  
 El valor NULL se trata como una cadena de caracteres vacía.  
  
 El valor de CONCAT_NULL_YIELDS_NULL también debe ser ON al crear o realizar cambios en los índices en columnas calculadas o vistas indizadas.  
  
> [!IMPORTANT]  
>  En una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], CONCAT_NULL_YIELDS_NULL siempre estará en ON y cualquier aplicación que establezca explícitamente la opción en OFF producirá un error. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan.  
  
 La configuración del nivel de conexión establecida mediante la instrucción SET invalida la configuración predeterminada de la base de datos para CONCAT_NULL_YIELDS_NULL. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión y establecen CONCAT_NULL_YIELDS_NULL en ON para la sesión al realizar la conexión con una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md).  
  
 El estado de esta opción se puede determinar mediante el examen de la columna is_concat_null_yields_null_on de la vista de catálogo sys.databases o la propiedad IsNullConcat de la función DATABASEPROPERTYEX.  
  
 QUOTED_IDENTIFIER { ON | OFF }  
 ON  
 Las comillas dobles se pueden usar para identificadores delimitados.  
  
 Todas las cadenas delimitadas por comillas dobles se interpretan como identificadores de objetos. Los identificadores entre comillas no tienen que adaptarse a las reglas de [!INCLUDE[tsql](../../includes/tsql-md.md)] para identificadores. Pueden ser palabras clave e incluir caracteres que no suelen permitirse en los identificadores de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Si una comilla simple (') forma parte de la cadena literal, puede representarse mediante comillas dobles (").  
  
 OFF  
 Los identificadores no se pueden incluir entre comillas y deben seguir todas las reglas de [!INCLUDE[tsql](../../includes/tsql-md.md)] para los identificadores. Los literales se pueden delimitar con comillas simples o dobles.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también permite delimitar los identificadores con corchetes ([ ]). Los identificadores entre corchetes pueden usarse siempre, independientemente de la configuración de QUOTED_IDENTIFIER. Para obtener más información, vea [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
 Al crear una tabla, la opción QUOTED IDENTIFIER siempre se almacena como ON en los metadatos de la tabla, incluso si la opción está establecida en OFF al crear la tabla.  
  
 La configuración en el nivel de conexión establecida mediante la instrucción SET invalida la configuración predeterminada de la base de datos para QUOTED_IDENTIFIER. De forma predeterminada, los clientes ODBC y OLE DB generan una instrucción SET en el nivel de conexión y establecen QUOTED_IDENTIFIER en ON al realizar la conexión con una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
 El estado de esta opción se puede determinar mediante el examen de la columna is_quoted_identifier_on de la vista de catálogo sys.databases o la propiedad IsQuotedIdentifiersEnabled de la función DATABASEPROPERTYEX.  
  
 NUMERIC_ROUNDABORT { ON | OFF }  
 ON  
 Se genera un error cuando se produce una pérdida de precisión en una expresión.  
  
 OFF  
 Las pérdidas de precisión no generan mensajes de error y el resultado se redondea con la precisión de la columna o variable que lo almacena.  
  
 El valor de NUMERIC_ROUNDABORT debe ser OFF al crear o realizar cambios en índices de columnas calculadas o vistas indizadas.  
  
 El estado de esta opción se puede determinar mediante el examen de la columna is_numeric_roundabort_on de la vista de catálogo sys.databases o la propiedad IsNumericRoundAbortEnabled de la función DATABASEPROPERTYEX.  
  
 RECURSIVE_TRIGGERS { ON | OFF }  
 ON  
 Se permite la activación recursiva de desencadenadores AFTER.  
  
 OFF  
 No se permite únicamente la activación recursiva directa de desencadenadores AFTER. Para deshabilitar también la repetición indirecta de desencadenadores AFTER, establezca la opción nested triggers servidor **0** utilizando **sp_configure**.  
  
> [!NOTE]  
>  La recursividad directa solo se evita cuando RECURSIVE_TRIGGERS se establece en OFF. Para deshabilitar la recursividad indirecta, también debe establecer la opción de servidor desencadenadores anidados en 0.  
  
 El estado de esta opción se puede determinar mediante el examen de la columna is_recursive_triggers_on de la vista de catálogo sys.databases o la propiedad IsRecursiveTriggersEnabled de la función DATABASEPROPERTYEX.  
  
 **\<target_recovery_time_option >:: =**  
  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. No está disponible en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Especifica la frecuencia de puntos de comprobación indirectos por base de datos. A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] el valor predeterminado para nuevas bases de datos es 1 minuto, lo que indica la base de datos utilizará puntos de comprobación indirectos. Para versiones anteriores, el valor predeterminado es 0, lo que indica que la base de datos utilizará puntos de comprobación automáticos, cuya frecuencia depende del valor de intervalo de recuperación de la instancia del servidor. [!INCLUDE[msCoName](../../includes/msconame-md.md)]recomienda 1 minuto para la mayoría de los sistemas.  
  
 TARGET_RECOVERY_TIME **=***target_recovery_time* { SECONDS | MINUTES }  
 *target_recovery_time*  
 Especifica el límite máximo de tiempo para recuperar la base de datos especificada en caso de bloqueo.  
  
 SECONDS  
 Indica que *target_recovery_time* se expresa como el número de segundos.  
  
 MINUTES  
 Indica que *target_recovery_time* se expresa como el número de minutos.  
  
 Para obtener más información sobre puntos de comprobación indirectos, vea [puntos de comprobación de base de datos &#40; SQL Server &#41; ](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
 **CON \<terminación >:: =**  
  
 Especifica el momento en que se revierten las transacciones incompletas cuando la base de datos pasa de un estado a otro. Si se omite la cláusula de terminación, la instrucción ALTER DATABASE espera indefinidamente a que se produzca un bloqueo en la base de datos. Solamente se puede especificar una cláusula de terminación y debe seguir a las cláusulas SET.  
  
> [!NOTE]  
>  No todas las opciones de base de datos usan WITH \<terminación > cláusula. Para obtener más información, vea la tabla situada en el apartado "[Configurar opciones](#SettingOptions) " en la sección "Comentarios" de este tema.  
  
 ROLLBACK AFTER *entero* [SECONDS] | REVERSIÓN INMEDIATA  
 Especifica si la operación de reversión se ejecuta transcurrido un número de segundos determinado o de forma inmediata.  
  
 NO_WAIT  
 Especifica que se producirá un error en la solicitud si el cambio solicitado en el estado u opción de la base de datos no se puede completar inmediatamente sin esperar a que las propias transacciones se confirmen o reviertan.  
  
##  <a name="SettingOptions"></a>Opciones de configuración  
 Para recuperar la configuración actual de las opciones de base de datos, use la [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) vista de catálogo o [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)  
  
 Una vez configurada una opción de la base de datos, la modificación surte efecto de inmediato.  
  
 Para cambiar los valores predeterminados de cualquiera de las opciones de las bases de datos recién creadas, cambie la opción adecuada en la base de datos model.  
  
 No todas las opciones de base de datos usan WITH \<terminación > cláusula o se pueden especificar en combinación con otras opciones. En la siguiente tabla se incluyen estas opciones, su estado y el estado de terminación.  
  
|Categoría de opciones|Se puede especificar con otras opciones|Puede utilizar WITH \<terminación > cláusula|  
|----------------------|-----------------------------------------|---------------------------------------------|  
|\<db_state_option >|Sí|Sí|  
|\<db_user_access_option >|Sí|Sí|  
|\<db_update_option >|Sí|Sí|  
|\<delayed_durability_option >|Sí|Sí|  
|\<external_access_option >|Sí|No|  
|\<cursor_option >|Sí|No|  
|\<auto_option >|Sí|No|  
|\<sql_option >|Sí|No|  
|\<recovery_option >|Sí|No|  
|\<target_recovery_time_option >|No|Sí|  
|\<database_mirroring_option >|No|No|  
|ALLOW_SNAPSHOT_ISOLATION|No|No|  
|READ_COMMITTED_SNAPSHOT|No|Sí|  
|MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT|Sí|Sí|  
|\<service_broker_option >|Sí|No|  
|DATE_CORRELATION_OPTIMIZATION|Sí|Sí|  
|\<parameterization_option >|Sí|Sí|  
|\<change_tracking_option >|Sí|Sí|  
|\<db_encryption >|Sí|No|  
  
 La memoria caché de planes para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se borra si se establece alguna de las opciones siguientes:  
  
|||  
|-|-|  
|OFFLINE|READ_WRITE|  
|ONLINE|MODIFY FILEGROUP DEFAULT|  
|MODIFY_NAME|MODIFY FILEGROUP READ_WRITE|  
|COLLATE|MODIFY FILEGROUP READ_ONLY|  
|READ_ONLY||  
  
 La memoria caché de procedimientos también se vacía en los escenarios siguientes.  
  
-   Una base de datos tiene la opción de base de datos AUTO_CLOSE establecida en ON. Cuando ninguna conexión de usuario hace referencia a la base de datos ni la usa, la tarea de segundo plano intenta cerrar la base de datos y apagarla de modo automático.  
  
-   Ejecuta varias consultas con una base de datos que tiene opciones predeterminadas. Después, la base de datos se quita.  
  
-   Se quita una instantánea de base de datos para una base de datos de origen.  
  
-   Volvió a generar correctamente el registro de transacciones para una base de datos.  
  
-   Restaura una copia de seguridad de una base de datos  
  
-   Separa una base de datos.  
  
 Al borrar la memoria caché de planes, se provoca una nueva compilación de todos los planes de ejecución posteriores y puede ocasionar una disminución repentina y temporal del rendimiento de las consultas. Para cada almacén de caché borrado de la memoria caché de planes, el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contendrá el siguiente mensaje informativo: "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha detectado %d instancias de vaciado del almacén de caché '%s' (parte de la memoria caché de planes) debido a determinadas operaciones de mantenimiento de base de datos o reconfiguración". Este mensaje se registra cada cinco minutos siempre que se vacíe la memoria caché dentro de ese intervalo de tiempo.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-setting-options-on-a-database"></a>A. Configurar opciones en una base de datos  
 En el siguiente ejemplo se establece el modelo de recuperación y las opciones de comprobación de páginas de datos para la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY FULL PAGE_VERIFY CHECKSUM;  
GO  
  
```  
  
### <a name="b-setting-the-database-to-readonly"></a>B. Establecer la base de datos en READ_ONLY  
 El cambio del estado de una base de datos o un grupo de archivos a READ_ONLY o READ_WRITE requiere el acceso exclusivo a la base de datos. En el siguiente ejemplo la base de datos se establece en el modo `SINGLE_USER` para obtener acceso exclusivo. A continuación, el ejemplo establece el estado de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] en `READ_ONLY` y devuelve el acceso a la base de datos a todos los usuarios.  
  
> [!NOTE]  
>  En este ejemplo se utiliza la opción de terminación `WITH ROLLBACK IMMEDIATE` en la primera instrucción `ALTER DATABASE` . Todas las transacciones incompletas se revierten y las restantes conexiones con la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] se desconectan de inmediato.  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
SET SINGLE_USER  
WITH ROLLBACK IMMEDIATE;  
GO  
ALTER DATABASE AdventureWorks2012  
SET READ_ONLY  
GO  
ALTER DATABASE AdventureWorks2012  
SET MULTI_USER;  
GO  
  
```  
  
### <a name="c-enabling-snapshot-isolation-on-a-database"></a>C. Habilitar el aislamiento de instantánea en una base de datos  
 En el siguiente ejemplo se habilita la opción del marco de aislamiento de instantánea para la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
USE AdventureWorks2012;  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
SET ALLOW_SNAPSHOT_ISOLATION ON;  
GO  
-- Check the state of the snapshot_isolation_framework  
-- in the database.  
SELECT name, snapshot_isolation_state,   
    snapshot_isolation_state_desc AS description  
FROM sys.databases  
WHERE name = N'AdventureWorks2012';  
GO  
  
```  
  
 El conjunto de resultados muestra que el marco de aislamiento de instantánea está habilitado.  
  
 |name |snapshot_isolation_state |description|  
 |-------------------- |------------------------  |----------|  
 |AdventureWorks2012   |1                        | ON |  
  
### <a name="d-enabling-modifying-and-disabling-change-tracking"></a>D. Habilitar, modificar y deshabilitar el seguimiento de cambios  
 En el ejemplo siguiente se habilita el seguimiento de cambios para la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] y se establece el período de retención en `2` días.  
  
```  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = ON  
(AUTO_CLEANUP = ON, CHANGE_RETENTION = 2 DAYS);  
```  
  
 En el ejemplo siguiente se muestra cómo cambiar el período de retención a `3` días.  
  
```  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING (CHANGE_RETENTION = 3 DAYS);  
```  
  
 En el ejemplo siguiente se muestra cómo deshabilitar el seguimiento de cambios para la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = OFF;  
```  
  
### <a name="e-enabling-the-query-store"></a>E. Habilitar el almacén de consultas  
 **Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 En el ejemplo siguiente se habilita el almacén de consultas y configura los parámetros de almacén de consultas.  
  
```  
ALTER DATABASE AdventureWorks2012  
SET QUERY_STORE = ON   
    (  
      OPERATION_MODE = READ_ONLY   
    , CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 5 )  
    , DATA_FLUSH_INTERVAL_SECONDS = 2000   
    , MAX_STORAGE_SIZE_MB = 10   
    , INTERVAL_LENGTH_MINUTES = 10   
    );  
```  
  
## <a name="see-also"></a>Vea también  
 [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [Reflejo de la base de datos ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)   
 [ALTER DATABASE SET HADR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)   
 [Estadísticas](../../relational-databases/statistics/statistics.md)   
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Habilitar y deshabilitar el seguimiento de cambios &#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [SET TRANSACTION ISOLATION LEVEL &#40; Transact-SQL &#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [Sys.data_spaces &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)  
  
  

