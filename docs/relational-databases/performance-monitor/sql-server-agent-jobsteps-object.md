---
title: JobSteps (objeto del Agente SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- JobSteps object
- SQLAgent:JobSteps
ms.assetid: 44f9983c-1753-4fe0-8475-973aa2460b3a
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: b3d0c8197f275801140bec48ab05dc6bc19324eb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85787383"
---
# <a name="sql-server-agent-jobsteps-object"></a>JobSteps (objeto del Agente SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  El objeto de rendimiento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] JobSteps **del Agente** contiene contadores de rendimiento que informan sobre los pasos de trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . En la siguiente tabla se enumeran los contadores incluidos en este objeto.  
  
 La siguiente tabla contiene los contadores de **SQLAgent:JobSteps** .  
  
|Nombre|Descripción|  
|----------|-----------------|  
|**Pasos activos**|Este contador muestra el número de pasos de trabajo que se están ejecutando actualmente.|  
|**Pasos en cola**|Este contador informa acerca del número de pasos de trabajo preparados para que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los ejecute, pero cuya ejecución aún no se ha iniciado.|  
|**Total de reintentos de pasos**|Este contador informa del número total de veces que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha reintentado un paso de trabajo desde el último reinicio del servidor.|  
  
 Cada contador del objeto contiene las instancias siguientes:  
  
|Instancia|Descripción|  
|--------------|-----------------|  
|**_Total**|Información de todos los pasos de trabajo.|  
|**ActiveScripting**|Información de los pasos de trabajo que utilizan el subsistema **ActiveScripting** .|  
|**ANALYSISCOMMAND**|Información de los pasos de trabajo que utilizan el subsistema ANALYSISCOMMAND.|  
|**ANALYSISQUERY**|Información de los pasos de trabajo que utilizan el subsistema ANALYSISQUERY.|  
|**CmdExec**|Información de los pasos de trabajo que utilizan el subsistema **CmdExec** .|  
|**Distribución**|Información de los pasos de trabajo que utilizan el subsistema **Distribution** .|  
|**Dts**|Información de los pasos de trabajo que utilizan el subsistema [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|**LogReader**|Información de los pasos de trabajo que utilizan el subsistema **LogReader** .|  
|**Combinar**|Información de los pasos de trabajo que utilizan el subsistema **Merge** .|  
|**PowerShell**|Información de los pasos de trabajo que utilizan el subsistema **PowerShell** .|  
|**QueueReader**|Información de los pasos de trabajo que utilizan el subsistema **QueueReader** .|  
|**Instantánea**|Información de los pasos de trabajo que utilizan el subsistema **Snapshot** .|  
|**TSQL**|Información de los pasos de trabajo que ejecutan [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
  
## <a name="see-also"></a>Consulte también  
 [Administrar pasos de trabajo](../../ssms/agent/manage-job-steps.md)   
 [Usar objetos de rendimiento](../../ssms/agent/use-performance-objects.md)   
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
