---
title: Plan de mantenimiento (Administrar conexiones) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
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
- sql13.swb.maint.connections.f1
ms.assetid: 95ad9375-6584-423e-b9de-0e86782f8017
caps.latest.revision: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6f7a35cc6e39beb2e81b092d862b881e4922c491
ms.sourcegitcommit: 6e16d1616985d65484c72f5e0f34fb2973f828f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/16/2018
---
# <a name="maintenance-plan-manage-connections"></a>Plan de mantenimiento (Administrar conexiones)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilice el cuadro de diálogo **Administrar conexiones** para especificar las propiedades de las conexiones que utilizan los planes de mantenimiento. Cuando crea un plan de mantenimiento, se crea una conexión local al servidor donde se ha creado el plan. Utilice esta conexión para crear tareas que realicen trabajos en esta conexión local. Si es necesario, utilice el cuadro de diálogo **Administrar conexiones** para agregarlas. Cuando se configuran conexiones adicionales, éstas aparecen en el cuadro de conexiones de las tareas.  
  
## <a name="options"></a>.  
 **Server**  
 Instancia del servidor.  
  
 **Autenticación**  
 Indica si la conexión se establece con autenticación de Windows o autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

> [!IMPORTANT]  
> El paquete está almacenado en la base de datos **msdb** con su **ProtectionLevel** establecido en **ServerStorage**, por lo que cuando se use la *autenticación de SQL Server*, la contraseña no se cifrará en **msdb**. Puede usar la *autenticación de SQL Server* mientras la base de datos **msdb** sea segura, aunque se recomienda usar la *autenticación de Windows*.

## <a name="see-also"></a>Ver también  
 [Planes de mantenimiento](../../relational-databases/maintenance-plans/maintenance-plans.md)  
  
  
