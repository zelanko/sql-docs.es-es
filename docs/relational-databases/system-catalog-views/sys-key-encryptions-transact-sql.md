---
title: Sys.key_encryptions (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.key_encryptions
- key_encryptions_TSQL
- sys.key_encryptions_TSQL
- key_encryptions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.key_encryptions catalog view
ms.assetid: c39cecf8-af63-40b9-98e5-f84a5bf3ae54
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: c41272a595304a309e1dbb5a13bd5b03460613f0
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39545905"
---
# <a name="syskeyencryptions-transact-sql"></a>sys.key_encryptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve una fila por cada cifrado de clave simétrica especificado mediante el uso de la cláusula ENCRYPTION BY de la instrucción CREATE SYMMETRIC KEY.  

  
|Nombres de columna|Tipos de datos|Descripción|  
|------------------|----------------|-----------------|  
|**key_id**|**int**|Id. de la clave cifrada.|  
|**Huella digital**|**varbinary(32)**|Hash SHA-1 del certificado o GUID de la clave simétrica con el que se cifra la clave.|  
|**crypt_type**|**(4)**|Tipo de cifrado:<br /><br /> ESKS = Cifrado mediante clave simétrica<br /><br /> ESP3, ESP2 o ESKP = cifrado mediante contraseña<br /><br /> EPUC = Cifrado mediante certificado<br /><br /> EPUA = Cifrado mediante clave asimétrica<br /><br /> ESKM = Cifrado mediante clave maestra|  
|**crypt_type_desc**|**nvarchar(60)**|Descripción del tipo de cifrado:<br /><br /> ENCRYPTION BY SYMMETRIC KEY<br /><br /> ENCRYPTION BY PASSWORD <br />(A partir [!INCLUDE[sssqlv14_md](../../includes/sssqlv14-md.md)], incluye un número de versión para su uso por CSS.)<br /><br /> ENCRYPTION BY CERTIFICATE<br /><br /> ENCRYPTION BY ASYMMETRIC KEY<br /><br /> ENCRYPTION BY MASTER KEY<br /><br /> Nota: Se usan Windows DPAPI para proteger la clave maestra de servicio.|  
|**crypt_property**|**varbinary(max)**|Bits firmados o cifrados.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
  
