---
title: DECRYPTBYKEYAUTOASYMKEY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 09/09/2015
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DECRYPTBYKEYAUTOASYMKEY_TSQL
- DECRYPTBYKEYAUTOASYMKEY
dev_langs: TSQL
helpviewer_keywords: DECRYPTBYKEYAUTOASYMSKEY function
ms.assetid: 5521d4cf-740c-4ede-98b6-4ba90b84e32d
caps.latest.revision: "23"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6d2e418ce7df83c5c10e6af9517b087ccc877273
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="decryptbykeyautoasymkey-transact-sql"></a>DECRYPTBYKEYAUTOASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Descifra mediante una clave simétrica que se descifra automáticamente con una clave asimétrica.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DecryptByKeyAutoAsymKey ( akey_ID , akey_password   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }   
  [ , { authenticator | @authenticator } ] ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *akey_ID*  
 Es el identificador de la clave asimétrica que se usa para proteger la clave simétrica. *akey_ID* es **int**.  
  
 *akey_password*  
 Es la contraseña que protege la clave privada de la clave asimétrica. Puede ser NULL si la clave privada está protegida por la clave maestra de la base de datos. *akey_password* es **nvarchar**.  
  
 '*texto cifrado*'  
 Son los datos que se cifraron con la clave. *texto cifrado* es **varbinary**.  
  
 @ciphertext  
 Es una variable de tipo **varbinary** que contiene datos que se cifraron con la clave.  
  
 *add_authenticator*  
 Indica si se ha cifrado un autenticador junto con el texto simple. Debe ser el mismo valor que se pasó a EncryptByKey al cifrar los datos. Es 1 si se ha utilizado un autenticador. *add_authenticator* es **int**.  
  
 @add_authenticator  
 Indica si se ha cifrado un autenticador junto con el texto simple. Debe ser el mismo valor que se pasó a EncryptByKey al cifrar los datos.  
  
 *autenticador*  
 Son los datos a partir de los cuales se generará un autenticador. Debe coincidir con el valor que se proporcionó para EncryptByKey. *autenticador* es **sysname**.  
  
 @authenticator  
 Es una variable que contiene los datos a partir de los cuales se generará un autenticador. Debe coincidir con el valor que se proporcionó para EncryptByKey.  
  
## <a name="return-types"></a>Tipos devueltos  
 **varbinary** con un tamaño máximo de 8.000 bytes.  
  
## <a name="remarks"></a>Comentarios  
 DecryptByKeyAutoAsymKey combina la funcionalidad de OPEN SYMMETRIC KEY con la de DecryptByKey. En una sola operación descifra una clave simétrica y usa esa clave para descifrar texto cifrado.  
  
## <a name="permissions"></a>Permissions  
 Se requiere el permiso VIEW DEFINITION sobre la clave simétrica y el permiso CONTROL sobre la clave asimétrica.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra cómo se puede utilizar `DecryptByKeyAutoAsymKey` para simplificar código de descifrado. Este código se debería ejecutar en una base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] que aún no tenga una clave maestra de base de datos.  
  
```  
--Create the keys and certificate.  
USE AdventureWorks2012;  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'mzkvdMlk979438teag$$ds987yghn)(*&4fdg^';  
OPEN MASTER KEY DECRYPTION BY PASSWORD = 'mzkvdMlk979438teag$$ds987yghn)(*&4fdg^';  
CREATE ASYMMETRIC KEY SSN_AKey   
    WITH ALGORITHM = RSA_2048 ;   
GO  
CREATE SYMMETRIC KEY SSN_Key_02 WITH ALGORITHM = DES  
    ENCRYPTION BY ASYMMETRIC KEY SSN_AKey;  
GO  
--  
--Add a column of encrypted data.  
ALTER TABLE HumanResources.Employee  
    ADD EncryptedNationalIDNumber2 varbinary(128);   
OPEN SYMMETRIC KEY SSN_Key_02  
   DECRYPTION BY ASYMMETRIC KEY SSN_AKey;  
UPDATE HumanResources.Employee  
SET EncryptedNationalIDNumber2  
    = EncryptByKey(Key_GUID('SSN_Key_02'), NationalIDNumber);  
GO  
--Close the key used to encrypt the data.  
CLOSE SYMMETRIC KEY SSN_Key_02;  
--  
--There are two ways to decrypt the stored data.  
--  
--OPTION ONE, using DecryptByKey()  
--1. Open the symmetric key.  
--2. Decrypt the data.  
--3. Close the symmetric key.  
OPEN SYMMETRIC KEY SSN_Key_02  
   DECRYPTION BY ASYMMETRIC KEY SSN_AKey;  
SELECT NationalIDNumber, EncryptedNationalIDNumber2    
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKey(EncryptedNationalIDNumber2))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
CLOSE SYMMETRIC KEY SSN_Key_02;  
--  
--OPTION TWO, using DecryptByKeyAutoAsymKey()  
SELECT NationalIDNumber, EncryptedNationalIDNumber2   
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKeyAutoAsymKey ( AsymKey_ID('SSN_AKey') , NULL ,EncryptedNationalIDNumber2))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [ENCRYPTBYKEY &#40; Transact-SQL &#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [DECRYPTBYKEY &#40; Transact-SQL &#41;](../../t-sql/functions/decryptbykey-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
