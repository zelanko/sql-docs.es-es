---
title: Schema_name (Transact-SQL) | Documentos de Microsoft
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
- SCHEMA_NAME
- SCHEMA_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SCHEMA_NAME function
- schemas [SQL Server], names
ms.assetid: 20071b77-2b6e-4ce7-a8e3-fa71480baf73
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: bbc8d08ff59f85544fe3f11712c6780431bc76d7
ms.contentlocale: es-es
ms.lasthandoff: 10/17/2017

---
# <a name="schemaname-transact-sql"></a>SCHEMA_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el nombre de esquema asociado a un Id. de esquema.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SCHEMA_NAME ( [ schema_id ] )  
```  
  
## <a name="arguments"></a>Argumentos  
  
|Término|Definición|  
|----------|----------------|  
|*schema_id*|El identificador del esquema. *schema_id* es un **int**. Si *schema_id* no es definido, SCHEMA_NAME devolverá el nombre del esquema predeterminado del autor de la llamada.|  
  
## <a name="return-types"></a>Tipos devueltos  
 **sysname**  
  
 Devuelve NULL cuando *schema_id* no es un identificador válido.  
  
## <a name="remarks"></a>Comentarios  
 SCHEMA_NAME devuelve nombres de esquemas del sistema y esquemas definidos por el usuario. SCHEMA_NAME se puede llamar en una lista de selección, en una cláusula WHERE y en cualquier lugar en el que se permita una expresión.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-the-name-of-the-default-schema-of-the-caller"></a>A. Devolver el nombre del esquema predeterminado del llamador  
  
```  
SELECT SCHEMA_NAME();  
```  
  
### <a name="b-returning-the-name-of-a-schema-by-using-an-id"></a>B. Devolver el nombre de un esquema utilizando un Id.  
  
```  
SELECT SCHEMA_NAME(1);  
```  
  
## <a name="see-also"></a>Vea también  
 [Expresiones &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [SCHEMA_ID &#40; Transact-SQL &#41;](../../t-sql/functions/schema-id-transact-sql.md)   
 [Sys.Schemas &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [Funciones de metadatos &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [DONDE &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  


