---
title: Habilitación de la inicialización con una copia de seguridad (transaccional)
description: Obtenga información sobre cómo habilitar la inicialización desde una copia de seguridad para las publicaciones transaccionales en SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
- transactional replication, backup and restore
- backups [SQL Server replication], transactional replication
ms.assetid: 9df00514-aa9d-4ac6-9766-d226c9958175
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 11670347380a3336068091601e739b28d4d34a39
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "75321729"
---
# <a name="enable-initialization-with-backup-for-transactional-publications"></a>Habilitar la inicialización con una copia de seguridad para las publicaciones transaccionales
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Para inicializar una suscripción a una publicación transaccional desde una copia de seguridad, habilite la publicación para permitir la inicialización desde la copia de seguridad y, después, especifique la información de la copia de seguridad al crear la suscripción:  
  
-   Habilite la publicación en la página **Opciones de suscripción** del cuadro de diálogo **Propiedades de la publicación: \<Publicación>** . Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
-   Especifique la información de la copia de seguridad con el procedimiento almacenado [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Para obtener más información sobre los parámetros requeridos por **sp_addsubscription**, consulte [Inicializar una suscripción transaccional desde una copia de seguridad &#40;programación de la replicación con Transact-SQL&#41;](../../relational-databases/replication/initialize-a-transactional-subscription-from-a-backup.md).  
  
### <a name="to-enable-initialization-with-a-backup"></a>Para habilitar la inicialización con una copia de seguridad  
  
1.  En la página **Opciones de suscripción** del cuadro de diálogo **Propiedades de la publicación: \<Publicación>** , seleccione un valor de **True** para la opción **Permitir inicialización desde archivos de copia de seguridad**.  
  
## <a name="see-also"></a>Consulte también  
 [Inicializar una suscripción transaccional sin una instantánea](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  
