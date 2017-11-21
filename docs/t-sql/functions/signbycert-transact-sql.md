---
title: SIGNBYCERT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
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
- SIGNBYCERT
- SIGNBYCERT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- text signing [SQL Server]
- encryption [SQL Server], certificates
- certificates [SQL Server], text signing
- SignByCert function
- signing text [SQL Server]
- SIGNBYCERT function
- cryptography [SQL Server], certificates
ms.assetid: b4c6bced-4473-4bae-85b9-56deced495f9
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b753e29b576d70b8c77dc40b570ab10dc314f22e
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="signbycert-transact-sql"></a>SIGNBYCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Firma texto con un certificado y devuelve la firma.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SignByCert ( certificate_ID , @cleartext [ , 'password' ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *certificate_ID*  
 Id. de un certificado de la base de datos actual. *certificate_ID* es **int**.  
  
 *@cleartext*  
 Es una variable de tipo **nvarchar**, **char**, **varchar**, o **nchar** que contiene los datos que se firmará.  
  
 **'** *contraseña* **'**  
 Es la contraseña con la que se cifró la clave privada del certificado. *contraseña* es **nvarchar (128)**.  
  
## <a name="return-types"></a>Tipos devueltos  
 **varbinary** con un tamaño máximo de 8.000 bytes.  
  
## <a name="remarks"></a>Comentarios  
 Requiere el permiso CONTROL en el certificado.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se firma el texto `@SensitiveData` con certificado `ABerglundCert07`, descifrar el certificado con la contraseña "pGFD4bb925DGvbd2439587y". A continuación, se inserta el texto sin cifrar y la firma en la tabla `SignedData04`.  
  
```  
DECLARE @SensitiveData nvarchar(max);  
SET @SensitiveData = N'Saddle Price Points are   
    2, 3, 5, 7, 11, 13, 17, 19, 23, 29';  
INSERT INTO [SignedData04]  
    VALUES( N'data signed by certificate ''ABerglundCert07''',  
    @SensitiveData, SignByCert( Cert_Id( 'ABerglundCert07' ),   
    @SensitiveData, N'pGFD4bb925DGvbd2439587y' ));  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [VERIFYSIGNEDBYCERT &#40; Transact-SQL &#41;](../../t-sql/functions/verifysignedbycert-transact-sql.md)   
 [CERT_ID &#40; Transact-SQL &#41;](../../t-sql/functions/cert-id-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [Eliminar certificado &#40; Transact-SQL &#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

