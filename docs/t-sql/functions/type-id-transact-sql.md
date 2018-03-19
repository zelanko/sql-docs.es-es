---
title: TYPE_ID (Transact-SQL) | Microsoft Docs
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
- TYPE_ID
- TYPE_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IDs [SQL Server], types
- TYPE_ID function
- type IDs [SQL Server]
- data types [SQL Server], IDs
ms.assetid: 647d17ef-b878-4922-b446-56642322ebad
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8d307359649804e1f57dc427edd907e15ba15bb0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="typeid-transact-sql"></a>TYPE_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el Id. de un nombre de tipo de datos especificado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
TYPE_ID ( [ schema_name ] type_name )   
```  
  
## <a name="arguments"></a>Argumentos  
 *type_name*  
 Es el nombre del tipo de datos. *type_name* es de tipo **nvarchar**. *type_name* puede ser un tipo de datos del sistema o definido por el usuario.  
  
## <a name="return-types"></a>Tipos devueltos  
 **int**  
  
## <a name="exceptions"></a>Excepciones  
 Devuelve NULL si se produce un error o si el autor de la llamada no tiene permiso para ver el objeto.  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], un usuario solo puede ver los metadatos de elementos protegibles que posea o para los que se le haya concedido permiso. Esto significa que las funciones integradas de emisión de metadatos, como TYPE_ID, pueden devolver NULL si el usuario no tiene ningún permiso para el objeto. Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Notas  
 TYPE_ID devuelve NULL si el nombre del tipo no es válido o si el autor de la llamada no tiene suficientes permisos para hacer referencia al tipo.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-looking-up-the-type-id-values-for-single--and-two-part-type-names"></a>A. Buscar los valores de TYPE_ID para nombres de tipo de una sola parte y de dos partes  
 En el siguiente ejemplo se devuelve el valor de TYPE_ID para nombres de una sola parte y de dos partes.  
  
```  
USE tempdb;  
GO  
CREATE TYPE NewType FROM int;  
GO  
CREATE SCHEMA NewSchema;  
GO  
CREATE TYPE NewSchema.NewType FROM int;  
GO  
SELECT TYPE_ID('NewType') AS [1 Part Data Type ID],  
       TYPE_ID('NewSchema.NewType') AS [2 Part Data Type ID];  
GO  
```  
  
### <a name="b-looking-up-the-type-id-of-a-system-data-type"></a>B. Buscar el valor de TYPE_ID de un tipo de datos del sistema  
 En el siguiente ejemplo se devuelve el valor de `TYPE ID` para el tipo de datos del sistema `datetime`.  
  
```  
SELECT TYPE_NAME(TYPE_ID('datetime')) AS [TYPE_NAME]  
    ,TYPE_ID('datetime') AS [TYPE_ID];  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-looking-up-the-type-id-of-a-system-data-type"></a>C. Buscar el valor de TYPE_ID de un tipo de datos del sistema  
 En el siguiente ejemplo se devuelve el valor de `TYPE ID` para el tipo de datos del sistema `datetime`.  
  
```  
SELECT TYPE_NAME(TYPE_ID('datetime')) AS typeName,   
    TYPE_ID('datetime') AS typeID FROM table1;  
```  
  
## <a name="see-also"></a>Ver también  
 [TYPE_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/type-name-transact-sql.md)   
 [TYPEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/typeproperty-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)   
 [Metadata Functions &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md) [Funciones de metadatos &#40;Transact-SQL&#41;]  
  
  

