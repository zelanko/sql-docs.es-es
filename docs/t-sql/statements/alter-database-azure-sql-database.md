---
title: ALTER DATABASE (base de datos SQL Azure) | Documentos de Microsoft
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 08/07/2017
ms.prod: 
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6fc5fd95-2045-4f20-a914-3598091bc7cc
caps.latest.revision: 37
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fe1ad8f6331d853b65ac10c64ae9d0349d962cfb
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="alter-database-azure-sql-database"></a>ALTER DATABASE (base de datos SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Modifica un [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Cambia el nombre de un objetivo de la base de datos, la edición y el servicio de una base de datos, un grupo elástico de combinación y conjuntos de opciones de base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
      -- Azure SQL Database Syntax  
ALTER DATABASE { database_name }  
{  
    MODIFY NAME =new_database_name  
  | MODIFY ( <edition_options> [, ... n] )   
  | SET { <option_spec> [ ,... n ] }   
  | ADD SECONDARY ON SERVER <partner_server_name>  
      [WITH (\<add-secondary-option>::= [, ... n] ) ]  
  | REMOVE SECONDARY ON SERVER <partner_server_name>  
  | FAILOVER  
  | FORCE_FAILOVER_ALLOW_DATA_LOSS  
}  
  
<edition_options> ::=   
{  

      MAXSIZE = { 100 MB | 250 MB | 500 MB | 1 … 1024 … 4096 GB }    
    | EDITION = { 'basic' | 'standard' | 'premium' | 'premiumrs' }   
    | SERVICE_OBJECTIVE =   
                 {  'S0' | 'S1' | 'S2' | 'S3'| 'S4'| 'S6'| 'S7'| 'S9'| 'S12' |
                 | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15' | 
                 | 'PRS1' | 'PRS2' | 'PRS4' | 'PRS6' |
                 | { ELASTIC_POOL (name = <elastic_pool_name>) }   
                 }   
}  

<add-secondary-option> ::=  
   {  
      ALLOW_CONNECTIONS = { ALL | NO }  
     | SERVICE_OBJECTIVE =   
                 {  'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' |
                 | 'P1' | 'P2' | 'P4'| 'P6' | 'P11' | 'P15' |
                 | 'PRS1' | 'PRS2' | 'PRS4' | 'PRS6' |  
                 | { ELASTIC_POOL ( name = <elastic_pool_name>) }   
                 }   
   }  
  
 [;]  
```  
  
```  
SET OPTIONS AVAILABLE FOR SQL Database  
Full descriptions of the set options are available in the topic   
ALTER DATABASE SET Options. The supported syntax is listed here.  
  
<optionspec> ::=   
{  
    <auto_option>   
  | <compatibility_level_option>  
  | <cursor_option>   
  | <db_encryption_option>  
  | <db_update_option>   
  | <db_user_access_option>   
  | <delayed_durability_option>  
  | <parameterization_option>  
  | <query_store_options>  
  | <snapshot_option>  
  | <sql_option>   
  | <target_recovery_time_option>   
  | <termination>  
  | <temporal_history_retention>  
}  
  
<auto_option> ::=   
{  
    AUTO_CREATE_STATISTICS { OFF | ON [ ( INCREMENTAL = { ON | OFF } ) ] }   
  | AUTO_SHRINK { ON | OFF }   
  | AUTO_UPDATE_STATISTICS { ON | OFF }   
  | AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }  
}  
  
<compatibility_level_option>::=  
COMPATIBILITY_LEVEL = { 130 | 120 | 110 | 100 }  
  
<cursor_option> ::=   
{  
    CURSOR_CLOSE_ON_COMMIT { ON | OFF }   
}  
  
<db_encryption_option> ::=  
    ENCRYPTION { ON | OFF }  
  
<db_update_option> ::=  
    { READ_ONLY | READ_WRITE }  
  
<db_user_access_option> ::=  
    { RESTRICTED_USER | MULTI_USER }  
  
<delayed_durability_option> ::=    DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }  
  
<parameterization_option> ::=  
    PARAMETERIZATION { SIMPLE | FORCED }  
  
