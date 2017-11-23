---
title: Sys.sql_logins (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 01/20/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sql_logins_TSQL
- sql_logins_TSQL
- sys.sql_logins
- sql_logins
dev_langs: TSQL
helpviewer_keywords: sys.sql_logins catalog view
ms.assetid: 0d9c5b09-86fe-40ff-baab-00b7c051402f
caps.latest.revision: "43"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 12dcc799255ebc44ed2b8d6401de80a98d83bcbb
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="syssqllogins-transact-sql"></a>sys.sql_logins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  Devuelve una fila para cada inicio de sesión para la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**\<hereda columnas >**|--|Hereda de **sys.server_principals**.|  
|**is_policy_checked**|**bit**|Se comprueba la directiva de contraseñas.|  
|**is_expiration_checked**|**bit**|Se comprueba la expiración de contraseñas.|  
|**password_hash**|**varbinary(256)**|Hash de la contraseña de inicio de sesión de SQL. A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]almacenadas información de contraseña se calcula con SHA-512 de la contraseña con sal.|  
  
 Para obtener una lista de columnas que hereda esta vista, consulte [sys.server_principals &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md).  
  
## <a name="remarks"></a>Comentarios  
 Para ver ambos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicios de sesión de autenticación y los inicios de sesión de autenticación de Windows, vea [sys.server_principals &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md).  
  
 Cuando lo contiene están habilitados los usuarios de base de datos, las conexiones pueden realizarse sin inicios de sesión. Para identificar esas cuentas, vea [sys.database_principals &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Cualquier inicio de sesión para la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede ver su propio nombre de inicio de sesión y el de sa. Para ver otros inicios de sesión, se requiere ALTER ANY LOGIN o un permiso en el inicio de sesión.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Directiva de contraseñas](../../relational-databases/security/password-policy.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
