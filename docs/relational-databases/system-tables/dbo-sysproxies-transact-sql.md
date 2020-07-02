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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1e49698ae6692a06c141a4182df3c54cd4f61d43
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750305"
---
# <a name="dbosysproxies-transact-sql"></a>dbo.sysproxies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Define atributos de una cuenta de proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta tabla se almacena en la base de datos **msdb** .  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|Id. de la cuenta de proxy.|  
|**name**|**sysname**|Nombre de la cuenta de proxy.|  
|**credential_id**|**int**|Id. de la credencial que utiliza la cuenta de proxy.|  
|**activó**|**tinyint**|Estado de la cuenta de proxy:<br /><br /> **0** = deshabilitado. **1** = habilitada.|  
|**description**|**nvarchar(512)**|Descripción proporcionada por el usuario cuando se creó la cuenta de proxy.|  
|**user_sid**|**varbinary(85)**|*Security_identifier* de Microsoft Windows del usuario o grupo asociado a la credencial del proxy.|  
|**credential_date_created**|**datetime**|Es la fecha y hora en que se creó la credencial.|  
  
## <a name="remarks"></a>Comentarios  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden tener acceso a la tabla **sysproxies** .  
  
## <a name="see-also"></a>Consulte también  
 [dbo.sysProxyLogin &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxylogin-transact-sql.md)   
 [dbo.sysproxysubsystem &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [dbo.syssubsistemas &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-syssubsystems-transact-sql.md)  
  
  
