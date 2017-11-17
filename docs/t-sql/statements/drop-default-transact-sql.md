---
title: DESTINO predeterminado (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_DEFAULT_TSQL
- DROP DEFAULT
dev_langs:
- TSQL
helpviewer_keywords:
- DROP DEFAULT statement
- defaults [SQL Server], removing
ms.assetid: d2d3af25-8877-46ba-95d9-1844961d97ee
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cb7de5514d74ed4650d44bed145c32e9bea2c845
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="drop-default-transact-sql"></a>DROP DEFAULT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita uno o más valores predeterminados definidos por el usuario de la base de datos actual.  
  
> [!IMPORTANT]  
>  DROP DEFAULT se quitará en la próxima versión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No use DROP DEFAULT en un nuevo trabajo de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta función. En su lugar, use definiciones predeterminadas que pueden crear mediante la palabra clave DEFAULT de [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) o [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
DROP DEFAULT [ IF EXISTS ] { [ schema_name . ] default_name } [ ,...n ] [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *IF EXISTE*  
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Quita condicionalmente el valor predeterminado solo si ya existe.  
  
 *schema_name*  
 Es el nombre del esquema al que pertenece el valor predeterminado.  
  
 *default_name*  
 Es el nombre de un valor predeterminado existente. Para ver una lista de valores predeterminados existentes, ejecute **sp_help**. Los valores predeterminados deben cumplir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md). Especificar el nombre del esquema predeterminado es opcional.  
  
## <a name="remarks"></a>Comentarios  
 Antes de quitar un valor predeterminado, desenlazar el valor predeterminado mediante la ejecución de **sp_unbindefault** si el valor predeterminado está enlazado actualmente a una columna o un tipo de datos de alias.  
  
 Después de quitar un valor predeterminado de una columna que permite valores nulos, se inserta NULL en esa posición cuando se agregan filas y no se proporciona un valor explícitamente. Después de quitar un valor predeterminado de una columna NOT NULL, se devuelve un mensaje de error cuando se agregan filas y no se proporciona un valor explícitamente. Estas filas se agregan posteriormente como parte del comportamiento habitual de la instrucción INSERT.  
  
## <a name="permissions"></a>Permissions  
 Para ejecutar DROP DEFAULT, como mínimo, un usuario debe tener permiso ALTER en el esquema al que pertenece el valor predeterminado.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-dropping-a-default"></a>A. Quitar un valor predeterminado  
 Si no se ha enlazado un valor predeterminado a una columna o a un tipo de datos de alias, se puede quitar simplemente con DROP DEFAULT. El siguiente ejemplo quita un valor predeterminado creado por el usuario denominado `datedflt`.  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.objects  
         WHERE name = 'datedflt'   
            AND type = 'D')  
   DROP DEFAULT datedflt;  
GO  
```  
  
 A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] puede utilizar la siguiente sintaxis.  
  
```  
DROP DEFAULT IF EXISTS datedflt;  
GO  
```  
  
### <a name="b-dropping-a-default-that-has-been-bound-to-a-column"></a>B. Quitar un valor predeterminado enlazado a una columna  
 El siguiente ejemplo cancela el enlace del valor predeterminado asociado con la columna `EmergencyContactPhone` de la tabla `Contact` y, a continuación, quita el valor predeterminado denominado `phonedflt`.  
  
```  
USE AdventureWorks2012;  
GO  
   BEGIN   
      EXEC sp_unbindefault 'Person.Contact.Phone'  
      DROP DEFAULT phonedflt  
   END;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_unbindefault &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)  
  
  

