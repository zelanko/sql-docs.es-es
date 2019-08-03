---
title: sp_helpconstraint (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpconstraint
- sp_helpconstraint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpconstraint
ms.assetid: 29d6cd36-535d-4765-bca8-62f9d9886ff5
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d722d3b54c2f0b6d73660e2195aed4039e1eda2c
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771084"
---
# <a name="sphelpconstraint-transact-sql"></a>sp_helpconstraint (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Devuelve la lista de todos los tipos de restricciones, el nombre definido por el usuario o proporcionado por el sistema, las columnas en que se han definido y la expresión que define la restricción (solo para las restricciones DEFAULT y CHECK).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpconstraint [ @objname = ] 'table'   
     [ , [ @nomsg = ] 'no_message' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @objname = ] 'table'`Es la tabla sobre la que se devuelve información de restricciones. La tabla especificada debe encontrarse en la base de datos actual. *TABLE* es de tipo **nvarchar (776)** y no tiene ningún valor predeterminado.  
  
`[ @nomsg = ] 'no_message'`Es un parámetro opcional que imprime el nombre de la tabla. *no_message* es de tipo **VARCHAR (5)** y su valor predeterminado es **MSG**. **nomsg** suprime la impresión.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **sp_helpconstraint** muestra una columna indizada descendente si participó en las claves principales. El nombre de la columna indizada en orden descendente irá seguido de un signo menos (-) en el conjunto de resultados. La columna predeterminada, indizada en orden ascendente, aparecerá solo por su nombre.  
  
## <a name="remarks"></a>Comentarios  
 La ejecución de la_tabla_ **sp_help**informa de toda la información acerca de la tabla especificada. Para ver solo la información de restricción, use **sp_helpconstraint**.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestran todas las restricciones de la tabla `Product`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helpconstraint 'Production.Product';  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos &#40;almacenados de motor de base de datos TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.key_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [sys.check_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)   
 [sys.default_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-default-constraints-transact-sql.md)  
  
  
