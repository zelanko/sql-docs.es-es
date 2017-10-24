---
title: "REGLA de eliminación (Transact-SQL) | Documentos de Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_RULE_TSQL
- DROP RULE
dev_langs:
- TSQL
helpviewer_keywords:
- rules [SQL Server], removing
- deleting roles
- DROP RULE statement
- removing roles
- dropping roles
ms.assetid: 8370b730-7fd5-43fe-a7f6-8300b3caa16d
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ba898b1c9f94f4e38102da929709b4a05f889b7e
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="drop-rule-transact-sql"></a>DROP RULE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita una o más reglas definidas por el usuario de la base de datos actual.  
  
> [!IMPORTANT]  
>  DROP RULE se quitará en la próxima versión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No lo use en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que usan actualmente DROP RULE. En su lugar, utilice restricciones CHECK que pueden crear mediante la palabra clave CHECK de [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) o [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md). Para más información, consulte [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
DROP RULE [ IF EXISTS ] { [ schema_name . ] rule_name } [ ,...n ] [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *IF EXISTE*  
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Quita condicionalmente la regla solo si ya existe.  
  
 *schema_name*  
 Es el nombre del esquema al que pertenece la regla.  
  
 *regla*  
 Es la regla que se va a quitar. Los nombres de reglas deben cumplir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md). Especificar el nombre de esquema de la regla es opcional.  
  
## <a name="remarks"></a>Comentarios  
 Para quitar una regla, primero desenlace la regla si ésta está enlazada actualmente a una columna o a un tipo de datos de alias. Para desenlazar la regla, use **sp_unbindrule**. Si la regla está enlazada, al intentar quitarla se muestra un mensaje de error y se cancela la instrucción DROP RULE.  
  
 Después de quitar una regla, los datos nuevos escritos en las columnas que controlaba anteriormente la regla se escriben sin las restricciones de la regla. Los datos existentes no se ven afectados de ninguna forma.  
  
 La instrucción DROP RULE no se aplica a las restricciones CHECK. Para obtener más información acerca de cómo quitar restricciones CHECK, vea [ALTER TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Para ejecutar DROP RULE, el usuario debe tener, como mínimo, el permiso ALTER para el esquema al que pertenece la regla.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente desenlaza primero y después quita la regla llamada `VendorID_rule`. 
  
```  
sp_unbindrule 'Production.ProductVendor.VendorID'  
DROP RULE VendorID_rule  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [sp_bindrule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_unbindrule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)  


