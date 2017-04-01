---
title: "Propiedades del distribuidor, General | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.configdistwizard.distproperties.general.f1"
helpviewer_keywords: 
  - "Propiedades del distribuidor, cuadro de diálogo"
ms.assetid: ab4120ec-e524-4c0c-8b48-f2f40adb1a3b
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Propiedades del distribuidor, General
  La página **General** del cuadro de diálogo **Propiedades del distribuidor** le permite agregar y eliminar bases de datos de distribución y configurar las propiedades de la base de datos de distribución.  
  
 En la base de datos de distribución se almacenan metadatos y datos del historial de todos los tipos de replicación y transacciones de replicación transaccional. En muchas ocasiones, una sola base de datos de distribución resulta suficiente. Pero si varios publicadores utilizan un único distribuidor, podría ser aconsejable crear una base de datos de distribución para cada publicador. De esta forma, se garantiza que los datos que pasan por cada base de datos de distribución son distintos.  
  
## Opciones  
 **Bases de datos**  
 El **bases de datos** cuadrícula de propiedades muestra las propiedades name y retención de las bases de datos de distribución en el distribuidor. **Retención de transacción** es la longitud de las transacciones de hora se almacenan en la replicación transaccional (retención de transacción también es conocido como retención de distribución). **Retención de historial** representa el tiempo de almacenamiento de los metadatos del historial de todos los tipos de replicación. Para obtener más información acerca de la retención de distribución, consulte [caducidad de la suscripción y la desactivación](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
 Haga clic en el botón de propiedades (**...**) en el **bases de datos** cuadrícula de propiedad para iniciar el **Propiedades de la base de datos de distribución** cuadro de diálogo.  
  
 **Nuevo**  
 Haga clic para crear una nueva base de datos de distribución.  
  
 **Delete**  
 Seleccione una base de datos de distribución existente en el **bases de datos** cuadrícula de propiedades y haga clic en **Eliminar** para eliminar la base de datos. No puede eliminar la base de datos de distribución si solo existe dicha base de datos; cada distribuidor debe poseer al menos una base de datos de distribución. Para eliminar todas las bases de datos de distribución, deberá deshabilitar la distribución en el equipo. Para obtener más información, consulte [Deshabilitar la publicación y distribución](../../relational-databases/replication/disable-publishing-and-distribution.md).  
  
 **Valores predeterminados de perfil**  
 Haga clic en perfiles de agente de replicación de acceso en la **perfiles de agente** cuadro de diálogo. Para obtener más información acerca de los perfiles, vea [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## Vea también  
 [Configurar la distribución](../../relational-databases/replication/configure-distribution.md)   
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)  
  
  