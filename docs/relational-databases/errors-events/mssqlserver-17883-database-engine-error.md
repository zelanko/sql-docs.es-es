---
title: MSSQLSERVER_17883 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 17883 (Database Engine error)
ms.assetid: adaf1c04-e397-4a69-90b8-9353a37277ea
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8a311db0cc2fcc129046a918d90d306347ec0853
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver17883"></a>MSSQLSERVER_17883
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|17883|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SRV_SCHEDULER_NONYIELDING|  
|Texto del mensaje|Parece que el proceso %ld:%ld:%ld (0x%lx) Trabajo 0x%p no rinde en el programador %ld. Thread creation time: %I64d. CPU usada por el subproceso (aprox.): kernel %I64d ms, usuario %I64d ms. Uso del proceso %d%%. Sistema inactivo %d%%. Intervalo: %I64d ms.|  
  
## <a name="explanation"></a>Explicación  
Indica que hay un posible problema con un subproceso que no rinde en un programador.  Esto podría deberse a un error en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o a que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no esté obteniendo bastantes ciclos para ejecutarse.  Este error podría desaparecer si el subproceso rinde finalmente.  
  
## <a name="user-action"></a>Acción del usuario  
Si la carga es excesiva en el sistema, redúzcala; de lo contrario, póngase en contacto con los servicios de soporte al cliente de Microsoft.  
  
