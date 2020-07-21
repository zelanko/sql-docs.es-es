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
ms.openlocfilehash: b2a25f62b563a01aa9cafb522d9ea32ab0f32fc9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85682036"
---
# <a name="encryptbycert-transact-sql"></a>ENCRYPTBYCERT (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Cifra datos con la clave pública de un certificado.  
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```syntaxsql
  
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
* **binary** 
* **varbinary**
* **nchar**
  
## <a name="return-types"></a>Tipos de valor devuelto  
**varbinary** con un tamaño máximo de 8000 bytes.  
  
## <a name="remarks"></a>Observaciones  
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
  
  