<query_store_options> ::=  
{  
    QUERY_STORE   
    {  
          = OFF   
        | = ON [ ( <query_store_option_list> [,... n] ) ]  
        | ( < query_store_option_list> [,... n] )  
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
}  
  
<snapshot_option> ::=  
{  
    ALLOW_SNAPSHOT_ISOLATION { ON | OFF }  
  | READ_COMMITTED_SNAPSHOT {ON | OFF }  
  | MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT {ON | OFF }  
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
  
<termination>  ::=   
{  
    ROLLBACK AFTER integer [ SECONDS ]   
  | ROLLBACK IMMEDIATE   
  | NO_WAIT  
}  

<temporal_history_retention>  ::=  TEMPORAL_HISTORY_RETENTION { ON | OFF }
```  
  
 Para obtener una descripción completa de las opciones set, vea [ALTER DATABASE SET Options &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) y [modificar el nivel de compatibilidad de base de datos &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Es el nombre de la base de datos que se va a modificar.  
  
 CURRENT  
 Designa que la base de datos actual en uso se debe modificar.  
  
 MODIFY NAME  **=**  *new_database_name*  
 Cambia el nombre de la base de datos con el nombre especificado como *new_database_name*.  
  
 MODIFICAR (edición  **=**  ["básico" | 'estándar' | 'premium' | 'premiumrs'])    
 Cambia el nivel de servicio de la base de datos.  Cambio de edición se produce un error si la propiedad MAXSIZE de la base de datos se establece en un valor fuera del intervalo válido admitido por esa edición.  
  
 MODIFICAR (MAXSIZE  **=**  [100 MB | 500 MB | 1 | 1024... 4096] GB)  
 Especifica el tamaño máximo de la base de datos. El tamaño máximo debe cumplir con el conjunto válido de valores de la propiedad EDITION de la base de datos. Cambiar el tamaño máximo de la base de datos puede causar que cambie también el valor de EDITION de la base de datos. En la tabla siguiente se muestran los valores admitidos de MAXSIZE y los valores predeterminados (D) para los niveles de servicio de [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
|**MAXSIZE**|**Básico**|**S0-S2**|**S12 S3**|**P1-P6 y PRS1 PRS6**| **P11 P15** 
|-----------------|---------------|------------------|-----------------|-----------------|-----------------|-----------------|  
|100 MB|√|√|√|√|√|  
|250 MB|√|√|√|√|√|  
|500 MB|√|√|√|√|√|  
|1 GB|√|√|√|√|√|  
|2 GB|√ (D)|√|√|√|√|  
|5 GB|N/D|√|√|√|√|  
|10 GB|N/D|√|√|√|√|  
|20 GB|N/D|√|√|√|√|  
|30 GB|N/D|√|√|√|√|  
|40 GB|N/D|√|√|√|√|  
|50 GB|N/D|√|√|√|√|  
|100 GB|N/D|√|√|√|√|  
|150 GB|N/D|√|√|√|√|  
|200 GB|N/D|√|√|√|√|  
|250 GB|N/D|√ (D)|√ (D)|√|√|  
|300 GB|N/D|√|√|√|√|  
|400 GB|N/D|√|√|√|√|
|500 GB|N/D|√|√|√ (D)|√|
|750 GB|N/D|√|√|√|√|
|1024 GB|N/D|√|√|√|√ (D)|
|De 1024 GB hasta 4096 GB en incrementos de 256 GB *|N/D|N/D|N/D|N/D|√|√|  
  
 \*P11 y P15 permiten MAXSIZE hasta 4 TB con 1024 GB que el tamaño predeterminado.  P11 y P15 pueden utilizar hasta 4 TB de almacenamiento incluyen sin cargo adicional. En el nivel Premium, MAXSIZE mayor de 1 TB está actualmente disponible en las siguientes regiones: nos East2, oeste de Estados Unidos, nos Gov Virginia, Europa occidental, Alemania Central, sur Asia oriental, este de Japón, Australia Oriental, Canadá Central y este de Canadá. Para las limitaciones actuales, vea [solo las bases de datos](https://docs.microsoft.com/azure/sql-database-single-database-resources).  

  
 Las reglas siguientes se aplican a los argumentos MAXSIZE y EDITION:  
  
-   El valor MAXSIZE, si se especifica, tiene que ser un valor válido, que se muestra en la tabla anterior.  
  
-   Si se especifica EDITION pero no se especifica MAXSIZE, se usa el valor predeterminado de la edición. Por ejemplo, si EDITION está establecido en Standard y MAXSIZE no se especifica, el valor de MAXSIZE se establece automáticamente en 500 MB.  
  
-   Si se especifica MAXSIZE ni EDITION, EDITION se establece en estándar (S0) y MAXSIZE está establecido en 250 GB.  
  
 MODIFICAR SERVICE_OBJECTIVE {'S0' | 'S1' | 'S2' | ' S3 "| 'S4' | 'S6' | 'S7' | 'S9' | 'S12' | 'P1' | 'P2' | 'P4' | 'P6' | 'P11' | 'P15' | 'PRS1' | 'PRS2' | 'PRS4' | 'PRS6' |  
 Especifica el nivel de rendimiento. Para obtener más información sobre el tamaño, las ediciones y las combinaciones de objetivos de servicio y descripciones de objetivo de servicio, consulte [niveles de servicio de base de datos de SQL Azure y los niveles de rendimiento](http://msdn.microsoft.com/library/azure/dn741336.aspx). Si el SERVICE_OBJECTIVE especificado no es compatible con la edición, recibirá un error. Para cambiar el valor SERVICE_OBJECTIVE de un nivel a otro (por ejemplo, de S1 a P1), también debe cambiar el valor EDITION.  
  
ELASTIC_POOL (nombre = \<elastic_pool_name >) para agregar una base de datos existente a un grupo elástico, establezca el SERVICE_OBJECTIVE de la base de datos en ELASTIC_POOL y proporcione el nombre del grupo elástico. También puede usar esta opción para cambiar la base de datos a un grupo elástico diferentes dentro del mismo servidor. Para obtener más información, consulte [crear y administrar un grupo elástico de base de datos SQL](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/). Para quitar una base de datos de un grupo elástico, utilice ALTER DATABASE para establecer el SERVICE_OBJECTIVE en un nivel de rendimiento de la base de datos único.  

 Agregar secundario ON SERVER \<partner_server_name >  
 Crea una base de datos de replicación geográfica secundaria con el mismo nombre en un servidor de socio comercial, hacer que la base de datos local en una replicación geográfica principal y comienza a replicar datos de forma asincrónica desde el servidor principal a la nueva base de datos secundaria. Si ya existe una base de datos con el mismo nombre en la base de datos secundaria, se produce un error en el comando. El comando se ejecuta en la base de datos maestra en el servidor que hospeda la base de datos local que se convierte en el servidor principal.  
  
 CON ALLOW_CONNECTIONS {TODOS | **N** }  
 Cuando no se especifica ALLOW_CONNECTIONS, se establece en NO de forma predeterminada. Si se establece todas, es una base de datos de solo lectura que permite a todos los inicios de sesión con los permisos adecuados para conectarse.  
  
 CON SERVICE_OBJECTIVE {'S0' | 'S1' | 'S2' | ' S3 "| 'S4' | 'S6' | 'S7' | 'S9' | 'S12' | 'P1' | 'P2' | 'P4' | 'P6' | 'P11' | 'P15' | 'PRS1' | 'PRS2' | 'PRS4' | 'PRS6'}  
 Cuando no se especifica SERVICE_OBJECTIVE, se crea la base de datos secundaria en el mismo nivel de servicio que la base de datos principal. Cuando se especifica SERVICE_OBJECTIVE, se crea la base de datos secundaria en el nivel especificado. Esta opción permite crear secundarias replicadas geográficamente con niveles de servicio más económico. El SERVICE_OBJECTIVE especificado debe estar en la misma edición que el origen. Por ejemplo, no puede especificar S0 si es de la edición premium.  
  
 ELASTIC_POOL (nombre = \<elastic_pool_name)  
 Cuando no se especifica ELASTIC_POOL, la base de datos secundaria no se crea en un grupo elástico. Cuando se especifica ELASTIC_POOL, se crea la base de datos secundaria en el grupo especificado.  
  
> [!IMPORTANT]  
>  El usuario que ejecuta el comando Agregar secundario debe ser DBManager en servidor principal, ser miembro de db_owner en la base de datos local y DBManager en servidor secundario.  
  
 QUITAR secundaria ON SERVER \<partner_server_name >  
 Quita la replicación geográfica secundaria base de datos especificada en el servidor especificado. El comando se ejecuta en la base de datos maestra en el servidor que hospeda la base de datos principal.  
  
> [!IMPORTANT]  
>  El usuario que ejecuta el comando Quitar secundario debe ser DBManager en el servidor principal.  
  
 FAILOVER  
 Promueve la base de datos secundaria en colaboración de replicación geográfica en la que el comando se ejecuta para convertirlo en el servidor principal y degrada el principal actual para convertirse en la nueva base de datos secundaria. Como parte de este proceso, el modo de replicación geográfica temporalmente cambian de modo asincrónico a modo sincrónico. Durante el proceso de conmutación por error:  
  
1.  El servidor principal deja de realizar nuevas transacciones.  
  
2.  Todas las transacciones pendientes se vacían en la base de datos secundaria.  
  
3.  La base de datos secundaria se convierte en el servidor principal y comienza la replicación geográfica asincrónica con el elemento principal anterior y la nueva base de datos secundaria.  
  
 Este orden garantiza que se produce ninguna pérdida de datos. El período durante el cual están disponibles ambas bases de datos es del orden de 0-25 segundos mientras se intercambiarán los roles. La operación total debería tardar no más de un minuto aproximadamente. Si la base de datos principal no está disponible cuando se emite este comando, el comando produce un error con un mensaje de error que indica que la base de datos principal no está disponible. Si el proceso de conmutación por error no se completa y aparece bloqueado, puede usar el comando para forzar la conmutación por error y aceptar la pérdida de datos - y, a continuación, si tiene que recuperar los datos perdidos, llame a devops (CSS) para recuperar los datos perdidos.  
  
> [!IMPORTANT]  
>  El usuario que ejecuta el comando de conmutación por error debe ser DBManager en el servidor principal y el servidor secundario.  
  
 FORCE_FAILOVER_ALLOW_DATA_LOSS  
 Promueve la base de datos secundaria en colaboración de replicación geográfica en la que el comando se ejecuta para convertirlo en el servidor principal y degrada el principal actual para convertirse en la nueva base de datos secundaria. Utilice este comando solo cuando la réplica principal actual ya no está disponible. Está diseñado para la recuperación de desastres, al restaurar la disponibilidad es crítico y alguna pérdida de datos es aceptable.  
  
 Durante una conmutación por error forzada:  
  
1.  La base de datos secundaria especificada inmediatamente se convierte en la base de datos principal y comienza a aceptar las nuevas transacciones.  
  
2.  Cuando la réplica principal original puede volver a conectar con el nuevo elemento principal, una copia de seguridad incremental se realiza en el original principal y la réplica principal original se convierte en una nueva base de datos secundaria.  
  
3.  Para recuperar datos desde esta copia de seguridad incremental en el servidor principal anterior, el usuario pone devops/CSS.  
  
4.  Si no hay réplicas secundarias adicionales, automáticamente se configuren para ser elementos secundarios de la nueva réplica principal. Este proceso es asincrónico y puede haber un retraso hasta que se complete este proceso. Hasta que se haya completado la reconfiguración, los servidores secundarios continúan siendo secundarias de la réplica principal anterior.  
  
> [!IMPORTANT]  
>  El usuario que ejecuta el comando FORCE_FAILOVER_ALLOW_DATA_LOSS debe ser DBManager en el servidor principal y el servidor secundario.  
  
## <a name="remarks"></a>Comentarios  
 Para quitar una base de datos, use [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md).  
  
 Para reducir el tamaño de una base de datos, utilice [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).  
  
 La instrucción ALTER DATABASE se debe ejecutar en el modo de confirmación automática (modo de administración de transacciones predeterminado) y no se permite en una transacción explícita o implícita.  
  
 Al borrar la memoria caché de planes, se provoca una nueva compilación de todos los planes de ejecución posteriores y puede ocasionar una disminución repentina y temporal del rendimiento de las consultas. Para cada almacén de caché borrado de la memoria caché de planes, el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contendrá el siguiente mensaje informativo: "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha detectado %d instancias de vaciado del almacén de caché '%s' (parte de la memoria caché de planes) debido a determinadas operaciones de mantenimiento de base de datos o reconfiguración". Este mensaje se registra cada cinco minutos siempre que se vacíe la memoria caché dentro de ese intervalo de tiempo.  
  
 La memoria caché de procedimientos también se vacía en los escenarios siguientes:  
  
-   Una base de datos tiene la opción de base de datos AUTO_CLOSE establecida en ON. Cuando ninguna conexión de usuario hace referencia a la base de datos ni la usa, la tarea de segundo plano intenta cerrar la base de datos y apagarla de modo automático.  
  
-   Ejecuta varias consultas con una base de datos que tiene opciones predeterminadas. Después, la base de datos se quita.  
  
-   Volvió a generar correctamente el registro de transacciones para una base de datos.  
  
-   Restaura una copia de seguridad de una base de datos  
  
-   Separa una base de datos.  
  
## <a name="viewing-database-information"></a>Ver la información de la base de datos  
 Se pueden utilizar vistas de catálogo, funciones del sistema y procedimientos almacenados del sistema para devolver información sobre bases de datos, archivos y grupos de archivos.  
  
## <a name="permissions"></a>Permissions  
 Solo el inicio de sesión principal de nivel de servidor (creado por el proceso de aprovisionamiento) o los miembros del rol de base de datos `dbmanager` pueden modificar una base de datos.  
  
> [!IMPORTANT]  
>  El propietario de la base de datos no puede modificarla a menos que sea miembro del rol `dbmanager`.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-changing-the-name-of-a-database"></a>A. Cambiar el nombre de una base de datos  
 En el ejemplo siguiente se cambia el nombre de la base de datos `db1` a `db2`.  
  
```  
ALTER DATABASE db1  
Modify Name = db2 ;  
```    

### <a name="b-changing-the-edition-size-and-service-objective-for-an-existing-database"></a>B. Cambiar el objetivo de edición, el tamaño y el servicio para una base de datos existente

```
ALTER DATABASE [db1] MODIFY (EDITION = 'Premium', MAXSIZE = 1024 GB, SERVICE_OBJECTIVE = 'P15');
```

### <a name="c-moving-a-database-to-a-different-elastic-pool"></a>C. Mover una base de datos a otro grupo elástico  
 Mueve una base de datos existente en un grupo denominado pool1:  
  
```  
ALTER DATABASE db1   
MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = pool1 ) ) ;  
```  
  
### <a name="d-add-a-geo-replication-secondary"></a>D. Agregar un elemento secundario de replicación geográfica  
 Crea una base de datos secundaria ilegible db1 en secondaryserver de servidor de la Bd1 en el servidor local.  
  
```  
ALTER DATABASE db1   
ADD SECONDARY ON SERVER secondaryserver   
WITH ( ALLOW_CONNECTIONS = NO )  
```  
  
### <a name="e-remove-a-geo-replication-secondary"></a>E. Quitar un elemento secundario de replicación geográfica  
 Quita la Bd1 de base de datos secundaria en secondaryserver de servidor.  
  
```  
ALTER DATABASE db1   
REMOVE SECONDARY ON SERVER testsecondaryserver   
```  
  
### <a name="f-failover-to-a-geo-replication-secondary"></a>F. Conmutación por error a un elemento secundario de replicación geográfica  
 Promueve un secundario de la base de datos db1 en secondaryserver de servidor se convierta en la nueva base de datos principal cuando se ejecuta en el servidor secondaryserver.  
  
```  
ALTER DATABASE db1 FAILOVER  
```  
  
## <a name="see-also"></a>Vea también  
 [Crear base de datos &#40; Base de datos SQL Azure &#41;](../../t-sql/statements/create-database-azure-sql-database.md)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [SET TRANSACTION ISOLATION LEVEL &#40; Transact-SQL &#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [Sys.database_mirroring_witnesses &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [Sys.data_spaces &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [Sys.FileGroups &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [Sys.master_files &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [Bases de datos del sistema](../../relational-databases/databases/system-databases.md)  
  
  

