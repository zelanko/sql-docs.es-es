---
title: Sys.fn_check_object_signatures (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.fn_check_object_signatures_TSQL
- fn_check_object_signatures_TSQL
- fn_check_object_signatures
- sys.fn_check_object_signatures
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_check_object_signatures function
ms.assetid: 47509566-d3d7-46a9-89c1-91b4895d56b9
caps.latest.revision: 15
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>= aps-pdw-2016 || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4d516472fb5ccec63498d7ab13401e2df1f4bf10
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sysfncheckobjectsignatures-transact-sql"></a>sys.fn_check_object_signatures (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Devuelve una lista de todos los objetos que se pueden firmar e indica si una clave asimétrica o certificado especificados firman un objeto. Si la clave asimétrica o certificado especificados firman el objeto, también devuelve si la firma del objeto es válida.  
  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn_ check_object_signatures (   
    { '@class' } , { @thumbprint }   
  )   
```  
  
## <a name="arguments"></a>Argumentos  
 {' @*clase*'}  
 Identifica el tipo de huella digital que se proporciona:  
  
-   'certificado'  
  
-   'clave asimétrica'  
  
 @*clase* es **sysname**.  
  
 {@*huella digital* }  
 El valor hash SHA-1 del certificado o GUID de la clave asimétrica con el que se cifra la clave. @*huella digital* es **varbinary(20)**.  
  
## <a name="tables-returned"></a>Tablas devueltas  
 En la tabla siguiente se muestra las columnas que **fn_check_object_signatures** devuelve.  
  
|Columna|Tipo|Description|  
|------------|----------|-----------------|  
|Tipo|**nvarchar(120)**|Devuelve la descripción del tipo o ensamblado.|  
|entity_id|**int**|Devuelve el identificador de objeto del objeto que se está evaluando.|  
|is_signed|**int**|Devuelve 0 cuando la huella digital proporcionada no firma el objeto. Devuelve 1 cuando la huella digital proporcionada firma el objeto.|  
|is_signature_valid|**int**|Cuando el valor de is_signed es 1, devuelve 0 si la firma no es válida. Devuelve 1 cuando la firma es válida.<br /><br /> Cuando el valor de is_signed es 0, siempre devuelve 0.|  
  
## <a name="remarks"></a>Comentarios  
 Use **fn_check_object_signatures** para confirmar que los usuarios malintencionados no han alterado los objetos.  
  
## <a name="permissions"></a>Permissions  
 Se requiere VIEW DEFINITION sobre el certificado o la clave asimétrica.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se busca el certificado de firma del esquema para la base de datos `master` y se devuelve el valor 1 de `is_signed` y el valor 1 de `is_signature_valid` para los objetos firmados por el certificado de firma del esquema que tienen firmas válidas.  
  
```  
USE master;  
-- Declare a variable to hold the thumbprint.  
DECLARE @thumbprint varbinary(20) ;  
-- Populate the thumbprint variable with the master database schema signing certificate.  
SELECT @thumbprint = thumbprint   
FROM sys.certificates   
WHERE name LIKE '%SchemaSigningCertificate%' ;  
-- Evaluates the objects signed by the schema signing certificate  
SELECT type, entity_id, OBJECT_NAME(entity_id) AS [object name], is_signed, is_signature_valid  
FROM sys.fn_check_object_signatures ('certificate', @thumbprint) ;  
GO  
  
```  
  
## <a name="see-also"></a>Vea también  
 [IS_OBJECTSIGNED &#40;Transact-SQL&#41;](../../t-sql/functions/is-objectsigned-transact-sql.md)  
  
  
