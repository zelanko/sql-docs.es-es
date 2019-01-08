---
title: Configurar propiedades de instantáneas (programación de la replicación con Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots [SQL Server replication], properties
ms.assetid: 978d150f-8971-458a-ab2b-3beba5937b46
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 880f2f6fc155338aa65637fbc71402ba7ec55821
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52800217"
---
# <a name="configure-snapshot-properties-replication-transact-sql-programming"></a>Configurar propiedades de instantáneas (programación de la replicación con Transact-SQL)
  Las propiedades de las instantáneas se pueden definir y modificar mediante programación usando procedimientos almacenados de replicación, los cuales dependerán del tipo de publicación.  
  
### <a name="to-configure-snapshot-properties-when-creating-a-snapshot-or-transactional-publication"></a>Para configurar propiedades de instantáneas al crear una instantánea o una publicación transaccional  
  
1.  En el publicador, ejecute [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql). Especifique un nombre de publicación para **@publication**, el valor **snapshot** o **continuous** para **@repl_freq**y uno o más de los siguientes parámetros relacionados con instantáneas:  
  
    -   **@alt_snapshot_folder** - especifique una ruta si a la instantánea de esta publicación se tiene acceso desde esa ubicación en lugar o además de desde la carpeta predeterminada para instantáneas.  
  
    -   **@compress_snapshot** - especifique el valor **true** si los archivos de instantáneas de la carpeta de instantáneas están comprimidos en el formato de archivo CAB de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .  
  
    -   **@pre_snapshot_script** - especifique el nombre de archivo y la ruta completa de un archivo **.sql** que se ejecutará en el suscriptor durante la inicialización antes de que se aplique la instantánea inicial.  
  
    -   **@post_snapshot_script** - especifique el nombre de archivo y la ruta completa de un archivo **.sql** que se ejecutará en el suscriptor durante la inicialización antes de que se aplique la instantánea inicial.  
  
    -   **@snapshot_in_defaultfolder** - especifique el valor **false** si la instantánea únicamente está disponible en una ubicación que no es la predeterminada.  
  
     Para obtener más información acerca de la creación de publicaciones, vea [Create a Publication](create-a-publication.md).  
  
### <a name="to-configure-snapshot-properties-when-creating-a-merge-publication"></a>Para configurar propiedades de instantáneas al crear una publicación de combinación  
  
1.  En el publicador, ejecute [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql). Especifique un nombre de publicación para **@publication**, el valor **snapshot** o **continuous** para **@repl_freq**y uno o más de los siguientes parámetros relacionados con instantáneas:  
  
    -   **@alt_snapshot_folder** - especifique una ruta si a la instantánea de esta publicación se tiene acceso desde esa ubicación en lugar o además de desde la carpeta predeterminada para instantáneas.  
  
    -   **@compress_snapshot** - especifique el valor **true** si los archivos de instantáneas de la carpeta de instantáneas están comprimidos en el formato de archivo CAB.  
  
    -   **@pre_snapshot_script** - especifique el nombre de archivo y la ruta completa de un archivo **.sql** que se ejecutará en el suscriptor durante la inicialización antes de que se aplique la instantánea inicial.  
  
    -   **@post_snapshot_script** - especifique el nombre de archivo y la ruta completa de un archivo **.sql** que se ejecutará en el suscriptor durante la inicialización antes de que se aplique la instantánea inicial.  
  
    -   **@snapshot_in_defaultfolder** - especifique el valor **false** si la instantánea únicamente está disponible en una ubicación que no es la predeterminada.  
  
2.  Para obtener más información acerca de la creación de publicaciones, vea [Create a Publication](create-a-publication.md).  
  
### <a name="to-modify-snapshot-properties-of-an-existing-snapshot-or-transactional-publication"></a>Para modificar las propiedades de instantánea de una instantánea o de una publicación transaccional existente  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql). Especifique el valor **1** para **@force_invalidate_snapshot** y uno de los valores siguientes para **@property**:  
  
    -   **alt_snapshot_folder** - especifique también una nueva ruta a la carpeta de instantáneas alternativa para **@value**.  
  
    -   **compress_snapshot** - especifique también el valor **true** o **false** para **@value** para indicar si los archivos de instantáneas de la carpeta de instantáneas alternativa están comprimidos en el formato de archivo CAB.  
  
    -   **pre_snapshot_script** - especifique también para **@value** el nombre de archivo y la ruta completa de un archivo **.sql** que se ejecutará en el suscriptor durante la inicialización antes de que se aplique la instantánea inicial.  
  
    -   **post_snapshot_script** - especifique también para **@value** el nombre de archivo y la ruta completa de un archivo **.sql** que se ejecutará en el suscriptor durante la inicialización antes de que se aplique la instantánea inicial.  
  
    -   **snapshot_in_defaultfolder** - especifique también el valor **true** o **false** para indicar si la instantánea está disponible únicamente en una ubicación que no es la predeterminada.  
  
2.  (Opcional) En la base de datos de publicación del publicador, ejecute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql). Especifique **@publication** y uno o más de los parámetros de credenciales de seguridad o de programación que se están cambiando.  
  
    > [!IMPORTANT]  
    >  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
