---
description: eliminar trabajos
title: eliminar trabajos
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- delete jobs
ms.assetid: bffb915e-bc84-4417-aa35-183243ca3312
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2fd58cfc92b1d80578ed2d15d63fae5eedd00b94
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038011"
---
# <a name="delete-jobs"></a>eliminar trabajos
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance), actualmente son compatibles la mayoría de las características del Agente SQL Server. Consulte [Diferencias entre T-SQL de Azure SQL Managed Instance y SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para más información.

Un trabajo es una serie específica de operaciones que el Agente SQL Server realiza secuencialmente. De forma predeterminada, los trabajos no se eliminan cuando finaliza la ejecución. Puede eliminar uno o más trabajos del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] independientemente del éxito o del fracaso del trabajo. También puede configurar el Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que elimine los trabajos automáticamente cuando se realizan correctamente, con error o se completan.  
  
De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar el procedimiento almacenamiento del sistema [sp_delete_job (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md) para eliminar un trabajo. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
Los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_delete_job** para eliminar cualquier trabajo. Un usuario que no sea miembro del rol fijo de servidor **sysadmin** solo puede eliminar los trabajos de los que sea propietario.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción|Tema|  
|-|-|   
|Describe cómo eliminar uno o varios de los trabajos del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|[Eliminar uno o más trabajos](../../ssms/agent/delete-one-or-more-jobs.md)|  
|Describe cómo configurar el Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que elimine los trabajos automáticamente cuando se realizan correctamente, con error o se completan.|[Automatically Delete a Job](../../ssms/agent/automatically-delete-a-job.md)|  
