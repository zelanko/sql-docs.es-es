---
description: sys.login_token (Transact-SQL)
title: Sys. login_token (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- login_token_TSQL
- sys.login_token_TSQL
- sys.login_token
- login_token
dev_langs:
- TSQL
helpviewer_keywords:
- sys.login_token catalog view
- logins [SQL Server], security tokens
- tokens [SQL Server]
ms.assetid: 86e06938-9d0a-44e5-99e2-55c8ef5f2f84
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 339964a859d5e95d88853781a8b2b43f341f23be
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88377811"
---
# <a name="syslogin_token-transact-sql"></a>sys.login_token (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Devuelve una fila por cada entidad de seguridad de servidor que forma parte del token de inicio de sesión.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**principal_id**|**int**|Id. de la entidad de seguridad. Este valor es único en el servidor.|  
|**sid**|**varbinary(85)**|Identificador de seguridad de la entidad de seguridad. Si se trata de una entidad de seguridad de Windows, **SID** = SID de Windows. Si el inicio de sesión está asignado a un certificado, **SID** = GUID del certificado.|  
|**name**|**nvarchar(128)**|Nombre de la entidad de seguridad. Este valor es único en el servidor.|  
|**type**|**nvarchar(128)**|Descripción del tipo de entidad de seguridad. Todos los tipos se asignan a **SID**. El valor puede ser uno de los siguientes:<br /><br /> SQL LOGIN<br /><br /> WINDOWS LOGIN<br /><br /> WINDOWS GROUP<br /><br /> SERVER ROLE<br /><br /> LOGIN MAPPED TO CERTIFICATE<br /><br /> LOGIN MAPPED TO ASYMMETRIC KEY<br /><br /> CERTIFICADO<br /><br /> ASYMMETRIC KEY|  
|**uso**|**nvarchar(128)**|Indica que la entidad de seguridad participa en la evaluación de los permisos GRANT o DENY o sirve como autenticador.<br /><br /> Este valor puede ser uno de los siguientes:<br /><br /> GRANT o DENY<br /><br /> DENY ONLY<br /><br /> AUTHENTICATOR|  
  
## <a name="see-also"></a>Consulte también  
 [Sys. user_token &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-user-token-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
