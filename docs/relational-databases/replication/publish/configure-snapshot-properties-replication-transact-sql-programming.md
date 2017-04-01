---
title: "Configurar propiedades de instant&#225;neas (programaci&#243;n de la replicaci&#243;n con Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
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
  - "instantáneas [replicación de SQL Server], propiedades"
ms.assetid: 978d150f-8971-458a-ab2b-3beba5937b46
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Configurar propiedades de instant&#225;neas (programaci&#243;n de la replicaci&#243;n con Transact-SQL)
  Las propiedades de las instantáneas se pueden definir y modificar mediante programación usando procedimientos almacenados de replicación, los cuales dependerán del tipo de publicación.  
  
### Para configurar propiedades de instantáneas al crear una instantánea o una publicación transaccional  
  
1.  En el publicador, ejecute [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md). Especifique un nombre de publicación para **@publication**, valor **instantánea** o **continua** para **@repl_freq**, y uno o más de los siguientes parámetros relacionados con instantáneas:  
  
    -   **@alt_snapshot_folder** -Especifique una ruta de acceso si se tiene acceso a la instantánea para esta publicación desde esa ubicación en lugar de o además de la carpeta de instantáneas predeterminada.  
  
    -   **@compress_snapshot** -Especifique un valor de **true** si los archivos de instantáneas en la carpeta de instantáneas alternativa están comprimidos en el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] formato de archivo CAB.  
  
    -   **@pre_snapshot_script** -Especifique el nombre de archivo y ruta de acceso completa de un **.sql** archivo que se ejecuta en el suscriptor durante la inicialización antes de aplica la instantánea inicial.  
  
    -   **@post_snapshot_script** -Especifique el nombre de archivo y ruta de acceso completa de un **.sql** archivo que se ejecuta en el suscriptor durante la inicialización después de aplicar la instantánea inicial.  
  
    -   **@snapshot_in_defaultfolder** -Especifique un valor de **false** Si la instantánea sólo está disponible en una ubicación no predeterminada.  
  
     Para obtener más información acerca de la creación de publicaciones, vea [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
### Para configurar propiedades de instantáneas al crear una publicación de combinación  
  
1.  En el publicador, ejecute [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Especifique un nombre de publicación para **@publication**, valor **instantánea** o **continua** para **@repl_freq**, y uno o más de los siguientes parámetros relacionados con instantáneas:  
  
    -   **@alt_snapshot_folder** -Especifique una ruta de acceso si se tiene acceso a la instantánea para esta publicación desde esa ubicación en lugar de o además de la carpeta de instantáneas predeterminada.  
  
    -   **@compress_snapshot** -Especifique un valor de **true** si los archivos de instantáneas en la carpeta de instantáneas alternativa están comprimidos en formato de archivo CAB.  
  
    -   **@pre_snapshot_script** -Especifique el nombre de archivo y ruta de acceso completa de un **.sql** archivo que se ejecuta en el suscriptor durante la inicialización antes de aplica la instantánea inicial.  
  
    -   **@post_snapshot_script** -Especifique el nombre de archivo y ruta de acceso completa de un **.sql** archivo que se ejecuta en el suscriptor durante la inicialización después de aplicar la instantánea inicial.  
  
    -   **@snapshot_in_defaultfolder** -Especifique un valor de **false** Si la instantánea sólo está disponible en una ubicación no predeterminada.  
  
2.  Para obtener más información acerca de la creación de publicaciones, vea [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
### Para modificar las propiedades de instantánea de una instantánea o de una publicación transaccional existente  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md). Especifique un valor de **1** para **@force_invalidate_snapshot** y uno de los siguientes valores para **@property**:  
  
    -   **alt_snapshot_folder** -Especifique también una nueva ruta de acceso a la carpeta de instantáneas alternativa para **@value**.  
  
    -   **compress_snapshot** -también especificar un valor de uno de ellos **true** o **false** para **@value** para indicar si los archivos de instantáneas en la carpeta de instantáneas alternativa están comprimidos en formato de archivo.  
  
    -   **pre_snapshot_script** - también para **@value** especificar el nombre de archivo y ruta de acceso completa de un **.sql** archivo que se ejecuta en el suscriptor durante la inicialización antes de aplica la instantánea inicial.  
  
    -   **post_snapshot_script** - también para **@value** especificar el nombre de archivo y ruta de acceso completa de un **.sql** archivo que se ejecuta en el suscriptor durante la inicialización después de aplicar la instantánea inicial.  
  
    -   **snapshot_in_defaultfolder** -también especificar un valor de uno de ellos **true** o **false** para indicar si la instantánea está disponible sólo en una ubicación no predeterminada.  
  
2.  (Opcional) En el publicador de la base de datos de publicación, ejecute [sp_changepublication_snapshot](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md). Especifique **@publication** y uno o más de los parámetros de credenciales de seguridad o de programación que se están cambiando.  
  
    > [!IMPORTANT]  
    >  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
3.  Ejecute el [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md) desde el símbolo del sistema o inicie el trabajo del Agente de instantáneas para generar una nueva instantánea. Para más información, consulte [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
### Para modificar las propiedades de instantánea de una publicación de combinación existente  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md). Especifique un valor de **1** para **@force_invalidate_snapshot** y uno de los siguientes valores para **@property**:  
  
    -   **alt_snapshot_folder** -Especifique también una nueva ruta de acceso a la carpeta de instantáneas alternativa para **@value**.  
  
    -   **compress_snapshot** -también especificar un valor de uno de ellos **true** o **false** para **@value** para indicar si los archivos de instantáneas en la carpeta de instantáneas alternativa están comprimidos en formato de archivo.  
  
    -   **pre_snapshot_script** - también para **@value** especificar el nombre de archivo y ruta de acceso completa de un **.sql** archivo que se ejecuta en el suscriptor durante la inicialización antes de aplica la instantánea inicial.  
  
    -   **post_snapshot_script** - también para **@value** especificar el nombre de archivo y ruta de acceso completa de un **.sql** archivo que se ejecuta en el suscriptor durante la inicialización después de aplicar la instantánea inicial.  
  
    -   **snapshot_in_defaultfolder** -también especificar un valor de uno de ellos **true** o **false** para indicar si la instantánea está disponible sólo en una ubicación no predeterminada.  
  
2.  Ejecute el [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md) desde el símbolo del sistema o inicie el trabajo del Agente de instantáneas para generar una nueva instantánea. Para obtener más información, consulte [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
## Ejemplo  
 En este ejemplo se crea una publicación que usa una carpeta de instantáneas alternativa y una instantánea comprimida.  
  
 [!code-sql[HowTo#sp_mergealtsnapshot](../../../relational-databases/replication/codesnippet/tsql/configure-snapshot-prope_1.sql)]  
  
## Vea también  
 [Ubicaciones alternativas para las carpetas de instantáneas](../../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [Instantáneas comprimidas](../../../relational-databases/replication/compressed-snapshots.md)   
 [Ejecutar scripts antes y después de aplicar la instantánea](../../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)   
 [Conceptos sobre los procedimientos almacenados del sistema de replicación](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Transferir instantáneas mediante FTP](../../../relational-databases/replication/transfer-snapshots-through-ftp.md)   
 [Cambiar las propiedades de la publicación y de los artículos](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)  
  
  