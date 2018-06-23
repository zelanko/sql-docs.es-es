---
title: MSSQLSERVER_17883 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 17883 (Database Engine error)
ms.assetid: adaf1c04-e397-4a69-90b8-9353a37277ea
caps.latest.revision: 15
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ee743a1346dfa555a848b525d6ba48f04e4f9c48
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201815"
---
# <a name="mssqlserver17883"></a>MSSQLSERVER_17883
    
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
  
  