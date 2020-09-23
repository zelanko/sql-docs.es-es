---
description: Implementar trabajos
title: Implementar trabajos
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent]
- SQL Server Agent jobs
- SQL Server Agent jobs, about jobs
- jobs [SQL Server Agent], about jobs
ms.assetid: 69e06724-25c7-4fb3-8a5b-3d4596f21756
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 503f2a0ab50d38b70a1002f3a12ad6508479d755
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463093"
---
# <a name="implement-jobs"></a>Implementar trabajos
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Azure SQL Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), actualmente son compatibles la mayoría de las características del Agente SQL Server. Consulte [Diferencias entre T-SQL de Azure SQL Managed Instance y SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para más información.

Puede utilizar los trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para automatizar tareas administrativas rutinarias y ejecutarlas periódicamente, lo que permite que la administración sea más eficaz.  
  
Un trabajo es una serie específica de operaciones que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza secuencialmente. Un trabajo puede realizar una amplia variedad de actividades, incluidos scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] , aplicaciones de línea de comandos, scripts de Microsoft ActiveX, paquetes de Integration Services, comandos y consultas de Analysis Services o tareas de replicación. Los trabajos pueden ejecutar tareas repetitivas o que se pueden programar y pueden notificar automáticamente a los usuarios el estado del trabajo mediante alertas, simplificando mucho la administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
Puede ejecutar los trabajos manualmente o configurarlos para que se ejecuten de acuerdo con una programación o en respuesta a alertas.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción|Tema|  
|-|-|   
|Contiene información sobre cómo crear trabajos y asignar su propiedad.|[Crear trabajos](../../ssms/agent/create-jobs.md)|  
|Contiene información sobre cómo organizar trabajos en categorías.|[organizar los trabajos](../../ssms/agent/organize-jobs.md)|  
|Contiene información acerca de los diferentes tipos de pasos de trabajo que puede crear y cómo administrarlos.|[Administrar pasos de trabajo](../../ssms/agent/manage-job-steps.md)|  
|Contiene información acerca de cómo definir cuándo se iniciarán los trabajos que se ejecutan y la frecuencia con la que deben ejecutarse.|[Crear y adjuntar programaciones a trabajos](../../ssms/agent/create-and-attach-schedules-to-jobs.md)|  
|Contiene información acerca de la ejecución manual de trabajos (sin una programación).|[Ejecutar trabajos](../../ssms/agent/run-jobs.md)|  
|Contiene información acerca de cómo se puede configurar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que responda a los trabajos. Por ejemplo, se puede configurar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que notifique a los administradores cuándo finalicen los trabajos.|[Especificar respuestas de trabajos](../../ssms/agent/specify-job-responses.md)|  
|Contiene información acerca de cómo ver los trabajos existentes, su historial cuando se han ejecutado y cómo modificarlos.|[Ver o modificar trabajos](../../ssms/agent/view-or-modify-jobs.md)|  
|Contiene información acerca de cómo eliminar trabajos.|[eliminar trabajos](../../ssms/agent/delete-jobs.md)|  
  
## <a name="see-also"></a>Consulte también  
[Implementar la seguridad del Agente SQL Server](../../ssms/agent/implement-sql-server-agent-security.md)  
  
