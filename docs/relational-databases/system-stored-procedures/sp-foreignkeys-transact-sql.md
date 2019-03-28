---
title: sp_foreignkeys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_foreignkeys_TSQL
- sp_foreignkeys
dev_langs:
- TSQL
helpviewer_keywords:
- sp_foreignkeys
ms.assetid: 935fe385-19ff-41a4-8d0b-30618966991d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: af2441fadc30254871a5d74209d645fc93a99456
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533828"
---
# <a name="spforeignkeys-transact-sql"></a>sp_foreignkeys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve las claves externas que hacen referencia a las claves principales de la tabla en el servidor vinculado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_foreignkeys [ @table_server = ] 'table_server'   
     [ , [ @pktab_name = ] 'pktab_name' ]   
     [ , [ @pktab_schema = ] 'pktab_schema' ]   
     [ , [ @pktab_catalog = ] 'pktab_catalog' ]   
     [ , [ @fktab_name = ] 'fktab_name' ]   
     [ , [ @fktab_schema = ] 'fktab_schema' ]   
     [ , [ @fktab_catalog = ] 'fktab_catalog' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @table_server = ] 'table_server'` Es el nombre del servidor vinculado que se va a devolver información de la tabla. *table_server* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @pktab_name = ] 'pktab_name'` Es el nombre de la tabla con una clave principal. *pktab_name* es **sysname**, su valor predeterminado es null.  
  
`[ @pktab_schema = ] 'pktab_schema'` Es el nombre del esquema con una clave principal. *pktab_schema*es **sysname**, su valor predeterminado es null. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], contiene el nombre del propietario.  
  
`[ @pktab_catalog = ] 'pktab_catalog'` Es el nombre del catálogo con una clave principal. *pktab_catalog*es **sysname**, su valor predeterminado es null. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], contiene el nombre de la base de datos.  
  
`[ @fktab_name = ] 'fktab_name'` Es el nombre de la tabla con una clave externa. *fktab_name*es **sysname**, su valor predeterminado es null.  
  
`[ @fktab_schema = ] 'fktab_schema'` Es el nombre del esquema con una clave externa. *fktab_schema*es **sysname**, su valor predeterminado es null.  
  
`[ @fktab_catalog = ] 'fktab_catalog'` Es el nombre del catálogo con una clave externa. *fktab_catalog*es **sysname**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Varios productos DBMS admiten nombres de tres partes para tablas (_catálogo_**.** _esquema_**.** _tabla_), que se representa en el conjunto de resultados.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**PKTABLE_CAT**|**sysname**|Catálogo de la tabla en que reside la clave principal.|  
|**PKTABLE_SCHEM**|**sysname**|Esquema de la tabla en que reside la clave principal.|  
|**PKTABLE_NAME**|**sysname**|Nombre de la tabla (con la clave principal). Este campo siempre devuelve un valor.|  
|**PKCOLUMN_NAME**|**sysname**|Nombre de la columna de clave principal o columnas, para cada columna de la **TABLE_NAME** devuelto. Este campo siempre devuelve un valor.|  
|**FKTABLE_CAT**|**sysname**|Catálogo de la tabla en que reside la clave externa.|  
|**FKTABLE_SCHEM**|**sysname**|Esquema de la tabla en que reside la clave externa.|  
|**FKTABLE_NAME**|**sysname**|Nombre de la tabla (con una clave externa). Este campo siempre devuelve un valor.|  
|**FKCOLUMN_NAME**|**sysname**|Nombre de las columnas de clave externa por cada columna de TABLE_NAME devuelta. Este campo siempre devuelve un valor.|  
|**KEY_SEQ**|**smallint**|Número de secuencia de la columna en una clave principal con varias columnas. Este campo siempre devuelve un valor.|  
|**UPDATE_RULE**|**smallint**|Acción aplicada a la clave externa si la operación de SQL es una actualización. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve 0, 1 o 2 para estas columnas:<br /><br /> 0=CASCADE cambia a clave externa.<br /><br /> 1=NO ACTION cambia si la clave externa está presente.<br /><br /> 2=SET_NULL; establece la clave externa como NULL.|  
|**DELETE_RULE**|**smallint**|Acción aplicada a la clave externa si la operación de SQL es una eliminación. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve 0, 1 o 2 para estas columnas:<br /><br /> 0=CASCADE cambia a clave externa.<br /><br /> 1=NO ACTION cambia si la clave externa está presente.<br /><br /> 2=SET_NULL; establece la clave externa como NULL.|  
|**FK_NAME**|**sysname**|Identificador de la clave externa. Es NULL si no es aplicable al origen de datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve el nombre de la restricción FOREIGN KEY.|  
|**PK_NAME**|**sysname**|Identificador de la clave principal. Es NULL si no es aplicable al origen de datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve el nombre de la restricción PRIMARY KEY.|  
|**APLAZAMIENTO NO**|**smallint**|Indica si se puede diferir la comprobación de restricciones.|  
  
 En el conjunto de resultados, las columnas FK_NAME y PK_NAME siempre devuelven NULL.  
  
## <a name="remarks"></a>Comentarios  
 **sp_foreignkeys** consulta el conjunto de filas FOREIGN_KEYS de la **IDBSchemaRowset** interfaz del proveedor OLE DB que corresponde a *table_server*. El *table_name*, *table_schema*, *table_catalog*, y *columna* los parámetros se pasan a esta interfaz para restringir las filas Devuelve.  
  
## <a name="permissions"></a>Permisos  
 Es necesario contar con un permiso de tipo SELECT sobre el esquema.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se devuelve información de clave externa acerca de la tabla `Department` de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] del servidor vinculado `Seattle1`.  
  
```  
EXEC sp_foreignkeys @table_server = N'Seattle1',   
   @pktab_name = N'Department',   
   @pktab_catalog = N'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_column_privileges &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_primarykeys &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [sp_tables_ex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
