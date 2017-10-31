---
title: IS_OBJECTSIGNED (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IS_OBJECTSIGNED
- IS_OBJECTSIGNED_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IS_OBJECTSIGNED function
ms.assetid: afbc4f7f-8266-4ee6-9802-14a2dbe69ef6
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e346fb803e18d9a43afe15984166985ff0a3e408
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="isobjectsigned-transact-sql"></a>IS_OBJECTSIGNED (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Indica si un objeto está firmado por un certificado o clave asimétrica especificados.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IS_OBJECTSIGNED (   
'OBJECT', @object_id, @class, @thumbprint  
  )   
```  
  
## <a name="arguments"></a>Argumentos  
 **'OBJECT'**  
 Tipo de la clase protegible.  
  
 *@object_id*  
 Valor object_id del objeto que se va a probar. *@object_id*es de tipo **int**.  
  
 *@class*  
 Clase del objeto:  
  
-   'certificado'  
  
-   'clave asimétrica'  
  
 *@class*es **sysname**.  
  
 *@thumbprint*  
 Huella digital SHA del objeto. *@thumbprint*es de tipo **varbinary(32)**.  
  
## <a name="returned-types"></a>Tipos devueltos  
 **int**  
  
## <a name="remarks"></a>Comentarios  
 IS_OBJECTSIGNED devuelve los siguientes valores.  
  
|Valor devuelto|Description|  
|------------------|-----------------|  
|NULL|El objeto no está firmado, o el objeto no es válido.|  
|0|El objeto está firmado, pero la firma no es válida.|  
|1|El objeto está firmado.|  
  
## <a name="permissions"></a>Permissions  
 Se requiere VIEW DEFINITION sobre el certificado o la clave asimétrica.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-displaying-extended-properties-on-a-database"></a>A. Mostrar las propiedades extendidas de una base de datos  
 En el ejemplo siguiente se comprueba si la tabla spt_fallback_db de la **maestro** base de datos está firmado por el certificado de firma del esquema.  
  
```  
USE master;  
-- Declare a variable to hold a thumbprint and an object name  
DECLARE @thumbprint varbinary(20), @objectname sysname;  
  
-- Populate the thumbprint variable with the thumbprint of   
-- the master database schema signing certificate  
SELECT @thumbprint = thumbprint   
FROM sys.certificates   
WHERE name LIKE '%SchemaSigningCertificate%';  
  
-- Populate the object name variable with a table name in master  
SELECT @objectname = 'spt_fallback_db';  
  
-- Query to see if the table is signed by the thumbprint  
SELECT @objectname AS [object name],  
IS_OBJECTSIGNED(  
'OBJECT', OBJECT_ID(@objectname), 'certificate', @thumbprint  
) AS [Is the object signed?] ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Sys.fn_check_object_signatures &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-check-object-signatures-transact-sql.md)  
  
  

