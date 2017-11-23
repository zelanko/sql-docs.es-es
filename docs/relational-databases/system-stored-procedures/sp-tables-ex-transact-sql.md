---
title: sp_tables_ex (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_tables_ex
- sp_tables_ex_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_tables_ex
ms.assetid: 33755c33-7e1e-4ef7-af14-a9cebb1e2ed4
caps.latest.revision: "33"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6e30848a44d0d3ba7b1bce23d7e330ae69d7a891
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sptablesex-transact-sql"></a>sp_tables_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información de tabla acerca de las tablas del servidor vinculado especificado.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_tables_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]  
     [ , [ @table_catalog = ] 'table_catalog' ]   
     [ , [ @table_type = ] 'table_type' ]   
     [ , [@fUsePattern = ] 'fUsePattern' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@table_server=** ] **'***table_server***'**  
 Es el nombre del servidor vinculado para el que se devuelve información de tabla. *table_server* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **,** [  **@table_name=** ] **'***table_name***'**]  
 Es el nombre de la tabla vinculado para la que se devuelve información de tipo de datos. *table_name*es **sysname**, su valor predeterminado es null.  
  
 [  **@table_schema=** ] **'***table_schema***'**]  
 Es el esquema de la tabla. *TABLE_SCHEMA*es **sysname**, su valor predeterminado es null.  
  
 [  **@table_catalog=** ] **'***table_catalog***'**  
 Es el nombre de la base de datos en el que el especificado *table_name* reside. *TABLE_CATALOG* es **sysname**, su valor predeterminado es null.  
  
 [  **@table_type=** ] **'***table_type***'**  
 Es el tipo de la tabla que se va a devolver. *TABLE_TYPE* es **sysname**, su valor predeterminado es null y puede tener uno de los siguientes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**ALIAS**|Nombre de un alias.|  
|**TEMPORAL GLOBAL**|Nombre de una tabla temporal disponible en todo el sistema.|  
|**TEMPORAL LOCAL**|Nombre de una tabla temporal disponible solo para el trabajo actual.|  
|**SYNONYM**|Nombre de un sinónimo.|  
|**TABLA DEL SISTEMA**|Nombre de una tabla del sistema.|  
|**VISTA DEL SISTEMA**|Nombre de una vista del sistema.|  
|**TABLE**|Nombre de una tabla de usuario.|  
|**VIEW**|Nombre de una vista.|  
  
 [  **@fUsePattern=** ] **'***fUsePattern***'**  
 Determina si los caracteres **_**,  **%** , **[**, y **]** se interpretan como caracteres comodín. Los valores válidos son 0 (coincidencia de patrón desactivada) y 1 (coincidencia de patrón activada). *fUsePattern* es **bits**, su valor predeterminado es 1.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 Ninguno  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|Nombre del calificador de tabla. Varios productos DBMS admiten nombres de tres partes para tablas (*calificador***.** *propietario***.** *nombre*). En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta columna representa el nombre de la base de datos. En otros productos, representa el nombre del servidor del entorno de base de datos de la tabla. Este campo puede ser NULL.|  
|**SEGÚN TABLE_SCHEM**|**sysname**|Nombre de propietario de la tabla. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta columna representa el nombre de usuario de base de datos que creó la tabla. Este campo siempre devuelve un valor.|  
|**TABLE_NAME**|**sysname**|Nombre de la tabla. Este campo siempre devuelve un valor.|  
|**TABLE_TYPE**|**varchar (32)**|Tabla, tabla del sistema o vista.|  
|**COMENTARIOS**|**varchar(254)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no devuelve ningún valor para esta columna.|  
  
## <a name="remarks"></a>Comentarios  
 **sp_tables_ex** se ejecuta al consultar el conjunto de filas TABLES de la **IDBSchemaRowset** interfaz del proveedor OLE DB correspondiente a *table_server*. El *table_name*, *table_schema*, *table_catalog*, y *columna* parámetros se pasan a esta interfaz para restringir las filas Devuelve.  
  
 **sp_tables_ex** devuelve un resultado vacío establecer si el proveedor OLE DB del servidor vinculado especificado no es compatible con el conjunto de filas TABLES de la **IDBSchemaRowset** interfaz.  
  
## <a name="permissions"></a>Permissions  
 Es necesario contar con un permiso de tipo SELECT sobre el esquema.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se devuelve información sobre las tablas contenidas en el esquema `HumanResources` de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] del servidor vinculado `LONDON2`.  
  
```  
EXEC sp_tables_ex @table_server = 'LONDON2',   
@table_catalog = 'AdventureWorks2012',   
@table_schema = 'HumanResources',   
@table_type = 'TABLE';  
```  
  
## <a name="see-also"></a>Vea también  
 [Las consultas distribuidas almacenan procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_catalogs &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_columns_ex &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-columns-ex-transact-sql.md)   
 [sp_column_privileges &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_foreignkeys &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_indexes &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_table_privileges &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
