---
title: sp_update_jobschedule (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_update_jobschedule_TSQL
- sp_update_jobschedule
dev_langs: TSQL
helpviewer_keywords: sp_update_jobschedule
ms.assetid: 4df02594-4cd1-49a9-8d97-37c44e4d5423
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7af3408d791d25020d090620cc2eea1330a5444f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="spupdatejobschedule-transact-sql"></a>sp_update_jobschedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia la configuración de la programación del trabajo especificado.  
  
 **sp_update_jobschedule** se proporciona por compatibilidad con versiones anteriores.  
  
> [!IMPORTANT]  
>  Para obtener más información acerca de la sintaxis utilizada en versiones anteriores de Microsoft SQL Server, vea Microsoft SQL Server 2000 de Transact-SQL Referencefor*.*  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
## <a name="remarks"></a>Comentarios  
 Ahora, las programaciones de trabajos se pueden administrar independientemente de los trabajos. Para actualizar una programación, utilice **sp_update_schedule**.  
  
## <a name="permissions"></a>Permissions  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Solo los miembros del **sysadmin** puede usar este procedimiento almacenado para actualizar programaciones de trabajos que pertenecen a otros usuarios.  
  
## <a name="see-also"></a>Vea también  
 [Agente SQL Server almacena procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_update_schedule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)  
  
  
