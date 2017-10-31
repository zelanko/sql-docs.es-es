---
title: CLOSE SYMMETRIC KEY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CLOSE SYMMETRIC KEY
- CLOSE_SYMMETRIC_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- closing symmetric keys
- encryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], closing
- CLOSE SYMMETRIC KEY statement
- cryptography [SQL Server], symmetric keys
ms.assetid: 3b083cbb-3c6a-4f59-8d34-601db1efcc83
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 18a4215cf009ebf89bf6ce709c0517455731c4b5
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="close-symmetric-key-transact-sql"></a>CLOSE SYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Cierra una clave simétrica o cierra todas las claves simétricas abiertas en la sesión actual.  
  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
CLOSE { SYMMETRIC KEY key_name | ALL SYMMETRIC KEYS }  
```  
  
## <a name="arguments"></a>Argumentos  
 *Key_name*  
 Es el nombre de la clave simétrica que se va a cerrar.  
  
## <a name="remarks"></a>Comentarios  
 Las claves simétricas abiertas están enlazadas a la sesión, no al contexto de seguridad. Una clave abierta seguirá disponible hasta que se cierre explícitamente o hasta que finalice la sesión. CLOSE ALL SYMMETRIC KEYS cerrará cualquier clave maestra de base de datos que se abrió en la sesión actual mediante el uso de la [OPEN MASTER KEY](../../t-sql/statements/open-master-key-transact-sql.md) instrucción.  Información acerca de las claves abiertas está visible en el [sys.openkeys &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-openkeys-transact-sql.md) vista de catálogo.  
  
## <a name="permissions"></a>Permissions  
 Para cerrar una clave simétrica no es necesario ningún permiso explícito.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-closing-a-symmetric-key"></a>A. Cerrar una clave simétrica  
 En el siguiente ejemplo se cierra la clave simétrica `ShippingSymKey04`.  
  
```  
CLOSE SYMMETRIC KEY ShippingSymKey04;  
GO  
```  
  
### <a name="b-closing-all-symmetric-keys"></a>B. Cerrar todas las claves simétricas  
 En el siguiente ejemplo se cierran todas las claves simétricas abiertas en la sesión actual y también la clave maestra de la base de datos abierta de forma explícita.  
  
```  
CLOSE ALL SYMMETRIC KEYS;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [Eliminar clave SIMÉTRICA &#40; Transact-SQL &#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)  
  
  

