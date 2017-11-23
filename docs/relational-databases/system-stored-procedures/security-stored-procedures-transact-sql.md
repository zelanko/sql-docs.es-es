---
title: Seguridad procedimientos almacenados (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
dev_langs: TSQL
helpviewer_keywords:
- system stored procedures [SQL Server], security
- stored procedures [SQL Server], security
- security [SQL Server], stored procedures
ms.assetid: 62b72907-7e95-4c97-9891-0c45d5b678ce
caps.latest.revision: "22"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 59a87a888f23e722857952d6cdacb6165a092805
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="security-stored-procedures-transact-sql"></a>Procedimientos almacenados de seguridad (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]admite el sistema siguiente procedimientos almacenados que se utilizan para administrar la seguridad. Algunos de estos procedimientos almacenados están en desuso pero siguen estando disponibles para la compatibilidad con versiones anteriores. Los temas correspondientes a procedimientos desusados indicarán su reemplazo.  

|||  
|-|-|  
[Sys.sp_add_trusted_assembly]( sys-sp-add-trusted-assembly-transact-sql.md) |[sp_addapprole](../../relational-databases/system-stored-procedures/sp-addapprole-transact-sql.md) (obsoleto)|
|[sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)|[sp_addlinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)
|[sp_addlogin](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md) (obsoleto) |[sp_addremotelogin](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md) (obsoleto)
|[sp_addrole](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md) (obsoleto) |[sp_addrolemember](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) (obsoleto)
|[sp_addserver](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md) (obsoleto) |[sp_addsrvrolemember](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md) (obsoleto)
|[sp_adduser](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md) (obsoleto) |[sp_approlepassword](../../relational-databases/system-stored-procedures/sp-approlepassword-transact-sql.md) (obsoleto)
|[sp_audit_write](../../relational-databases/system-stored-procedures/sp-audit-write-transact-sql.md) |[sp_change_users_login](../../relational-databases/system-stored-procedures/sp-change-users-login-transact-sql.md)
|[sp_changedbowner](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md) |[sp_changeobjectowner](../../relational-databases/system-stored-procedures/sp-changeobjectowner-transact-sql.md) (obsoleto)
|[sp_control_dbmasterkey_password](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md) |[sp_dbfixedrolepermission](../../relational-databases/system-stored-procedures/sp-dbfixedrolepermission-transact-sql.md) (obsoleto)
|[sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md) (obsoleto) |[sp_defaultlanguage](../../relational-databases/system-stored-procedures/sp-defaultlanguage-transact-sql.md) (obsoleto)
|[sp_denylogin](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md) (obsoleto) |[sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)
|[sp_dropalias](../../relational-databases/system-stored-procedures/sp-dropalias-transact-sql.md) (obsoleto) |[Sys.sp_drop_trusted_assembly]( sys-sp-drop-trusted-assembly-transact-sql.md) |
|[sp_dropapprole](../../relational-databases/system-stored-procedures/sp-dropapprole-transact-sql.md) (obsoleto) |[sp_droplinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md) |
|[sp_droplogin](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md) (obsoleto) |[sp_dropremotelogin](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md) (obsoleto) |
|[sp_droprole](../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md) (obsoleto) |[sp_droprolemember](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md) (obsoleto) |
|[sp_dropserver](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md) |[sp_dropsrvrolemember](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md) (obsoleto) |
|[sp_dropuser](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md) (obsoleto) |[sp_grantdbaccess](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md) (obsoleto) |
|[sp_grantlogin](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md) (obsoleto) |[sp_helpdbfixedrole](../../relational-databases/system-stored-procedures/sp-helpdbfixedrole-transact-sql.md) |
|[sp_helplinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-helplinkedsrvlogin-transact-sql.md) |[sp_helplogins](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md) |
|[sp_helpntgroup](../../relational-databases/system-stored-procedures/sp-helpntgroup-transact-sql.md) |[sp_helpremotelogin](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md) (obsoleto) |
|[sp_helprole](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md) |[sp_helprolemember](../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md) |
|[sp_helprotect](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md) (obsoleto) |[sp_helpsrvrole](../../relational-databases/system-stored-procedures/sp-helpsrvrole-transact-sql.md) |
|[sp_helpsrvrolemember](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md) |[sp_helpuser](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md) (obsoleto) |
|[sp_migrate_user_to_contained](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)|[sp_MShasdbaccess](../../relational-databases/system-stored-procedures/sp-mshasdbaccess-transact-sql.md) |
|[sp_password](../../relational-databases/system-stored-procedures/sp-password-transact-sql.md) (obsoleto)|[sp_refresh_parameter_encryption](../../relational-databases/system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md) |
|[sp_remoteoption](../../relational-databases/system-stored-procedures/sp-remoteoption-transact-sql.md) (obsoleto)|[sp_revokedbaccess](../../relational-databases/system-stored-procedures/sp-revokedbaccess-transact-sql.md) (obsoleto) |
|[sp_revokelogin](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md) (obsoleto)|[sp_setapprole](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md) |
|[sp_srvrolepermission](../../relational-databases/system-stored-procedures/sp-srvrolepermission-transact-sql.md) (obsoleto)|[sp_testlinkedserver](../../relational-databases/system-stored-procedures/sp-testlinkedserver-transact-sql.md) |
|[sp_unsetapprole](../../relational-databases/system-stored-procedures/sp-unsetapprole-transact-sql.md) |[sp_validatelogins](../../relational-databases/system-stored-procedures/sp-validatelogins-transact-sql.md) |
|[sp_xp_cmdshell_proxy_account](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md) | |

 
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Funciones de seguridad &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
