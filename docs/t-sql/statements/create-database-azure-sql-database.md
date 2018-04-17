---
title: CREATE DATABASE (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SERVICE_OBJECTIVE
- SERVICE_OBJECTIVE_TSQL
- ELASTIC_POOL
- ELASTIC_POOL_TSQL
- EDITION
- EDITION_TSQL
- MAXSIZE
- MAXSIZE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SERVICE_OBJECTIVE
- ELASTIC_POOL
- EDITION SQL Database
- MAXSIZE SQL Database
ms.assetid: 22b167f7-ae86-490b-adb3-ec02ca1c1508
caps.latest.revision: 62
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 646072361fe637daa24175742b36309252663cf4
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/05/2018
---
# <a name="create-database-azure-sql-database"></a>CREATE DATABASE (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Crea una nueva base de datos.  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

## <a name="syntax"></a>Sintaxis  

``` 
  
CREATE DATABASE database_name [ COLLATE collation_name ]  
{  
   (<edition_options> [, ...n]) 
}  

[ WITH CATALOG_COLLATION = { DATABASE_DEFAULT | SQL_Latin1_General_CP1_CI_AS }  ]
  
<edition_options> ::= 
{  

  MAXSIZE = { 100 MB | 250 MB | 500 MB | 1 … 1024 … 4096 GB }  
  | ( EDITION = {  'basic' | 'standard' | 'premium' | 'GeneralPurpose' | 'BusinessCritical' } 
  | SERVICE_OBJECTIVE = 
    {  'basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' | 
      | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15'  
      | 'GP_GEN4_1' | 'GP_GEN4_2' | 'GP_GEN4_4' | 'GP_GEN4_8' | 'GP_GEN4_16' 
      | 'BC_GEN4_1' | 'BC_GEN4_2' | 'BC_GEN4_4' | 'BC_GEN4_8' | 'BC_GEN4_16' | 
      | { ELASTIC_POOL(name = <elastic_pool_name>) } }  ) 
}  

 [;]  
  

```  

```
To copy a database:  
CREATE DATABASE database_name  
    AS COPY OF [source_server_name.] source_database_name  
    [ ( SERVICE_OBJECTIVE = 
      {  'basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' |  
        | 'P1' | 'P2' | 'P4'| 'P6' | 'P11' | 'P15'  
        | 'GP_GEN4_1' | 'GP_GEN4_2' | 'GP_GEN4_4' | 'GP_GEN4_8' | 'GP_GEN4_16' 
        | 'BC_GEN4_1' | 'BC_GEN4_2' | 'BC_GEN4_4' | 'BC_GEN4_8' | 'BC_GEN4_16' | 
        | { ELASTIC_POOL(name = <elastic_pool_name>) } } )  
  ]  
 [;] 
 
```  
  
## <a name="arguments"></a>Argumentos  
 Este diagrama de sintaxis muestra los argumentos admitidos en [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
*database_name* 
 
El nombre de la nueva base de datos. Este nombre debe ser único en el servidor SQL, que puede hospedar tanto bases de datos de [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] como de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], y cumplir con las reglas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para identificadores. Para obtener más información, consulte [Identificadores](http://go.microsoft.com/fwlink/p/?LinkId=180386).  
  
*Collation_name*  

Especifica la intercalación predeterminada de la base de datos. El nombre de intercalación puede ser un nombre de intercalación de Windows o un nombre de intercalación de SQL. Si no se especifica, a la base de datos se le asigna la intercalación predeterminada, que es SQL_Latin1_General_CP1_CI_AS.  
  
Para obtener más información sobre los nombres de intercalación de Windows y de SQL, consulte [COLLATE (Transact-SQL)](http://msdn.microsoft.com/library/ms184391.aspx).  
  
CATALOG_COLLATION  

Especifica la intercalación predeterminada del catálogo de metadatos. *DATABASE_DEFAULT* especifica que el catálogo de metadatos usado para las vistas y las tablas del sistema se intercalará para coincidir con la intercalación predeterminada de la base de datos.  Este es el comportamiento en SQL Server. 

*SQL_Latin1_General_CP1_CI_AS* especifica que el catálogo de metadatos usado para las tablas y vistas del sistema se intercalará en una intercalación fija SQL_Latin1_General_CP1_CI_AS.  Se trata de la configuración predeterminada en Azure SQL Database si no se especifica.

EDITION
 
Especifica el nivel de servicio de la base de datos. Los valores disponibles son: “basic”, “standard”, “premium”, “GeneralPurpose” y “BusinessCritical”. Se ha quitado la compatibilidad con "premiumrs". Si tiene preguntas, use este alias de correo electrónico: premium-rs@microsoft.com.
  
 Si se especifica EDITION, pero no MAXSIZE, este último se establece en el tamaño más restrictivo que admite la edición.  
  
 MAXSIZE

Especifica el tamaño máximo de la base de datos. El valor de MAXSIZE debe ser válido para el valor de EDITION (nivel de servicio) especificado A continuación se indican los valores de MAXSIZE admitidos y los valores predeterminados (D) de los niveles de servicio.

**Modelo basado en DTU**

|**MAXSIZE**|**Basic**|**S0-S2**|**S3-S12**|**P1-P6**| **P11-P15** | 
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
|300 GB|N/D|N/D|√|√|√|
|400 GB|N/D|N/D|√|√|√|
|500 GB|N/D|N/D|√|√ (D)|√|
|750 GB|N/D|N/D|√|√|√|
|1024 GB|N/D|N/D|√|√|√ (D)|
|Desde 1024 GB hasta 4096 GB en incrementos de 256 GB* |N/D|N/D|N/D|N/D|√|√|  
  
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
  
- Si se especifica EDITION pero no se especifica MAXSIZE, se usa el valor predeterminado de la edición. Por ejemplo, si EDITION está establecido en Standard y el valor de MAXSIZE no se especifica, este último se establece automáticamente en 250 MB.  
- Si no se especifican los valores de MAXSIZE ni EDITION, este último se establece en Standard (S0) y MAXSIZE en 250 GB.  

SERVICE_OBJECTIVE

Especifica el nivel de rendimiento. Los valores disponibles para el objetivo de servicio son: `S0`, `S1`, `S2`, `S3`, `S4`, `S6`, `S7`, `S9`, `S12`, `P1`, `P2`, `P4`, `P6`, `P11`, `P15`, `GP_GEN4_1`, `GP_GEN4_2`, `GP_GEN4_4`, `GP_GEN4_8`, `GP_GEN4_16`, `BC_GEN4_1` `BC_GEN4_2` `BC_GEN4_4` `BC_GEN4_8` `BC_GEN4_16`. 

Para obtener las descripciones de los objetivos de servicio y más información sobre las combinaciones de tamaño, ediciones y objetivos de servicio, vea [¿Qué son los niveles de servicio de Azure SQL Database?](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers). Si EDITION no admite el valor SERVICE_OBJECTIVE especificado, se devuelve un error. Para cambiar el valor SERVICE_OBJECTIVE de un nivel a otro (por ejemplo, de S1 a P1), también debe cambiar el valor EDITION. Para conocer las descripciones de los objetivos de servicio y obtener más información sobre las combinaciones de tamaño, ediciones y objetivos de servicio, consulte [Niveles de servicio y niveles de rendimiento de Azure SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/), [DTU-based resource limits](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits) (Límites de recursos basados en DTU) y [vCore-based resource limits](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits) (Límites de recursos basados en núcleo virtual).  Se ha quitado la compatibilidad para los objetivos de servicio de PRS. Si tiene preguntas, use este alias de correo electrónico: premium-rs@microsoft.com. 
  
ELASTIC_POOL (name = \<elastic_pool_name>)
 
Para crear una base de datos en un grupo de bases de datos elásticas, establezca el valor SERVICE_OBJECTIVE de la base de datos en ELASTIC_POOL e indique el nombre del grupo. Para obtener más información, consulte [Creación y administración de un grupo de bases de datos elásticas de SQL Database (versión preliminar)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/).  
  
AS COPY OF [source_server_name.]source_database_name

Para copiar una base de datos al mismo o a otro servidor de [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
*source_server_name*  

El nombre del servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)] donde está ubicada la base de datos de origen. Este parámetro es opcional cuando la base de datos de origen y la de destino van a estar ubicadas en el mismo servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
> [!NOTE]
> El argumento `AS COPY OF` no admite nombres de dominio únicos completos. En otras palabras, si el nombre de dominio completo del servidor es `serverName.database.windows.net`, utilice solo `serverName` durante la copia de la base de datos.  
  
*source_database_name*

El nombre de la base de datos que se va a copiar.  
  
[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] no admite los argumentos y las opciones siguientes cuando se usa la instrucción `CREATE DATABASE`:  
  
- Los parámetros relacionados con la ubicación física del archivo, como \<filespec> y \<filegroup>  
  
- Las opciones de acceso externo, como DB_CHAINING y TRUSTWORTHY  
  
- Adjuntar una base de datos  
  
- Las opciones de Service Broker, como ENABLE_BROKER, NEW_BROKER y ERROR_BROKER_CONVERSATIONS  
  
- Instantáneas de base de datos  
  
Para obtener más información acerca de los argumentos y de la instrucción `CREATE DATABASE`, vea [CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md).  
  
## <a name="remarks"></a>Notas
 
Las bases de datos de [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] tienen varios parámetros predeterminados que se establecen al crear la base de datos. Para obtener más información sobre estos parámetros predeterminados, consulte la lista de valores de [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md).  
  
MAXSIZE proporciona la capacidad de limitar el tamaño de la base de datos. Si el tamaño de la base de datos alcanza el valor MAXSIZE, se le mostrará el código de error 40544. Cuando esto sucede, no es posible insertar ni actualizar datos, ni tampoco crear nuevos objetos (como tablas, procedimientos almacenados, vistas y funciones). Sin embargo, todavía puede leer y eliminar datos, truncar tablas, quitar tablas e índices, y volver a generar índices. Seguidamente, puede actualizar MAXSIZE a un valor mayor que el tamaño actual de la base de datos o eliminar algunos datos para liberar espacio de almacenamiento. Puede haber un retraso de hasta quince minutos antes de que pueda insertar nuevos datos.  
  
> [!IMPORTANT]  
>  La instrucción `CREATE DATABASE` debe ser la única de un lote [!INCLUDE[tsql](../../includes/tsql-md.md)]. 
  
Para cambiar los valores de tamaño, edición u objetivo de servicio, use [ALTER DATABASE &#40;Azure SQL Database&#41;](../../t-sql/statements/alter-database-azure-sql-database.md).  

El argumento CATALOG_COLLATION solo está disponible durante la creación de la base de datos. 
  
## <a name="database-copies"></a>Copias de la base de datos  

La copia de una base de datos mediante la instrucción `CREATE DATABASE` es una operación asincrónica. Por tanto, no es necesaria una conexión con el servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)] durante todo el proceso de copia. La instrucción `CREATE DATABASE` devuelve el control al usuario una vez que se crea la entrada en sys.databases, pero antes de que se complete la operación de copia de la base de datos. Es decir, la instrucción `CREATE DATABASE` vuelve correctamente cuando la copia de la base de datos aún está en curso.  
  
- Supervisar el proceso de copia en un servidor de [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]: consulte las columnas `percentage_complete` o `replication_state_desc` en [dm_database_copies](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md) o la columna `state` en la vista **sys.databases**. También se puede usar la vista [sys.dm_operation_status](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md), ya que devuelve el estado de las operaciones de la base de datos, incluida la copia de esta.  
  
Cuando se completa correctamente el proceso de copia, la base de datos de destino es transaccionalmente coherente con la base de datos de origen.  
  
Se aplican las siguientes reglas semánticas y de sintaxis al uso del argumento `AS COPY OF`:  
  
- El nombre del servidor de origen y el nombre del servidor del destino de la copia pueden ser iguales o diferentes. Si son iguales, este parámetro es opcional y se usa el contexto de servidor de la sesión actual de forma predeterminada.  
  
- Los nombres de las bases de datos de origen y de destino deben especificarse, ser únicos y ajustarse a las reglas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para los identificadores. Para obtener más información, consulte [Identificadores](http://go.microsoft.com/fwlink/p/?LinkId=180386).  
  
- La instrucción `CREATE DATABASE` debe ejecutarse dentro del contexto de la base de datos maestra del servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)] donde se creará la nueva base de datos. 
- Una vez finalizada la copia, la base de datos de destino debe administrarse como una base de datos independiente. Puede ejecutar las instrucciones `ALTER DATABASE` y `DROP DATABASE` en la nueva base de datos de forma independiente de la base de datos de origen. También puede copiar la nueva base de datos en otra base de datos nueva.  
  
