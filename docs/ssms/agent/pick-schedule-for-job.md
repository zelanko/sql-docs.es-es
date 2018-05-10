---
title: Elegir programación para trabajo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.pickscheduleforjob.f1
helpviewer_keywords:
- Pick Schedule for Job dialog box
ms.assetid: 6de2025d-c25c-47b9-9a25-18c294935c15
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c561bb6100bb06318195f4c7a461056f35c65647
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="pick-schedule-for-job"></a>Elegir programación para trabajo
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

Utilice este cuadro de diálogo para elegir una programación existente para el trabajo del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
## <a name="options"></a>Opciones  
**Programaciones disponibles**  
Muestra las programaciones disponibles para este trabajo. Puesto a que un trabajo y una programación deben tener un mismo propietario, esta lista solo incluye las programaciones del propietario del trabajo.  
  
**Nombre**  
Muestra el nombre de la programación.  
  
**Enabled**  
Esta opción está seleccionada si la programación está habilitada.  
  
**Descripción**  
Describe las condiciones bajo las cuales la programación ejecuta el trabajo.  
  
**Trabajos en programación**  
Muestra los números de los trabajos adjuntados a la programación. Haga clic en un número para ver las propiedades del trabajo.  
  
**Propiedades**  
Abre el cuadro de diálogo **Propiedades de programación del trabajo** donde puede ver información acerca de la programación.  
  
## <a name="see-also"></a>Ver también  
[Crear y adjuntar programaciones a trabajos](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
  
