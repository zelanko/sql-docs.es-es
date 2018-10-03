---
title: sp_depends (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_depends
- sp_depends_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_depends
ms.assetid: d9934590-c6ae-4936-91c3-146055ef2c57
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f20945b6c4dc8fc1dda398c3dc9e721ff8b44d07
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47724643"
---
# <a name="spdepends-transact-sql"></a>sp_depends (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra información acerca de las dependencias de los objetos de la base de datos, tales como las vistas y procedimientos que dependen de una tabla o de una vista, y las tablas y vistas de las que depende la vista o el procedimiento. Las referencias a objetos que no se encuentran en la base de datos actual no se notifican.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [sys.dm_sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md) y [sys.dm_sql_referenced_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md) en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_depends [ @objname = ] '<object>'   
  
<object> ::=  
{  
    [ database_name. [ schema_name ] . | schema_name.  
    object_name  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Es el nombre de la base de datos.  
  
 *schema_name*  
 Es el nombre del esquema al que pertenece el objeto.  
  
 *object_name*  
 Es el objeto de base de datos cuyas dependencias se van a examinar. El objeto puede ser una tabla, una vista, un procedimiento almacenado, una función definida por el usuario o un desencadenador. o*bject_name* es **nvarchar(776)**, no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **sp_depends** muestra dos conjuntos de resultados.  
  
 El siguiente conjunto de resultados muestra los objetos que  *\<objeto >* depende.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Nombre**|**nvarchar (257** **)**|Nombre del elemento que tiene una dependencia.|  
|**Tipo**|**nvarchar(16)**|Tipo del elemento.|  
|**actualizado**|**nvarchar (7)**|Indica si el elemento está actualizado.|  
|**seleccionado**|**nvarchar (8)**|Indica si el elemento se utiliza en una instrucción SELECT.|  
|**column**|**sysname**|Columna o parámetro con el que existe la dependencia.|  
  
 El siguiente conjunto de resultados muestra los objetos que dependen de  *\<objeto >*.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Nombre**|**nvarchar (257** **)**|Nombre del elemento que tiene una dependencia.|  
|**Tipo**|**nvarchar(16)**|Tipo del elemento.|  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-listing-dependencies-on-a-table"></a>A. Enumerar dependencias en una tabla.  
 El ejemplo siguiente enumera los objetos de base de datos que dependen de la tabla `Sales.Customer` en la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Se especifican los nombres de esquema y de tabla.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_depends @objname = N'Sales.Customer' ;  
```  
  
### <a name="b-listing-dependencies-on-a-trigger"></a>B. Enumerar dependencias en un desencadenador.  
 En el ejemplo siguiente se enumeran los objetos de base de datos de los que depende el desencadenador `iWorkOrder`.  
  
```  
EXEC sp_depends @objname = N'AdventureWorks2012.Production.iWorkOrder' ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del motor de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Sys.sql_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md)  
  
  
