---
title: Ejecutar tarea de trabajo del Agente SQL Server | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.executesqlserveragentjobtask.f1
helpviewer_keywords:
- Execute SQL Server Agent Job task [Integration Services]
- jobs [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: 3aa3bc0e-1a1c-452e-81b8-b4e3422ea053
caps.latest.revision: 44
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: 65caffce1a119757743f8f2d6bf708112492e767
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="execute-sql-server-agent-job-task"></a>Tarea Ejecutar trabajo del Agente SQL Server
  La tarea Ejecutar trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecuta trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un servicio de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows que ejecuta trabajos definidos en una instancia de SQL Server. Puede crear trabajos que ejecuten instrucciones de Transact-SQL y scripts de ActiveX, realizar tareas de mantenimiento de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y Replicación, o ejecutar paquetes. También puede configurar un trabajo para supervisar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y activar alertas. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generalmente se utilizan para automatizar tareas que se realizan con frecuencia. Para obtener más información, vea [Implementar trabajos](http://msdn.microsoft.com/library/69e06724-25c7-4fb3-8a5b-3d4596f21756).  
  
 Un paquete puede utilizar la tarea Ejecutar trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para realizar tareas administrativas relacionadas con componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por ejemplo, un trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede ejecutar un procedimiento almacenado del sistema, como **sp_enum_dtspackages** , para obtener una lista de paquetes de una carpeta.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Agente debe estar ejecutándose antes de poder ejecutar automáticamente trabajos administrativos locales o multiservidor.  
  
 Esta tarea encapsula el procedimiento del sistema **sp_start_job** y pasa el nombre del trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al procedimiento como un argumento. Para obtener más información, vea [sp_start_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md).  
  
## <a name="configuring-the-execute-sql-server-agent-job-task"></a>Configurar la tarea Ejecutar trabajo del Agente SQL Server  
 Puede establecer propiedades a través del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Esta tarea se encuentra en la sección **Tareas del plan de mantenimiento** del **Cuadro de herramientas** , en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Tarea Ejecutar trabajo del Agente SQL Server &#40;Plan de mantenimiento&#41;](../../relational-databases/maintenance-plans/execute-sql-server-agent-job-task-maintenance-plan.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
  
