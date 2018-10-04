---
title: Eliminar trabajos | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- delete jobs
ms.assetid: bffb915e-bc84-4417-aa35-183243ca3312
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2afa9d161085a6907d14e536d2fef65b1b85ee46
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48101095"
---
# <a name="delete-jobs"></a>Eliminar trabajos
  Un trabajo es una serie específica de operaciones que el Agente SQL Server realiza secuencialmente. De forma predeterminada, los trabajos no se eliminan cuando finaliza la ejecución. Puede eliminar uno o más trabajos del Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] independientemente del éxito o del fracaso del trabajo. También puede configurar el Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que elimine los trabajos automáticamente cuando se realizan correctamente, con error o se completan.  
  
 De forma predeterminada, los miembros de la **sysadmin** rol fijo de servidor puede ejecutar el [sp_delete_job &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-delete-job-transact-sql) eliminar un trabajo de procedimiento almacenado del sistema. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](sql-server-agent-fixed-database-roles.md).  
  
 Los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_delete_job** para eliminar cualquier trabajo. Un usuario que no sea miembro del rol fijo de servidor **sysadmin** solo puede eliminar los trabajos de los que sea propietario.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Descripción**|**Tema**|  
|Describe cómo eliminar uno o varios de los trabajos del Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|[Eliminar uno o más trabajos](delete-one-or-more-jobs.md)|  
|Describe cómo configurar el Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que elimine los trabajos automáticamente cuando se realizan correctamente, con error o se completan.|[Automatically Delete a Job](automatically-delete-a-job.md)|  
  
  
