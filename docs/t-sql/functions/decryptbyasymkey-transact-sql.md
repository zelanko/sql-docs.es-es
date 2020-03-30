---
title: DECRYPTBYASYMKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECRYPTBYASYMKEY
- DECRYPTBYASYMKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], DECRYPTBYASYMKEY function
- DECRYPTBYASYMKEY function
- decryption [SQL Server], asymmetric keys
ms.assetid: d9ebcd30-f01c-4cfe-b95e-ffe6ea13788b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c187caf0dc0027d6d7fa86cbd1bee09e76f0228d
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68118961"
---
# <a name="decryptbyasymkey-transact-sql"></a>DECRYPTBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

En esta función se usa una clave asimétrica para descifrar los datos cifrados.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DecryptByAsymKey (Asym_Key_ID , { 'ciphertext' | @ciphertext }   
    [ , 'Asym_Key_Password' ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Asym_Key_ID*  
Id. de una clave asimétrica en la base de datos. *Asym_Key_ID* tiene un tipo de datos **int**.  
  
 *ciphertext*  
La cadena de datos cifrados con la clave asimétrica.  
  
 @ciphertext  
Una variable de tipo **varbinary** que contiene los datos cifrados con la clave asimétrica.  
  
 *Asym_Key_Password*  
La contraseña que se usa para cifrar la clave asimétrica en la base de datos.  
  
## <a name="return-types"></a>Tipos de valor devuelto  
**varbinary**, con un tamaño máximo de 8 000 bytes.  
  
## <a name="remarks"></a>Observaciones  
En comparación con el cifrado y descifrado simétricos, el cifrado y descifrado de claves asimétricas tiene un coste más elevado. Cuando se trabaja con grandes conjuntos de datos (por ejemplo, datos de usuario almacenados en tablas), se recomienda que los desarrolladores eviten el cifrado y descifrado de claves asimétricas.  
  
## <a name="permissions"></a>Permisos  
`DECRYPTBYASYMKEY` requiere el permiso CONTROL en la clave asimétrica.  
  
## <a name="examples"></a>Ejemplos  
En este ejemplo se descifra texto que originalmente se cifró con la clave asimétrica `JanainaAsymKey02`. Esta clave asimétrica se almacenó en `AdventureWorks2012.ProtectedData04`. En el ejemplo se descifran los datos devueltos con la clave asimétrica `JanainaAsymKey02`. En el ejemplo se usa la contraseña `pGFD4bb925DGvbd2439587y` para descifrar esta clave asimétrica. En el ejemplo se convierte el texto sin formato devuelto al tipo **nvarchar**.  
  
```  
SELECT CONVERT(nvarchar(max),  
    DecryptByAsymKey( AsymKey_Id('JanainaAsymKey02'),   
    ProtectedData, N'pGFD4bb925DGvbd2439587y' ))   
AS DecryptedData   
FROM [AdventureWorks2012].[Sales].[ProtectedData04]   
WHERE Description = N'encrypted by asym key''JanainaAsymKey02''';  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [ENCRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [Elegir un algoritmo de cifrado](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
