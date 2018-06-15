---
title: sp_tables (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_tables
- sp_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_tables
ms.assetid: 787a2fa5-87a1-49bd-938b-6043c245f46b
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b0a4e8b4ae1b78da17beb1a5289a90782979ad3c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33260015"
---
# <a name="sptables-transact-sql"></a>sp_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una lista de objetos que se pueden consultar en el entorno actual. Esto significa cualquier tabla o vista, excepto los objetos sinónimos.  
  
> [!NOTE]  
>  Para determinar el nombre del objeto de base de un sinónimo, consulte el [sys.synonyms](../../relational-databases/system-catalog-views/sys-synonyms-transact-sql.md) vista de catálogo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_tables [ [ @table_name = ] 'name' ]   
     [ , [ @table_owner = ] 'owner' ]   
     [ , [ @table_qualifier = ] 'qualifier' ]   
     [ , [ @table_type = ] "type" ]   
     [ , [@fUsePattern = ] 'fUsePattern'];  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@table_name=** ] **'***nombre***'**  
 Es la tabla que se usa para devolver información de catálogo. *nombre* es **nvarchar (384)**, su valor predeterminado es null. Se admite la coincidencia de patrón de caracteres comodín.  
  
 [  **@table_owner=** ] **'***propietario***'**  
 Es el propietario de la tabla de la tabla utilizada para devolver información del catálogo. *propietario* es **nvarchar (384)**, su valor predeterminado es null. Se admite la coincidencia de patrón de caracteres comodín. Si no se especifica el propietario, se aplican las reglas de visibilidad de tabla predeterminadas del DBMS subyacente.  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si el usuario actual posee una tabla en la que se especifica el nombre, se devuelven las columnas de esa tabla. Si no se especifica el propietario y el usuario actual no es el propietario de una tabla con el nombre especificado, este procedimiento busca una tabla con el nombre especificado que pertenezca al propietario de la base de datos. Si existe una, se devuelven las columnas de esa tabla.  
  
 [  **@table_qualifier=** ] **'***calificador***'**  
 Es el nombre del calificador de tabla. *calificador de* es **sysname**, su valor predeterminado es null. Varios productos DBMS admiten nombres de tres partes para tablas (*calificador ***.*** propietario ***.*** nombre*). En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta columna representa el nombre de la base de datos. En algunos productos, representa el nombre del servidor del entorno de base de datos de la tabla.  
  
 [ **,** [  **@table_type=** ] **"'***tipo***'**, **'** tipo **'"** ]  
 Es una lista de los valores, separados por comas, que proporcionan información acerca de todas las tablas de los tipos especificados. Puede tratarse de **tabla**, **SYSTEMTABLE**, y **vista**. *tipo de* es **varchar (100)**, su valor predeterminado es null.  
  
> [!NOTE]  
>  Cada tipo de tabla debe especificarse entre comillas simples y todo el parámetro debe especificarse entre comillas dobles. Los tipos de tabla deben especificarse en mayúsculas. Si SET QUOTED_IDENTIFIER está establecido en ON (activado), las comillas simples deben ser comillas dobles y todo el parámetro debe especificarse entre comillas simples.  
  
 [  **@fUsePattern =** ] **'***fUsePattern***'**  
 Determina si los caracteres de subrayado ( _ ), porcentaje ( % ) y paréntesis ( [ o ] ) se interpretan como caracteres comodín. Los valores válidos son 0 (coincidencia de patrón desactivada) y 1 (coincidencia de patrón activada). *fUsePattern* es **bits**, su valor predeterminado es 1.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_QUALIFIER**|**sysname**|Nombre del calificador de tabla. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta columna representa el nombre de la base de datos. Este campo puede ser NULL.|  
|**TABLE_OWNER**|**sysname**|Nombre de propietario de la tabla. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta columna representa el nombre de usuario de base de datos que creó la tabla. Este campo siempre devuelve un valor.|  
|**TABLE_NAME**|**sysname**|Nombre de la tabla. Este campo siempre devuelve un valor.|  
|**TABLE_TYPE**|**varchar (32)**|Tabla, tabla del sistema o vista.|  
|**COMENTARIOS**|**varchar(254)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no devuelve ningún valor para esta columna.|  
  
## <a name="remarks"></a>Comentarios  
 Para obtener la máxima interoperatividad, el cliente de la puerta de enlace solo debe dar por supuesta la concordancia del patrón estándar de SQL-92 (los caracteres comodín % y _).  
  
 No siempre se comprueba la información de privilegios acerca del acceso de lectura o de escritura del usuario actual para una tabla específica. Por lo tanto, el acceso no está garantizado. Este conjunto de resultados no solo incluye tablas y vistas, sino también sinónimos y alias para las puertas de enlace a productos DBMS que admiten dichos tipos. Si el atributo de servidor **ACCESSIBLE_TABLES** es Y en el conjunto de resultados **sp_server_info**, se devuelven únicamente las tablas que se pueden tener acceso el usuario actual.  
  
 **sp_tables** es equivalente a **SQLTables** en ODBC. Los resultados devueltos se ordenan por **TABLE_TYPE**, **TABLE_QUALIFIER**, **TABLE_OWNER**, y **TABLE_NAME**.  
  
## <a name="permissions"></a>Permissions  
 Es necesario contar con un permiso de tipo SELECT sobre el esquema.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-a-list-of-objects-that-can-be-queried-in-the-current-environment"></a>A. Devolver una lista de objetos que se pueden consultar en el entorno actual  
 En el siguiente ejemplo se devuelve una lista de objetos que pueden ser consultas en el entorno actual.  
  
```  
EXEC sp_tables ;  
```  
  
### <a name="b-returning-information-about-the-tables-in-a-specified-schema"></a>B. Devolver información sobre las tablas en un esquema especificado  
 En el siguiente ejemplo se devuelve información sobre las tablas que pertenecen al esquema `Person` de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_tables   
   @table_name = '%',  
   @table_owner = 'Person',  
   @table_qualifier = 'AdventureWorks2012';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-returning-a-list-of-objects-that-can-be-queried-in-the-current-environment"></a>C. Devolver una lista de objetos que se pueden consultar en el entorno actual  
 En el siguiente ejemplo se devuelve una lista de objetos que pueden ser consultas en el entorno actual.  
  
```  
EXEC sp_tables ;  
```  
  
### <a name="d-returning-information-about-the-tables-in-a-specified-schema"></a>D. Devolver información sobre las tablas en un esquema especificado  
 En el ejemplo siguiente se devuelve información acerca de las tablas de dimensiones en el `AdventureWorksPDW201` base de datos.  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_tables   
   @table_name = 'Dim%',  
   @table_owner = 'dbo',  
   @table_qualifier = 'AdventureWorksPDW2012';  
```  
  
## <a name="see-also"></a>Vea también  
 [Sys.SYNONYMS &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-synonyms-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

