---
title: ALTER DATABASE (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 02/13/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6fc5fd95-2045-4f20-a914-3598091bc7cc
caps.latest.revision: 37
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ddec688efe7ce468b7af1c05389b9cc1e86cf4c4
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/05/2018
---
# <a name="alter-database-azure-sql-database"></a>ALTER DATABASE (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Modifica una [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Cambia el nombre de una base de datos, el objetivo de edición y servicio de una base de datos, se une a un grupo elástico y establece opciones de base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Azure SQL Database Syntax  
ALTER DATABASE { database_name }  
{  
    MODIFY NAME = new_database_name  
  | MODIFY ( <edition_options> [, ... n] ) 
  | SET { <option_spec> [ ,... n ] } 
  | ADD SECONDARY ON SERVER <partner_server_name>  
    [WITH ( <add-secondary-option>::= [, ... n] ) ]  
  | REMOVE SECONDARY ON SERVER <partner_server_name>  
  | FAILOVER  
  | FORCE_FAILOVER_ALLOW_DATA_LOSS  
}  
[;] 

<edition_options> ::= 
{  

  MAXSIZE = { 100 MB | 250 MB | 500 MB | 1 … 1024 … 4096 GB }  
  | EDITION = { 'basic' | 'standard' | 'premium' | 'GeneralPurpose' | 'BusinessCritical'} 
  | SERVICE_OBJECTIVE = 
       {  <service-objective>
       | { ELASTIC_POOL (name = <elastic_pool_name>) } 
       } 
}  

<add-secondary-option> ::=  
   {  
      ALLOW_CONNECTIONS = { ALL | NO }  
     | SERVICE_OBJECTIVE = 
       {  <service-objective> 
       | { ELASTIC_POOL ( name = <elastic_pool_name>) } 
       } 
   }  

<service-objective> ::=  { 'S0' | 'S1' | 'S2' | 'S3'| 'S4'| 'S6'| 'S7'| 'S9'| 'S12' |
       | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15'
      | 'GP_GEN4_1' | 'GP_GEN4_2' | 'GP_GEN4_4' | 'GP_GEN4_8' | 'GP_GEN4_16' 
      | 'BC_GEN4_1' | 'BC_GEN4_2' | 'BC_GEN4_4' | 'BC_GEN4_8' | 'BC_GEN4_16' | 
      }

```  
  
```
-- SET OPTIONS AVAILABLE FOR SQL Database  
-- Full descriptions of the set options are available in the topic 
-- ALTER DATABASE SET Options. The supported syntax is listed here.  

<option_spec> ::= 
{  
    <auto_option> 
  | <change_tracking_option> 
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
  
<delayed_durability_option> ::=  DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }  
  
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
  | COMPATIBILITY_LEVEL = { 100 | 110 | 120 | 130 | 140 }  
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
  
 Para obtener las descripciones completas de las opciones, vea [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md) y [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## <a name="arguments"></a>Argumentos  

*database_name*  

Es el nombre de la base de datos que se va a modificar.  
  
CURRENT  

Designa que la base de datos actual en uso se debe modificar.  
  
MODIFY NAME **=***new_database_name*  

Reemplaza el nombre de la base de datos por el nombre especificado como *new_database_name*. En el ejemplo siguiente se cambia el nombre de la base de datos `db1` a `db2`:   

```  
ALTER DATABASE db1  
    MODIFY Name = db2 ;  
```    

MODIFY (EDITION **=** ['basic' | 'standard' | 'premium' |'GeneralPurpose' | 'BusinessCritical'])    

Cambia el nivel de servicio de la base de datos. Se ha quitado la compatibilidad con "premiumrs". Si tiene preguntas, use este alias de correo electrónico: premium-rs@microsoft.com.

En el ejemplo siguiente se cambia la edición a `premium`:
  
```  
ALTER DATABASE current 
    MODIFY (EDITION = 'premium');
``` 

Se produce un error en el cambio de EDITION si la propiedad MAXSIZE de la base de datos está establecida en un valor fuera del intervalo válido admitido por esa edición.  

MODIFY (MAXSIZE **=** [100 MB | 500 MB | 1 | 1024…4096] GB)  

Especifica el tamaño máximo de la base de datos. El tamaño máximo debe cumplir con el conjunto válido de valores de la propiedad EDITION de la base de datos. Cambiar el tamaño máximo de la base de datos puede causar que cambie también el valor de EDITION de la base de datos. En la tabla siguiente se muestran los valores admitidos de MAXSIZE y los valores predeterminados (D) para los niveles de servicio de [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
**Modelo basado en DTU**

|**MAXSIZE**|**Basic**|**S0-S2**|**S3-S12**|**P1-P6**|**P11-P15**|  
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
|Desde 1024 GB hasta 4096 GB en incrementos de 256 GB*|N/D|N/D|N/D|N/D|√|√|  
  
\* P11 y P15 permiten un valor de MAXSIZE de hasta 4 TB, con 1024 GB como tamaño predeterminado.  P11 y P15 pueden usar hasta 4 TB de almacenamiento incluido sin cargos adicionales. En el nivel Premium, un valor de MAXSIZE superior a 1 TB está actualmente disponible en las siguientes regiones: Este de EE. UU. 2, Oeste de EE. UU., Virginia Gob. EE. UU., Europa Occidental, Centro de Alemania, Asia Suroriental, Japón Oriental, Este de Australia, Canadá Central y Canadá Oriental. Para obtener más información sobre las limitaciones de recursos para el modelo basado en DTU, consulte [DTU-based resource limits](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits) (Límites de recursos basados en DTU).  

El valor MAXSIZE para el modelo basado en DTU, si se especifica, tiene que ser un valor válido según se muestra en la tabla anterior para el nivel de servicio especificado.
 
**Modelo basado en el núcleo virtual**

**Nivel de servicio de uso general**

|MAXSIZE|GP_Gen4_1|GP_Gen4_2|GP_Gen4_4|GP_Gen4_8|GP_Gen4_16|
|:--- | --: |--: |--: |--: |--: |
|Tamaño máximo de datos (GB)|1024|1024|1536|3072|4096|

**Nivel de servicio crítico para la empresa**

|Nivel de rendimiento|BC_Gen4_1|BC_Gen4_2|BC_Gen4_4|BC_Gen4_8|BC_Gen4_16|
|:--- | --: |--: |--: |--: |--: |
|Tamaño máximo de datos (GB)|1024|1024|1536|2048|2048|

Si no hay ningún valor `MAXSIZE` establecido al utilizar el modelo de núcleo virtual, el valor predeterminado es 32 GB. Para obtener más información sobre las limitaciones de recursos para el modelo basado en núcleo virtual, consulte [DTU-based resource limits](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits) (Límites de recursos basados en el núcleo virtual).
  
Las reglas siguientes se aplican a los argumentos MAXSIZE y EDITION:  
  
- Si se especifica EDITION pero no se especifica MAXSIZE, se usa el valor predeterminado de la edición. Por ejemplo, si EDITION está establecido en Standard y MAXSIZE no se especifica, el valor de MAXSIZE se establece automáticamente en 500 MB.  
  
- Si no se especifican los valores de MAXSIZE ni EDITION, este último se establece en Standard (S0) y MAXSIZE en 250 GB.  

MODIFY (SERVICE_OBJECTIVE = \<objetivo_de_servicio>)  

Especifica el nivel de rendimiento. El ejemplo siguiente se cambia el objetivo de servicio de una base de datos Premium a `P6`:
 
```sql  
ALTER DATABASE current 
    MODIFY (SERVICE_OBJECTIVE = 'P6');
```  

Especifica el nivel de rendimiento. Los valores disponibles para el objetivo de servicio son: `S0`, `S1`, `S2`, `S3`, `S4`, `S6`, `S7`, `S9`, `S12`, `P1`, `P2`, `P4`, `P6`, `P11`, `P15`, `GP_GEN4_1`, `GP_GEN4_2`, `GP_GEN4_4`, `GP_GEN4_8`, `GP_GEN4_16`, `BC_GEN4_1` `BC_GEN4_2` `BC_GEN4_4` `BC_GEN4_8` `BC_GEN4_16`. 

Para conocer las descripciones de los objetivos de servicio y obtener más información sobre las combinaciones de tamaño, ediciones y objetivos de servicio, consulte [Niveles de servicio y niveles de rendimiento de Azure SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/), [DTU-based resource limits](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits) (Límites de recursos basados en DTU) y [vCore-based resource limits](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits) (Límites de recursos basados en núcleo virtual). Se ha quitado la compatibilidad para los objetivos de servicio de PRS. Si tiene preguntas, use este alias de correo electrónico: premium-rs@microsoft.com. 
  
MODIFY (SERVICE_OBJECTIVE = ELASTIC\_POOL (name = \<elastic_pool_name>)  

Para agregar una base de datos existente a un grupo elástico, establezca el valor SERVICE_OBJECTIVE de la base de datos en ELASTIC_POOL e indique el nombre del grupo. También se puede usar esta opción para cambiar la base de datos a un grupo elástico diferente dentro del mismo servidor. Para obtener más información, vea [Create and manage a SQL Database elastic pool](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/) (Creación y administración de un grupo elástico de SQL Database). Para quitar una base de datos de un grupo elástico, use ALTER DATABASE para establecer el valor SERVICE_OBJECTIVE en un nivel de rendimiento de una sola base de datos.  

ADD SECONDARY ON SERVER \<partner_server_name>  

Crea una base de datos de replicación geográfica secundaria con el mismo nombre en un servidor asociado, lo que convierte a la base de datos local en una base de datos principal de replicación geográfica, y comienza a replicar los datos de forma asincrónica desde la base de datos principal a la nueva base de datos secundaria. Si ya existe una base de datos con el mismo nombre en la base de datos secundaria, se produce un error en el comando. El comando se ejecuta en la base de datos maestra en el servidor que hospeda la base de datos local que se convierte en la principal.  
  
WITH ALLOW_CONNECTIONS { **ALL** | NO }  

Cuando no se especifica ALLOW_CONNECTIONS, se establece en ALL de forma predeterminada. Si se establece en ALL, es una base de datos de solo lectura que permite la conexión de todos los inicios de sesión con los permisos adecuados.  
  
WITH SERVICE_OBJECTIVE {  `S0`, `S1`, `S2`, `S3`, `S4`, `S6`, `S7`, `S9`, `S12`, `P1`, `P2`, `P4`, `P6`, `P11`, `P15`, `GP_GEN4_1`, `GP_GEN4_2`, `GP_GEN4_4`, `GP_GEN4_8`, `GP_GEN4_16`, `BC_GEN4_1` `BC_GEN4_2` `BC_GEN4_4` `BC_GEN4_8` `BC_GEN4_16` }  

Cuando no se especifica SERVICE_OBJECTIVE, la base de datos secundaria se crea en el mismo nivel de servicio que la principal. Cuando se especifica SERVICE_OBJECTIVE, la base de datos secundaria se crea en el nivel especificado. Esta opción permite crear bases de datos secundarias con replicación geográfica con niveles de servicio más económicos. El valor SERVICE_OBJECTIVE especificado debe estar en la misma edición que el origen. Por ejemplo, no se puede especificar S0 si la edición es Premium.  
  
ELASTIC_POOL (name = \<elastic_pool_name)  

Cuando no se especifica ELASTIC_POOL, la base de datos secundaria no se crea en un grupo elástico. Cuando se especifica ELASTIC_POOL, la base de datos secundaria se crea en el grupo especificado.  
  
> [!IMPORTANT]  
>  El usuario que ejecuta el comando ADD SECONDARY debe ser DBManager en el servidor principal, ser miembro de db_owner en la base de datos local y DBManager en el servidor secundario.  
  
REMOVE SECONDARY ON SERVER  \<partner_server_name>  

Quita la base de datos secundaria con replicación geográfica especificada en el servidor especificado. El comando se ejecuta en la base de datos maestra en el servidor que hospeda la base de datos principal.  
  
> [!IMPORTANT]  
>  El usuario que ejecuta el comando REMOVE SECONDARY debe ser DBManager en el servidor principal.  
  
FAILOVER  

Promueve la base de datos secundaria en colaboración de replicación geográfica en la que el comando se ejecuta para convertirla en la principal y degrada la base de datos principal actual para convertirla en la nueva base de datos secundaria. Como parte de este proceso, el modo de replicación geográfica se cambia temporalmente de asincrónico a sincrónico. Durante el proceso de conmutación por error:  
  
1.  La base de datos principal deja de aceptar nuevas transacciones.  
  
2.  Todas las transacciones pendientes se vacían en la base de datos secundaria.  
  
3.  La base de datos secundaria se convierte en la principal y comienza la replicación geográfica asincrónica con la base de datos principal anterior y la base de datos secundaria nueva.  
  
Esta secuencia garantiza que no se produzca pérdida de datos. El período durante el que ambas bases de datos no están disponibles es de entre 0 y 25 segundos mientras se intercambian los roles. La operación total no debería tardar más de un minuto aproximadamente. Si la base de datos principal no está disponible cuando se emite este comando, el comando produce un error con un mensaje de error en el que se indica que la base de datos principal no está disponible. Si el proceso de conmutación por error no se completa y aparece bloqueado, se puede usar el comando para forzar la conmutación por error y aceptar la pérdida de datos, y después, si tiene que recuperar los datos perdidos, llama a devops (CSS) para recuperarlos.  
  
> [!IMPORTANT]  
>  El usuario que ejecuta el comando FAILOVER debe ser DBManager tanto en el servidor principal como en el secundario.  
  
FORCE_FAILOVER_ALLOW_DATA_LOSS  

Promueve la base de datos secundaria en colaboración de replicación geográfica en la que el comando se ejecuta para convertirla en la principal y degrada la base de datos principal actual para convertirla en la nueva base de datos secundaria. Use este comando solo cuando la base de datos principal actual ya no esté disponible. Está diseñado solo para la recuperación ante desastres, cuando la restauración de la disponibilidad sea esencial y se acepte cierta pérdida de datos.  
  
Durante una conmutación por error forzada:  
  
1. La base de datos secundaria especificada se convierte inmediatamente en la base de datos principal y comienza a aceptar nuevas transacciones.  
  
2. Cuando la base de datos principal original se pueda volver a conectar con la nueva base de datos principal, se toma una copia de seguridad incremental en la base de datos principal original y se convierte en una nueva base de datos secundaria.  
  
3. Para recuperar datos de esta copia de seguridad incremental en la base de datos principal anterior, el usuario usa devops/CSS.  
  
4. Si hay otras bases de datos secundarias, se reconfiguran de forma automática para convertirse en secundarias de la nueva base de datos principal. Este proceso es asincrónico y puede haber un retraso hasta que finalice. Hasta que se haya completado la reconfiguración, las bases de datos secundarias siguen siendo secundarias de la base de datos principal anterior.  
  
> [!IMPORTANT]  
>  El usuario que ejecuta el comando FORCE_FAILOVER_ALLOW_DATA_LOSS debe ser DBManager tanto en el servidor principal como en el secundario.  
  
## <a name="remarks"></a>Notas  

Para quitar una base de datos, use [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md).  
Para reducir el tamaño de una base de datos, use [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).  
  
La instrucción ALTER DATABASE se debe ejecutar en el modo de confirmación automática (modo de administración de transacciones predeterminado) y no se permite en una transacción explícita o implícita.  
  
Al borrar la memoria caché de planes, se provoca una nueva compilación de todos los planes de ejecución posteriores y puede ocasionar una disminución repentina y temporal del rendimiento de las consultas. Para cada almacén de caché borrado de la memoria caché de planes, el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contendrá el siguiente mensaje informativo: "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha detectado %d instancias de vaciado del almacén de caché '%s' (parte de la memoria caché de planes) debido a determinadas operaciones de mantenimiento de base de datos o reconfiguración". Este mensaje se registra cada cinco minutos siempre que se vacíe la memoria caché dentro de ese intervalo de tiempo.  
  
La memoria caché de procedimientos también se vacía en los escenarios siguientes:  
  
- Una base de datos tiene la opción de base de datos AUTO_CLOSE establecida en ON. Cuando ninguna conexión de usuario hace referencia a la base de datos ni la usa, la tarea de segundo plano intenta cerrar la base de datos y apagarla de modo automático.  
  
- Ejecuta varias consultas con una base de datos que tiene opciones predeterminadas. Después, la base de datos se quita.  
  
- Volvió a generar correctamente el registro de transacciones para una base de datos.  
  
- Restaura una copia de seguridad de una base de datos  
  
- Separa una base de datos.  
  
## <a name="viewing-database-information"></a>Ver la información de la base de datos  

Se pueden utilizar vistas de catálogo, funciones del sistema y procedimientos almacenados del sistema para devolver información sobre bases de datos, archivos y grupos de archivos.  
  
## <a name="permissions"></a>Permisos  

Solo el inicio de sesión principal de nivel de servidor (creado por el proceso de aprovisionamiento) o los miembros del rol de base de datos `dbmanager` pueden modificar una base de datos.  
  
> [!IMPORTANT]  
>  El propietario de la base de datos no puede modificarla a menos que sea miembro del rol `dbmanager`.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-check-the-edition-options-and-change-them"></a>A. Comprobación y cambio de las opciones de edición:

```sql
SELECT Edition = DATABASEPROPERTYEX('db1', 'EDITION'),
        ServiceObjective = DATABASEPROPERTYEX('db1', 'ServiceObjective'),
        MaxSizeInBytes =  DATABASEPROPERTYEX('db1', 'MaxSizeInBytes');

ALTER DATABASE [db1] MODIFY (EDITION = 'Premium', MAXSIZE = 1024 GB, SERVICE_OBJECTIVE = 'P15');
```

### <a name="b-moving-a-database-to-a-different-elastic-pool"></a>B. Movimiento de una base de datos a otro grupo elástico  

Mueve una base de datos existente en un grupo denominado pool1:  
  
```sql  
ALTER DATABASE db1   
MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = pool1 ) ) ;  
```  
  
### <a name="c-add-a-geo-replication-secondary"></a>C. Adición de una base de datos secundaria de replicación geográfica  

Crea una base de datos secundaria legible db1 en el servidor `secondaryserver` de db1 en el servidor local.  
  
```sql  
ALTER DATABASE db1   
ADD SECONDARY ON SERVER secondaryserver   
WITH ( ALLOW_CONNECTIONS = ALL )  
```  
  
### <a name="d-remove-a-geo-replication-secondary"></a>D. Eliminación de una base de datos secundaria de replicación geográfica  
 
Quita la base de datos secundaria db1 en el servidor `secondaryserver`.  
  
```sql  
ALTER DATABASE db1   
REMOVE SECONDARY ON SERVER testsecondaryserver   
```  
  
### <a name="e-failover-to-a-geo-replication-secondary"></a>E. Conmutación por error a una base de datos secundaria de replicación geográfica  

Promueve una base de datos secundaria db1 en el servidor `secondaryserver` para que se convierta en la nueva base de datos principal cuando se ejecute en el servidor `secondaryserver`.  
  
```sql  
ALTER DATABASE db1 FAILOVER  
```  
  
## <a name="see-also"></a>Vea también
  
[CREATE DATABASE - Azure SQL Database](../../t-sql/statements/create-database-azure-sql-database.md)   
 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)   
 [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [Bases de datos del sistema](../../relational-databases/databases/system-databases.md)  
  
  
