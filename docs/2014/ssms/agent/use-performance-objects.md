---
title: Usar objetos de rendimiento | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, monitoring
- SQL Server Agent service, monitoring
- SQL Server Agent service, performance objects
- SQL Server Agent, performance objects
- performance objects [SQL Server Agent]
- monitoring [SQL Server], SQL Server Agent
- monitoring [SQL Server Agent]
- performance counters [SQL Server], SQL Server Agent
- counters [SQL Server], SQL Server Agent
ms.assetid: 830b843a-6b2a-4620-a51b-98358e9fc54b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2ccba43aa28cadef1995fab001f66e1f4bebacde
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63245848"
---
# <a name="use-performance-objects"></a>Usar objetos de rendimiento
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El Agente incluye objetos y contadores de rendimiento para supervisar el rendimiento del servicio. Estos objetos de rendimiento le permiten utilizar el Monitor de rendimiento, una herramienta de Windows, para identificar las actividades que realiza el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en segundo plano. Por ejemplo, puede identificar cuántos trabajos activos ejecuta actualmente el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para identificar los trabajos bloqueados.  
  
 Hay objetos y contadores de rendimiento del servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalada en el equipo. La denominación que adoptan los objetos de rendimiento depende de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que representa cada uno de ellos.  
  
 La tabla siguiente muestra cómo se denominan los objetos de rendimiento del servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
|Tipo de instancia|Nombre del objeto|  
|-------------------|-----------------|  
|Default|**SQLAgent:** *objeto*:*contador*|  
|Con nombre|**SQLAgent$**<br /> ***instance_name* :** *objeto*:*contador*|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye los siguientes objetos de rendimiento para el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Nombre del objeto|Descripción|  
|-----------------|-----------------|  
|[SQLAgent:Jobs](../../relational-databases/performance-monitor/sql-server-agent-jobs-object.md)|Información de rendimiento acerca de trabajos que se han iniciado, tasas de éxito y estado actual|  
|[SQLAgent:JobSteps](../../relational-databases/performance-monitor/sql-server-agent-jobsteps-object.md)|Información de estado acerca de pasos de trabajos|  
|[SQLAgent:Alerts](../../relational-databases/performance-monitor/sql-server-agent-alerts-object.md)|Información acerca del número de alertas y notificaciones|  
|[SQLAgent:Statistics](../../relational-databases/performance-monitor/sql-server-agent-statistics-object.md)|Información general de rendimiento|  
  
## <a name="see-also"></a>Vea también  
 [Supervisión y optimización del rendimiento](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [Iniciar el Monitor de sistema &#40;Windows&#41;](../../relational-databases/performance/start-system-monitor-windows.md)  
  
  
