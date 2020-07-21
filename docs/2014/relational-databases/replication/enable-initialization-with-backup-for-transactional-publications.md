---
title: Habilitar la inicialización con una copia de seguridad para las publicaciones transaccionales (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: f5e22614c8c4f5250db3966e747b686091512774
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010723"
---
# <a name="enable-initialization-with-a-backup-for-transactional-publications-sql-server-management-studio"></a>Habilitar la inicialización con una copia de seguridad para las publicaciones transaccionales (SQL Server Management Studio)
  Para inicializar una suscripción a una publicación transaccional desde una copia de seguridad, habilite la publicación para permitir la inicialización desde la copia de seguridad y, después, especifique la información de la copia de seguridad al crear la suscripción:  
  
-   Habilite la publicación en la página **Opciones de suscripción** del cuadro de diálogo Propiedades de la **publicación: \<Publication> ** . Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  
  
-   Especifique la información de la copia de seguridad con el procedimiento almacenado [sp_addsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql). Para obtener más información sobre los parámetros requeridos por **sp_addsubscription**, consulte [Inicializar una suscripción transaccional desde una copia de seguridad &#40;programación de la replicación con Transact-SQL&#41;](initialize-a-transactional-subscription-from-a-backup.md).  
  
### <a name="to-enable-initialization-with-a-backup"></a>Para habilitar la inicialización con una copia de seguridad  
  
1.  En la **Página opciones de suscripción** del cuadro de diálogo Propiedades de la **publicación: \<Publication> ** , seleccione el valor **true** para la opción **permitir inicialización desde archivos de copia de seguridad** .  
  
## <a name="see-also"></a>Consulte también  
 [Inicializar una suscripción transaccional sin una instantánea](initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  
