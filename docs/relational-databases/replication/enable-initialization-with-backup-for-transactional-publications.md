---
title: "Habilitar la inicialización con una copia de seguridad para las publicaciones transaccionales | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
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
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
- transactional replication, backup and restore
- backups [SQL Server replication], transactional replication
ms.assetid: 9df00514-aa9d-4ac6-9766-d226c9958175
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b674b6debc307a6f87c5244a376174990631a1f0
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2018
---
# <a name="enable-initialization-with-backup-for-transactional-publications"></a>Habilitar la inicialización con una copia de seguridad para las publicaciones transaccionales
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Para inicializar una suscripción a una publicación transaccional desde una copia de seguridad, habilite la publicación para permitir la inicialización desde la copia de seguridad y, después, especifique la información de la copia de seguridad al crear la suscripción:  
  
-   Habilite la publicación en la página **Opciones de suscripción** del cuadro de diálogo **Propiedades de la publicación: \<Publicación>**. Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
-   Especifique la información de la copia de seguridad con el procedimiento almacenado [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Para obtener más información sobre los parámetros requeridos por **sp_addsubscription**, consulte [Inicializar una suscripción transaccional desde una copia de seguridad &#40;programación de la replicación con Transact-SQL&#41;](../../relational-databases/replication/initialize-a-transactional-subscription-from-a-backup.md).  
  
### <a name="to-enable-initialization-with-a-backup"></a>Para habilitar la inicialización con una copia de seguridad  
  
1.  En la página **Opciones de suscripción** del cuadro de diálogo **Propiedades de la publicación: \<Publicación>**, seleccione un valor de **True** para la opción **Permitir inicialización desde archivos de copia de seguridad**.  
  
## <a name="see-also"></a>Ver también  
 [Inicializar una suscripción transaccional sin una instantánea](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  
