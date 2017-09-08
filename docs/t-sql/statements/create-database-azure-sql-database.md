---
title: Crear base de datos (base de datos SQL Azure) | Documentos de Microsoft
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 08/28/2017
ms.prod: 
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fe808df2a3d0f55ab00946db2bd86aa8d9fb3511
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-database-azure-sql-database"></a>CREATE DATABASE (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Crea una nueva base de datos.  
  
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
    | ( EDITION = {  'basic' | 'standard' | 'premium' | 'premiumrs'}   
    | SERVICE_OBJECTIVE =   
          {  'basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' | 
            | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15'  
            | 'PRS1' | 'PRS2' | 'PRS4' | 'PRS6' 
            | { ELASTIC_POOL(name = <elastic_pool_name>) } }  ) 
}  

[ AS COPY OF [source_server_name.]source_database_name ]

 [;]  
  

```  

```
To copy a database:  
CREATE DATABASE database_name  
    AS COPY OF [source_server_name.] source_database_name  
    [ ( SERVICE_OBJECTIVE =   
          {  'basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' |  
            | 'P1' | 'P2' | 'P4'| 'P6' | 'P11' | 'P15'  
            | 'PRS1' | 'PRS2' | 'PRS4' | 'PRS6' 
            | { ELASTIC_POOL(name = <elastic_pool_name>) } } )  
    ]  
 [;] 
 
