---
title: sp_columns_ex (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_columns_ex
- sp_columns_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_columns_ex
ms.assetid: c12ef6df-58c6-4391-bbbf-683ea874bd81
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: aaf644b6a8795e9c68e0053eaed0023c4b9299b6
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/18/2018
ms.locfileid: "53588409"
---
# <a name="spcolumnsex-transact-sql"></a>sp_columns_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve la información de la columna, una fila por columna, de las tablas del servidor vinculado especificado. **sp_columns_ex** devuelve información de solo la columna específica si *columna* se especifica.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_columns_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]   
     [ , [ @column_name = ] 'column' ]   
     [ , [ @ODBCVer = ] 'ODBCVer' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@table_server =** ] **'**_table_server_**'**  
 Es el nombre del servidor vinculado del que se devuelve información de columnas. *table_server* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@table_name =** ] **'**_table_name_**'**  
 Es el nombre de la tabla para la que se devuelve información de columnas. *table_name* es **sysname**, su valor predeterminado es null.  
  
 [  **@table_schema =** ] **'**_table_schema_**'**  
 Es el nombre del esquema de la tabla para la que se devuelve información de columnas. *TABLE_SCHEMA* es **sysname**, su valor predeterminado es null.  
  
 [  **@table_catalog =** ] **'**_table_catalog_**'**  
 Es el nombre del catálogo de la tabla para la que se devuelve información de columnas. *TABLE_CATALOG* es **sysname**, su valor predeterminado es null.  
  
 [  **@column_name =** ] **'**_columna_**'**  
 Se trata del nombre de la columna de la base de datos cuya información se va a proporcionar. *columna* es **sysname**, su valor predeterminado es null.  
  
 [  **@ODBCVer =** ] **'**_ODBCVer_**'**  
 Es la versión de ODBC que se está usando. *ODBCVer* es **int**, con el valor predeterminado es 2. Esto indica ODBC Versión 2. Los valores válidos son 2 ó 3. Para obtener información acerca de las diferencias de comportamiento entre las versiones 2 y 3, vea la especificación ODBC SQLColumns.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|Nombre del calificador de la tabla o vista. Varios productos DBMS admiten nombres de tres partes para tablas (_calificador_**.** _propietario_**.** _nombre_). En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esta columna representa el nombre de base de datos. En algunos productos, representa el nombre del servidor del entorno de base de datos de la tabla. Este campo puede ser NULL.|  
|**SEGÚN TABLE_SCHEM**|**sysname**|Nombre del propietario de la tabla o vista. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta columna representa el nombre del usuario de la base de datos que creó la tabla. Este campo siempre devuelve un valor.|  
|**TABLE_NAME**|**sysname**|Nombre de la tabla o vista. Este campo siempre devuelve un valor.|  
|**COLUMN_NAME**|**sysname**|Nombre de columna para cada columna de la **TABLE_NAME** devuelto. Este campo siempre devuelve un valor.|  
|**DATA_TYPE**|**smallint**|Valor de tipo entero correspondiente a indicadores de tipo ODBC. Si se trata de un tipo de datos que no se puede asignar a un tipo de ODBC, el valor es NULL. Se devuelve el nombre de tipo de datos nativos en el **TYPE_NAME** columna.|  
|**TYPE_NAME**|**varchar (** 13 **)**|Cadena que representa un tipo de datos. El DBMS subyacente presenta este nombre del tipo de datos.|  
|**COLUMN_SIZE**|**int**|Número de dígitos significativos. El valor devuelto para la **precisión** columna es en base 10.|  
|**BUFFER_LENGTH**|**int**|Tamaño de transferencia de los datos.1|  
|**DECIMAL_DIGITS**|**smallint**|Número de dígitos a la derecha del separador decimal.|  
|**NUM_PREC_RADIX**|**smallint**|Base para los tipos de datos numéricos.|  
|**QUE ACEPTA VALORES NULL**|**smallint**|Especifica la nulabilidad.<br /><br /> 1 = Se admiten valores NULL.<br /><br /> 0 = No se admiten valores NULL.|  
|**COMENTARIOS**|**varchar (** 254 **)**|Este campo siempre devuelve NULL.|  
|**COLUMN_DEF**|**varchar (** 254 **)**|Valor predeterminado de la columna.|  
|**SQL_DATA_TYPE**|**smallint**|Valor del tipo de datos SQL tal como aparece en el campo TYPE del descriptor. Esta columna es el mismo que el **DATA_TYPE** columna, excepto para el **datetime** y SQL-92 **intervalo** tipos de datos. Esta columna siempre devuelve un valor.|  
|**SQL_DATETIME_SUB**|**smallint**|Código de subtipo para **datetime** y SQL-92 **intervalo** tipos de datos. Para otros tipos de datos, esta columna devuelve NULL.|  
|**CHAR_OCTET_LENGTH**|**int**|Longitud máxima en bytes de una columna de tipos de datos de caracteres o enteros. Para los demás tipos de datos, esta columna devuelve NULL.|  
|**ORDINAL_POSITION**|**int**|Posición ordinal de la columna en la tabla. La primera columna de la tabla es 1. Esta columna siempre devuelve un valor.|  
|**IS_NULLABLE**|**varchar (** 254 **)**|Nulabilidad de la columna de la tabla. Se siguen las normas ISO para determinar la nulabilidad. Un DBMS que cumpla la norma ISO SQL no puede devolver una cadena vacía.<br /><br /> YES = La columna puede incluir valores NULL.<br /><br /> NO = La columna no puede incluir valores NULL.<br /><br /> Esta columna devuelve una cadena de longitud cero si no se conoce la nulabilidad.<br /><br /> Devuelve el valor de esta columna es diferente del valor devuelto para la **NULLABLE** columna.|  
|**SS_DATA_TYPE**|**tinyint**|Tipo de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizado por los procedimientos almacenados extendidos.|  
  
 Para obtener más información, vea la documentación de Microsoft ODBC.  
  
## <a name="remarks"></a>Comentarios  
 **sp_columns_ex** se ejecuta al consultar el conjunto de filas COLUMNS de la **IDBSchemaRowset** interfaz del proveedor OLE DB correspondiente a *table_server*. El *table_name*, *table_schema*, *table_catalog*, y *columna* los parámetros se pasan a esta interfaz para restringir las filas Devuelve.  
  
 **sp_columns_ex** devuelve un resultado vacío se establece si el proveedor OLE DB del servidor vinculado especificado no es compatible con el conjunto de filas COLUMNS de la **IDBSchemaRowset** interfaz.  
  
## <a name="permissions"></a>Permisos  
 Es necesario contar con un permiso de tipo SELECT sobre el esquema.  
  
## <a name="remarks"></a>Comentarios  
 **sp_columns_ex** cumple los requisitos para los identificadores delimitados. Para obtener más información, vea [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
## <a name="examples"></a>Ejemplos  
 El siguiente ejemplo devuelve el tipo de datos de la columna `JobTitle` de la tabla `HumanResources.Employee` en la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] del servidor vinculado `Seattle1`.  
  
```  
EXEC sp_columns_ex 'Seattle1',   
   'Employee',   
   'HumanResources',   
   'AdventureWorks2012',   
   'JobTitle';  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_foreignkeys &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_primarykeys &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [sp_tables_ex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
