---
title: "Inicializar una suscripci&#243;n transaccional desde una copia de seguridad (programaci&#243;n de la replicaci&#243;n con Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/29/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "inicialización de suscripción manual [replicación de SQL Server]"
  - "suscripciones [replicación de SQL Server], inicializar"
  - "inicializar suscripciones [replicación de SQL Server], sin instantáneas"
  - "replicación transaccional, copia de seguridad y restauración"
  - "copias de seguridad [replicación de SQL Server], replicación transaccional"
ms.assetid: d0637fc4-27cc-4046-98ea-dc86b7a3bd75
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Inicializar una suscripci&#243;n transaccional desde una copia de seguridad (programaci&#243;n de la replicaci&#243;n con Transact-SQL)
  Aunque una suscripción a una publicación transaccional se inicializa normalmente con una instantánea, también se puede inicializar desde una copia de seguridad mediante procedimientos almacenados de replicación. Para obtener más información, consulte [inicializar una suscripción transaccional sin una instantánea](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
### Para inicializar una suscripción transaccional desde una copia de seguridad  
  
1.  Para una publicación existente, asegúrese de que la publicación admite la capacidad de inicializar desde copia de seguridad mediante la ejecución de [sp_helppublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md) en el publicador de la base de datos de publicación. Tenga en cuenta el valor de **allow_initialize_from_backup** conjunto de resultados.  
  
    -   Si el valor es **1**, la publicación admite esta funcionalidad.  
  
    -   Si el valor es **0**, ejecute [sp_changepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) en el publicador de la base de datos de publicación. Especifique un valor de **allow_initialize_from_backup** para **@property** y un valor de **true** para **@value**.  
  
2.  Para obtener una nueva publicación, ejecute [sp_addpublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) en el publicador de la base de datos de publicación. Especifique un valor de **true** para **allow_initialize_from_backup**. Para obtener más información, consulte [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
    > [!WARNING]  
    >  Para evitar la pérdida de datos del suscriptor, al usar **sp_addpublication** con `@allow_initialize_from_backup = N'true'`, utilice siempre `@immediate_sync = N'true'`.  
  
3.  Crear una copia de seguridad de la base de datos de publicación con el [copia de seguridad y Nº 40; Transact-SQL & #41;](../../t-sql/statements/backup-transact-sql.md) instrucción.  
  
4.  Restaurar la copia de seguridad en el suscriptor utilizando el [Restaurar & #40; Transact-SQL & #41;](../Topic/RESTORE%20\(Transact-SQL\).md) instrucción.  
  
5.  En el publicador de la base de datos de publicación, ejecute el procedimiento almacenado [sp_addsubscription & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Especifique los parámetros siguientes:  
  
    -   **@sync_type** -un valor de **inicializar con copia de seguridad**.  
  
    -   **@backupdevicetype** -el tipo de dispositivo de copia de seguridad: **lógico** (valor predeterminado), **disco**, o **cinta**.  
  
    -   **@backupdevicename** -el dispositivo de copia de seguridad físico o lógico que se utilizará para la restauración.  
  
         Para un dispositivo lógico, especifique el nombre del dispositivo de copia de seguridad especificado cuando **sp_addumpdevice** se utilizó para crear el dispositivo.  
  
         Para un dispositivo físico, especifique una ruta de acceso y un nombre de archivo completos, como `DISK = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\BACKUP\Mybackup.dat'` o `TAPE = '\\.\TAPE0'`.  
  
    -   (Opcional) **@password** -una contraseña que se proporcionó cuando se creó el conjunto de copia de seguridad.  
  
    -   (Opcional) **@mediapassword** -una contraseña que le proporcionó al dar formato al conjunto de medios.  
  
    -   (Opcional) **@fileidhint** -identificador de la copia de seguridad que se restaure. Por ejemplo, **1** indica el primer conjunto de copia de seguridad del medio de copia de seguridad y **2** indica el segundo conjunto de copia de seguridad.  
  
    -   (Opcional para los dispositivos de cinta) **@unload** -Especifique un valor de **1** (valor predeterminado) si se debe descargar desde la unidad de la cinta una vez finalizada la restauración y **0** Si no debe descargarse.  
  
6.  (Opcional) Para una suscripción de extracción, ejecute [sp_addpullsubscription & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md) y [sp_addpullsubscription_agent & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) en el suscriptor de la base de datos de suscripción. Para más información, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
7.  (Opcional) Inicio el Agente de distribución. Para obtener más información, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) o [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
## Vea también  
 [Copiar bases de datos con Copias de seguridad y restauración](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  