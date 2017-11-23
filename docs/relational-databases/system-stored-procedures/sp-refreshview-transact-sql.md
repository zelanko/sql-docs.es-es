---
title: sp_refreshview (Transact-SQL) | Documentos de Microsoft
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
- sp_refreshview
- sp_refreshview_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_refreshview
ms.assetid: 9ce1d07c-ee66-4a83-8c73-cd2cc104dd08
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: bf19db7a1a5f5c772b3456b5498da99b7929c986
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sprefreshview-transact-sql"></a>sp_refreshview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Actualiza los metadatos de la vista no enlazada a esquema especificada. Los metadatos persistentes de una vista pueden quedar desfasados debido a los cambios realizados en los objetos subyacentes de los que depende la vista.  
  
||  
|-|  
|**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_refreshview [ @viewname = ] 'viewname'   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@viewname=** ] **'***viewname***'**  
 Es el nombre de la vista. *ViewName* es **nvarchar**, no tiene ningún valor predeterminado. *ViewName* puede ser un identificador con varias partes, pero solo puede hacer referencia a vistas en la base de datos actual.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o un número distinto de cero (error)  
  
## <a name="remarks"></a>Comentarios  
 Si no se crea una vista con schemabinding, **sp_refreshview** deben ejecutarse cuando se realizan cambios en los objetos subyacentes de la vista que afectan a la definición de la vista. De lo contrario, la vista podría producir resultados inesperados en las consultas.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER en la vista y el permiso REFERENCES en los tipos definidos por el usuario Common Language Runtime (CLR) y las colecciones de esquemas XML a los que hacen referencia las columnas de la vista.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-updating-the-metadata-of-a-view"></a>A. Actualizar los metadatos de una vista  
 En el siguiente ejemplo se actualizan los metadatos de la vista `Sales.vIndividualCustomer`.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sp_refreshview N'Sales.vIndividualCustomer';  
```  
  
### <a name="b-creating-a-script-that-updates-all-views-that-have-dependencies-on-a-changed-object"></a>B. Crear un script que actualiza todas las vistas que tienen dependencias en un objeto modificado  
 Suponga que la tabla `Person.Person` se modificó de una forma que afecte a la definición de todas las vistas que se creen en ella. En el siguiente ejemplo se crea un script que actualiza los metadatos de todas las vistas que tienen una dependencia en la tabla `Person.Person`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT DISTINCT 'EXEC sp_refreshview ''' + name + ''''   
FROM sys.objects AS so   
INNER JOIN sys.sql_expression_dependencies AS sed   
    ON so.object_id = sed.referencing_id   
WHERE so.type = 'V' AND sed.referenced_id = OBJECT_ID('Person.Person');  
```  
  
## <a name="see-also"></a>Vea también  
 [Motor de base de datos almacenados procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [sp_refreshsqlmodule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-refreshsqlmodule-transact-sql.md)  
  
  
