---
title: DROP COLUMN ENCRYPTION KEY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP COLUMN ENCRYPTION
- DROP COLUMN ENCRYPTION KEY
- DROP_COLUMN_ENCRYPTION_TSQL
- DROP_COLUMN_ENCRYPTION_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP COLUMN ENCRYPTION KEY statement
- column encryption key, drop
ms.assetid: 86415302-1383-4d36-9fc7-f780831a2d37
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 47208c011acad2d06fdf91cb3762474ca848e23e
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="drop-column-encryption-key-transact-sql"></a>DROP COLUMN ENCRYPTION KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Quita una clave de cifrado de columna de una base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP COLUMN ENCRYPTION KEY key_name [;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *key_name*  
 Es el nombre por el que el cifrado de columna clave que se para van a quitar de la base de datos.  
  
## <a name="remarks"></a>Comentarios  
 No se puede quitar una clave de cifrado de columna si se usa para cifrar cualquier columna de la base de datos. Primero se deben quitar todas las columnas utilizando la clave de cifrado de columna.  
  
## <a name="permissions"></a>Permissions  
 Requiere **ALTER ANY COLUMN ENCRYPTION KEY** permiso en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-dropping-a-column-encryption-key"></a>A. Quitar una clave de cifrado de columna  
 En el ejemplo siguiente se quita una clave de cifrado de columna denominada `MyCEK`.  
  
```  
DROP COLUMN ENCRYPTION KEY MyCEK;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Always Encrypted &#40;motor de base de datos&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [ALTER COLUMN ENCRYPTION KEY &#40; Transact-SQL &#41;](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)  
  
  

