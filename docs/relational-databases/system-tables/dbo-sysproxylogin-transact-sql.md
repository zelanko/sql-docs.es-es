---
title: dbo.sysproxylogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysproxylogin_TSQL
- sysproxylogin_TSQL
- dbo.sysproxylogin
- sysproxylogin
dev_langs:
- TSQL
helpviewer_keywords:
- sysproxylogin system table
ms.assetid: 433d33cb-bdf2-47bb-af78-2a40b7c8dfce
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 00a3b3b53bcede7f43aad556465358b957331f45
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62470697"
---
# <a name="dbosysproxylogin-transact-sql"></a>dbo.sysproxylogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Registra qué inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están asociados a cada cuenta de proxy del Agente SQL Server. Esta tabla se almacena en el **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|Id. de la cuenta de proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este valor corresponde a la **proxy_id** columna en el **sysproxies** tabla.|  
|**sid**|**varbinary(85)**|Microsoft Windows *security_identifier* para el inicio de sesión de SQL Server.|  
|**principal_id**|**int**|Id. del usuario o grupo que tiene permiso para utilizar la cuenta de proxy para un paso de subsistema especificado.|  
|**flags**|**int**|Tipo de inicio de sesión:<br /><br /> **0** = usuario de Windows o grupo, y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión.<br /><br /> **1**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rol fijo del sistema<br /><br /> **2** = **msdb** rol de base de datos|  
  
## <a name="remarks"></a>Comentarios  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede tener acceso a esta tabla.  
  
## <a name="see-also"></a>Vea también  
 [dbo.sysproxies &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)  
  
  
