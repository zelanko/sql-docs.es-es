---
title: Propiedades del distribuidor, General | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.rep.configdistwizard.distproperties.general.f1
helpviewer_keywords:
- Distributor Properties dialog box
ms.assetid: ab4120ec-e524-4c0c-8b48-f2f40adb1a3b
caps.latest.revision: 22
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 72a19533f68de783317fbea0b8305d9f474b50bb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="distributor-properties-general"></a>Propiedades del distribuidor, General
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La página **General** del cuadro de diálogo **Propiedades del distribuidor** le permite agregar y eliminar bases de datos de distribución y configurar las propiedades de la base de datos de distribución.  
  
 En la base de datos de distribución se almacenan metadatos y datos del historial de todos los tipos de replicación y transacciones de replicación transaccional. En muchas ocasiones, una sola base de datos de distribución resulta suficiente. Pero si varios publicadores utilizan un único distribuidor, podría ser aconsejable crear una base de datos de distribución para cada publicador. De esta forma, se garantiza que los datos que pasan por cada base de datos de distribución son distintos.  
  
## <a name="options"></a>Opciones  
 **Bases de datos**  
 La cuadrícula de propiedades de **Bases de datos** muestra el nombre y las propiedades de retención de las bases de datos del distribuidor. **Retención de transacción** representa el tiempo de almacenamiento de las transacciones de replicación transaccional (la retención de transacción también se denomina retención de distribución). **Retención de historial** representa el tiempo de almacenamiento de los metadatos del historial de todos los tipos de replicación. Para más información sobre la retención de la distribución, vea [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md) (Expiración y desactivación de la suscripción).  
  
 Haga clic en el botón de propiedades (**...**) en la cuadrícula de propiedades de **Bases de datos** para abrir el cuadro de diálogo **Propiedades de base de datos de distribución** .  
  
 **Nueva**  
 Haga clic para crear una nueva base de datos de distribución.  
  
 **Eliminar**  
 Para eliminar una base de datos, seleccione una base de datos de distribución existente en la cuadrícula de propiedades de **Bases de datos** y haga clic en **Eliminar** . No puede eliminar la base de datos de distribución si solo existe dicha base de datos; cada distribuidor debe poseer al menos una base de datos de distribución. Para eliminar todas las bases de datos de distribución, deberá deshabilitar la distribución en el equipo. Para más información, vea [Disable Publishing and Distribution](../../relational-databases/replication/disable-publishing-and-distribution.md) (Deshabilitar la publicación y la distribución).  
  
 **Valores predeterminados de perfil**  
 Haga clic para tener acceso a los perfiles del agente de replicación en el cuadro de diálogo **Perfiles de agente** . Para obtener más información acerca de los perfiles, vea [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## <a name="see-also"></a>Ver también  
 [Configurar distribución](../../relational-databases/replication/configure-distribution.md)   
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)  
  
  
