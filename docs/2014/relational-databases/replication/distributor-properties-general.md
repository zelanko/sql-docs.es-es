---
title: Propiedades del distribuidor, General | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rep.configdistwizard.distproperties.general.f1
helpviewer_keywords:
- Distributor Properties dialog box
ms.assetid: ab4120ec-e524-4c0c-8b48-f2f40adb1a3b
caps.latest.revision: 21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d2a32e262bd8096ad77ce0ea813e7ced8440c1dc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37324185"
---
# <a name="distributor-properties-general"></a>Propiedades del distribuidor, General
  La página **General** del cuadro de diálogo **Propiedades del distribuidor** le permite agregar y eliminar bases de datos de distribución y configurar las propiedades de la base de datos de distribución.  
  
 En la base de datos de distribución se almacenan metadatos y datos del historial de todos los tipos de replicación y transacciones de replicación transaccional. En muchas ocasiones, una sola base de datos de distribución resulta suficiente. Pero si varios publicadores utilizan un único distribuidor, podría ser aconsejable crear una base de datos de distribución para cada publicador. De esta forma, se garantiza que los datos que pasan por cada base de datos de distribución son distintos.  
  
## <a name="options"></a>Opciones  
 **Bases de datos**  
 La cuadrícula de propiedades de **Bases de datos** muestra el nombre y las propiedades de retención de las bases de datos del distribuidor. **Retención de transacción** representa el tiempo de almacenamiento de las transacciones de replicación transaccional (la retención de transacción también se denomina retención de distribución). **Retención de historial** representa el tiempo de almacenamiento de los metadatos del historial de todos los tipos de replicación. Para más información sobre la retención de la distribución, vea [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md) (Expiración y desactivación de la suscripción).  
  
 Haga clic en el botón de propiedades (**...**) en la cuadrícula de propiedades de **Bases de datos** para abrir el cuadro de diálogo **Propiedades de base de datos de distribución** .  
  
 **Nueva**  
 Haga clic para crear una nueva base de datos de distribución.  
  
 **Eliminar**  
 Para eliminar una base de datos, seleccione una base de datos de distribución existente en la cuadrícula de propiedades de **Bases de datos** y haga clic en **Eliminar** . No puede eliminar la base de datos de distribución si solo existe dicha base de datos; cada distribuidor debe poseer al menos una base de datos de distribución. Para eliminar todas las bases de datos de distribución, deberá deshabilitar la distribución en el equipo. Para más información, vea [Disable Publishing and Distribution](disable-publishing-and-distribution.md) (Deshabilitar la publicación y la distribución).  
  
 **Valores predeterminados de perfil**  
 Haga clic para tener acceso a los perfiles del agente de replicación en el cuadro de diálogo **Perfiles de agente** . Para obtener más información acerca de los perfiles, vea [Replication Agent Profiles](agents/replication-agent-profiles.md).  
  
## <a name="see-also"></a>Vea también  
 [Configurar distribución](configure-distribution.md)   
 [Ver y modificar las propiedades del distribuidor y del publicador](view-and-modify-distributor-and-publisher-properties.md)  
  
  
