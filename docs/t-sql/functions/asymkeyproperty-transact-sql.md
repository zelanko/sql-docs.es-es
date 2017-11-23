---
title: ASYMKEYPROPERTY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ASYMKEYPROPERTY_TSQL
- ASYMKEYPROPERTY
dev_langs: TSQL
helpviewer_keywords: ASYMKEYPROPERTY
ms.assetid: a30581f2-e1b1-4996-93e6-527ff96b7c42
caps.latest.revision: "13"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 808f7c8d840f18d9e09fe9906e366fb7feb76cff
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="asymkeyproperty-transact-sql"></a>ASYMKEYPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve las propiedades de una clave asimétrica.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
ASYMKEYPROPERTY (Key_ID , 'algorithm_desc' | 'string_sid' | 'sid')  
```  
  
## <a name="arguments"></a>Argumentos  
*Valor Key_ID*  
Valor Key_ID de una clave asimétrica en la base de datos. Para buscar el valor Key_ID cuando solo se conoce el nombre de la clave, utilice ASYMKEY_ID. *Valor Key_ID* es de tipo de datos **int**.
  
**'**algorithm_desc**'**  
Especifica que la salida devuelve la descripción del algoritmo de la clave asimétrica. Solo está disponible para las claves asimétricas creadas a partir de un módulo EKM.
  
**'**string_sid**'**  
Especifica que la salida devuelve el SID de la clave asimétrica en **nvarchar()** formato.
  
**'**sid**'**  
Especifica que la salida devuelve el SID de la clave asimétrica en formato binario.
  
## <a name="return-types"></a>Tipos de valor devuelto  
**sql_variant**
  
## <a name="permissions"></a>Permissions  
Es necesario tener algún permiso sobre la clave asimétrica y que el autor de la llamada no tenga denegado el permiso VIEW sobre la clave asimétrica.
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se devuelven las propiedades de la clave asimétrica con un valor 256 para Key_ID.
  
```sql
SELECT   
ASYMKEYPROPERTY(256, 'algorithm_desc') AS Algorithm,  
ASYMKEYPROPERTY(256, 'string_sid') AS String_SID,  
ASYMKEYPROPERTY(256, 'sid') AS SID ;  
GO  
```  
  
## <a name="see-also"></a>Vea también
[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
[ALTER ASYMMETRIC KEY &#40; Transact-SQL &#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)  
[DROP ASYMMETRIC KEY &#40; Transact-SQL &#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)  
[SIGNBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/signbyasymkey-transact-sql.md)  
[VERIFYSIGNEDBYASYMKEY &#40; Transact-SQL &#41;](../../t-sql/functions/verifysignedbyasymkey-transact-sql.md)  
[Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
[Sys.asymmetric_keys &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-asymmetric-keys-transact-sql.md)  
[Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)  
[ASYMKEY_ID &#40; Transact-SQL &#41;](../../t-sql/functions/asymkey-id-transact-sql.md)  
[SYMKEYPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/symkeyproperty-transact-sql.md)
  
  
