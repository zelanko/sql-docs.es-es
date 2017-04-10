---
title: "Suscriptores | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.subscribers.f1"
helpviewer_keywords: 
  - "suscriptores [replicación de SQL Server]"
ms.assetid: 43fb2454-c220-4d25-a826-83c332eb00d2
caps.latest.revision: 26
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# Suscriptores
  Especifique el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o no-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los suscriptores que recibirán una suscripción a la publicación seleccionada.  
  
## Opciones  
 **Suscriptores**  
 Seleccione la casilla de verificación en la cuadrícula para habilitar el correspondiente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o no-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] origen de datos como un suscriptor a la publicación seleccionada en el **publicación** página. Si el suscriptor no aparece, haga clic en **Agregar suscriptor** o **Agregar suscriptor de SQL Server**.  
  
 **Base de datos de suscripciones**  
 La información mostrada y las acciones disponibles en esta columna dependen del tipo de suscriptor que aparece en el **suscriptores** columna:  
  
-   Para suscriptores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , seleccione una base de datos de suscripciones de la lista **Base de datos de suscripciones** o cree una nueva base de datos seleccionando el comando **Base de datos nueva** de la misma lista.  
  
    > [!NOTE]  
    >  Si va a habilitar el publicador como suscriptor, la base de datos de suscripciones debe ser diferente de la base de datos de publicaciones.  
  
-   Para suscriptores que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la base de datos de suscripciones no aparece. Especifique la base de datos, junto con otra información de conexión, en la **el nombre del origen de datos** campo de la **Agregar no son de SQL Server** cuadro de diálogo. Este cuadro de diálogo está disponible, haga clic en **Agregar suscriptor** y, a continuación, haga clic en **Agregar suscriptor que no son de SQL Server**.  
  
 **Agregar suscriptor**  
 Agregue un servidor a la lista de servidores que pueda habilitarse como suscriptores. Este botón aparece cuando se cumplen todas las condiciones siguientes:  
  
-   La publicación que ha seleccionado es una publicación de instantáneas o transaccional que no admite la actualización de suscripciones.  
  
    > [!NOTE]  
    >  Si la publicación a la que se va a suscribir tiene suscripciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y no está habilitada todavía para suscriptores que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], no se puede agregar una suscripción que no sea de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   La suscripción es una suscripción de inserción.  
  
-   El publicador de la publicación seleccionada es [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o posterior.  
  
 Haga clic en **Agregar suscriptor** muestra un menú con dos opciones: **Agregar suscriptor de SQL Server** y **Agregar suscriptor que no son de SQL Server**. Haga clic en **Agregar suscriptor que no son de SQL Server** para agregar un Oracle o el suscriptor de IBM DB2.  
  
 **Agregar suscriptor de SQL Server**  
 Agregue un servidor a la lista de servidores que pueda habilitarse como suscriptores. Este botón aparece cuando se cumplen una o varias de las condiciones siguientes:  
  
-   La publicación que ha seleccionado es una publicación de combinación, o una publicación de instantáneas o transaccional que admite actualización de suscripciones.  
  
-   La suscripción es una suscripción de extracción.  
  
-   El publicador de la publicación seleccionada es anterior a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para versiones anteriores, este botón solamente aparece cuando se cumplen una o varias de las condiciones siguientes:  
  
    -   Es miembro del rol fijo de servidor **sysadmin** en el publicador.  
  
    -   Se ha agregado el suscriptor a la página **Suscriptores** del cuadro de diálogo **Propiedades del publicador** .  
  
    -   La publicación permite suscripciones anónimas.  
  
## Vea también  
 [Crear una suscripción de extracción](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Crear una suscripción de inserción](../../relational-databases/replication/create-a-push-subscription.md)   
 [Suscriptores que no son de SQL Server](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)  
  
  