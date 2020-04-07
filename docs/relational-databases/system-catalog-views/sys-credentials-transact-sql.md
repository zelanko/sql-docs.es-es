---
title: sys.credentials (Transact-SQL) Microsoft Docs
ms.custom: ''
ms.date: 04/06/2020
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.credentials
- sys.credentials_TSQL
- credentials_TSQL
- credentials
dev_langs:
- TSQL
helpviewer_keywords:
- sys.credentials catalog view
ms.assetid: ea48cf80-904a-4273-a950-6d35b1b0a1b6
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f87378897256f8b4fae26b30263577bedede6175
ms.sourcegitcommit: c6a2efe551e37883c1749bdd9e3c06eb54ccedc9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2020
ms.locfileid: "80752887"
---
# <a name="syscredentials-transact-sql"></a>sys.credentials (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdbmi-asdw-pdw-md.md)]

  Devuelve una fila por cada credencial de nivel de servidor.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|credential_id|**int**|Identificador de la credencial. Es único en el servidor.|  
|name|**sysname**|Nombre de la credencial. Es único en el servidor.|  
|credential_identity|**nvarchar(4000)**|Nombre de la identidad que se va a utilizar. Suele ser un usuario de Windows. No tiene que ser único.|  
|create_date|**datetime**|Fecha y hora en que se creó la credencial.|  
|modify_date|**datetime**|Fecha y hora en que se modificó la credencial por última vez.|  
|target_type|**nvarchar(100)**|Tipo de credencial. Devuelve NULL para las credenciales tradicionales y CRYPTOGRAPHIC PROVIDER para las credenciales asignadas a un proveedor criptográfico. Para obtener más información acerca de los proveedores de administración de claves externos, vea Administración extensible de claves [&#40;&#41;EKM ](../../relational-databases/security/encryption/extensible-key-management-ekm.md).|  
|target_id|**int**|Identificador del objeto al que está asignada la credencial. Devuelve 0 para las credenciales tradicionales y un valor distinto de 0 para las credenciales asignadas a un proveedor criptográfico. Para obtener más información acerca de los proveedores de administración de claves externos, vea Administración extensible de claves [&#40;&#41;EKM ](../../relational-databases/security/encryption/extensible-key-management-ekm.md).|  

## <a name="remarks"></a>Observaciones  
Para obtener las credenciales de nivel de base de datos, consulte [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md).
  
## <a name="permissions"></a>Permisos  
 Requiere `VIEW ANY DEFINITION` permiso o `ALTER ANY CREDENTIAL` permiso. Además, no se debe `VIEW ANY DEFINITION` denegar el permiso a la entidad de seguridad.  
  
## <a name="see-also"></a>Consulte también  
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [Credenciales &#40;Motor de base de datosDatabase Engine&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [Las vistas del catálogo de seguridad &#40;&#41;de Transact-SQLTransact-SQL](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [&#41;de Motor de base de datos &#40;principales](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)  
  
  
