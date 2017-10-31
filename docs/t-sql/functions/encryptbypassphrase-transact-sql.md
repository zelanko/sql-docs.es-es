---
title: ENCRYPTBYPASSPHRASE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ENCRYPTBYPASSPHRASE
- ENCRYPTBYPASSPHRASE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTBYPASSPHRASE function
- encryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], ENCRYPTBYPASSPHRASE function
ms.assetid: f8dbb9e6-94d6-40d7-8b38-6833a409d597
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ddfbea4ac550f21787eb88db6119c391f2b1b85a
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="encryptbypassphrase-transact-sql"></a>ENCRYPTBYPASSPHRASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Cifra datos mediante una frase de contraseña usando el algoritmo TRIPLE DES con una longitud de clave de 128 bits.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
EncryptByPassPhrase ( { 'passphrase' | @passphrase }   
    , { 'cleartext' | @cleartext }  
  [ , { add_authenticator | @add_authenticator }  
    , { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *frase de contraseña*  
 Frase de contraseña a partir de la cual se genera una clave simétrica.  
  
 @passphrase  
 Una variable de tipo **nvarchar**, **char**, **varchar**, **binario**, **varbinary**, o **nchar** que contiene una frase de contraseña desde el que se va a generar una clave simétrica.  
  
 *texto no cifrado*  
 Texto no cifrado que se va a cifrar.  
  
 @cleartext  
 Una variable de tipo **nvarchar**, **char**, **varchar**, **binario**, **varbinary**, o **nchar** que contiene el texto sin cifrar. El tamaño máximo es de 8.000 bytes.  
  
 *add_authenticator*  
 Indica si se cifrará un autenticador junto con el texto sin cifrar. 1 si se va a agregar un autenticador. **int**.  
  
 @add_authenticator  
 Indica si se cifrará un hash junto con el texto no cifrado.  
  
 *autenticador*  
 Datos a partir de los cuales se obtiene un autenticador. **sysname**.  
  
 @authenticator  
 Variable que contiene datos a partir de los cuales se obtiene un autenticador.  
  
## <a name="return-types"></a>Tipos devueltos  
 **varbinary** con un tamaño máximo de 8.000 bytes.  
  
## <a name="remarks"></a>Comentarios  
 Una frase de contraseña es una contraseña que incluye espacios. La ventaja de usar una frase de contraseña es que es más fácil recordar una frase con significado que una cadena larga de caracteres.  
  
 Esta función no comprueba la complejidad de la contraseña.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se actualiza un registro de la tabla `SalesCreditCard` y se cifra el valor del número de la tarjeta de crédito almacenado en la columna `CardNumber_EncryptedbyPassphrase` utilizando la clave principal como un autenticador.  
  
```  
USE AdventureWorks2012;  
GO  
-- Create a column in which to store the encrypted data.  
ALTER TABLE Sales.CreditCard   
    ADD CardNumber_EncryptedbyPassphrase varbinary(256);   
GO  
-- First get the passphrase from the user.  
DECLARE @PassphraseEnteredByUser nvarchar(128);  
SET @PassphraseEnteredByUser   
    = 'A little learning is a dangerous thing!';  
  
-- Update the record for the user's credit card.  
-- In this case, the record is number 3681.  
UPDATE Sales.CreditCard  
SET CardNumber_EncryptedbyPassphrase = EncryptByPassPhrase(@PassphraseEnteredByUser  
    , CardNumber, 1, CONVERT( varbinary, CreditCardID))  
WHERE CreditCardID = '3681';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [DECRYPTBYPASSPHRASE &#40; Transact-SQL &#41;](../../t-sql/functions/decryptbypassphrase-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

