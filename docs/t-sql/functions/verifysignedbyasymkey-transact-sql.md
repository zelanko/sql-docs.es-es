---
description: VERIFYSIGNEDBYASYMKEY (Transact-SQL)
title: VERIFYSIGNEDBYASYMKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- VERIFYSIGNEDBYASYMKEY_TSQL
- VERIFYSIGNEDBYASYMKEY
dev_langs:
- TSQL
helpviewer_keywords:
- verifying digitally signed data for changes
- VERIFYSIGNEDBYASYMKEY
- testing digitally signed data for changes
- checking digitally signed data for changes
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 9f7c6e0b-5ba4-4dbb-994d-5bd59f4908de
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0257bd8b66a915ec5d7f0b59e3aa85f197f38867
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88362251"
---
# <a name="verifysignedbyasymkey-transact-sql"></a>VERIFYSIGNEDBYASYMKEY (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Comprueba si se han cambiado los datos firmados digitalmente desde que se firmaron.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
VerifySignedByAsymKey( Asym_Key_ID , clear_text , signature )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *Asym_Key_ID*  
 Es el identificador de un certificado de clave asimétrica en la base de datos.  
  
 *clear_text*  
 Son los datos de texto no cifrado que se van a comprobar.  
  
 *firma*  
 Es la firma adjunta a los datos firmados. *signature* es **varbinary**.  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 **int**  
  
 Devuelve 1 cuando las firmas coinciden; de lo contrario devuelve 0.  
  
## <a name="remarks"></a>Comentarios  
 **VerifySignedByAsymKey** descifra la firma de los datos utilizando la clave pública de la clave asimétrica especificada y compara el valor descifrado con un hash MD5 calculado recientemente de los datos. Si los valores coinciden, se confirma que la firma es válida.  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso VIEW DEFINITION en la clave asimétrica.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-testing-for-data-with-a-valid-signature"></a>A. Comprobar datos con una firma válida  
 En el siguiente ejemplo se devuelve 1 si los datos seleccionados no se han cambiado desde que se firmaron con la clave asimétrica `WillisKey74`. El ejemplo devuelve 0 si los datos no se han modificado.  
  
```  
SELECT Data,  
     VerifySignedByAsymKey( AsymKey_Id( 'WillisKey74' ), SignedData,  
     DataSignature ) as IsSignatureValid  
FROM [AdventureWorks2012].[SignedData04]   
WHERE Description = N'data encrypted by asymmetric key ''WillisKey74''';  
GO  
RETURN;  
```  
  
### <a name="b-returning-a-result-set-that-contains-data-with-a-valid-signature"></a>B. Devolver un conjunto de resultados que contiene datos con una firma válida  
 En el siguiente ejemplo se devuelven las filas de `SignedData04` que contienen datos que no se han cambiado desde que se firmaron con la clave asimétrica `WillisKey74`. El ejemplo llama a la función `AsymKey_ID` para obtener el identificador de la clave asimétrica de la base de datos.  
  
```  
SELECT Data   
FROM [AdventureWorks2012].[SignedData04]   
WHERE VerifySignedByAsymKey( AsymKey_Id( 'WillisKey74' ), Data,  
     DataSignature ) = 1  
AND Description = N'data encrypted by asymmetric key ''WillisKey74''';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [ASYMKEY_ID &#40;Transact-SQL&#41;](../../t-sql/functions/asymkey-id-transact-sql.md)   
 [SIGNBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/signbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
