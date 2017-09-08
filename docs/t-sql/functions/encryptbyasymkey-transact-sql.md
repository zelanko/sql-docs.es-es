---
title: ENCRYPTBYASYMKEY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 711b5887a9411c10c215cc766eb0995c3e056d77
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="encryptbyasymkey-transact-sql"></a>ENCRYPTBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Cifra datos con una clave asimétrica.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
EncryptByAsymKey ( Asym_Key_ID , { 'plaintext' | @plaintext } )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Asym_Key_ID*  
 Id. de una clave asimétrica en la base de datos. **int**.  
  
 *texto no cifrado*  
 Cadena de datos que se cifrará con la clave asimétrica.  
  
 **@plaintext**  
 Es una variable de tipo **nvarchar**, **char**, **varchar**, **binario**, **varbinary**, o **nchar** que contiene los datos van a cifrar con la clave asimétrica.  
  
## <a name="return-types"></a>Tipos devueltos  
 **varbinary** con un tamaño máximo de 8.000 bytes.  
  
## <a name="remarks"></a>Comentarios  
 El cifrado/descifrado con una clave asimétrica es muy costoso si lo comparamos con el cifrado/descifrado con una clave simétrica. No es recomendable cifrar con una clave asimétrica grandes conjuntos de datos, como los datos de usuarios almacenados en tablas. En lugar de ello, se deben cifrar los datos con una clave simétrica segura y cifrar la clave simétrica con una clave asimétrica.  
  
 **EncryptByAsymKey** devolver **NULL** si la entrada supera un cierto número de bytes, dependiendo del algoritmo. Los límites son: una clave RSA de 512 bits puede cifrar hasta 53 bytes, una clave de 1024 bits puede cifrar hasta 117 bytes y una clave de 2048 bits puede cifrar hasta 245 bytes. (Tenga en cuenta que en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tanto los certificados como las claves asimétricas son contenedores de claves RSA).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se cifra el texto almacenado en `@cleartext` con la clave asimétrica `JanainaAsymKey02`. Los datos cifrados se insertan en la `ProtectedData04` tabla.  
  
```  
INSERT INTO AdventureWorks2012.Sales.ProtectedData04   
    VALUES( N'Data encrypted by asymmetric key ''JanainaAsymKey02''',  
    EncryptByAsymKey(AsymKey_ID('JanainaAsymKey02'), @cleartext) );  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [DECRYPTBYASYMKEY &#40; Transact-SQL &#41;](../../t-sql/functions/decryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