```  
  
## <a name="arguments"></a>Argumentos  
 Este diagrama de sintaxis muestra los argumentos admitidos en [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 *database_name*  
 El nombre de la nueva base de datos. Este nombre debe ser único en el servidor SQL, que puede hospedar ambos [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] bases de datos y [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] bases de datos y cumplir con la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reglas de los identificadores. Para obtener más información, consulte [identificadores](http://go.microsoft.com/fwlink/p/?LinkId=180386).  
  
 *Collation_name*  
 Especifica la intercalación predeterminada de la base de datos. El nombre de intercalación puede ser un nombre de intercalación de Windows o un nombre de intercalación de SQL. Si no se especifica, a la base de datos se le asigna la intercalación predeterminada, que es SQL_Latin1_General_CP1_CI_AS.  
  
 Para obtener más información acerca de los nombres de intercalación de Windows y SQL, [COLLATE (Transact-SQL)](http://msdn.microsoft.com/library/ms184391.aspx).  
  
 *CATALOG_COLLATION*  
Especifica la intercalación predeterminada para el catálogo de metadatos. *DATABASE_DEFAULT* especifica que el catálogo de metadatos se usa para vistas del sistema y las tablas del sistema se intercalan para que coincida con la intercalación predeterminada de la base de datos.  Éste es el comportamiento en SQL Server. 

*SQL_Latin1_General_CP1_CI_AS* especifica que el catálogo de metadatos se usa para tablas y vistas del sistema se intercalan a una intercalación SQL_Latin1_General_CP1_CI_AS fija.  Se trata de la configuración predeterminada en la base de datos de SQL Azure si no se especifica.

 *EDICIÓN*  
 Especifica el nivel de servicio de la base de datos. Los valores disponibles son: 'basic', 'standard', 'premium' y 'premiumrs'.  
  
 Cuando se especifica EDITION pero no se especifica MAXSIZE, MAXSIZE se establece en el tamaño más restrictivo que admita la edición.  
  
 *MAXSIZE*  
 Especifica el tamaño máximo de la base de datos. El valor de MAXSIZE debe ser válido para el valor de EDITION (nivel de servicio) especificado A continuación se indican los valores de MAXSIZE admitidos y los valores predeterminados (D) de los niveles de servicio.  
  
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
|De 1024 GB hasta 4096 GB en incrementos de 256 GB * |N/D|N/D|N/D|N/D|√|√|  
  
 \*P11 y P15 permiten MAXSIZE hasta 4 TB con 1024 GB que el tamaño predeterminado.  P11 y P15 pueden utilizar hasta 4 TB de almacenamiento incluyen sin cargo adicional. En el nivel Premium, MAXSIZE mayor de 1 TB está actualmente disponible en las siguientes regiones: nos East2, oeste de Estados Unidos, nos Gov Virginia, Europa occidental, Alemania Central, sur Asia oriental, este de Japón, Australia Oriental, Canadá Central y este de Canadá. Para las limitaciones actuales, vea [solo las bases de datos](https://docs.microsoft.com/azure/sql-database-single-database-resources).  
  
 Las reglas siguientes se aplican a los argumentos MAXSIZE y EDITION:  
  
-   El valor de MAXSIZE, si se especifica, tiene que ser un valor válido mostrado en la tabla anterior.  
  
-   Si se especifica EDITION pero no se especifica MAXSIZE, se usa el valor predeterminado de la edición. Por ejemplo, si se establece la edición estándar y no se especifica el valor de MAXSIZE, MAXSIZE se establece automáticamente a 250 MB.  
  
-   Si se especifica MAXSIZE ni EDITION, EDITION se establece en estándar (S0) y MAXSIZE está establecido en 250 GB.  
  
 SERVICE_OBJECTIVE  
 Especifica el nivel de rendimiento. Para obtener más información sobre el tamaño, las ediciones y las combinaciones de objetivos de servicio y descripciones de objetivo de servicio, consulte [niveles de servicio de base de datos de SQL Azure y los niveles de rendimiento](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/) y [recursos de base de datos SQL límites de](https://azure.microsoft.com/documentation/articles/sql-database-resource-limits). Si EDITION no admite el valor SERVICE_OBJECTIVE especificado, se devuelve un error.  
  
 ELASTIC_POOL (nombre = \<elastic_pool_name >) para crear una nueva base de datos en un grupo de bases de datos elásticas, establezca el SERVICE_OBJECTIVE de la base de datos en ELASTIC_POOL y proporcione el nombre del grupo. Para obtener más información, consulte [crear y administrar un grupo de base de datos elástica de base de datos SQL (vista previa)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/).  
  
 *COMO COPY OF [source_server_name.] nombre_de_base_de_datos_de_origen*  
 Para copiar una base de datos al mismo o a otro servidor de [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 *source_server_name*  
 El nombre del servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)] donde está ubicada la base de datos de origen. Este parámetro es opcional cuando la base de datos de origen y la de destino van a estar ubicadas en el mismo servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Nota: El argumento `AS COPY OF` no admite nombres de dominio únicos completos. En otras palabras, si el nombre de dominio completo del servidor es `serverName.database.windows.net`, utilice solo `serverName` durante la copia de la base de datos.  
  
 *nombre_de_base_de_datos_de_origen*  
 El nombre de la base de datos que se va a copiar.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]no admite los siguientes argumentos y opciones cuando se usa el `CREATE DATABASE` instrucción:  
  
-   Los parámetros relacionados con la ubicación física del archivo, como \<filespec > y \<grupo de archivos >  
  
-   Las opciones de acceso externo, como DB_CHAINING y TRUSTWORTHY  
  
-   Adjuntar una base de datos  
  
-   Las opciones de Service Broker, como ENABLE_BROKER, NEW_BROKER y ERROR_BROKER_CONVERSATIONS  
  
-   Instantáneas de base de datos  
  
 Para obtener más información acerca de los argumentos y la `CREATE DATABASE` instrucción, consulte [CREATE DATABASE &#40; Transact-SQL de SQL Server &#41; ](../../t-sql/statements/create-database-sql-server-transact-sql.md).  
  
## <a name="remarks"></a>Comentarios  
 Las bases de datos de [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] tienen varios parámetros predeterminados que se establecen al crear la base de datos. Para obtener más información acerca de estos valores predeterminados, consulte la lista de valores en [DATABASEPROPERTYEX &#40; Transact-SQL &#41; ](../../t-sql/functions/databasepropertyex-transact-sql.md).  
  
 MAXSIZE proporciona la capacidad de limitar el tamaño de la base de datos. Si el tamaño de la base de datos alcanza el valor de MAXSIZE, recibirá un código de error 40544. Cuando esto sucede, no es posible insertar ni actualizar datos, ni tampoco crear nuevos objetos (como tablas, procedimientos almacenados, vistas y funciones). Sin embargo, todavía puede leer y eliminar datos, truncar tablas, quitar tablas e índices, y volver a generar índices. Seguidamente, puede actualizar MAXSIZE a un valor mayor que el tamaño actual de la base de datos o eliminar algunos datos para liberar espacio de almacenamiento. Puede haber un retraso de hasta quince minutos antes de que pueda insertar nuevos datos.  
  
> [!IMPORTANT]  
>  La instrucción `CREATE DATABASE` debe ser la única de un lote [!INCLUDE[tsql](../../includes/tsql-md.md)]. 
  
 Para cambiar el tamaño, edición o valores de objetivos de servicio más adelante, utilice [ALTER DATABASE &#40; Base de datos SQL Azure &#41; ](../../t-sql/statements/alter-database-azure-sql-database.md).  

El argumento CATALOG_COLLATION solo está disponible durante la creación de la base de datos. 
  
## <a name="database-copies"></a>Copias de la base de datos  
 Copia de una base de datos mediante el `CREATE DATABASE` instrucción es una operación asincrónica. Por tanto, no es necesaria una conexión con el servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)] durante todo el proceso de copia. El `CREATE DATABASE` instrucción devuelve el control al usuario después de crea la entrada en sys.databases pero antes de la copia de la base de datos es completa la operación. Es decir, la instrucción `CREATE DATABASE` vuelve correctamente cuando la copia de la base de datos aún está en curso.  
  
-   Supervisar el proceso de copia en un [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] server: consulta el `percentage_complete` o `replication_state_desc` columnas en el [dm_database_copies](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md) o `state` columna en el **sys.databases** vista. El [sys.dm_operation_status](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md) vista se puede utilizar también devuelve el estado de copia de la base de datos de operaciones de base de datos.  
  
 Cuando se completa correctamente el proceso de copia, la base de datos de destino es transaccionalmente coherente con la base de datos de origen.  
  
 Se aplican las siguientes reglas semánticas y de sintaxis al uso del argumento `AS COPY OF`:  
  
-   El nombre del servidor de origen y el nombre del servidor del destino de la copia pueden ser iguales o diferentes. Cuando son iguales, este parámetro es opcional y el contexto de servidor de la sesión actual se utiliza de forma predeterminada.  
  
-   Los nombres de las bases de datos de origen y de destino deben especificarse, ser únicos y ajustarse a las reglas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para los identificadores. Para obtener más información, consulte [identificadores](http://go.microsoft.com/fwlink/p/?LinkId=180386).  
  
-   La instrucción `CREATE DATABASE` debe ejecutarse dentro del contexto de la base de datos maestra del servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)] donde se creará la nueva base de datos.  
  
-   Una vez finalizada la copia, la base de datos de destino debe administrarse como una base de datos independiente. Puede ejecutar las instrucciones `ALTER DATABASE` y `DROP DATABASE` en la nueva base de datos de forma independiente de la base de datos de origen. También puede copiar la nueva base de datos en otra base de datos nueva.  
  
-   Se puede seguir teniendo acceso a la base de datos de origen mientras la copia de la base de datos está en curso.  
  
 Para obtener más información, consulte [crear una copia de una base de datos de SQL Azure mediante Transact-SQL](https://azure.microsoft.com/documentation/articles/sql-database-copy-transact-sql/).  
  
## <a name="permissions"></a>Permissions  
 Para crear un inicio de sesión de una base de datos debe ser uno de los siguientes:  
  
-   El inicio de sesión de entidad de seguridad de nivel de servidor  
  
-   El Administrador de Azure AD para el servidor local de SQL Azure  
  
-   Un inicio de sesión que sea miembro de la `dbmanager` rol de base de datos  
  
 **Requisitos adicionales para usar `CREATE DATABASE ... AS COPY OF` sintaxis:** el inicio de sesión que se ejecuta la instrucción en el servidor local también debe ser al menos el `db_owner` en el servidor de origen. Si el inicio de sesión se basa en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación, el inicio de sesión que se ejecuta la instrucción en el servidor local debe tener un inicio de sesión correspondiente en el origen de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] server, con un nombre idéntico y una contraseña.  
  
## <a name="examples"></a>Ejemplos  
Para obtener un tutorial de inicio rápido que muestra cómo conectarse a una base de datos de SQL Azure con SQL Server Management Studio, consulte [base de datos de SQL Azure: usar SQL Server Management Studio para conectarse y consultar datos](/azure/sql-database/sql-database-connect-query-ssms).  
  
### <a name="simple-example"></a>Ejemplo sencillo  
 Un ejemplo sencillo para crear una base de datos.  
  
```tsql  
CREATE DATABASE TestDB1;  
```  
  
### <a name="simple-example-with-edition"></a>Ejemplo sencillo con edición  
 Un ejemplo sencillo para crear una base de datos estándar.  
  
```tsql  
CREATE DATABASE TestDB2  
( EDITION = 'standard' );  
```  
  
### <a name="example-with-additional-options"></a>Ejemplo con opciones adicionales  
 Un ejemplo de cómo utilizar varias opciones.  
  
```tsql  
CREATE DATABASE hito   
COLLATE Japanese_Bushu_Kakusu_100_CS_AS_KS_WS   
( MAXSIZE = 500 MB, EDITION = 'standard', SERVICE_OBJECTIVE = 'S1' ) ;  
```  
  
### <a name="creating-a-copy"></a>Crear una copia  
 Un ejemplo de creación de una copia de una base de datos.  
  
```tsql  
CREATE DATABASE escuela   
AS COPY OF school;  
```  
  
### <a name="creating-a-database-in-an-elastic-pool"></a>Crear una base de datos en un grupo elástico  
 Crea la base de datos en el grupo llamado S3M100:  
  
```tsql  
CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = S3M100 ) ) ;  
```  
  
### <a name="creating-a-copy-of-a-database-on-another-server"></a>Crear una copia de una base de datos en otro servidor  
 En el ejemplo siguiente se crea una copia de la base de datos db_original denominado db_copy en el nivel de rendimiento P2 para una sola base de datos.  Esto es cierto independientemente de si db_original está en un grupo elástico o un nivel de rendimiento de una sola base de datos.  
  
```tsql  
CREATE DATABASE db_copy   
    AS COPY OF ozabzw7545.db_original ( SERVICE_OBJECTIVE = 'P2' )  ;  
