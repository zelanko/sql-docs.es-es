---
title: Plan de mantenimiento (Servidores) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.maint.servers.f1
- sql13.swb.maint.maintplanproperties.server.f1
ms.assetid: ac24d1a8-dd2f-4162-b804-c0df1fc1e61d
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 758892ce93264618ee293e8a5de074ab2a513f11
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="maintenance-plan-servers"></a>Plan de mantenimiento (Servidores)
  Use el cuadro de diálogo **Servidores** para seleccionar los servidores donde desea ejecutar el plan de mantenimiento.  
  
 Para crear un plan de mantenimiento multiservidor debe configurarse un entorno multiservidor que contenga un servidor maestro y uno o varios servidores de destino. En los planes de mantenimiento multiservidor, el servidor local debe configurarse como servidor maestro. En entornos multiservidor, este cuadro de diálogo muestra el servidor maestro **(local)** y todos los servidores de destino correspondientes. Para el servidor local, se crea un trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se habilita o deshabilita dependiendo de si se selecciona el servidor **(local)** . Si se seleccionan servidores de destino, se crea un trabajo multiservidor y se descarga en cada uno de los servidores de destino seleccionados. Si no se seleccionan servidores de destino, el trabajo multiservidor se elimina.  
  
## <a name="see-also"></a>Vea también  
 [Planes de mantenimiento](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Crear un entorno multiservidor](http://msdn.microsoft.com/library/edc2b60d-15da-40a1-8ba3-f1d473366ee6)   
 [Establecer un servidor maestro](http://msdn.microsoft.com/library/05739a73-1fdf-4d9d-92a6-70f328380322)   
 [Establecer un servidor de destino](http://msdn.microsoft.com/library/13aabe2d-67fe-4c67-8d49-2928dd705b7a)  
  
  