3.  Ejecute el [Replication Snapshot Agent](../agents/replication-snapshot-agent.md) desde el símbolo del sistema o inicie el trabajo del Agente de instantáneas para generar una nueva instantánea. Para más información, consulte [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md).  
  
### <a name="to-modify-snapshot-properties-of-an-existing-merge-publication"></a>Para modificar las propiedades de instantánea de una publicación de combinación existente  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql). Especifique el valor **1** para **@force_invalidate_snapshot** y uno de los valores siguientes para **@property**:  
  
    -   **alt_snapshot_folder** - especifique también una nueva ruta a la carpeta de instantáneas alternativa para **@value**.  
  
    -   **compress_snapshot** - especifique también el valor **true** o **false** para **@value** para indicar si los archivos de instantáneas de la carpeta de instantáneas alternativa están comprimidos en el formato de archivo CAB.  
  
    -   **pre_snapshot_script** - especifique también para **@value** el nombre de archivo y la ruta completa de un archivo **.sql** que se ejecutará en el suscriptor durante la inicialización antes de que se aplique la instantánea inicial.  
  
    -   **post_snapshot_script** - especifique también para **@value** el nombre de archivo y la ruta completa de un archivo **.sql** que se ejecutará en el suscriptor durante la inicialización antes de que se aplique la instantánea inicial.  
  
    -   **snapshot_in_defaultfolder** - especifique también el valor **true** o **false** para indicar si la instantánea está disponible únicamente en una ubicación que no es la predeterminada.  
  
2.  Ejecute el [Replication Snapshot Agent](../agents/replication-snapshot-agent.md) desde el símbolo del sistema o inicie el trabajo del Agente de instantáneas para generar una nueva instantánea. Para obtener más información, consulte [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md).  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo se crea una publicación que usa una carpeta de instantáneas alternativa y una instantánea comprimida.  
  
 [!code-sql[HowTo#sp_mergealtsnapshot](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubaltsnapshot.sql#sp_mergealtsnapshot)]  
  
## <a name="see-also"></a>Vea también  
 [Ubicaciones alternativas para las carpetas de instantáneas](../alternate-snapshot-folder-locations.md)   
 [Instantáneas comprimidas](../compressed-snapshots.md)   
 [Ejecutar scripts antes y después de aplicar la instantánea](../execute-scripts-before-and-after-the-snapshot-is-applied.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [Transferir instantáneas mediante FTP](../transfer-snapshots-through-ftp.md)   
 [Cambiar las propiedades de la publicación y de los artículos](change-publication-and-article-properties.md)  
  
  
