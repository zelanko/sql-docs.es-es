---
title: Inicialización de una suscripción desde una copia de seguridad (transaccional)
description: Obtenga información sobre cómo usar procedimientos almacenados de replicación para inicializar una publicación transaccional a partir de una copia de seguridad en SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
- transactional replication, backup and restore
- backups [SQL Server replication], transactional replication
ms.assetid: d0637fc4-27cc-4046-98ea-dc86b7a3bd75
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7d2da79cc46ac546099e492af3b6d5f4f726a2a2
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "75320482"
---
# <a name="initialize-a-transactional-subscription-from-a-backup"></a>Inicializar una suscripción transaccional desde una copia de seguridad
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Aunque una suscripción a una publicación transaccional se inicializa normalmente con una instantánea, también se puede inicializar desde una copia de seguridad mediante procedimientos almacenados de replicación. Para obtener más información, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
### <a name="to-initialize-a-transactional-subscriber-from-a-backup"></a>Para inicializar una suscripción transaccional desde una copia de seguridad  
  
1.  En una publicación existente, asegúrese de que la publicación admite la capacidad de inicializarse desde la copia de seguridad ejecutando [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md) en la base de datos de publicación del publicador. Tenga en cuenta el valor de **allow_initialize_from_backup** en el conjunto de resultados.  
  
    -   Si el valor es **1**, la publicación admite esta funcionalidad.  
  
    -   Si el valor es **0**, ejecute [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) en el Publicador de la base de datos de publicación. Especifique un valor de **allow_initialize_from_backup** para `@property` y un valor de **true** para `@value`.  
  
2.  Para una nueva publicación, ejecute [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) en el Publicador de la base de datos de publicación. Especifique un valor de **true** para **allow_initialize_from_backup**. Para obtener más información, vea [Crear una suscripción](../../relational-databases/replication/publish/create-a-publication.md).  
  
    > [!WARNING]  
    >  Para evitar perder los datos del suscriptor, al utilizar **sp_addpublication** o **sp_changepublication** con `@allow_initialize_from_backup = N'true'`, utilice siempre `@immediate_sync = N'true'`.  
  
3.  Cree una copia de seguridad de la base de datos de publicación con la instrucción [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md).  
  
4.  Restaure la copia de seguridad en el suscriptor con la instrucción [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
5.  En la base de datos de publicación del publicador, ejecute el procedimiento almacenado [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Especifique los parámetros siguientes:  
  
    -   `@sync_type`: un valor de **initialize with backup**.  
  
    -   `@backupdevicetype`: el tipo de dispositivo de copia de seguridad: **logical** (predeterminado), **disk** o **tape**.  
  
    -   `@backupdevicename`: el dispositivo de copia de seguridad físico o lógico que se va a usar para la restauración.  
  
         Para una unidad lógica, especifique el nombre del dispositivo de copia de seguridad especificado cuando se usó **sp_addumpdevice** para crear el dispositivo.  
  
         Para un dispositivo físico, especifique una ruta de acceso y un nombre de archivo completos, como `DISK = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\BACKUP\Mybackup.dat'` o `TAPE = '\\.\TAPE0'`.  
  
    -   (Opcional) `@password`: una contraseña que se ha proporcionado al crear el conjunto de copia de seguridad.  
  
    -   (Opcional) `@mediapassword`: una contraseña que se ha proporcionado al dar formato al conjunto de medios.  
  
    -   (Opcional) `@fileidhint`: el identificador para el conjunto de copia de seguridad que se va a restaurar. Por ejemplo, **1** indica el primer conjunto de copia de seguridad del medio de copia de seguridad y **2** indica el segundo conjunto de copia de seguridad.  
  
    -   (Opcional para los dispositivos de cinta) `@unload`: especifique un valor de **1** (predeterminado) si la cinta se debe descargar de la unidad una vez completada la restauración y de **0** si no se debe descargar.  
  
6.  (Opcional) Para una suscripción de extracción, ejecute [sp_addpullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md) y [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) en el suscriptor de la base de datos de suscripción. Para obtener más información, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
7.  (Opcional) Inicio el Agente de distribución. Para obtener más información, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) o [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
## <a name="see-also"></a>Consulte también  
 [Copiar bases de datos con Copias de seguridad y restauración](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
 [Copia de seguridad y restauración de bases de datos de SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  