```  
  
 En el ejemplo siguiente se crea una copia de la base de datos db_original denominado db_copy en un grupo elástico denominado ep1.  Esto es cierto independientemente de si db_original está en un grupo elástico o un nivel de rendimiento de una sola base de datos.  Si db_original está en un grupo elástico con un nombre diferente, db_copy todavía se crea en ep1.  
  
```tsql  
CREATE DATABASE db_copy   
    AS COPY OF ozabzw7545.db_original   
    (SERVICE_OBJECTIVE = ELASTIC_POOL( name = ep1 ) ) ;  
```  

### <a name="create-database-with-specified-catalog-collation-value"></a>Crear base de datos con el valor de intercalación de catálogo especificado

En el ejemplo siguiente se establece la intercalación del catálogo en DATABASE_DEFAULT durante la creación de la base de datos, que establece la intercalación de catálogo que se va a ser la misma que la intercalación de base de datos.

```tsql
CREATE DATABASE TestDB3 COLLATE Japanese_XJIS_140  (MAXSIZE = 100 MB, EDITION = ‘basic’)  
      WITH CATALOG_COLLATION = DATABASE_DEFAULT 
```
  
## <a name="see-also"></a>Vea también  

-  [Sys.dm_database_copies &#40; Base de datos SQL Azure &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)

-   [ALTER DATABASE &#40; Base de datos SQL Azure &#41;](https://msdn.microsoft.com/library/mt574871.aspx)   
    
  


