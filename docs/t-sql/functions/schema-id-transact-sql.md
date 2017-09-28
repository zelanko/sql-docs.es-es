---
title: SCHEMA_ID (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SCHEMA_ID
- SCHEMA_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- identification numbers [SQL Server], schemas
- schemas [SQL Server], IDs
- SCHEMA_ID function
- IDs [SQL Server], schemas
- default schema IDs
ms.assetid: c8e34df5-3eea-459f-ae40-050909ce9fda
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3e364abf5b75159600715be0a4823ba8fce847e2
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="schemaid-transact-sql"></a>SCHEMA_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el identificador de esquema asociado a un nombre de esquema.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SCHEMA_ID ( [ schema_name ] )   
```  
  
## <a name="arguments"></a>Argumentos  
  
|Término|Definición|  
|----------|----------------|  
|*schema_name*|Es el nombre del esquema. *schema_name* es un **sysname**. Si *schema_name* no se especifica, SCHEMA_ID devolverá el Id. del esquema predeterminado del autor de la llamada.|  
  
## <a name="return-types"></a>Tipos devueltos  
 **int**  
  
 Se devolverá NULL si *schema_name* no es un esquema válido.  
  
## <a name="remarks"></a>Comentarios  
 SCHEMA_ID devolverá los Id. de los esquemas del sistema y de los esquemas definidos por el usuario. Se puede llamar a SCHEMA_ID en una lista de selección, en una cláusula WHERE y en cualquier lugar en el que se permita una expresión.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-the-default-schema-id-of-a-caller"></a>A. Devolver el identificador del esquema predeterminado del llamador  
  
```  
SELECT SCHEMA_ID();  
GO  
```  
  
### <a name="b-returning-the-schema-id-of-a-named-schema"></a>B. Devolver el identificador de un esquema con nombre  
  
```  
USE AdventureWorks2012;  
GO  
SELECT SCHEMA_ID('HumanResources');  
GO   
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-returning-the-default-schema-id-of-a-caller"></a>C. Devolver el identificador del esquema predeterminado del llamador  
  
```  
SELECT SCHEMA_ID();  
```  
  
### <a name="d-returning-the-schema-id-of-a-named-schema"></a>D. Devolver el identificador de un esquema con nombre  
  
```  
SELECT SCHEMA_ID('dbo');  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de metadatos &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [Schema_name &#40; Transact-SQL &#41;](../../t-sql/functions/schema-name-transact-sql.md)   
 [Sys.Schemas &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)  
  
  


