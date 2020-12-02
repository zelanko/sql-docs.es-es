---
description: Plan de mantenimiento (Servidores)
title: Plan de mantenimiento (Servidores) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.servers.f1
- sql13.swb.maint.maintplanproperties.server.f1
ms.assetid: ac24d1a8-dd2f-4162-b804-c0df1fc1e61d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1a991404f0acaba448958773f54a4836032ecd07
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/26/2020
ms.locfileid: "88420859"
---
# <a name="maintenance-plan-servers"></a>Plan de mantenimiento (Servidores)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
   Use el cuadro de diálogo **Servidores** para seleccionar los servidores donde desea ejecutar el plan de mantenimiento.  
  
 Para crear un plan de mantenimiento multiservidor debe configurarse un entorno multiservidor que contenga un servidor maestro y uno o varios servidores de destino. En los planes de mantenimiento multiservidor, el servidor local debe configurarse como servidor maestro. En entornos multiservidor, este cuadro de diálogo muestra el servidor maestro **(local)** y todos los servidores de destino correspondientes. Para el servidor local, se crea un trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se habilita o deshabilita dependiendo de si se selecciona el servidor **(local)** . Si se seleccionan servidores de destino, se crea un trabajo multiservidor y se descarga en cada uno de los servidores de destino seleccionados. Si no se seleccionan servidores de destino, el trabajo multiservidor se elimina.  
  
## <a name="see-also"></a>Vea también  
 [Planes de mantenimiento](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Crear un entorno multiservidor](../../ssms/agent/create-a-multiserver-environment.md)   
 [Establecer un servidor maestro](../../ssms/agent/make-a-master-server.md)   
 [Establecer un servidor de destino](../../ssms/agent/make-a-target-server.md)  
  
  
