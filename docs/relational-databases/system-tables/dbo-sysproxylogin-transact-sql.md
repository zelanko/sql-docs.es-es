---
title: dbo.sysProxyLogin (Transact-SQL) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b798627a09a9bb96e753221750711dbfe465657f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750295"
---
# <a name="dbosysproxylogin-transact-sql"></a>dbo.sysproxylogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Registra qué inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están asociados a cada cuenta de proxy del Agente SQL Server. Esta tabla se almacena en la base de datos **msdb** .  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|Id. de la cuenta de proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este valor corresponde al **proxy_id** columna de la tabla **sysproxies** .|  
|**sid**|**varbinary(85)**|Microsoft Windows *security_identifier* para el inicio de sesión de SQL Server.|  
|**principal_id**|**int**|Id. del usuario o grupo que tiene permiso para utilizar la cuenta de proxy para un paso de subsistema especificado.|  
|**flags**|**int**|Tipo de inicio de sesión:<br /><br /> **0** = usuario o grupo de Windows e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Inicio de sesión.<br /><br /> **1**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rol fijo de sistema<br /><br /> **2**  =  rol de base de datos **msdb**|  
  
## <a name="remarks"></a>Comentarios  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden tener acceso a esta tabla.  
  
## <a name="see-also"></a>Consulte también  
 [dbo.sysproxies &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)  
  
  
