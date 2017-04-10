---
title: "Hacer copias de seguridad y restaurar bases de datos replicadas | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "copias de seguridad [replicación de SQL Server]"
  - "administrar replicación, restaurar"
  - "realizar copias de seguridad de bases de datos de replicación"
  - "copias de seguridad [replicación de SQL Server], acerca de las copias de seguridad"
  - "restaurar bases de datos de replicación [replicación de SQL Server]"
  - "recuperación [replicación de SQL Server], acerca de la recuperación"
  - "restaurar bases de datos [SQL Server], bases de datos replicadas"
  - "copia de seguridad de bases de datos [SQL Server], bases de datos replicadas"
  - "restaurar [replicación de SQL Server], acerca de la restauración"
  - "recuperación [replicación de SQL Server]"
  - "replicación [SQL Server], administrar"
  - "bases de datos de distribución [SQL Server], copia de seguridad"
  - "restauración [replicación de SQL Server]"
  - "administrar replicación, copia de seguridad"
ms.assetid: 04588807-21e7-4bbe-9727-b72f692cffa7
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# Hacer copias de seguridad y restaurar bases de datos replicadas
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Las bases de datos replicadas requieren una atención especial en relación con la copia de seguridad y restauración de los datos. En este tema se proporciona información preliminar y vínculos a información adicional sobre las estrategias para realizar copias de seguridad y restauración de cada tipo de replicación.  
  
 La replicación permite restaurar las bases de datos replicadas en el mismo servidor y base de datos de los que se creó la copia de seguridad. Si restaura una copia de seguridad de una base de datos replicada en otro servidor o base de datos, no se conservará la configuración de la replicación. En este caso, debe volver a crear todas las publicaciones y suscripciones después de restaurar las copias de seguridad.  
  
> [!NOTE]  
>  Es posible restaurar una base de datos replicada en un servidor en espera si se utiliza el trasvase de registros. Para obtener más información, consulte [trasvase de registros y replicación & #40; SQL Server & #41;](../../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md).  
  
 La copia de seguridad de las bases de datos replicadas y las bases de datos del sistema asociadas debe realizarse con regularidad. Realice una copia de seguridad de las siguientes bases de datos:  
  
-   Base de datos de publicaciones en el publicador  
  
-   Base de datos de distribución en el distribuidor  
  
-   Base de datos de suscripciones en el suscriptor  
  
-   Las bases de datos del sistema **maestra** y **msdb** en el publicador, el distribuidor y todos los suscriptores. La copia de seguridad de cada una de estas bases de datos debe realizarse al mismo tiempo que la de las otras y la base de datos de replicación correspondiente. Por ejemplo, cree la copia de seguridad de las bases de datos **master** y **msdb** en el publicador al mismo tiempo que crea la copia de seguridad de la base de datos de publicaciones. Al restaurar la base de datos de publicaciones, asegúrese de que las bases de datos **master** y **msdb** sean coherentes con la base de datos de publicaciones en términos de configuración general y configuración de la replicación.  
  
 Si realiza regularmente copias de seguridad de registros, éstas deben capturar todos los cambios relacionados con la replicación. Si no se realizan copias de seguridad de registros, debe realizarse una copia de seguridad siempre que se cambie un valor importante en la replicación. Para más información, consulte [Common Actions Requiring an Updated Backup](../../../relational-databases/replication/administration/common-actions-requiring-an-updated-backup.md).  
  
## Estrategias para realizar copias de seguridad y restauración  
 Las estrategias de copia de seguridad y restauración de cada nodo en una topología de replicación difieren según el tipo de replicación utilizada. Para obtener información sobre las estrategias para realizar copias de seguridad y restauración de cada tipo de replicación, vea los siguientes temas:  
  
-   [Estrategias para hacer copias de seguridad y restaurar replicación de instantáneas o replicación transaccional](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)  
  
-   [Estrategias para hacer copias de seguridad y restaurar la replicación de mezcla](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-merge-replication.md)  
  
 Como parte de cualquier estrategia de recuperación, mantenga siempre el script actual de la configuración de replicación en un lugar seguro. En el caso de un error en un servidor o de que sea necesario establecer un entorno de pruebas, puede modificar el script con solo cambiar las referencias al nombre del servidor y utilizarla para volver a crear la configuración de replicación. Además de generar script para la configuración de replicación actual, debe generar script para habilitar y deshabilitar la replicación. Para obtener información acerca del scripting para de objetos de replicación, vea [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
## Vea también  
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Prácticas recomendadas para la administración de replicación](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)  
  
  