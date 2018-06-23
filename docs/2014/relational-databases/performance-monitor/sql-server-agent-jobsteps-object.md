---
title: JobSteps (objeto del Agente SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- JobSteps object
- SQLAgent:JobSteps
ms.assetid: 44f9983c-1753-4fe0-8475-973aa2460b3a
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 36fd1f3af30a3b9637df64ca5e118b6381e3bd06
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202279"
---
# <a name="sql-server-agent-jobsteps-object"></a>JobSteps (objeto del Agente SQL Server)
  El objeto de rendimiento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] JobSteps **del Agente** contiene contadores de rendimiento que informan sobre los pasos de trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . En la siguiente tabla se enumeran los contadores incluidos en este objeto.  
  
 La siguiente tabla contiene los contadores de **SQLAgent:JobSteps** .  
  
|Nombre|Descripción|  
|----------|-----------------|  
|**Pasos activos**|Este contador muestra el número de pasos de trabajo que se están ejecutando actualmente.|  
|**Pasos en cola**|Este contador informa acerca del número de pasos de trabajo preparados para que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los ejecute, pero cuya ejecución aún no se ha iniciado.|  
|**Total de reintentos de pasos**|Este contador informa acerca del número total de veces que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha intentado ejecutar un paso de trabajo desde la última vez que se reinició el servidor.|  
  
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
|**Mezcla**|Información de los pasos de trabajo que utilizan el subsistema **Merge** .|  
|**PowerShell**|Información de los pasos de trabajo que utilizan el subsistema **PowerShell** .|  
|**QueueReader**|Información de los pasos de trabajo que utilizan el subsistema **QueueReader** .|  
|**Snapshot**|Información de los pasos de trabajo que utilizan el subsistema **Snapshot** .|  
|**TSQL**|Información de los pasos de trabajo que ejecutan [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
  
## <a name="see-also"></a>Vea también  
 [Administrar pasos de trabajo](../../ssms/agent/manage-job-steps.md)   
 [Usar objetos de rendimiento](../../ssms/agent/use-performance-objects.md)   
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  