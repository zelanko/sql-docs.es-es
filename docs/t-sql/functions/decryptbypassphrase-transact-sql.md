---
title: DECRYPTBYPASSPHRASE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
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
- DECRYPTBYPASSPHRASE
- DECRYPTBYPASSPHRASE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- decryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], DECRYPTBYPASSPHRASE function
- DECRYPTBYPASSPHRASE function
ms.assetid: ca34b5cd-07b3-4dca-b66a-ed8c6a826c95
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0af2f19acced57d722427c8f341db62dbdb34198
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="decryptbypassphrase-transact-sql"></a>DECRYPTBYPASSPHRASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Descifra los datos que se cifraron con una frase de contraseña.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DecryptByPassPhrase ( { 'passphrase' | @passphrase }   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }  
    , { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *frase de contraseña*  
 Frase de contraseña que se utilizará para generar la clave para el descifrado.  
  
 @passphrase  
 Es una variable de tipo **nvarchar**, **char**, **varchar**, o **nchar** que contiene la frase de contraseña que se utilizará para generar la clave para descifrado.  
  
 '*texto cifrado*'  
 Es el texto cifrado que hay que descifrar.  
  
 @ciphertext  
 Es una variable de tipo **varbinary** que contiene el texto cifrado. El tamaño máximo es 8.000 bytes.  
  
 *add_authenticator*  
 Indica si se ha cifrado un autenticador junto con el texto simple. Es 1 si se ha utilizado un autenticador. **int**.  
  
 @add_authenticator  
 Indica si se ha cifrado un autenticador junto con el texto simple. Es 1 si se ha utilizado un autenticador. **int**.  
  
 *autenticador*  
 Son los datos del autenticador. **sysname**.  
  
 @authenticator  
 Es una variable que contiene los datos de los que se derivará un autenticador.  
  
## <a name="return-types"></a>Tipos devueltos  
 **varbinary** con un tamaño máximo de 8.000 bytes.  
  
## <a name="remarks"></a>Comentarios  
 No es necesario ningún permiso para ejecutar esta función.  
  
 Devuelve NULL si se utiliza la información de autenticador o frase de contraseña errónea.  
  
 La frase de contraseña se utiliza para generar una clave de descifrado, que no será permanente.  
  
 Si al cifrar el texto cifrado se incluyó un autenticador, éste debe incluirse en el momento del descifrado. Si el valor del autenticador proporcionado en el momento del descifrado no coincide con el valor cifrado con los datos, se producirá un error en el descifrado.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se descifra el registro actualizado en [EncryptByPassPhrase](../../t-sql/functions/encryptbypassphrase-transact-sql.md).  
  
```  
USE AdventureWorks2012;  
-- Get the pass phrase from the user.  
DECLARE @PassphraseEnteredByUser nvarchar(128);  
SET @PassphraseEnteredByUser   
= 'A little learning is a dangerous thing!';  
  
-- Decrypt the encrypted record.  
SELECT CardNumber, CardNumber_EncryptedbyPassphrase   
    AS 'Encrypted card number', CONVERT(nvarchar,  
    DecryptByPassphrase(@PassphraseEnteredByUser, CardNumber_EncryptedbyPassphrase, 1   
    , CONVERT(varbinary, CreditCardID)))  
    AS 'Decrypted card number' FROM Sales.CreditCard   
    WHERE CreditCardID = '3681';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Elegir un algoritmo de cifrado](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [ENCRYPTBYPASSPHRASE &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbypassphrase-transact-sql.md)  
  
  

