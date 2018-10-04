---
title: sp_update_jobschedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_jobschedule_TSQL
- sp_update_jobschedule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_jobschedule
ms.assetid: 4df02594-4cd1-49a9-8d97-37c44e4d5423
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3d6604a2fb40effa3fd419068ca2e604de4dde3c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47774413"
---
# <a name="spupdatejobschedule-transact-sql"></a>sp_update_jobschedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia la configuración de la programación del trabajo especificado.  
  
 **sp_update_jobschedule** se proporciona por razones de compatibilidad.  
  
> [!IMPORTANT]  
>  Para obtener más información acerca de la sintaxis utilizada en versiones anteriores de Microsoft SQL Server, vea Transact-SQL Referencefor Microsoft SQL Server 2000 *.*  
  
## <a name="remarks"></a>Comentarios  
 Ahora, las programaciones de trabajos se pueden administrar independientemente de los trabajos. Para actualizar una programación, use **sp_update_schedule**.  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Solo los miembros del **sysadmin** puede usar este procedimiento almacenado para actualizar programaciones de trabajos que pertenecen a otros usuarios.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del Agente SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_update_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)  
  
  
