---
title: Sys.Credentials (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 02/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: eb947ed99a99bffaad56f912213d6a14f618c326
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="syscredentials-transact-sql"></a>sys.credentials (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Devuelve una fila por cada credencial de nivel de servidor.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|credential_id|**int**|Identificador de la credencial. Es único en el servidor.|  
|name|**sysname**|Nombre de la credencial. Es único en el servidor.|  
|credential_identity|**nvarchar(4000)**|Nombre de la identidad que se va a utilizar. Suele ser un usuario de Windows. No tiene que ser único.|  
|create_date|**datetime**|Fecha y hora en que se creó la credencial.|  
|modify_date|**datetime**|Fecha y hora en que se modificó la credencial por última vez.|  
|target_type|**nvarchar (100)**|Tipo de credencial. Devuelve NULL para las credenciales tradicionales y CRYPTOGRAPHIC PROVIDER para las credenciales asignadas a un proveedor criptográfico. Para obtener más información acerca de los proveedores de administración de claves externas, vea [administración Extensible de claves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md).|  
|target_id|**int**|Identificador del objeto al que está asignada la credencial. Devuelve 0 para las credenciales tradicionales y un valor distinto de 0 para las credenciales asignadas a un proveedor criptográfico. Para obtener más información acerca de los proveedores de administración de claves externas, vea [administración Extensible de claves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md).|  

## <a name="remarks"></a>Comentarios  
Para las credenciales de nivel de base de datos, vea [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md).
  
## <a name="permissions"></a>Permissions  
 Las necesita palabras clave `VIEW ANY DEFINITION` permiso o `ALTER ANY CREDENTIAL` permiso. Además, la entidad de seguridad no se debe denegar `VIEW ANY DEFINITION` permiso.  
  
## <a name="see-also"></a>Vea también  
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [Credenciales &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)  
  
  
