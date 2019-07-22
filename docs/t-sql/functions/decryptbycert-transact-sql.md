---
title: DECRYPTBYCERT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DecryptByCert_TSQL
- DECRYPTBYCERT
dev_langs:
- TSQL
helpviewer_keywords:
- certificates [SQL Server], decryption
- decryption [SQL Server], certificates
- DECRYPTBYCERT function
ms.assetid: 4950d787-40fa-4e26-bce8-2cb2ceca12fb
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: febf3a874ba0632c90117d52e74ce31926bfbbc3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118950"
---
# <a name="decryptbycert-transact-sql"></a>DECRYPTBYCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

En esta función se usa la clave privada de un certificado para descifrar los datos cifrados.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DecryptByCert ( certificate_ID , { 'ciphertext' | @ciphertext }   
    [ , { 'cert_password' | @cert_password } ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *certificate_ID*  
Id. de un certificado de la base de datos. *certificate_ID* tiene un tipo de datos **int**.  
  
 *ciphertext*  
La cadena de datos cifrados con la clave pública del certificado.  
  
 @ciphertext  
Una variable de tipo **varbinary** que contiene los datos cifrados con el certificado.  
  
 *cert_password*  
La contraseña que se usa para cifrar la clave privada del certificado. *cert_password* debe tener un formato de datos Unicode.  
  
 @cert_password  
Una variable de tipo **nchar** o **nvarchar** que contiene la contraseña que se usa para cifrar la clave privada del certificado. *@cert_password* debe tener un formato de datos Unicode.  

## <a name="return-types"></a>Tipos devueltos  
**varbinary**, con un tamaño máximo de 8 000 bytes.  
  
## <a name="remarks"></a>Notas  
Esta función descifra datos con la clave privada de un certificado. Las transformaciones cifradas que utilizan claves asimétricas consumen gran cantidad de recursos. Por tanto, se recomienda que los desarrolladores eviten el uso de [ENCRYPTBYCERT](./encryptbycert-transact-sql.md) y DECRYPTBYCERT para el cifrado y descifrado de datos de usuario rutinarios.  

## <a name="permissions"></a>Permisos  
`DECRYPTBYCERT` requiere el permiso CONTROL en el certificado.  
  
## <a name="examples"></a>Ejemplos  
En este ejemplo se seleccionan filas de `[AdventureWorks2012].[ProtectedData04]` marcadas como datos que originalmente se cifraron mediante el certificado `JanainaCert02`. En el ejemplo, primero se descifra la clave privada del certificado `JanainaCert02` con la contraseña del certificado `pGFD4bb925DGvbd2439587y`. Después, en el ejemplo se descifra el texto cifrado con esta clave privada. En el ejemplo, los datos descifrados se convierten de **varbinary** a **nvarchar**.  

```  
SELECT convert(nvarchar(max), DecryptByCert(Cert_Id('JanainaCert02'),  
    ProtectedData, N'pGFD4bb925DGvbd2439587y'))  
FROM [AdventureWorks2012].[ProtectedData04]   
WHERE Description   
    = N'data encrypted by certificate '' JanainaCert02''';  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [ENCRYPTBYCERT &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbycert-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
