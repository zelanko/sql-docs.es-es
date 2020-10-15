---
description: Configuración del cierre de la ejecución de trabajos
title: Configuración del cierre de la ejecución de trabajos
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], stopping
- SQL Server Agent jobs, stopping
- stopping jobs
- SQL Server Agent jobs, execution shutdowns
ms.assetid: ac23e88f-53fc-41de-bb16-0c27c002d5a5
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8c026afb3b77baf2fb274909e73e3dd527487d2e
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036535"
---
# <a name="set-job-execution-shutdown"></a>Configuración del cierre de la ejecución de trabajos

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance), actualmente son compatibles la mayoría de las características del Agente SQL Server. Consulte [Diferencias entre T-SQL de Azure SQL Managed Instance y SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para más información.

En este tema se describe cómo configurar el tiempo que el Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esperará a que finalice la ejecución de los trabajos antes de que el propio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] finalice en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="security"></a><a name="Security"></a>Seguridad  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permisos  
De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden establecer el tiempo que el Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esperará a que finalice la ejecución de los trabajos antes de que el propio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] finalice. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-set-job-execution-shutdown"></a>Para configurar el cierre de la ejecución de trabajos  
  
1.  En **El Explorador de objetos** , haga clic en el signo más para expandir el servidor en el que desea establecer un intervalo de cierre de la ejecución de trabajos.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server** y seleccione **Propiedades**.  
  
3.  En **Seleccionar una página**, seleccione **Sistema de trabajo**.  
  
4.  Configure **Intervalo de tiempo de espera de cierre** en segundos para aumentar o reducir dicho intervalo. Así se determina el tiempo que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] va a esperar a que finalice la ejecución de los trabajos antes de que se cierre el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
