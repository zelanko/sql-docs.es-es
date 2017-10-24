---
title: SYMKEYPROPERTY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SYMKEYPROPERTY_TSQL
- SYMKEYPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- SYMKEYPROPERTY
ms.assetid: 3d1f7075-3a3c-4660-8cd0-ed938b86fecd
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 12eaae508f3e6874e02e67ef7ece84da070bbb28
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="symkeyproperty-transact-sql"></a>SYMKEYPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve el algoritmo de una clave simétrica creada a partir de un módulo EKM.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SYMKEYPROPERTY ( Key_ID , 'algorithm_desc' | 'string_sid' | 'sid' )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Valor Key_ID*  
 Es el valor Key_ID de una clave asimétrica de la base de datos. Para buscar el valor Key_ID cuando solo se conoce el nombre de la clave, utilice SYMKEY_ID. *Valor Key_ID* es de tipo de datos **int**.  
  
 **'**algorithm_desc**'**  
 Especifica que la salida devuelve la descripción del algoritmo de la clave simétrica. Solo está disponible para las claves simétricas creadas a partir de un módulo EKM.  
  
## <a name="return-types"></a>Tipos devueltos  
 **sql_variant**  
  
## <a name="permissions"></a>Permissions  
 Es necesario tener algún permiso sobre la clave simétrica y que el autor de la llamada no tenga denegado el permiso VIEW sobre la clave simétrica.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve el algoritmo de la clave simétrica con un valor 256 para Key_ID.  
  
```  
SELECT SYMKEYPROPERTY(256, 'algorithm_desc') AS Algorithm ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [ASYMKEY_ID &#40; Transact-SQL &#41;](../../t-sql/functions/asymkey-id-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Sys.symmetric_keys &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Valor KEY_ID &#40; Transact-SQL &#41;](../../t-sql/functions/key-id-transact-sql.md)   
 [ASYMKEYPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/asymkeyproperty-transact-sql.md)  
  
  

