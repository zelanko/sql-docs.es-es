---
title: TYPE_NAME (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TYPE_NAME_TSQL
- TYPE_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- names [SQL Server], data types
- unqualified type names
- type names [SQL Server]
- data types [SQL Server], names
- TYPE_NAME function
ms.assetid: e4075a2e-5f70-440f-986b-9ec8434e07c1
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: efd210bc036ed301f426e81feb6c783984f9fb4d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="typename-transact-sql"></a>TYPE_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el nombre de tipo no calificado de un Id. de tipo específico.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
TYPE_NAME ( type_id )   
```  
  
## <a name="arguments"></a>Argumentos  
 *type_id*  
 Es el identificador del tipo que se va a utilizar. *type_id* es un **int**, y puede hacer referencia a un tipo de cualquier esquema que el llamador tiene permiso de acceso.  
  
## <a name="return-types"></a>Tipos devueltos  
 **sysname**  
  
## <a name="exceptions"></a>Excepciones  
 Devuelve NULL si se produce un error o si el autor de la llamada no tiene permiso para ver el objeto.  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], un usuario solo puede ver los metadatos de elementos protegibles que posea o para los que se le haya concedido permiso. Esto significa que las funciones integradas de emisión de metadatos, como TYPE_NAME, pueden devolver NULL si el usuario no tiene ningún permiso para el objeto. Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Comentarios  
 TYPE_NAME devolverá NULL cuando *type_id* no es válido o cuando el llamador no tiene permisos suficientes para el tipo de referencia.  
  
 TYPE_NAME funciona con tipos de datos de sistema así como con tipos de datos definidos por el usuario. El tipo puede estar contenido en cualquier esquema, pero siempre se devuelve un nombre de tipo no calificado. Esto significa que no tiene el nombre de la *esquema***.** prefijo.  
  
 Funciones de sistema se pueden usar en la lista de selección en la cláusula WHERE, y en cualquier lugar en que se permita una expresión. Para obtener más información, vea [expresiones &#40; Transact-SQL &#41; ](../../t-sql/language-elements/expressions-transact-sql.md) y [donde &#40; Transact-SQL &#41; ](../../t-sql/queries/where-transact-sql.md).  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve el nombre del objeto, de la columna y del tipo perteneciente a cada columna de la tabla `Vendor` de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
SELECT o.name AS obj_name, c.name AS col_name,  
       TYPE_NAME(c.user_type_id) AS type_name  
FROM sys.objects AS o   
JOIN sys.columns AS c  ON o.object_id = c.object_id  
WHERE o.name = 'Vendor'  
ORDER BY col_name;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
obj_name        col_name                  type_name
--------------- ------------------------ --------------
Vendor          AccountNumber            AccountNumber
Vendor          ActiveFlag               Flag
Vendor          BusinessEntityID         int
Vendor          CreditRating             tinyint
Vendor          ModifiedDate             datetime
Vendor          Name                     Name
Vendor          PreferredVendorStatus    Flag
Vendor          PurchasingWebServiceURL  nvarchar

(8 row(s) affected)
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 El ejemplo siguiente devuelve el `TYPE ID` para el tipo de datos con Id. de `1`.  
  
```  
SELECT TYPE_NAME(36) AS Type36, TYPE_NAME(239) AS Type239;  
GO  
```  
  
 Para obtener una lista de tipos, consulte sys.types.  
  
```  
SELECT * FROM sys.types;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [TYPE_ID &#40; Transact-SQL &#41;](../../t-sql/functions/type-id-transact-sql.md)   
 [TYPEPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/typeproperty-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)   
 [Funciones de metadatos &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
  
  

