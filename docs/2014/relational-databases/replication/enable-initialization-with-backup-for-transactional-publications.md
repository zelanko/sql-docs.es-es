---
title: Habilitar la inicialización con una copia de seguridad para las publicaciones transaccionales (SQL Server Management Studio) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
- transactional replication, backup and restore
- backups [SQL Server replication], transactional replication
ms.assetid: 9df00514-aa9d-4ac6-9766-d226c9958175
caps.latest.revision: 28
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ed84233679e563576e5affe6f889a501904ce897
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107857"
---
# <a name="enable-initialization-with-a-backup-for-transactional-publications-sql-server-management-studio"></a>Habilitar la inicialización con una copia de seguridad para las publicaciones transaccionales (SQL Server Management Studio)
  Para inicializar una suscripción a una publicación transaccional desde una copia de seguridad, habilite la publicación para permitir la inicialización desde la copia de seguridad y, después, especifique la información de la copia de seguridad al crear la suscripción:  
  
-   Habilite la publicación en la página **Opciones de suscripción** del cuadro de diálogo **Propiedades de la publicación: \<Publicación>**. Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  
  
-   Especifique la información de la copia de seguridad con el procedimiento almacenado [sp_addsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql). Para obtener más información sobre los parámetros requeridos por **sp_addsubscription**, consulte [Inicializar una suscripción transaccional desde una copia de seguridad &#40;programación de la replicación con Transact-SQL&#41;](initialize-a-transactional-subscription-from-a-backup.md).  
  
### <a name="to-enable-initialization-with-a-backup"></a>Para habilitar la inicialización con una copia de seguridad  
  
1.  En la página **Opciones de suscripción** del cuadro de diálogo **Propiedades de la publicación: \<Publicación>**, seleccione un valor de **True** para la opción **Permitir inicialización desde archivos de copia de seguridad**.  
  
## <a name="see-also"></a>Vea también  
 [Inicializar una suscripción transaccional sin una instantánea](initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  
