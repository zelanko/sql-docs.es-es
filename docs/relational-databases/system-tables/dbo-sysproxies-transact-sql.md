---
title: dbo.sysproxies (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysproxies_TSQL
- sysproxies_TSQL
- dbo.sysproxies
- sysproxies
dev_langs:
- TSQL
helpviewer_keywords:
- sysproxies system table
ms.assetid: a73da875-be22-45fc-b5e2-ea7ebd48e2d6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1dd486757a912d8f0364f55570a368292cf39ab7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67984896"
---
# <a name="dbosysproxies-transact-sql"></a>dbo.sysproxies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Define atributos de una cuenta de proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta tabla se almacena en el **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|Id. de la cuenta de proxy.|  
|**name**|**sysname**|Nombre de la cuenta de proxy.|  
|**credential_id**|**int**|Id. de la credencial que utiliza la cuenta de proxy.|  
|**enabled**|**tinyint**|Estado de la cuenta de proxy:<br /><br /> **0** = disabled. **1** = habilitado.|  
|**description**|**nvarchar(512)**|Descripción proporcionada por el usuario cuando se creó la cuenta de proxy.|  
|**user_sid**|**varbinary(85)**|Microsoft Windows *security_identifier* del usuario o grupo asociado con la credencial del proxy.|  
|**credential_date_created**|**datetime**|Es la fecha y hora en que se creó la credencial.|  
  
## <a name="remarks"></a>Comentarios  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede tener acceso a la **sysproxies** tabla.  
  
## <a name="see-also"></a>Vea también  
 [dbo.sysproxylogin &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxylogin-transact-sql.md)   
 [dbo.sysproxysubsystem &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [dbo.syssubsystems &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-syssubsystems-transact-sql.md)  
  
  
