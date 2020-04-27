---
title: Hacer copias de seguridad y restaurar bases de datos replicadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- backups [SQL Server replication]
- administering replication, restoring
- backing up replicated databases
- backups [SQL Server replication], about backups
- restoring replicated databases [SQL Server replication]
- recovery [SQL Server replication], about recovery
- restoring databases [SQL Server], replicated databases
- backing up databases [SQL Server], replicated databases
- restoring [SQL Server replication], about restoring
- recovery [SQL Server replication]
- replication [SQL Server], administering
- distribution databases [SQL Server replication], backing up
- restoring [SQL Server replication]
- administering replication, backing up
ms.assetid: 04588807-21e7-4bbe-9727-b72f692cffa7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: af4229037b9c34bbc9a0316ef073f294209be6d5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62629648"
---
# <a name="back-up-and-restore-replicated-databases"></a>Hacer copias de seguridad y restaurar bases de datos replicadas
  Las bases de datos replicadas requieren una atención especial en relación con la copia de seguridad y restauración de los datos. En este tema se proporciona información preliminar y vínculos a información adicional sobre las estrategias para realizar copias de seguridad y restauración de cada tipo de replicación.  
  
 La replicación permite restaurar las bases de datos replicadas en el mismo servidor y base de datos de los que se creó la copia de seguridad. Si restaura una copia de seguridad de una base de datos replicada en otro servidor o base de datos, no se conservará la configuración de la replicación. En este caso, debe volver a crear todas las publicaciones y suscripciones después de restaurar las copias de seguridad.  
  
> [!NOTE]  
>  Es posible restaurar una base de datos replicada en un servidor en espera si se utiliza el trasvase de registros. Para obtener más información, vea [Trasvase de registros y replicación &#40;SQL Server&#41;](../../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md).  
  
 La copia de seguridad de las bases de datos replicadas y las bases de datos del sistema asociadas debe realizarse con regularidad. Realice una copia de seguridad de las siguientes bases de datos:  
  
-   Base de datos de publicaciones en el publicador  
  
-   Base de datos de distribución en el distribuidor  
  
-   Base de datos de suscripciones en el suscriptor  
  
-   Las bases de datos del sistema **maestra** y **msdb** en el publicador, el distribuidor y todos los suscriptores. La copia de seguridad de cada una de estas bases de datos debe realizarse al mismo tiempo que la de las otras y la base de datos de replicación correspondiente. Por ejemplo, cree la copia de seguridad de las bases de datos **master** y **msdb** en el publicador al mismo tiempo que crea la copia de seguridad de la base de datos de publicaciones. Al restaurar la base de datos de publicaciones, asegúrese de que las bases de datos **master** y **msdb** sean coherentes con la base de datos de publicaciones en términos de configuración general y configuración de la replicación.  
  
 Si realiza regularmente copias de seguridad de registros, éstas deben capturar todos los cambios relacionados con la replicación. Si no se realizan copias de seguridad de registros, debe realizarse una copia de seguridad siempre que se cambie un valor importante en la replicación. Para más información, vea [Common Actions Requiring an Updated Backup](common-actions-requiring-an-updated-backup.md).  
  
## <a name="backup-and-restore-strategies"></a>Estrategias para realizar copias de seguridad y restauración  
 Las estrategias de copia de seguridad y restauración de cada nodo en una topología de replicación difieren según el tipo de replicación utilizada. Para obtener información sobre las estrategias para realizar copias de seguridad y restauración de cada tipo de replicación, vea los siguientes temas:  
  
-   [Estrategias para hacer copias de seguridad y restaurar replicación de instantáneas o replicación transaccional](strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)  
  
-   [Estrategias para hacer copias de seguridad y restaurar la replicación de mezcla](strategies-for-backing-up-and-restoring-merge-replication.md)  
  
 Como parte de cualquier estrategia de recuperación, mantenga siempre el script actual de la configuración de replicación en un lugar seguro. En el caso de un error en un servidor o de que sea necesario establecer un entorno de pruebas, puede modificar el script con solo cambiar las referencias al nombre del servidor y utilizarla para volver a crear la configuración de replicación. Además de generar script para la configuración de replicación actual, debe generar script para habilitar y deshabilitar la replicación. Para obtener información acerca del scripting para de objetos de replicación, vea [Scripting Replication](../scripting-replication.md).  
  
## <a name="see-also"></a>Consulte también  
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Best Practices for Replication Administration](best-practices-for-replication-administration.md)  
  
  
