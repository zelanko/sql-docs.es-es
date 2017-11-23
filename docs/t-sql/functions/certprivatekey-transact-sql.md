---
title: CERTPRIVATEKEY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CERTPRIVATEKEY
- CERTPRIVATEKEY_TSQL
dev_langs: TSQL
helpviewer_keywords: CERTPRIVATEKEY
ms.assetid: 33e0f01e-39ac-46da-94ff-fe53b1116df4
caps.latest.revision: "13"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: df513e6ce63ff49e31ad05e5a4dca0372de69c83
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="certprivatekey-transact-sql"></a>CERTPRIVATEKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Devuelve la clave privada de un certificado en formato binario. Esta función toma tres argumentos.
-   Un identificador de certificado.  
-   Una contraseña de cifrado que se utiliza para cifrar los bits de clave privada cuando son devueltos por la función, de modo que las claves no son texto sin cifrar expuesto a los usuarios.  
-   Una contraseña de descifrado que es opcional. Si se especifica una contraseña de descifrado, se utiliza para descifrar la clave privada del certificado; de lo contrario, se utiliza la clave maestra de base de datos.  
  
Solo los usuarios que tienen acceso a la clave privada del certificado podrán utilizar esta función. Esta función devuelve la clave privada en formato PVK.
  
## <a name="syntax"></a>Sintaxis  
  
```sql
CERTPRIVATEKEY   
    (  
          cert_ID   
        , ' encryption_password '   
      [ , ' decryption_password ' ]  
    )  
```  
  
## <a name="arguments"></a>Argumentos  
*certificate_ID*  
Es el **certificate_id** del certificado. Esta opción está disponible desde sys.certificates o mediante la [CERT_ID &#40; Transact-SQL &#41; ](../../t-sql/functions/cert-id-transact-sql.md) (función). *cert_id* es de tipo **int**
  
*encryption_password*  
La contraseña utilizada para cifrar el valor binario devuelto.
  
*decryption_password*  
La contraseña utilizada para descifrar el valor binario devuelto.
  
## <a name="return-types"></a>Tipos de valor devuelto
**varbinary**
  
## <a name="remarks"></a>Comentarios  
**CERTENCODED** y **CERTPRIVATEKEY** se usan juntas para devolver diferentes partes de un certificado en formato binario.
  
## <a name="permissions"></a>Permissions  
**CERTPRIVATEKEY** está disponible al público.
  
## <a name="examples"></a>Ejemplos  
  
```sql
CREATE DATABASE TEST1;  
GO  
USE TEST1  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'Use 5tr0ng P^55Words'  
GO  
CREATE CERTIFICATE Shipping04   
WITH SUBJECT = 'Sammamish Shipping Records',   
EXPIRY_DATE = '20141031';  
GO  
SELECT CERTPRIVATEKEY(CERT_ID('Shipping04'), 'jklalkaa/; uia3dd');  
```  
  
Para obtener un ejemplo más complejo que usa **CERTPRIVATEKEY** y **CERTENCODED** para copiar un certificado en otra base de datos, vea el ejemplo B en el tema [CERTENCODED &#40; Transact-SQL &#41; ](../../t-sql/functions/certencoded-transact-sql.md).
  
## <a name="see-also"></a>Vea también
[Funciones de seguridad &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
[Crear certificado &#40; Transact-SQL &#41; ](../../t-sql/statements/create-certificate-transact-sql.md) 
 [Funciones de seguridad &#40; Transact-SQL &#41; ](../../t-sql/functions/security-functions-transact-sql.md) 
 [sys.certificates &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)
  
  
