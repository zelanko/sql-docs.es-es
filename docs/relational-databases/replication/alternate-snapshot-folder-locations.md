---
title: "Ubicaciones alternativas para las carpetas de instantáneas | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], alternate folder locations
- snapshot replication [SQL Server], alternate folder locations
- alternate snapshot folders [SQL Server replication]
ms.assetid: 437553b0-19df-4522-8f27-06b5bc747c69
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 00c990b2fabc64f4cf704cc2fb18999f490507f8
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2018
---
# <a name="alternate-snapshot-folder-locations"></a>Ubicaciones alternativas para las carpetas de instantáneas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Las ubicaciones alternativas para las instantáneas permiten almacenar archivos de instantáneas en una ubicación distinta de la predeterminada o en otra ubicación además de la predeterminada, que suele encontrarse en el distribuidor. Las ubicaciones alternativas pueden encontrarse en otro servidor, en una unidad de red o en medios extraíbles, como discos CD-ROM o discos extraíbles.  
  
 Las ubicaciones alternativas de las instantáneas se almacenan como una propiedad de la publicación. Debido a que la ubicación alternativa de la instantánea es una propiedad de la publicación, el Agente de distribución y el de mezcla pueden localizar la instantánea adecuada como parte del proceso de sincronización.  
  
 Si desea especificar una ubicación diferente para la carpeta de instantáneas o si desea comprimir los archivos de instantáneas, cree la publicación sin crear la instantánea inicial inmediatamente, defina las propiedades de la publicación para la ubicación de la instantánea y ejecute el Agente de instantáneas para dicha publicación. Si cambia la ubicación alternativa después de crear la instantánea inicial, la ubicación de una instantánea generada para la publicación no se reubicará en la nueva ubicación alternativa. En este caso, dependiendo de la configuración de la publicación, es posible que el Agente de mezcla o el Agente de distribución encuentren los archivos de instantáneas en la nueva ubicación alternativa.  
  
> [!NOTE]  
>  No especifique una ubicación alternativa (con el cuadro de diálogo **Propiedades de la publicación** o [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)), que sea la misma que la ubicación de la carpeta predeterminada de instantáneas.  
  
> [!CAUTION]  
>  No use WebSync y las ubicaciones alternativas de carpeta de instantáneas a la vez.  
  
 **Para especificar ubicaciones alternativas de instantáneas**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Especificar una ubicación de carpeta de instantáneas alternativa &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/publish/specify-an-alternate-snapshot-folder-location-sql-server-management-studio.md)  
  
-   Programación de la replicación con [!INCLUDE[tsql](../../includes/tsql-md.md)]: [Configurar propiedades de instantáneas &#40;programación de la replicación con Transact-SQL&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## <a name="see-also"></a>Ver también  
 [Inicializar una suscripción con una instantánea](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Opciones de instantánea](../../relational-databases/replication/snapshot-options.md)  
  
  
