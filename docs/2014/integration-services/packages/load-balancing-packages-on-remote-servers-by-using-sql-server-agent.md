---
title: Realizar el equilibrio de carga de paquetes en servidores remotos mediante el Agente SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- load-balancing [Integration Services]
- parent packages [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: 9281c5f8-8da3-4ae8-8142-53c5919a4cfe
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a7c1f4792d97ae82561f0d05fe9754daae0a2bf3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62890187"
---
# <a name="load-balancing-packages-on-remote-servers-by-using-sql-server-agent"></a>Realizar el equilibrio de carga de paquetes en servidores remotos mediante el Agente SQL Server
  Cuando se tienen que ejecutar varios paquetes, es conveniente utilizar otros servidores que están disponibles. Se denomina equilibrio de carga a este método de utilizar otros servidores para ejecutar paquetes cuando los paquetes están todos bajo el control de un paquete primario. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], el equilibrio de carga es un procedimiento manual que deben diseñar los propietarios de los paquetes. Los servidores no realizan el equilibrio de carga automáticamente. Asimismo, los paquetes ejecutados en los servidores remotos deben ser paquetes completos, y no tareas individuales en otros paquetes.  
  
 El equilibrio de carga es útil en los siguientes escenarios:  
  
-   Los paquetes se pueden ejecutar al mismo tiempo.  
  
-   Los paquetes son grandes y, si se ejecutan de manera secuencial, el tiempo de ejecución puede ser superior al permitido para procesamiento.  
  
 Los administradores y arquitectos pueden determinar si la utilización de servidores adicionales para procesamiento beneficiaría sus procesos.  
  
## <a name="illustration-of-load-balancing"></a>Ilustración de equilibrio de carga  
 El siguiente diagrama muestra un paquete primario en un servidor. El paquete primario contiene varias tareas Ejecutar trabajo del Agente SQL. Cada tarea del paquete primario llama a un Agente SQL Server en un servidor remoto. Esos servidores remotos contienen trabajos del Agente SQL Server que incluyen un paso que llama a un paquete en ese servidor.  
  
 ![Información general de la arquitectura de equilibrio de carga SSIS](../media/loadbalancingoverview.gif "Información general de la arquitectura de equilibrio de carga SSIS")  
  
 Los pasos requeridos para el equilibrio de carga en esta arquitectura no son conceptos nuevos. En lugar de ello, el equilibrio de carga se logra al utilizar conceptos existentes y objetos SSIS comunes de una nueva manera.  
  
## <a name="execution-of-packages-on-a-remote-instance-by-using-sql-server-agent"></a>Ejecución de paquetes en una instancia remota mediante el Agente SQL Server  
 En la arquitectura básica de la ejecución remota de paquetes, un paquete central reside en la instancia del SQL Server que controla a los otros paquetes remotos. El diagrama muestra este paquete central, denominado primario SSIS. La instancia en la que reside este paquete primario controla la ejecución de los trabajos del Agente SQL Server que ejecutan los paquetes secundarios. La ejecución de los paquetes secundarios no sigue un programa fijo bajo el control del Agente SQL Server en el servidor remoto. En su lugar, el Agente SQL Server inicia los paquetes secundarios cuando los llama el paquete primario y se ejecutan en la misma instancia de SQL Server en la que reside el Agente SQL Server.  
  
 Para poder ejecutar un paquete remoto a través del Agente SQL Server, primero debe configurar los paquetes primarios y secundarios, además de configurar los trabajos del Agente SQL Server que controlan los paquetes secundarios. Las siguientes secciones proporcionan más información sobre cómo crear, configurar, ejecutar y mantener paquetes que se ejecutan en servidores remotos. Este proceso comprende varios pasos:  
  
-   Crear paquetes secundarios e instalarlos en servidores remotos.  
  
-   Crear los trabajos del Agente SQL Server en las instancias remotas que ejecutarán los paquetes.  
  
-   Crear el paquete primario.  
  
-   Determinar el escenario de registro de los paquetes secundarios.  
  
 La tabla siguiente proporciona vínculos a temas que lo guían a través del proceso.  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Implementación de paquetes secundarios](../implementation-of-child-packages.md)|Describe la instalación de paquetes y la creación de los trabajos del Agente SQL Server para ejecutar los paquetes.|  
|[Implementación del paquete primario](../implementation-of-the-parent-package.md)|Describe la creación del paquete primario que contiene varias tareas Ejecutar trabajo del Agente SQL Server. Cada tarea ejecuta uno de los paquetes secundarios.|  
|[Registro para la carga de paquetes equilibrados en servidores remotos](../logging-for-load-balanced-packages-on-remote-servers.md)|Describe el escenario de registro de los paquetes remotos.|  
  
## <a name="related-tasks"></a>Related Tasks  
 [Programar un paquete mediante el Agente SQL Server](../schedule-a-package-by-using-sql-server-agent.md)  
  
  
