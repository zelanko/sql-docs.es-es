---
title: Sys.symmetric_keys (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- symmetric_keys
- sys.symmetric_keys
- sys.symmetric_keys_TSQL
- symmetric_keys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.symmetric_keys catalog view
ms.assetid: d410eae1-3a52-45de-b9a1-52d2bd93a8eb
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: bf3916f92f71e0d5ca7ec3b1a994b4c9a46bf913
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="syssymmetrickeys-transact-sql"></a>sys.symmetric_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una fila por cada clave simétrica creada con la instrucción CREATE SYMMETRIC KEY.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre de la clave. Es único dentro de la base de datos.|  
|**principal_id**|**int**|Identificador de la entidad de seguridad de la base de datos que posee la clave.|  
|**symmetric_key_id**|**int**|Id. de la clave. Es único en la base de datos.|  
|**longitudDeClave**|**int**|Longitud de la clave, en bits.|  
|**key_algorithm**|**char(2)**|Algoritmo utilizado con la clave:<br /><br /> R2 = RC2<br /><br /> R4 = RC4<br /><br /> D = DES<br /><br /> D3 = Triple DES<br /><br /> DT = TRIPLE_DES_3KEY<br /><br /> DX = DESX<br /><br /> A1 = AES 128<br /><br /> A2 = AES 192<br /><br /> A3 = AES 256<br /><br /> NA = clave EKM|  
|**algorithm_desc**|**nvarchar(60)**|Descripción del algoritmo usado con la clave:<br /><br /> RC2<br /><br /> RC4<br /><br /> DES<br /><br /> Triple_DES<br /><br /> TRIPLE_DES_3KEY<br /><br /> DESX<br /><br /> AES_128<br /><br /> AES_192<br /><br /> AES_256<br /><br /> Descripción de la Administración extensible de claves, solamente los algoritmos (NULL)|  
|**create_date**|**datetime**|Fecha de creación de la clave.|  
|**modify_date**|**datetime**|Fecha de modificación de la clave.|  
|**key_guid**|**uniqueidentifier**|Identificador único global (GUID) asociado a la clave. Se genera automáticamente para claves permanentes. Los GUID para claves temporales se obtienen a partir de la frase de contraseña suministrada por el usuario.|  
|**key_thumbprint**|**sql_variant**|Hash de la tecla 1 SHA. El hash es globalmente único. Para las claves que no sean de Administración extensible de claves, este valor será NULL.|  
|**provider_type**|**nvarchar(120)**|Tipo de proveedor criptográfico:<br /><br /> CRYPTOGRAPHIC PROVIDER = claves de Administración extensible de claves<br /><br /> NULL = Claves que no sean de Administración extensible de claves|  
|**cryptographic_provider_guid**|**uniqueidentifier**|GUID del proveedor criptográfico. Para las claves que no sean de Administración extensible de claves, este valor será NULL.|  
|**cryptographic_provider_algid**|**sql_variant**|Identificador del algoritmo del proveedor criptográfico. Para las claves que no sean de Administración extensible de claves, este valor será NULL.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Comentarios  
 El algoritmo RC4 está obsoleto. [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
> [!NOTE]  
>  El algoritmo RC4 se admite únicamente por razones de compatibilidad con versiones anteriores. El material nuevo solo se puede cifrar con RC4 o RC4_128 cuando la base de datos tenga el nivel de compatibilidad 90 o 100. (No se recomienda). Use un algoritmo más reciente como uno de los algoritmos AES en su lugar. En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] el material cifrado con RC4 o RC4_128 se puede descifrar en cualquier nivel de compatibilidad.  
  
 **Clarificación con respecto a los algoritmos DES:**  
  
-   DESX se denominó incorrectamente. Las claves simétricas creadas con ALGORITHM = DESX realmente utilizan el cifrado TRIPLE DES con una clave de 192 bits. No se proporciona el algoritmo DESX. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
-   Las claves simétricas creadas con ALGORITHM = TRIPLE_DES_3KEY utilizan TRIPLE DES con una clave de 192 bits.  
  
-   Las claves simétricas creadas con ALGORITHM = TRIPLE_DES utilizan TRIPLE DES con una clave de 128 bits.  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Administración extensible de claves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
  
