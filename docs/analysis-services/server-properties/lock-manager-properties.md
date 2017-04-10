---
title: "Propiedades del administrador de bloqueos | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "administrador de bloqueos, propiedades [Analysis Services]"
  - "LockWaitGranularityMS, propiedad"
  - "DefaultLockTimeoutMS, propiedad"
  - "DeadlockDetectionGranularityMS, propiedad"
ms.assetid: 15fe9ead-825b-4ac3-9191-7a07caa2861b
caps.latest.revision: 16
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 16
---
# Propiedades del administrador de bloqueos
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite las propiedades de servidor del administrador de bloqueos que aparecen en la siguiente tabla. Para obtener más información sobre otras propiedades de servidor y cómo establecerlas, vea [Configurar las propiedades de servidor en Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Se aplica a:** modo de servidor multidimensional y tabular  
  
## Propiedades  
 **DefaultLockTimeoutMS**  
 Propiedad de entero de 32 bits con signo que define el tiempo de espera de bloqueo predeterminado en milisegundos para las solicitudes de bloqueo internas.  
  
 El valor predeterminado de esta propiedad es -1, que indica que no hay tiempo de espera para las solicitudes de bloqueo internas.  
  
 **LockWaitGranularityMS**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DeadlockDetectionGranularityMS**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## Vea también  
 [Configurar las propiedades de servidor en Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determinar el modo de servidor de una instancia de Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  