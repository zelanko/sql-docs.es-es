---
title: KEY_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Key_ID
- Key_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- identification numbers [SQL Server], symmetric keys
- KEY_ID function
- symmetric keys [SQL Server], IDs
- IDs [SQL Server], symmetric keys
ms.assetid: d7309542-dbbe-41dc-b42e-5d9a1c8b4838
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f6d364316629f63071a6e818dabc479eba2567d4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85752261"
---
# <a name="key_id-transact-sql"></a>KEY_ID (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Devuelve el Id. de una clave simétrica en la base de datos actual.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Key_ID ( 'Key_Name' )  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *Key_Name* **'**  
 El nombre de una clave simétrica en la base de datos.  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 **int**  
  
## <a name="remarks"></a>Observaciones  
 El nombre de una clave temporal debe comenzar con un signo de número (#).  
  
## <a name="permissions"></a>Permisos  
 No se requieren permisos para el acceso a las claves temporales, dado que éstas solo están disponibles en la sesión en la que se crean. Para tener acceso a una clave que no es temporal, el solicitante necesita tener algún permiso en la clave y no se le debe haber denegado el permiso VIEW en la clave.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-the-id-of-a-symmetric-key"></a>A. Devolver el identificador de una clave simétrica  
 El ejemplo siguiente devuelve el Id. de una clave denominada `ABerglundKey1`.  
  
```  
SELECT KEY_ID('ABerglundKey1');  
```  
  
### <a name="b-returning-the-id-of-a-temporary-symmetric-key"></a>B. Devolver el identificador de una clave simétrica temporal  
 El ejemplo siguiente devuelve el Id. de una clave simétrica temporal. Observe que `#` se antepone al nombre de la clave.  
  
```  
SELECT KEY_ID('#ABerglundKey2');  
```  
  
## <a name="see-also"></a>Consulte también  
 [KEY_GUID &#40;Transact-SQL&#41;](../../t-sql/functions/key-guid-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [sys.symmetric_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [sys.key_encryptions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-encryptions-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
