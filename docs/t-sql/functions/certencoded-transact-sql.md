---
title: CERTENCODED (Transact-SQL) | Documentos de Microsoft
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
- CERTENCODED
- CERTENCODED_TSQL
dev_langs: TSQL
helpviewer_keywords: CERTENCODED
ms.assetid: 677a0719-7b9a-4f0b-bc61-41634563f924
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 635720f8ed9c3d2aa48d2f5cbf03438171b1fe78
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="certencoded-transact-sql"></a>CERTENCODED (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Devuelve la parte pública de un certificado en formato binario. Esta función toma un identificador de certificado y devuelve el certificado codificado. El resultado binario puede pasarse a **crear certificado... CON binario** para crear un nuevo certificado.
  
## <a name="syntax"></a>Sintaxis  
  
```sql
CERTENCODED ( cert_id )  
```  
  
## <a name="arguments"></a>Argumentos  
*cert_id*  
Es el **certificate_id** del certificado. Esta opción está disponible desde sys.certificates o mediante la [CERT_ID &#40; Transact-SQL &#41; ](../../t-sql/functions/cert-id-transact-sql.md) (función). *cert_id* es de tipo **int**
  
## <a name="return-types"></a>Tipos de valor devuelto
**varbinary**
  
## <a name="remarks"></a>Comentarios  
**CERTENCODED** y **CERTPRIVATEKEY** se usan juntas para devolver diferentes partes de un certificado en formato binario.
  
## <a name="permissions"></a>Permissions  
**CERTENCODED** está disponible al público.
  
## <a name="examples"></a>Ejemplos  
  
### <a name="simple-example"></a>Ejemplo sencillo  
En el ejemplo siguiente se crea un certificado denominado `Shipping04` y, a continuación, usa el **CERTENCODED** función para devolver la codificación binaria del certificado.
  
```sql
CREATE DATABASE TEST1;  
GO  
USE TEST1  
CREATE CERTIFICATE Shipping04   
ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
WITH SUBJECT = 'Sammamish Shipping Records',   
EXPIRY_DATE = '20161031';  
GO  
SELECT CERTENCODED(CERT_ID('Shipping04'));  
  
```  
  
### <a name="b-copying-a-certificate-to-another-database"></a>B. Copiar un certificado a otra base de datos  
En el ejemplo más complejo siguiente se crean dos bases de datos, `SOURCE_DB` y `TARGET_DB`. El objetivo es crear un certificado en `SOURCE_DB`, copiarlo en `TARGET_DB` y, después, mostrar que los datos cifrados en `SOURCE_DB` se pueden descifrar en `TARGET_DB` mediante la copia del certificado.
  
Para crear el entorno de ejemplo, cree las bases de datos `SOURCE_DB` y `TARGET_DB` y una clave maestra en cada una. A continuación, cree un certificado en `SOURCE_DB`.
  
```sql
USE master;  
GO  
CREATE DATABASE SOURCE_DB;  
GO  
USE SOURCE_DB;  
GO  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0URCE_DB KEY Pa$$W0rd';  
GO  
CREATE DATABASE TARGET_DB;  
GO  
USE TARGET_DB  
GO  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'Pa$$W0rd in TARGET_DB';  
GO  
  
-- Create a certificate in SOURCE_DB  
USE SOURCE_DB;  
GO  
CREATE CERTIFICATE SOURCE_CERT WITH SUBJECT = 'SOURCE_CERTIFICATE';  
GO  
```  
  
Ahora extraiga la descripción binaria del certificado.
  
```sql
DECLARE @CERTENC VARBINARY(MAX);  
DECLARE @CERTPVK VARBINARY(MAX);  
SELECT @CERTENC = CERTENCODED(CERT_ID('SOURCE_CERT'));  
SELECT @CERTPVK = CERTPRIVATEKEY(CERT_ID('SOURCE_CERT'),  
       'CertEncryptionPa$$word');  
SELECT @CERTENC AS BinaryCertificate;  
SELECT @CERTPVK AS EncryptedBinaryCertificate;  
GO  
```  
  
Cree el certificado duplicado en la base de datos `TARGET_DB`. Debe modificar el código siguiente, insertando los dos valores binarios devueltos en el paso anterior.
  
```sql
-- Create the duplicate certificate in the TARGET_DB database  
USE TARGET_DB  
GO  
CREATE CERTIFICATE TARGET_CERT  
FROM BINARY = <insert the binary value of the @CERTENC variable>  
WITH PRIVATE KEY (  
BINARY = <insert the binary value of the @CERTPVK variable>  
, DECRYPTION BY PASSWORD = 'CertEncryptionPa$$word');  
-- Compare the certificates in the two databases  
-- The two certificates should be the same   
-- except for name and (possibly) the certificate_id  
SELECT * FROM SOURCE_DB.sys.certificates  
UNION  
SELECT * FROM TARGET_DB.sys.certificates;  
```  
  
El siguiente código ejecutado como un solo lote muestra que los datos cifrados en `SOURCE_DB` se pueden descifrar en `TARGET_DB`.
  
```sql
USE SOURCE_DB;  
  
DECLARE @CLEARTEXT nvarchar(100);  
DECLARE @CIPHERTEXT varbinary(8000);  
DECLARE @UNCIPHEREDTEXT_Source nvarchar(100);  
SET @CLEARTEXT = N'Hello World';  
SET @CIPHERTEXT = ENCRYPTBYCERT(CERT_ID('SOURCE_CERT'), @CLEARTEXT);  
SET @UNCIPHEREDTEXT_Source =   
    DECRYPTBYCERT(CERT_ID('SOURCE_CERT'), @CIPHERTEXT)  
-- Encryption and decryption result in SOURCE_DB  
SELECT @CLEARTEXT AS SourceClearText, @CIPHERTEXT AS SourceCipherText,   
       @UNCIPHEREDTEXT_Source AS SourceDecryptedText;  
  
-- SWITCH DATABASE  
USE TARGET_DB;  
  
DECLARE @UNCIPHEREDTEXT_Target nvarchar(100);  
SET @UNCIPHEREDTEXT_Target = DECRYPTBYCERT(CERT_ID('TARGET_CERT'), @CIPHERTEXT);  
-- Encryption and decryption result in TARGET_DB  
SELECT @CLEARTEXT AS ClearTextInTarget, @CIPHERTEXT AS CipherTextInTarget, @UNCIPHEREDTEXT_Target AS DecriptedTextInTarget;   
GO  
```  
  
## <a name="see-also"></a>Vea también
[Funciones de seguridad &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
[CERTPRIVATEKEY &#40; Transact-SQL &#41;](../../t-sql/functions/certprivatekey-transact-sql.md)  
[sys.certificates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)
  
  
