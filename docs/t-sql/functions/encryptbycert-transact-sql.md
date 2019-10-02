---
title: ENCRYPTBYCERT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ENCRYPTBYCERT
- ENCRYPTBYCERT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- certificates [SQL Server], encryption
- encryption [SQL Server], certificates
- ENCRYPTBYCERT function
ms.assetid: ab66441f-e2d2-4e3a-bcae-bcc09e12f3c1
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f1548aa3b7b436f89ad4dee73b7c1ed7034e0f87
ms.sourcegitcommit: a24f6e12357979f1134a54a036ebc58049484a4f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71314590"
---
# <a name="encryptbycert-transact-sql"></a>ENCRYPTBYCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Cifra datos con la clave pública de un certificado.  
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
EncryptByCert ( certificate_ID , { 'cleartext' | @cleartext } )  
```  
  
## <a name="arguments"></a>Argumentos  
_certificate\_ID_  
Id. de un certificado de la base de datos. **int**.  
  
_cleartext_  
Cadena de datos que se cifrarán con el certificado.  
  
**\@cleartext**  
Una variable de uno de los siguientes tipos que contiene datos que se cifrarán con la clave pública del certificado:

* **nvarchar** 
* **char**
* **varchar**
* **binario** 
* **varbinary**
* **nchar**
  
## <a name="return-types"></a>Tipos devueltos  
**varbinary** con un tamaño máximo de 8000 bytes.  
  
## <a name="remarks"></a>Notas  
Esta función cifra los datos con la clave pública del certificado. El texto cifrado solo puede descifrarse con la correspondiente clave privada. Estas transformaciones asimétricas son muy costosas en comparación con el cifrado y el descifrado mediante una clave simétrica. Por lo tanto, no se recomienda el cifrado asimétrico cuando se trabaja con grandes conjuntos de datos.
  
## <a name="examples"></a>Ejemplos  
En este ejemplo se cifra el texto simple almacenado en `@cleartext` con el certificado denominado `JanainaCert02`. Los datos cifrados se insertan en la tabla `ProtectedData04`.  
  
```  
INSERT INTO [AdventureWorks2012].[ProtectedData04]   
    VALUES ( N'Data encrypted by certificate ''Shipping04''',  
    EncryptByCert(Cert_ID('JanainaCert02'), @cleartext) );  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
[DECRYPTBYCERT &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbycert-transact-sql.md)   
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
[ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
[DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
[BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
[Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
