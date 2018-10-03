---
title: sp_column_privileges_ex (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_column_privileges_ex
- sp_column_privileges_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_column_privileges_ex
ms.assetid: 98cb6e58-4007-40fc-b048-449fb2e7e6be
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f9f86f83637cbf71dd128dd262ad1621b2d58270
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47658672"
---
# <a name="spcolumnprivilegesex-transact-sql"></a>sp_column_privileges_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve privilegios de columna para la tabla especificada del servidor vinculado indicado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_column_privileges_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@table_server =** ] **'***table_server***'**  
 Es el nombre del servidor vinculado para el que se devuelve información. *table_server* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@table_name =** ] **'***table_name***'**  
 Es el nombre de la tabla que contiene la columna especificada. *table_name* es **sysname**, su valor predeterminado es null.  
  
 [  **@table_schema =** ] **'***table_schema***'**  
 Es el esquema de la tabla. *TABLE_SCHEMA* es **sysname**, su valor predeterminado es null.  
  
 [  **@table_catalog =** ] **'***table_catalog***'**  
 Es el nombre de la base de datos en el que el especificado *table_name* reside. *TABLE_CATALOG* es **sysname**, su valor predeterminado es null.  
  
 [  **@column_name =** ] **'***column_name***'**  
 Es el nombre de la columna para la que se va a proporcionar información acerca de los privilegios. *column_name* es **sysname**, su valor predeterminado es null (común para todos).  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 En la siguiente tabla se muestran las columnas del conjunto de resultados. Los resultados devueltos se ordenan por **TABLE_QUALIFIER**, **TABLE_OWNER**, **TABLE_NAME**, **COLUMN_NAME**, y  **PRIVILEGIO**.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|Nombre del calificador de tabla. Varios productos DBMS admiten nombres de tres partes para tablas (*calificador ***.*** propietario ***.*** nombre*). En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta columna representa el nombre de la base de datos. En algunos productos, representa el nombre del servidor del entorno de base de datos de la tabla. Este campo puede ser NULL.|  
|**SEGÚN TABLE_SCHEM**|**sysname**|Nombre de propietario de la tabla. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta columna representa el nombre del usuario de base de datos que creó la tabla. Este campo siempre devuelve un valor.|  
|**TABLE_NAME**|**sysname**|Nombre de la tabla. Este campo siempre devuelve un valor.|  
|**COLUMN_NAME**|**sysname**|Nombre de columna para cada columna de la **TABLE_NAME** devuelto. Este campo siempre devuelve un valor.|  
|**OTORGANTE DE PERMISOS**|**sysname**|Nombre de usuario de base de datos que ha concedido permisos **COLUMN_NAME** al **receptor**. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta columna siempre es el mismo que el **TABLE_OWNER**. Este campo siempre devuelve un valor.<br /><br /> El **otorgante de permisos** columna puede ser el propietario de la base de datos (**TABLE_OWNER**) o un usuario a los que el propietario de la base de datos concedido permisos mediante la cláusula WITH GRANT OPTION en la instrucción GRANT.|  
|**RECEPTOR DE PERMISOS**|**sysname**|Nombre de usuario de base de datos que se ha concedido permisos sobre este **COLUMN_NAME** por la lista **otorgante de permisos**. Este campo siempre devuelve un valor.|  
|**PRIVILEGIO**|**varchar (** 32 **)**|Uno de los permisos de columna disponibles. Los permisos de columna pueden ser uno de los valores siguientes (u otros valores compatibles con el origen de datos cuando se define la implementación):<br /><br /> Seleccione = **receptor** puede recuperar datos de las columnas.<br /><br /> INSERT = **receptor** puede proporcionar datos para esta columna cuando se inserten nuevas filas (por el **receptor**) en la tabla.<br /><br /> UPDATE = **receptor** puede modificar datos existentes en la columna.<br /><br /> REFERENCIAS = **receptor** puede hacer referencia a una columna de una tabla externa en una relación de clave principal/clave externa. Las relaciones entre clave principal y clave externa se definen con restricciones de tabla.|  
|**IS_GRANTABLE**|**varchar (** 3 **)**|Indica si el **receptor** tiene permiso para conceder permisos a otros usuarios (a menudo denominados permiso "conceder por concesión"). Puede ser YES, NO o NULL. Un valor desconocido, o NULL, hace referencia a un origen de datos en el que no se aplica “conceder por concesión”.|  
  
## <a name="permissions"></a>Permisos  
 Es necesario contar con un permiso de tipo SELECT sobre el esquema.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se devuelve información de privilegios de columna de la tabla `HumanResources.Department` de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] del servidor vinculado `Seattle1`.  
  
```  
EXEC sp_column_privileges_ex @table_server = 'Seattle1',   
   @table_name = 'Department',   
   @table_schema = 'HumanResources',  
   @table_catalog ='AdventureWorks2012';  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_table_privileges_ex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-ex-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
