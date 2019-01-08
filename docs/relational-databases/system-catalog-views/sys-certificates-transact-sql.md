---
title: Sys.Certificates (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- certificates
- certificates_TSQL
- sys.certificates_TSQL
- sys.certificates
dev_langs:
- TSQL
helpviewer_keywords:
- sys.certificates catalog view
ms.assetid: e5046102-a65c-401e-b80d-05636884dec9
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 634fbc4ddd96fd407aa124c98ae2b55897edaa71
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52391233"
---
# <a name="syscertificates-transact-sql"></a>sys.certificates (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una fila por cada certificado en la base de datos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre del certificado. Es único en la base de datos.|  
|**certificate_id**|**int**|Id. del certificado. Es único en la base de datos.|  
|**principal_id**|**int**|Id. de la entidad de seguridad de la base de datos que posee este certificado.|  
|**pvt_key_encryption_type**|**char(2)**|Indica cómo se ha cifrado la clave privada.<br /><br /> NA = No hay clave privada para el certificado<br /><br /> MK = La clave privada se ha cifrado mediante la clave maestra<br /><br /> PW = La clave privada se ha cifrado mediante una contraseña definida por el usuario<br /><br /> SK = La clave privada se ha cifrado mediante la clave maestra del servicio|  
|**pvt_key_encryption_type_desc**|**nvarchar(60)**|Descripción de cómo se ha cifrado la clave privada.<br /><br /> NO_PRIVATE_KEY<br /><br /> ENCRYPTED_BY_MASTER_KEY<br /><br /> ENCRYPTED_BY_PASSWORD<br /><br /> ENCRYPTED_BY_SERVICE_MASTER_KEY|  
|**is_active_for_begin_dialog**|**bit**|Si el valor es 1, este certificado se utiliza para iniciar diálogos de servicio cifrados.|  
|**issuer_name**|**nvarchar(442)**|Nombre del emisor del certificado.|  
|**cert_serial_number**|**Nvarchar (64)**|Número de serie del certificado.|  
|**SID**|**varbinary(85)**|SID (identificador de seguridad) de inicio de sesión para este certificado.|  
|**string_sid**|**nvarchar(128)**|Representación en forma de cadena del SID de inicio de sesión para este certificado.|  
|**Asunto**|**nvarchar(4000)**|Asunto del certificado.|  
|**expiry_date**|**datetime**|Fecha en que expira el certificado.|  
|**start_date**|**datetime**|Fecha en que se valida el certificado.|  
|**Huella digital**|**varbinary(32)**|Hash SHA-1 del certificado. El hash SHA-1 es único globalmente.|  
|**attested_by**|**nvarchar(260)**|Solo para uso del sistema.|  
|pvt_key_last_backup_date|**datetime**|La fecha y la hora que clave privada del certificado se exportó por última vez.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
  
  