- Se puede seguir teniendo acceso a la base de datos de origen mientras la copia de la base de datos está en curso.  
  
 Para obtener más información, consulte [Crear una copia de una base de datos de SQL Azure mediante Transact-SQL](https://azure.microsoft.com/documentation/articles/sql-database-copy-transact-sql/).  
  
## <a name="permissions"></a>Permisos  
 Para crear una base de datos, el inicio de sesión debe ser uno de los siguientes:  
  
- El inicio de sesión de entidad de seguridad a nivel de servidor  
  
- El administrador de Azure AD para el Azure SQL Server local  
  
- El inicio de sesión de un miembro del rol de base de datos `dbmanager`  
  
 **Requisitos adicionales para usar la sintaxis `CREATE DATABASE ... AS COPY OF`:** el inicio de sesión que ejecute la instrucción en el servidor local debe tener también al menos el rol de `db_owner` en el servidor de origen. Si el inicio de sesión se basa en la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el inicio de sesión que ejecute la instrucción en el servidor local debe tener un inicio de sesión correspondiente en el servidor de origen de [!INCLUDE[ssSDS](../../includes/sssds-md.md)], con un nombre y una contraseña idénticos.  
  
## <a name="examples"></a>Ejemplos  
Para ver un tutorial de inicio rápido en el que se muestra cómo conectarse a una base de datos de Azure SQL usando SQL Server Management Studio, consulte [Azure SQL Database: use SQL Server Management Studio para conectarse a los datos y realizar consultas en ellos](/azure/sql-database/sql-database-connect-query-ssms).  
  
### <a name="simple-example"></a>Ejemplo sencillo  
 Un ejemplo sencillo para crear una base de datos.  
  
```sql  
CREATE DATABASE TestDB1;  
```  
  
### <a name="simple-example-with-edition"></a>Ejemplo sencillo con Edition  
 Un ejemplo sencillo para crear una base de datos estándar.  
  
```sql  
CREATE DATABASE TestDB2  
( EDITION = 'standard' );  
```  
  
### <a name="example-with-additional-options"></a>Ejemplo con opciones adicionales  
 Un ejemplo en el que se usan varias opciones.  
  
```sql  
CREATE DATABASE hito 
COLLATE Japanese_Bushu_Kakusu_100_CS_AS_KS_WS 
( MAXSIZE = 500 MB, EDITION = 'standard', SERVICE_OBJECTIVE = 'S1' ) ;  
```  
  
### <a name="creating-a-copy"></a>Crear una copia  
 Un ejemplo en el que se crea una copia de una base de datos.  
  
```sql  
CREATE DATABASE escuela 
AS COPY OF school;  
```  
  
### <a name="creating-a-database-in-an-elastic-pool"></a>Crear una base de datos en un grupo elástico  
 Crea una nueva base de datos en un grupo denominado S3M100:  
  
```sql  
CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = S3M100 ) ) ;  
```  
  
### <a name="creating-a-copy-of-a-database-on-another-server"></a>Crear una copia de una base de datos en otro servidor  
 En el siguiente ejemplo se crea una copia de la base de datos db_original, denominada db_copy, en el nivel de rendimiento P2 para una única base de datos.  Esto es válido independientemente de si db_original está en un grupo elástico o un nivel de rendimiento para una única base de datos.  
  
```sql  
CREATE DATABASE db_copy 
  AS COPY OF ozabzw7545.db_original ( SERVICE_OBJECTIVE = 'P2' )  ;  
```  
  
 En el siguiente ejemplo se crea una copia de la base de datos db_original, denominada db_copy, en un grupo elástico llamado ep1.  Esto es válido independientemente de si db_original está en un grupo elástico o un nivel de rendimiento para una única base de datos.  Si db_original está en un grupo elástico con un nombre distinto, db_copy se sigue creando en ep1.  
  
```sql  
CREATE DATABASE db_copy 
  AS COPY OF ozabzw7545.db_original 
  (SERVICE_OBJECTIVE = ELASTIC_POOL( name = ep1 ) ) ;  
```  

### <a name="create-database-with-specified-catalog-collation-value"></a>Crear una base de datos con un valor de intercalación de catálogo especificado

En el siguiente ejemplo se establece la intercalación de catálogo en DATABASE_DEFAULT durante la creación de la base de datos, lo que establece la intercalación de catálogo como la misma que la intercalación de base de datos.

```sql
CREATE DATABASE TestDB3 COLLATE Japanese_XJIS_140  (MAXSIZE = 100 MB, EDITION = ‘basic’)  
  WITH CATALOG_COLLATION = DATABASE_DEFAULT 
```
  
## <a name="see-also"></a>Vea también  

-  [sys.dm_database_copies &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)

- [ALTER DATABASE &#40;Azure SQL Database&#41;](alter-database-azure-sql-database.md) 
  
  

