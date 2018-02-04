---
title: sp_special_columns_100 (almacenamiento de datos SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5774fadc-77cc-46f8-8f9f-a0f9efe95e21
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 64aafbee1cae4cbdf8a2d43c7367fdbae6e40b27
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="spspecialcolumns100-sql-data-warehouse"></a>sp_special_columns_100 (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Devuelve el conjunto óptimo de columnas que identifican de forma única a una fila de la tabla. También devuelve las columnas actualizadas automáticamente cuando una transacción actualiza cualquier valor de la fila.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_special_columns_100 [ @table_name = ] 'table_name'     
     [ , [ @table_owner = ] 'table_owner' ]   
     [ , [ @qualifier = ] 'qualifier' ]   
     [ , [ @col_type = ] 'col_type' ]   
     [ , [ @scope = ] 'scope' ]  
     [ , [ @nullable = ] 'nullable' ]   
     [ , [ @ODBCVer = ] 'ODBCVer' ]   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @table_name=] '*table_name*'  
 Es el nombre de la tabla que se utiliza para devolver información de catálogo. *nombre* es **sysname**, no tiene ningún valor predeterminado. No se admite la coincidencia de patrón de caracteres comodín.  
  
 [ @table_owner=] '*table_owner*'  
 Es el propietario de la tabla de la tabla utilizada para devolver información del catálogo. *propietario* es **sysname**, su valor predeterminado es null. No se admite la coincidencia de patrón de caracteres comodín. Si *propietario* no se especifica, se aplican las reglas de visibilidad de tabla predeterminadas del DBMS subyacente.  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si el usuario actual posee una tabla en la que se especifica el nombre, se devuelven las columnas de esa tabla. Si *propietario* no se especifica y el usuario actual no posee una tabla del elemento especificado *nombre*, este procedimiento busca una tabla del elemento especificado *nombre* pertenecen a la base de datos propietario. Si la tabla existe, se devuelven sus columnas.  
  
 [ @qualifier=] '*calificador*'  
 Es el nombre del calificador de tabla. *calificador de* es **sysname**, su valor predeterminado es null. Varios productos DBMS admiten nombres de tres partes para tablas (*qualifier.owner.name*). En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta columna representa el nombre de la base de datos. En algunos productos, representa el nombre del servidor del entorno de base de datos de la tabla.  
  
 [ @col_type=] '*col_type*'  
 Es el tipo de columna. *Col_type* es **char (**1**)**, su valor predeterminado es R. tipo R devuelve la columna óptima o el conjunto de columnas que, al recuperar valores de la columna o columnas, permite que cualquier fila de la manera especificada tabla para identificarse de forma exclusiva. Una columna puede ser una pseudocolumna diseñada específicamente para este propósito o bien la columna o columnas de cualquier índice único de la tabla. El tipo V devuelve la columna o columnas de la tabla especificada (en su caso) que el origen de datos actualiza automáticamente cuando una transacción actualiza cualquier valor de la fila.  
  
 [ @scope=] '*ámbito*'  
 Es el ámbito mínimo necesario del ROWID. *ámbito* es **char (**1**)**, su valor predeterminado es T. el ámbito C especifica que el ROWID es válido solo cuando se coloca en esa fila. El ámbito T especifica que el ROWID es válido para la transacción.  
  
 [ @nullable=] '*que aceptan valores NULL*'  
 Indica si las columnas especiales pueden o no aceptar un valor NULL. *que aceptan valores NULL* es **char (**1**)**, su valor predeterminado es U. o especifica columnas especiales que no permiten valores null. U especifica columnas que admiten parcialmente valores NULL.  
  
 [ @ODBCVer=] '*ODBCVer*'  
 Es la versión de ODBC utilizada. *ODBCVer* es **int (**4**)**, su valor predeterminado es 2. Esto indica ODBC versión 2.0. Para obtener más información acerca de las diferencias entre ODBC versión 2.0 y ODBC versión 3.0, consulte la especificación SQLSpecialColumns para ODBC versión 3.0.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|SCOPE|**smallint**|Ámbito real del identificador de fila. Puede ser 0, 1 o 2. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]siempre devuelve 0. Este campo siempre devuelve un valor.<br /><br /> 0 = SQL_SCOPE_CURROW. Se garantiza que el Id. de fila es válido solo mientras esté colocado en esa fila. Una nueva selección posterior mediante el Id. de fila podría no devolver una fila si otra transacción ha actualizado o eliminado la fila.<br /><br /> 1 = SQL_SCOPE_TRANSACTION. Se garantiza que el Id. de fila es válido mientras dura la transacción actual.<br /><br /> 2 = SQL_SCOPE_SESSION. Se garantiza que el identificador de fila sea válido mientras dure la sesión (en los límites de la transacción).|  
|COLUMN_NAME|**sysname**|Nombre de columna para cada columna de la *tabla*devuelto. Este campo siempre devuelve un valor.|  
|DATA_TYPE|**smallint**|Tipo de datos de ODBC SQL.|  
|TYPE_NAME|**sysname**|Nombre de tipo de datos dependiente del origen de datos; Por ejemplo, **char**, **varchar**, **dinero**, o **texto**.|  
|PRECISION|**Int**|Precisión de la columna en el origen de datos. Este campo siempre devuelve un valor.|  
|LENGTH|**Int**|Longitud, en bytes, necesaria para el tipo de datos en su formato binario en el origen de datos, por ejemplo, 10 para **char (**10**)**, 4 para **entero**y 2 para **smallint** .|  
|SCALE|**smallint**|Escala de la columna en el origen de datos. NULL se devuelve para los tipos de datos a los que no se aplica la escala.|  
|PSEUDO_COLUMN|**smallint**|Indica si la columna es una pseudocolumna. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siempre devuelve 1:<br /><br /> 0 = SQL_PC_UNKNOWN<br /><br /> 1 = SQL_PC_NOT_PSEUDO<br /><br /> 2 = SQL_PC_PSEUDO|  
  
## <a name="remarks"></a>Comentarios  
 sp_special_columns es equivalente a SQLSpecialColumns en ODBC. Los resultados devueltos se ordenan por medio de SCOPE.  
  
## <a name="permissions"></a>Permissions  
 Es necesario contar con un permiso de tipo SELECT sobre el esquema.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 En el siguiente ejemplo se devuelve información acerca de la columna que identifica de forma exclusiva las filas en la tabla `FactFinance`.  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_special_columns_100 @table_name = 'FactFinance';  
```  
  
## <a name="see-also"></a>Vea también  
 [Los procedimientos almacenados de almacenamiento de datos SQL](../../relational-databases/system-stored-procedures/sql-data-warehouse-stored-procedures.md)  
  
  

