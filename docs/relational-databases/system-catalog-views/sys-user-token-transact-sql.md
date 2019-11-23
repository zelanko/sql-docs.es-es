---
title: sys.user_token (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.user_token
- user_token
- sys.user_token_TSQL
- user_token_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], security tokens
- sys.user_token catalog view
- user tokens [SQL Server]
- tokens [SQL Server]
- user_token catalog view
ms.assetid: be018103-5e57-43a4-9160-9bf420892aa7
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions|| = azure-sqldw-latest
ms.openlocfilehash: 9b3e389b97cee8a8a6d548eb93ad70b94d09ba40
ms.sourcegitcommit: 71fac5fee00e0eca57e555f44274dd7e08d47e1e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70160738"
---
# <a name="sysuser_token-transact-sql"></a>sys.user_token (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md.md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  Devuelve una fila por cada entidad de seguridad de base de datos que forma parte del token del usuario en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**principal_id**|**int**|Id. de la entidad de seguridad. El valor es único en la base de datos.|  
|**sid**|**varbinary(85)**|Identificador de seguridad de la entidad de seguridad si ésta está definida como externa a la base de datos. Por ejemplo, puede ser un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], un inicio de sesión de Windows, un inicio de sesión del grupo de Windows o un inicio de sesión asignado a un certificado; de lo contrario, este valor es NULL.|  
|**Nombre**|**nvarchar (128)**|Nombre de la entidad de seguridad. El valor es único en la base de datos.|  
|**tipo**|**nvarchar (128)**|Descripción del tipo de entidad de seguridad. Todos los tipos se asignan a **SID**. El valor puede ser uno de los siguientes:<br /><br /> SQL USER<br /><br /> WINDOWS LOGIN<br /><br /> WINDOWS GROUP<br /><br /> Rol<br /><br /> APPLICATION ROLE<br /><br /> ROL DE BASE DE DATOS<br /><br /> USER MAPPED TO CERTIFICATE<br /><br /> USER MAPPED TO ASYMMETRIC KEY<br /><br /> CERTIFICATE<br /><br /> ASYMMETRIC KEY|  
|**usage**|**nvarchar (128)**|Indica que la entidad de seguridad participa en la evaluación de los permisos GRANT o DENY o sirve como autenticador.<br /><br /> Este valor puede ser uno de los siguientes:<br /><br /> GRANT o DENY<br /><br /> DENY ONLY<br /><br /> AUTHENTICATOR|  
  
## <a name="see-also"></a>Vea también  
 [sys.login_token &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-login-token-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
