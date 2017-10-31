---
title: ENCRYPTBYKEY (Transact-SQL) | Documentos de Microsoft
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
- ENCRYPTBYKEY_TSQL
- ENCRYPTBYKEY
dev_langs:
- TSQL
helpviewer_keywords:
- authenticators [SQL Server]
- encryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], ENCRYPTBYKEY function
- ENCRYPTBYKEY function
ms.assetid: 0e11f8c5-f79d-46c1-ab11-b68ef05d6787
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 17b9b4aea4916cfb74efbead6d06c830698a4167
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="encryptbykey-transact-sql"></a>ENCRYPTBYKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Cifra los datos usando una clave simétrica.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
EncryptByKey ( key_GUID , { 'cleartext' | @cleartext }  
    [, { add_authenticator | @add_authenticator }  
     , { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *key_GUID*  
 Es el GUID de la clave que se utilizará para cifrar el *texto no cifrado*. **uniqueidentifier**.  
  
 '*texto no cifrado*'  
 Son los datos que se cifrarán con la clave.  
  
 @cleartext  
 Es una variable de tipo **nvarchar**, **char**, **varchar**, **binario**, **varbinary**, o **nchar** que contiene datos que se van a cifrar con la clave.  
  
 *add_authenticator*  
 Indica si se cifrará un autenticador junto con el *texto no cifrado*. Debe ser 1 cuando se utilice un autenticador. **int**.  
  
 @add_authenticator  
 Indica si se cifrará un autenticador junto con el *texto no cifrado*. Debe ser 1 cuando se utilice un autenticador. **int**.  
  
 *autenticador*  
 Son los datos de los que se derivará un autenticador. **sysname**.  
  
 @authenticator  
 Es una variable que contiene los datos de los que se derivará un autenticador.  
  
## <a name="return-types"></a>Tipos devueltos  
 **varbinary** con un tamaño máximo de 8.000 bytes.  
  
 Devuelve NULL si la clave no está abierta, si la clave no existe o si se trata de una clave RC4 desusada y la base de datos no está en el nivel de compatibilidad 110 o superior.  
  
## <a name="remarks"></a>Comentarios  
 EncryptByKey usa una clave simétrica. Esta clave debe estar abierta. Si la clave simétrica ya está abierta en la sesión actual, no tiene que abrirla de nuevo en el contexto de la consulta.  
  
 El autenticador le ayudará a impedir la sustitución de todo el valor de los campos cifrados. Por ejemplo, considere la siguiente tabla de datos de nóminas:  
  
|Employee_ID|Standard_Title|Base_Pay|  
|------------------|---------------------|---------------|  
|345|Copy Room Assistant|Fskj%7^edhn00|  
|697|Chief Financial Officer|M0x8900f56543|  
|694|Data Entry Supervisor|Cvc97824%^34f|  
  
 Sin romper el cifrado, un usuario malintencionado puede obtener información importante del contexto en el que se almacena el texto cifrado. Puesto que al Chief Financial Official se le paga más que al Copy Room Assistant, el valor cifrado como M0x8900f56543 debe ser mayor que el valor cifrado como Fskj%7^edhn00. En este caso, cualquier usuario con el permiso ALTER en la tabla puede elevar al Copy Room Assistant al sustituir los datos en su campo Base_Pay con una copia de los datos almacenados en el campo Base_Pay del Chief Financial Officer. Este ataque de sustitución del valor completo omite el cifrado completamente.  
  
 Estos ataques de sustitución de valor completo se pueden combatir agregando información contextual al texto simple antes de cifrarlo. Esta información contextual se usa para comprobar que el texto simple no se ha movido.  
  
 Si se especifica un parámetro de autenticador al cifrar los datos, se necesita el mismo autenticador para descifrar los datos mediante DecryptByKey. En el momento del cifrado, se cifra un hash del autenticador junto con el texto simple. En el momento del descifrado, el mismo autenticador se debe pasar a DecryptByKey. Si los dos no coinciden, se produce un error en el descifrado. Esto indica que el valor se ha movido desde que se cifró. Recomendamos que utilice una columna que contenga un valor único e invariable como autenticador. Si el valor del autenticador cambia, podría perder el acceso a los datos.  
  
 El cifrado y descifrado simétrico es relativamente rápido y se puede adaptar para trabajar con grandes cantidades de datos.  
  
> [!IMPORTANT]  
>  El uso de las funciones de cifrado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] junto con el valor ANSI_PADDING OFF podría provocar la pérdida de datos debido a las conversiones implícitas. Para obtener más información sobre ANSI_PADDING, consulte [SET ANSI_PADDING &#40; Transact-SQL &#41; ](../../t-sql/statements/set-ansi-padding-transact-sql.md).  
  
## <a name="examples"></a>Ejemplos  
 La funcionalidad ilustrada en los ejemplos siguientes se basa en claves y certificados que se crean en [How To: cifrar una columna de datos](../../relational-databases/security/encryption/encrypt-a-column-of-data.md).  
  
### <a name="a-encrypting-a-string-with-a-symmetric-key"></a>A. Cifrar una cadena con una clave simétrica  
 En el ejemplo siguiente se agrega una columna a la tabla `Employee` y, a continuación, se cifra el valor del número de seguridad social almacenado en la columna `NationalIDNumber`.  
  
```  
USE AdventureWorks2012;  
GO  
  
-- Create a column in which to store the encrypted data.  
ALTER TABLE HumanResources.Employee  
    ADD EncryptedNationalIDNumber varbinary(128);   
GO  
  
-- Open the symmetric key with which to encrypt the data.  
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037;  
  
-- Encrypt the value in column NationalIDNumber with symmetric key  
-- SSN_Key_01. Save the result in column EncryptedNationalIDNumber.  
UPDATE HumanResources.Employee  
SET EncryptedNationalIDNumber  
    = EncryptByKey(Key_GUID('SSN_Key_01'), NationalIDNumber);  
GO  
```  
  
### <a name="b-encrypting-a-record-together-with-an-authentication-value"></a>B. Cifrar un registro junto con un valor de autenticación  
  
```  
USE AdventureWorks2012;  
  
-- Create a column in which to store the encrypted data.  
ALTER TABLE Sales.CreditCard.   
    ADD CardNumber_Encrypted varbinary(128);   
GO  
  
-- Open the symmetric key with which to encrypt the data.  
OPEN SYMMETRIC KEY CreditCards_Key11  
    DECRYPTION BY CERTIFICATE Sales09;  
  
-- Encrypt the value in column CardNumber with symmetric   
-- key CreditCards_Key11.  
-- Save the result in column CardNumber_Encrypted.    
UPDATE Sales.CreditCard  
SET CardNumber_Encrypted = EncryptByKey(Key_GUID('CreditCards_Key11'),   
    CardNumber, 1, CONVERT( varbinary, CreditCardID) );  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [DECRYPTBYKEY &#40; Transact-SQL &#41;](../../t-sql/functions/decryptbykey-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [HASHBYTES &#40; Transact-SQL &#41;](../../t-sql/functions/hashbytes-transact-sql.md)  
  
  

