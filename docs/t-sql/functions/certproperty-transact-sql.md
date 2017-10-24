---
title: CERTPROPERTY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CERTPROPERTY
- CERTPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- certificates [SQL Server], schema names
- schemas [SQL Server], names
- CERTPROPERTY function
ms.assetid: 966c09aa-bc4e-45b0-ba53-c8381871f638
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4b43b587688b574c6d6395b72c5b368b82e617fd
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="certproperty-transact-sql"></a>CERTPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve el valor de una propiedad de certificado especificada.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
CertProperty ( Cert_ID , '<PropertyName>' )  
  
<PropertyName> ::=  
   Expiry_Date | Start_Date | Issuer_Name   
   | Cert_Serial_Number | Subject | SID | String_SID   
```  
  
## <a name="arguments"></a>Argumentos  
*Cert_ID*  
Es el id. del certificado. *Cert_ID* es de tipo int.
  
*Expiry_Date*  
Es la fecha de expiración del certificado.
  
*Start_Date*  
Es la fecha en que el certificado pasa a ser válido.
  
*Issuer_Name*  
Es el nombre del emisor del certificado.
  
*Cert_Serial_Number*  
Es el número de serie del certificado.
  
*Asunto*  
Es el asunto del certificado.
  
 *SID*  
Es el SID del certificado. También es el SID de cualquier inicio de sesión o usuario asignado a este certificado.
  
*String_SID*  
Es el SID del certificado como una cadena de caracteres. También es el SID de cualquier inicio de sesión o usuario asignado al certificado.
  
## <a name="return-types"></a>Tipos de valor devuelto
La especificación de propiedad debe estar entre comillas simples.
  
El tipo devuelto depende de la propiedad especificada en la llamada de función. Todos los valores devuelven se agrupan en el tipo de valor devuelto de **sql_variant**.
-   *Expiry_Date* y *Start_Date* devolver **datetime**.  
-   *Cert_Serial_Number*, *Issuer_Name*, *asunto*, y *String_SID* devolver **nvarchar**.  
-   *SID* devuelve **varbinary**.  
  
## <a name="remarks"></a>Comentarios  
Información acerca de los certificados es visible en el [sys.certificates](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md) vista de catálogo.
  
## <a name="permissions"></a>Permissions  
Requiere algunos permisos en el certificado y que el llamador no tenga denegado el permiso VIEW DEFINITION en el certificado.
  
## <a name="examples"></a>Ejemplos  
En el siguiente ejemplo se devuelve el asunto del certificado.
  
```sql
-- First create a certificate.  
CREATE CERTIFICATE Marketing19 WITH   
    START_DATE = '04/04/2004' ,  
    EXPIRY_DATE = '07/07/2007' ,  
    SUBJECT = 'Marketing Print Division';  
GO  
  
-- Now use CertProperty to examine certificate  
-- Marketing19's properties.  
DECLARE @CertSubject sql_variant;  
set @CertSubject = CertProperty( Cert_ID('Marketing19'), 'Subject');  
PRINT CONVERT(nvarchar, @CertSubject);  
GO  
```  
  
## <a name="see-also"></a>Vea también
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
[ALTER CERTIFICATE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)  
[CERT_ID &#40; Transact-SQL &#41; ](../../t-sql/functions/cert-id-transact-sql.md) 
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)
[sys.certificates &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md) 
 [Vistas de catálogo de seguridad &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)
  
  

