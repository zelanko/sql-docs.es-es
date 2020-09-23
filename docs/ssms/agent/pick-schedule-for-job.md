---
description: Elegir programación para trabajo
title: Elegir programación para trabajo
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.pickscheduleforjob.f1
helpviewer_keywords:
- Pick Schedule for Job dialog box
ms.assetid: 6de2025d-c25c-47b9-9a25-18c294935c15
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a67a94e03c606fc6b5f80bfe9fde51cbe4083a9c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88318821"
---
# <a name="pick-schedule-for-job"></a>Elegir programación para trabajo
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Azure SQL Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), actualmente son compatibles la mayoría de las características del Agente SQL Server. Para más información, consulte [Diferencias entre Azure SQL Managed Instance y SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Use este cuadro de diálogo para elegir una programación existente para el trabajo del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="options"></a>Opciones  
**Programaciones disponibles**  
Muestra las programaciones disponibles para este trabajo. Puesto a que un trabajo y una programación deben tener un mismo propietario, esta lista solo incluye las programaciones del propietario del trabajo.  
  
**Nombre**  
Muestra el nombre de la programación.  
  
**Habilitado**  
Esta opción está seleccionada si la programación está habilitada.  
  
**Descripción**  
Describe las condiciones bajo las cuales la programación ejecuta el trabajo.  
  
**Trabajos en programación**  
Muestra los números de los trabajos adjuntados a la programación. Haga clic en un número para ver las propiedades del trabajo.  
  
**Propiedades**  
Abre el cuadro de diálogo **Propiedades de programación del trabajo** donde puede ver información acerca de la programación.  
  
## <a name="see-also"></a>Consulte también  
[Crear y adjuntar programaciones a trabajos](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
  
