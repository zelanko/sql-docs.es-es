---
title: ENCRYPTBYASYMKEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ENCRYPTBYASYMKEY
- ENCRYPTBYASYMKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTBYASYMKEY function
- encryption [SQL Server], asymmetric keys
- asymmetric keys [SQL Server], ENCRYPTBYASYMKEY function
ms.assetid: 86bb2588-ab13-4db2-8f3c-42c9f572a67b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6ef212d976ca8f84881695d85e56f5ab1cbca020
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="encryptbyasymkey-transact-sql"></a>ENCRYPTBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Cifra datos con una clave asimétrica.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
EncryptByAsymKey ( Asym_Key_ID , { 'plaintext' | @plaintext } )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Asym_Key_ID*  
 Id. de una clave asimétrica en la base de datos. **int**.  
  
 *cleartext*  
 Cadena de datos que se cifrará con la clave asimétrica.  
  
 **@plaintext**  
 Variable de tipo **nvarchar**, **char**, **varchar**, **binary**, **varbinary** o **nchar** que contiene datos que se van a cifrar con la clave asimétrica.  
  
## <a name="return-types"></a>Tipos devueltos  
 **varbinary** con un tamaño máximo de 8000 bytes.  
  
## <a name="remarks"></a>Notas  
 El cifrado/descifrado con una clave asimétrica es muy costoso si lo comparamos con el cifrado/descifrado con una clave simétrica. No es recomendable cifrar con una clave asimétrica grandes conjuntos de datos, como los datos de usuarios almacenados en tablas. En lugar de ello, se deben cifrar los datos con una clave simétrica segura y cifrar la clave simétrica con una clave asimétrica.  
  
 **EncryptByAsymKey** devuelve **NULL** si la entrada supera un número determinado de bytes, según el algoritmo. Los límites son: una clave RSA de 512 bits puede cifrar hasta 53 bytes, una clave de 1024 bits puede cifrar hasta 117 bytes y una clave de 2048 bits puede cifrar hasta 245 bytes. (Tenga en cuenta que en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tanto los certificados como las claves asimétricas son contenedores de claves RSA).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se cifra el texto almacenado en `@cleartext` con la clave asimétrica `JanainaAsymKey02`. Los datos cifrados se insertan en la tabla `ProtectedData04`.  
  
```  
INSERT INTO AdventureWorks2012.Sales.ProtectedData04   
    VALUES( N'Data encrypted by asymmetric key ''JanainaAsymKey02''',  
    EncryptByAsymKey(AsymKey_ID('JanainaAsymKey02'), @cleartext) );  
GO  
```  
  
## <a name="see-also"></a>Ver también  
 [DECRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
