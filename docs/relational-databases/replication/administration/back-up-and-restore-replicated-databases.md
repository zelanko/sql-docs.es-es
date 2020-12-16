---
title: Hacer copias de seguridad y restaurar bases de datos replicadas | Microsoft Docs
description: Revise la información general y los vínculos a la información adicional sobre las estrategias para realizar copias de seguridad y restauración de cada tipo de replicación en SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: a5b27549630a5ac835e4e9b32f8ebcde5ac6e5d0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97469126"
---
# <a name="back-up-and-restore-replicated-databases"></a>Hacer copias de seguridad y restaurar bases de datos replicadas
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]

  Las bases de datos replicadas requieren una atención especial en relación con la copia de seguridad y restauración de los datos. En este tema se proporciona información preliminar y vínculos a información adicional sobre las estrategias para realizar copias de seguridad y restauración de cada tipo de replicación.  
  
 La replicación permite restaurar las bases de datos replicadas en el mismo servidor y base de datos de los que se creó la copia de seguridad. Si restaura una copia de seguridad de una base de datos replicada en otro servidor o base de datos, no se conservará la configuración de la replicación. En este caso, debe volver a crear todas las publicaciones y suscripciones después de restaurar las copias de seguridad.  
  
> [!NOTE]  
>  Es posible restaurar una base de datos replicada en un servidor en espera si se utiliza el trasvase de registros. Para obtener más información, vea [Trasvase de registros y replicación &#40;SQL Server&#41;](../../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md).  
  
 La copia de seguridad de las bases de datos replicadas y las bases de datos del sistema asociadas debe realizarse con regularidad. Realice una copia de seguridad de las siguientes bases de datos:  
  
-   Base de datos de publicaciones en el publicador  
  
-   Base de datos de distribución en el distribuidor  
  
-   Base de datos de suscripciones en el suscriptor  
  
-   Las bases de datos del sistema **maestra** y **msdb** en el publicador, el distribuidor y todos los suscriptores. La copia de seguridad de cada una de estas bases de datos debe realizarse al mismo tiempo que la de las otras y la base de datos de replicación correspondiente. Por ejemplo, cree la copia de seguridad de las bases de datos **master** y **msdb** en el publicador al mismo tiempo que crea la copia de seguridad de la base de datos de publicaciones. Al restaurar la base de datos de publicaciones, asegúrese de que las bases de datos **master** y **msdb** sean coherentes con la base de datos de publicaciones en términos de configuración general y configuración de la replicación.  
  
 Si realiza regularmente copias de seguridad de registros, éstas deben capturar todos los cambios relacionados con la replicación. Si no se realizan copias de seguridad de registros, debe realizarse una copia de seguridad siempre que se cambie un valor importante en la replicación. Para más información, vea [Common Actions Requiring an Updated Backup](../../../relational-databases/replication/administration/common-actions-requiring-an-updated-backup.md).  
  
## <a name="backup-and-restore-strategies"></a>Estrategias para realizar copias de seguridad y restauración  
 Las estrategias de copia de seguridad y restauración de cada nodo en una topología de replicación difieren según el tipo de replicación utilizada. Para obtener información sobre las estrategias para realizar copias de seguridad y restauración de cada tipo de replicación, vea los siguientes temas:  
  
-   [Estrategias para hacer copias de seguridad y restaurar replicación de instantáneas o replicación transaccional](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)  
  
-   [Estrategias para hacer copias de seguridad y restaurar la replicación de mezcla](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-merge-replication.md)  
  
 Como parte de cualquier estrategia de recuperación, mantenga siempre el script actual de la configuración de replicación en un lugar seguro. En el caso de un error en un servidor o de que sea necesario establecer un entorno de pruebas, puede modificar el script con solo cambiar las referencias al nombre del servidor y utilizarla para volver a crear la configuración de replicación. Además de generar script para la configuración de replicación actual, debe generar script para habilitar y deshabilitar la replicación. Para obtener información acerca del scripting para de objetos de replicación, vea [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
## <a name="see-also"></a>Consulte también  
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Best Practices for Replication Administration](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)  
  
  
