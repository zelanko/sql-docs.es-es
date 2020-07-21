---
title: Sys. sql_logins (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sql_logins_TSQL
- sql_logins_TSQL
- sys.sql_logins
- sql_logins
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_logins catalog view
ms.assetid: 0d9c5b09-86fe-40ff-baab-00b7c051402f
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c3dba46f4d0e2ecdebda13fe3fe9412219c2a755
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "79448475"
---
# <a name="syssql_logins-transact-sql"></a>sys.sql_logins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  Devuelve una fila para cada inicio de sesión para la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**\<columnas heredadas>**|--|Hereda de **Sys. server_principals**.|  
|**is_policy_checked**|**bit**|Se comprueba la directiva de contraseñas.|  
|**is_expiration_checked**|**bit**|Se comprueba la expiración de contraseñas.|  
|**password_hash**|**varbinary (256)**|Hash de la contraseña de inicio de sesión de SQL. A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], la información de la contraseña almacenada se calcula con las funciones SHA-512 de la contraseña salada.|  
  
 Para obtener una lista de las columnas que hereda esta vista, vea [Sys. server_principals &#40;&#41;de Transact-SQL ](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md). Las columnas `owning_principal_id` y `is_fixed_role` no se heredan de sys. server_principals.
  
## <a name="remarks"></a>Observaciones  
 Para ver los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicios de sesión de autenticación de y los inicios de sesión de autenticación de Windows, vea [sys. server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md).  
  
 Cuando los usuarios de base de datos independiente están habilitados, las conexiones se pueden realizar sin inicios de sesión. Para identificar esas cuentas, vea [Sys. database_principals &#40;&#41;de Transact-SQL ](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
 Cualquier inicio de sesión para la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede ver su propio nombre de inicio de sesión y el de sa. Para ver otros inicios de sesión, se requiere ALTER ANY LOGIN o un permiso en el inicio de sesión.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Directiva de contraseñas](../../relational-databases/security/password-policy.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
