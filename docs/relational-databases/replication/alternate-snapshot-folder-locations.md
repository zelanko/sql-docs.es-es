---
title: "Ubicaciones alternativas para las carpetas de instant&#225;neas | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "instantáneas [replicación de SQL Server], ubicaciones de carpetas alternativas"
  - "replicación de instantáneas [SQL Server], ubicaciones de carpetas alternativas"
  - "carpetas de instantáneas alternativas [replicación de SQL Server]"
ms.assetid: 437553b0-19df-4522-8f27-06b5bc747c69
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# Ubicaciones alternativas para las carpetas de instant&#225;neas
  Las ubicaciones alternativas para las instantáneas permiten almacenar archivos de instantáneas en una ubicación distinta de la predeterminada o en otra ubicación además de la predeterminada, que suele encontrarse en el distribuidor. Las ubicaciones alternativas pueden encontrarse en otro servidor, en una unidad de red o en medios extraíbles, como discos CD-ROM o discos extraíbles.  
  
 Las ubicaciones alternativas de las instantáneas se almacenan como una propiedad de la publicación. Debido a que la ubicación alternativa de la instantánea es una propiedad de la publicación, el Agente de distribución y el de mezcla pueden localizar la instantánea adecuada como parte del proceso de sincronización.  
  
 Si desea especificar una ubicación diferente para la carpeta de instantáneas o si desea comprimir los archivos de instantáneas, cree la publicación sin crear la instantánea inicial inmediatamente, defina las propiedades de la publicación para la ubicación de la instantánea y ejecute el Agente de instantáneas para dicha publicación. Si cambia la ubicación alternativa después de crear la instantánea inicial, la ubicación de una instantánea generada para la publicación no se reubicará en la nueva ubicación alternativa. En este caso, dependiendo de la configuración de la publicación, es posible que el Agente de mezcla o el Agente de distribución encuentren los archivos de instantáneas en la nueva ubicación alternativa.  
  
> [!NOTE]  
>  No especifica una ubicación alternativa (mediante el **Propiedades de la publicación** cuadro de diálogo o [sp_changepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)) es el mismo que la ubicación predeterminada de la carpeta de instantáneas.  
  
> [!CAUTION]  
>  No use WebSync y las ubicaciones alternativas de carpeta de instantáneas a la vez.  
  
 **Para especificar ubicaciones alternativas de instantáneas**  
  
-   [! INCLUIR [ssManStudioFull] (.. / Token/ssManStudioFull_md.md)]: [Specify an Alternate Snapshot Folder Location &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/publish/specify-an-alternate-snapshot-folder-location-sql-server-management-studio.md)  
  
-   Replicación [!INCLUDE[tsql](../../includes/tsql-md.md)] programming: [Configurar propiedades de la instantánea & #40; Programación de replicación Transact-SQL & #41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## Vea también  
 [Inicializar una suscripción con una instantánea](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Opciones de instantánea](../../relational-databases/replication/snapshot-options.md)  
  
  