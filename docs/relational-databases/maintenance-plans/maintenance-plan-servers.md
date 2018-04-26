---
title: Plan de mantenimiento (Servidores) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: maintenance-plans
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.maint.servers.f1
- sql13.swb.maint.maintplanproperties.server.f1
ms.assetid: ac24d1a8-dd2f-4162-b804-c0df1fc1e61d
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0d5dc28d4981d00b357f292724a2899d703f4f89
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="maintenance-plan-servers"></a>Plan de mantenimiento (Servidores)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use el cuadro de diálogo **Servidores** para seleccionar los servidores donde desea ejecutar el plan de mantenimiento.  
  
 Para crear un plan de mantenimiento multiservidor debe configurarse un entorno multiservidor que contenga un servidor maestro y uno o varios servidores de destino. En los planes de mantenimiento multiservidor, el servidor local debe configurarse como servidor maestro. En entornos multiservidor, este cuadro de diálogo muestra el servidor maestro **(local)** y todos los servidores de destino correspondientes. Para el servidor local, se crea un trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se habilita o deshabilita dependiendo de si se selecciona el servidor **(local)** . Si se seleccionan servidores de destino, se crea un trabajo multiservidor y se descarga en cada uno de los servidores de destino seleccionados. Si no se seleccionan servidores de destino, el trabajo multiservidor se elimina.  
  
## <a name="see-also"></a>Ver también  
 [Planes de mantenimiento](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Crear un entorno multiservidor](http://msdn.microsoft.com/library/edc2b60d-15da-40a1-8ba3-f1d473366ee6)   
 [Establecer un servidor maestro](http://msdn.microsoft.com/library/05739a73-1fdf-4d9d-92a6-70f328380322)   
 [Establecer un servidor de destino](http://msdn.microsoft.com/library/13aabe2d-67fe-4c67-8d49-2928dd705b7a)  
  
  
