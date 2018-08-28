---
title: Plan de mantenimiento (Servidores) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: maintenance-plans
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.servers.f1
- sql13.swb.maint.maintplanproperties.server.f1
ms.assetid: ac24d1a8-dd2f-4162-b804-c0df1fc1e61d
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 76cb168d9e5bfd65cadd01a657132c79d5f02a06
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40410060"
---
# <a name="maintenance-plan-servers"></a>Plan de mantenimiento (Servidores)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use el cuadro de diálogo **Servidores** para seleccionar los servidores donde desea ejecutar el plan de mantenimiento.  
  
 Para crear un plan de mantenimiento multiservidor debe configurarse un entorno multiservidor que contenga un servidor maestro y uno o varios servidores de destino. En los planes de mantenimiento multiservidor, el servidor local debe configurarse como servidor maestro. En entornos multiservidor, este cuadro de diálogo muestra el servidor maestro **(local)** y todos los servidores de destino correspondientes. Para el servidor local, se crea un trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se habilita o deshabilita dependiendo de si se selecciona el servidor **(local)** . Si se seleccionan servidores de destino, se crea un trabajo multiservidor y se descarga en cada uno de los servidores de destino seleccionados. Si no se seleccionan servidores de destino, el trabajo multiservidor se elimina.  
  
## <a name="see-also"></a>Ver también  
 [Planes de mantenimiento](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Crear un entorno multiservidor](../../ssms/agent/create-a-multiserver-environment.md)   
 [Establecer un servidor maestro](../../ssms/agent/make-a-master-server.md)   
 [Establecer un servidor de destino](../../ssms/agent/make-a-target-server.md)  
  
  
