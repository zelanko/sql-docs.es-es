---
title: sp_statistics (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_statistics_TSQL
- sp_statistics
dev_langs: TSQL
helpviewer_keywords: sp_statistics
ms.assetid: 0bb6495f-258a-47ec-9f74-fd16671d23b8
caps.latest.revision: "32"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: acb1e775a99bb3c296064a65aa9eed7be5d17745
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spstatistics-transact-sql"></a>sp_statistics (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una lista de todos los índices y estadísticas de una vista indizada o tabla especificada.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_statistics [ @table_name = ] 'table_name'    
     [ , [ @table_owner = ] 'owner' ]   
     [ , [ @table_qualifier = ] 'qualifier' ]   
     [ , [ @index_name = ] 'index_name' ]   
     [ , [ @is_unique = ] 'is_unique' ]  
     [ , [ @accuracy = ] 'accuracy' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@table_name=** ] **'***table_name***'**  
 Especifica la tabla que se usa para devolver información de catálogo. *table_name* es **sysname**, no tiene ningún valor predeterminado. No se admite la coincidencia de patrón de caracteres comodín.  
  
 [  **@table_owner=** ] **'***propietario***'**  
 Es el nombre del propietario de la tabla de la tabla utilizada para devolver información del catálogo. *TABLE_OWNER* es **sysname**, su valor predeterminado es null. No se admite la coincidencia de patrón de caracteres comodín. Si *propietario* no se especifica, se aplican las reglas de visibilidad de tabla predeterminadas del DBMS subyacente.  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si el usuario actual es propietario de una tabla en la que se especifica el nombre, se devuelven los índices de esa tabla. Si *propietario* no se especifica y el usuario actual no posee una tabla con los valores especificados *nombre*, este procedimiento busca una tabla con los valores especificados *nombre* pertenecen a la propietario de la base de datos. Si existe una, se devuelven los índices de esa tabla.  
  
 [  **@table_qualifier=** ] **'***calificador***'**  
 Es el nombre del calificador de tabla. *calificador de* es **sysname**, su valor predeterminado es null. Varios productos DBMS admiten nombres de tres partes para tablas (*calificador***.** *propietario***.** *nombre*). En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], este parámetro representa el nombre de la base de datos. En algunos productos, representa el nombre del servidor del entorno de base de datos de la tabla.  
  
 [  **@index_name=** ] **'***index_name***'**  
 Es el nombre del índice. *index_name* es **sysname**, su valor predeterminado es %. Se admite la coincidencia de patrón de caracteres comodín.  
  
 [  **@is_unique=** ] **'***is_unique***'**  
 Es si solo los índices únicos (si **Y**) se devuelven. *is_unique* es **char (1)**, su valor predeterminado es **N**.  
  
 [  **@accuracy=** ] **'***precisión***'**  
 Es el nivel de cardinalidad y la precisión de página de las estadísticas. *precisión* es **char (1)**, su valor predeterminado es **preguntas**. Especifique **E** para asegurarse de que las estadísticas se actualizan para que la cardinalidad y las páginas son precisas.  
  
 El valor **E** (SQL_ENSURE) pide al controlador que recupere incondicionalmente las estadísticas.  
  
 El valor **preguntas** (SQL_QUICK) pide al controlador que recupere la cardinalidad y las páginas solo si están siempre disponibles desde el servidor. En este caso, el controlador no garantiza que los valores sean actuales. Las aplicaciones que están escritas en el estándar Open Group siempre adoptarán el comportamiento de SQL_QUICK de los controladores compatibles con ODBC 3x.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_QUALIFIER**|**sysname**|Nombre del calificador de tabla. Esta columna puede ser NULL.|  
|**TABLE_OWNER**|**sysname**|Nombre de propietario de la tabla. Esta columna siempre devuelve un valor.|  
|**TABLE_NAME**|**sysname**|Nombre de la tabla. Esta columna siempre devuelve un valor.|  
|**NON_UNIQUE**|**smallint**|NOT NULL.<br /><br /> 0 = Único<br /><br /> 1 = No único|  
|**INDEX_QUALIFIER**|**sysname**|Nombre de propietario del índice. Algunos productos DBMS permiten crear índices a usuarios que no sean los propietarios de la tabla. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta columna siempre es el mismo que **TABLE_NAME**.|  
|**INDEX_NAME**|**sysname**|Es el nombre del índice. Esta columna siempre devuelve un valor.|  
|**TYPE**|**smallint**|Esta columna siempre devuelve un valor:<br /><br /> 0 = Estadísticas de una tabla<br /><br /> 1 = Clúster<br /><br /> 2 = Hash<br /><br /> 3 = no clúster|  
|**SEQ_IN_INDEX**|**smallint**|Posición de la columna dentro del índice.|  
|**COLUMN_NAME**|**sysname**|Nombre de columna para cada columna de la **TABLE_NAME** devuelto. Esta columna siempre devuelve un valor.|  
|**INTERCALACIÓN**|**Char (1)**|Orden utilizado en la intercalación. Puede ser:<br /><br /> A = Ascendente<br /><br /> D = Descendente<br /><br /> NULL = No aplicable|  
|**CARDINALIDAD**|**int**|Número de filas de la tabla o valores únicos del índice.|  
|**PÁGINAS**|**int**|Número de páginas para el almacenamiento del índice o tabla.|  
|**FILTER_CONDITION**|**varchar (128)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no devuelve ningún valor.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 Ninguno  
  
## <a name="remarks"></a>Comentarios  
 Los índices en el conjunto de resultados aparecen en orden ascendente por las columnas **NON_UNIQUE**, **tipo**, **INDEX_NAME**, y **SEQ_IN_INDEX**.  
  
 El tipo de índice clúster hace referencia a un índice en el que los datos de la tabla se almacenan en el orden del índice. Esto corresponde a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] índices agrupados.  
  
 El tipo de índice en hash acepta búsquedas de coincidencia exacta o de intervalos, pero las búsquedas de coincidencia de patrón no utilizan el índice.  
  
 **sp_statistics** es equivalente a **SQLStatistics** en ODBC. Los resultados devueltos se ordenan por **NON_UNIQUE**, **tipo**, **INDEX_QUALIFIER**, **INDEX_NAME**, y **SEQ_IN_ ÍNDICE**. Para obtener más información, consulte el [referencia de la API de ODBC](http://go.microsoft.com/fwlink/?LinkId=68323).  
  
## <a name="permissions"></a>Permissions  
 Es necesario contar con un permiso de tipo SELECT sobre el esquema.  
  
## <a name="example-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplo: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 En el ejemplo siguiente se devuelve información sobre la `DimEmployee` tabla.  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_statistics DimEmployee;  
```  
  
## <a name="see-also"></a>Vea también  
 [Catálogo de procedimientos almacenados &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

