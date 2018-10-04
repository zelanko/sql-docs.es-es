---
title: sp_table_privileges (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_table_privileges
- sp_table_privileges_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_table_privileges
ms.assetid: 0512e688-4fc0-4557-8dc8-016672c1e3fe
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dcc3d02505a1bd568d440d5b70fc06bcfff93ae9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47815753"
---
# <a name="sptableprivileges-transact-sql"></a>sp_table_privileges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una lista de permisos de tabla (como INSERT, DELETE, UPDATE, SELECT o REFERENCES) para la tabla o las tablas especificadas.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_table_privileges [ @table_name = ] 'table_name'     
     [ , [ @table_owner = ] 'table_owner' ]   
     [ , [ @table_qualifier = ] 'table_qualifier' ]   
     [ , [ @fUsePattern = ] 'fUsePattern' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @table_name=] '*table_name*'  
 Es la tabla que se usa para devolver información de catálogo. *table_name* es **nvarchar (** 384 **)**, no tiene ningún valor predeterminado. Se admite la coincidencia de patrón de caracteres comodín.  
  
 [ @table_owner=] '*table_owner*'  
 Es el propietario de la tabla de la tabla utilizada para devolver información del catálogo. *TABLE_OWNER*es **nvarchar (** 384 **)**, su valor predeterminado es null. Se admite la coincidencia de patrón de caracteres comodín. Si no se especifica el propietario, se aplican las reglas de visibilidad de tabla predeterminadas del DBMS subyacente.  
  
 Si el usuario actual posee una tabla con el nombre especificado, se devuelven las columnas de dicha tabla. Si *propietario* no se especifica y el usuario actual no posee una tabla con los valores especificados *nombre*, este procedimiento busca una tabla con los valores especificados *table_name* que pertenecen a la propietario de la base de datos. Si existe una, se devuelven las columnas de esa tabla.  
  
 [ @table_qualifier=] '*table_qualifier*'  
 Es el nombre del calificador de tabla. *TABLE_QUALIFIER* es **sysname**, su valor predeterminado es null. Varios productos DBMS admiten nombres de tres partes para tablas (*qualifier.owner.name*). En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta columna representa el nombre de la base de datos. En algunos productos, representa el nombre del servidor del entorno de base de datos de la tabla.  
  
 [ @fUsePattern=] '*fUsePattern*'  
 Determina si el carácter de subrayado (_), porcentaje (%) y entre corchetes ([o]) caracteres se interpretan como caracteres comodín. Los valores válidos son 0 (coincidencia de patrón desactivada) y 1 (coincidencia de patrón activada). *fUsePattern* es **bit**, su valor predeterminado es 1.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|TABLE_QUALIFIER|**sysname**|Nombre del calificador de tabla. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta columna representa el nombre de la base de datos. Este campo puede ser NULL.|  
|TABLE_OWNER|**sysname**|Nombre de propietario de la tabla. Este campo siempre devuelve un valor.|  
|TABLE_NAME|**sysname**|Nombre de la tabla. Este campo siempre devuelve un valor.|  
|GRANTOR|**sysname**|Nombre del usuario de la base de datos que ha concedido permisos para TABLE_NAME al GRANTEE que aparece. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta columna es siempre la misma que en TABLE_OWNER. Este campo siempre devuelve un valor. Asimismo, la columna GRANTOR podría ser el propietario de la base de datos (TABLE_OWNER) o un usuario al que el propietario de la base de datos haya concedido permiso mediante la cláusula WITH GRANT OPTION en la instrucción GRANT.|  
|GRANTEE|**sysname**|Nombre del usuario de la base de datos al que GRANTOR ha concedido permisos sobre TABLE_NAME. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta columna incluye siempre un usuario de base de datos de la vista sys.database_principalssystem. Este campo siempre devuelve un valor.|  
|PRIVILEGE|**sysname**|Uno de los permisos de tabla disponibles. Los permisos de tabla pueden ser uno de los valores siguientes (u otros valores que el origen de datos admita al definirse la implementación):<br /><br /> SELECT = GRANTEE puede recuperar datos para una o varias columnas.<br /><br /> INSERT = GRANTEE puede proporcionar datos para nuevas filas de una o más de las columnas.<br /><br /> UPDATE = GRANTEE puede modificar datos existentes de una o más de las columnas.<br /><br /> DELETE = GRANTEE puede quitar filas de la tabla.<br /><br /> REFERENCES = GRANTEE puede hacer referencia a una columna de una tabla externa en una relación entre clave principal y clave externa. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], las relaciones entre clave principal y clave externa se definen con restricciones de tabla.<br /><br /> El ámbito de acción dado a GRANTEE por un privilegio de tabla específico depende del origen de datos. Por ejemplo, el privilegio UPDATE podría permitir que GRANTEE actualizara todas las columnas de una tabla en un origen de datos y solo aquellas columnas para las que GRANTOR tiene el privilegio UPDATE en otro origen de datos.|  
|IS_GRANTABLE|**sysname**|Indica si se permite que GRANTEE conceda permisos a otros usuarios (que a menudo se conoce como el permiso “conceder por concesión”). Puede ser YES, NO o NULL. Un valor desconocido (o NULL) hace referencia a un origen de datos para el que "conceder por concesión" no se aplica.|  
  
## <a name="remarks"></a>Comentarios  
 El procedimiento almacenado sp_table_privileges es equivalente a SQLTablePrivileges en ODBC. Los resultados devueltos se ordenan por TABLE_QUALIFIER, TABLE_OWNER, TABLE_NAME y PRIVILEGE.  
  
## <a name="permissions"></a>Permisos  
 Es necesario contar con un permiso de tipo SELECT sobre el esquema.  
  
## <a name="examples"></a>Ejemplos  
 El siguiente ejemplo devuelve información de privilegios de todas las tablas cuyos nombres comiencen por la palabra `Contact`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_table_privileges   
   @table_name = 'Contact%';  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
