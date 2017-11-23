---
title: sp_helpconstraint (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_helpconstraint
- sp_helpconstraint_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_helpconstraint
ms.assetid: 29d6cd36-535d-4765-bca8-62f9d9886ff5
caps.latest.revision: "33"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dbd28705c736817c224762b1535acd34a22dc15e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpconstraint-transact-sql"></a>sp_helpconstraint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve la lista de todos los tipos de restricciones, el nombre definido por el usuario o proporcionado por el sistema, las columnas en que se han definido y la expresión que define la restricción (solo para las restricciones DEFAULT y CHECK).  
  
||  
|-|  
|**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpconstraint [ @objname = ] 'table'   
     [ , [ @nomsg = ] 'no_message' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@objname=** ] **'***tabla***'**  
 Es la tabla de la que se devuelve información de restricciones. La tabla especificada debe encontrarse en la base de datos actual. *tabla* es **nvarchar(776)**, no tiene ningún valor predeterminado.  
  
 [  **@nomsg=**] **'***no_message***'**  
 Es un parámetro opcional que imprime el nombre de tabla. *no_message* es **varchar (5)**, su valor predeterminado es **msg**. **nomsg** suprime la impresión.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **sp_helpconstraint** muestra una columna de índice descendente si forma parte de las claves principales. El nombre de la columna indizada en orden descendente irá seguido de un signo menos (-) en el conjunto de resultados. La columna predeterminada, indizada en orden ascendente, aparecerá solo por su nombre.  
  
## <a name="remarks"></a>Comentarios  
 Ejecutar **sp_help***tabla* presenta toda la información acerca de la tabla especificada. Para ver la información de restricciones, utilice **sp_helpconstraint**.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestran todas las restricciones de la tabla `Product`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helpconstraint 'Production.Product';  
```  
  
## <a name="see-also"></a>Vea también  
 [Motor de base de datos almacenados procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Sys.key_constraints &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [Sys.CHECK_CONSTRAINTS &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)   
 [Sys.default_constraints &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-default-constraints-transact-sql.md)  
  
  
