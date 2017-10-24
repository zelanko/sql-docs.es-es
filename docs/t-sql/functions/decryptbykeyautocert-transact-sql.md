---
title: DECRYPTBYKEYAUTOCERT() (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 09/09/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DECRYPTBYKEYAUTOCERT
- DECRYPTBYKEYAUTOCERT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DECRYPTBYKEYAUTOCERT function
ms.assetid: 6b45fa2e-ffaa-46f7-86ff-5624596eda4a
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0842000cd08e3ca82dab181f32ae96f4a0280d5d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# DECRYPTBYKEYAUTOCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Se descifra mediante una clave simétrica que se descifra automáticamente con un certificado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Sintaxis  
  
```  
  
DecryptByKeyAutoCert ( cert_ID , cert_password   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }   
  [ , { authenticator | @authenticator } ] ] )  
```  
  
## Argumentos  
 *cert_ID*  
 Es el identificador del certificado que se usa para proteger la clave simétrica. *cert_ID* es **int**.  
  
 *cert_password*  
 Contraseña que protege la clave privada del certificado. Puede ser NULL si la clave privada está protegida por la clave maestra de la base de datos. *cert_password* es **nvarchar**.  
  
 '*texto cifrado*'  
 Son los datos que se cifraron con la clave. *texto cifrado* es **varbinary**.  
  
 @ciphertext  
 Es una variable de tipo **varbinary** que contiene datos que se cifraron con la clave.  
  
 *add_authenticator*  
 Indica si se ha cifrado un autenticador junto con el texto simple. Debe ser el mismo valor que se pasó a EncryptByKey al cifrar los datos. Es **1** si se usó un autenticador. *add_authenticator* es **int**.  
  
 @add_authenticator  
 Indica si se ha cifrado un autenticador junto con el texto simple. Debe ser el mismo valor que se pasó a EncryptByKey al cifrar los datos.  
  
 *autenticador*  
 Son los datos a partir de los cuales se generará un autenticador. Debe coincidir con el valor que se proporcionó para EncryptByKey. *autenticador* es **sysname**.  
  
 @authenticator  
 Es una variable que contiene los datos a partir de los cuales se generará un autenticador. Debe coincidir con el valor que se proporcionó para EncryptByKey.  
  
## Tipos devueltos  
 **varbinary** con un tamaño máximo de 8.000 bytes.  
  
## Comentarios  
 DecryptByKeyAutoCert combina la funcionalidad de OPEN SYMMETRIC KEY con la de DecryptByKey. En una sola operación descifra una clave simétrica y utiliza esa clave para descifrar texto cifrado.  
  
## Permissions  
 Se requiere el permiso VIEW DEFINITION sobre la clave simétrica y el permiso CONTROL sobre el certificado.  
  
## Ejemplos  
 En el ejemplo siguiente se muestra cómo se puede utilizar `DecryptByKeyAutoCert` para simplificar código de descifrado. Este código se debería ejecutar en una base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] que aún no tenga una clave maestra de base de datos.  
  
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
  
## Vea también  
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [ENCRYPTBYKEY &#40; Transact-SQL &#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [DECRYPTBYKEY &#40; Transact-SQL &#41;](../../t-sql/functions/decryptbykey-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

