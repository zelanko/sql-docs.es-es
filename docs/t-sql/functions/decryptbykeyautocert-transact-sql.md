---
title: DECRYPTBYKEYAUTOCERT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2015
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECRYPTBYKEYAUTOCERT
- DECRYPTBYKEYAUTOCERT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DECRYPTBYKEYAUTOCERT function
ms.assetid: 6b45fa2e-ffaa-46f7-86ff-5624596eda4a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 6b799c8fd5dd4a7f44efc358949166d902f88abd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135955"
---
# <a name="decryptbykeyautocert-transact-sql"></a>DECRYPTBYKEYAUTOCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Esta función descifra datos con una clave simétrica. Esa clave simétrica se descifra de forma automática con un certificado.  

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DecryptByKeyAutoCert ( cert_ID , cert_password   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }   
  [ , { authenticator | @authenticator } ] ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *cert_ID*  
El identificador del certificado que se usa para proteger la clave simétrica. *cert_ID* tiene un tipo de datos **int**.  
  
*cert_password*  
La contraseña que se usa para cifrar la clave privada del certificado. Puede tener un valor `NULL` si la clave maestra de la base de datos protege la clave privada. *cert_password* tiene un tipo de datos **nvarchar**.  

'*ciphertext*'  
La cadena de datos cifrados con la clave. *ciphertext* tiene un tipo de datos **varbinary**.  

@ciphertext  
Una variable de tipo **varbinary** que contiene los datos cifrados con la clave.  

*add_authenticator*  
Indica si el proceso de cifrado original incluía, y cifraba, un autenticador junto con el texto sin formato. Debe coincidir con el valor que se pasa a [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) durante el proceso de cifrado de datos. *add_authenticator* tiene un valor de 1 si el proceso de cifrado usó un autenticador. *add_authenticator* tiene un tipo de datos **int**.  
  
@add_authenticator  
Una variable que indica si el proceso de cifrado original incluía, y cifraba, un autenticador junto con el texto sin formato. Debe coincidir con el valor que se pasa a [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md) durante el proceso de cifrado de datos. *@add_authenticator* tiene un tipo de datos **int**.  
  
*authenticator*  
Los datos que se usaron como base para la generación del autenticador. Debe coincidir con el valor que se proporcionó a [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md). *autenticador* tiene un tipo de datos **sysname**.  
  
@authenticator  
Una variable que contiene datos a partir de los que se genera un autenticador. Debe coincidir con el valor que se proporcionó a [ENCRYPTBYKEY (Transact-SQL)](./encryptbykey-transact-sql.md). *@authenticator* tiene un tipo de datos **sysname**.  
  
## <a name="return-types"></a>Tipos devueltos  
**varbinary**, con un tamaño máximo de 8 000 bytes.  
  
## <a name="remarks"></a>Notas  
`DECRYPTBYKEYAUTOCERT` combina las funciones de `OPEN SYMMETRIC KEY` y `DECRYPTBYKEY`. En una sola operación, primero descifra una clave simétrica y después la usa para descifrar el texto cifrado.  
  
## <a name="permissions"></a>Permisos  
Se requiere el permiso `VIEW DEFINITION` en la clave simétrica y el permiso `CONTROL` en el certificado.   
  
## <a name="examples"></a>Ejemplos  
En este ejemplo se muestra cómo `DECRYPTBYKEYAUTOCERT` puede simplificar el código de descifrado. Este código se debería ejecutar en una base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] que aún no tenga una clave maestra de base de datos.  
  
```  
--Create the keys and certificate.  
USE AdventureWorks2012;  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'mzkvdlk979438teag$$ds987yghn)(*&4fdg^';  
OPEN MASTER KEY DECRYPTION BY PASSWORD = 'mzkvdlk979438teag$$ds987yghn)(*&4fdg^';  
CREATE CERTIFICATE HumanResources037   
   WITH SUBJECT = 'Sammamish HR',   
   EXPIRY_DATE = '10/31/2009';  
CREATE SYMMETRIC KEY SSN_Key_01 WITH ALGORITHM = DES  
    ENCRYPTION BY CERTIFICATE HumanResources037;  
GO  
----Add a column of encrypted data.  
ALTER TABLE HumanResources.Employee  
    ADD EncryptedNationalIDNumber varbinary(128);   
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037 ;  
UPDATE HumanResources.Employee  
SET EncryptedNationalIDNumber  
    = EncryptByKey(Key_GUID('SSN_Key_01'), NationalIDNumber);  
GO  
--  
--Close the key used to encrypt the data.  
CLOSE SYMMETRIC KEY SSN_Key_01;  
--  
--There are two ways to decrypt the stored data.  
--  
--OPTION ONE, using DecryptByKey()  
--1. Open the symmetric key  
--2. Decrypt the data  
--3. Close the symmetric key  
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037;  
SELECT NationalIDNumber, EncryptedNationalIDNumber    
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKey(EncryptedNationalIDNumber))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
CLOSE SYMMETRIC KEY SSN_Key_01;  
--  
--OPTION TWO, using DecryptByKeyAutoCert()  
SELECT NationalIDNumber, EncryptedNationalIDNumber   
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKeyAutoCert ( cert_ID('HumanResources037') , NULL ,EncryptedNationalIDNumber))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
```  
  
## <a name="see-also"></a>Consulte también  
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [DECRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbykey-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
