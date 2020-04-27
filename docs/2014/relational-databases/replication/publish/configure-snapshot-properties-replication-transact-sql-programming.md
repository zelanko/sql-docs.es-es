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
ms.openlocfilehash: b03dd7f886cee5816d591034d1be63ece45d8d1d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63021336"
---
# <a name="configure-snapshot-properties-replication-transact-sql-programming"></a>Configurar propiedades de instantáneas (programación de la replicación con Transact-SQL)
  Las propiedades de las instantáneas se pueden definir y modificar mediante programación usando procedimientos almacenados de replicación, los cuales dependerán del tipo de publicación.  
  
### <a name="to-configure-snapshot-properties-when-creating-a-snapshot-or-transactional-publication"></a>Para configurar propiedades de instantáneas al crear una instantánea o una publicación transaccional  
  
1.  En el publicador, ejecute [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql). Especifique un nombre de publicación **@publication**para, un valor de **Snapshot** o **Continuous** para **@repl_freq**, y uno o varios de los siguientes parámetros relacionados con la instantánea:  
  
    -   **@alt_snapshot_folder**-Especifique una ruta de acceso si se tiene acceso a la instantánea para esta publicación desde esa ubicación en lugar de o además de la carpeta de instantáneas predeterminada.  
  
    -   **@compress_snapshot**-Especifique el valor **true** si los archivos de instantáneas de la carpeta de instantáneas alternativa están [!INCLUDE[msCoName](../../../includes/msconame-md.md)] comprimidos en el formato de archivo. cab.  
  
    -   **@pre_snapshot_script**-Especifique el nombre de archivo y la ruta de acceso completa de un archivo **. SQL** que se ejecutará en el suscriptor durante la inicialización antes de que se aplique la instantánea inicial.  
  
    -   **@post_snapshot_script**-Especifique el nombre de archivo y la ruta de acceso completa de un archivo **. SQL** que se ejecutará en el suscriptor durante la inicialización después de aplicar la instantánea inicial.  
  
    -   **@snapshot_in_defaultfolder**-Especifique el valor **false** si la instantánea solo está disponible en una ubicación que no sea la predeterminada.  
  
     Para obtener más información acerca de la creación de publicaciones, vea [Create a Publication](create-a-publication.md).  
  
### <a name="to-configure-snapshot-properties-when-creating-a-merge-publication"></a>Para configurar propiedades de instantáneas al crear una publicación de combinación  
  
1.  En el publicador, ejecute [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql). Especifique un nombre de publicación **@publication**para, un valor de **Snapshot** o **Continuous** para **@repl_freq**, y uno o varios de los siguientes parámetros relacionados con la instantánea:  
  
    -   **@alt_snapshot_folder**-Especifique una ruta de acceso si se tiene acceso a la instantánea para esta publicación desde esa ubicación en lugar de o además de la carpeta de instantáneas predeterminada.  
  
    -   **@compress_snapshot**-Especifique el valor **true** si los archivos de instantáneas de la carpeta de instantáneas alternativa están comprimidos en el formato de archivo. cab.  
  
    -   **@pre_snapshot_script**-Especifique el nombre de archivo y la ruta de acceso completa de un archivo **. SQL** que se ejecutará en el suscriptor durante la inicialización antes de que se aplique la instantánea inicial.  
  
    -   **@post_snapshot_script**-Especifique el nombre de archivo y la ruta de acceso completa de un archivo **. SQL** que se ejecutará en el suscriptor durante la inicialización después de aplicar la instantánea inicial.  
  
    -   **@snapshot_in_defaultfolder**-Especifique el valor **false** si la instantánea solo está disponible en una ubicación que no sea la predeterminada.  
  
2.  Para obtener más información acerca de la creación de publicaciones, vea [Create a Publication](create-a-publication.md).  
  
### <a name="to-modify-snapshot-properties-of-an-existing-snapshot-or-transactional-publication"></a>Para modificar las propiedades de instantánea de una instantánea o de una publicación transaccional existente  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql). Especifique un valor de **1** para **@force_invalidate_snapshot** y uno de los siguientes valores para **@property**:  
  
    -   **alt_snapshot_folder** : especifique también una nueva ruta de acceso a la carpeta de **@value**instantáneas alternativa para.  
  
    -   **compress_snapshot** -especifique también el valor **true** o **false** para **@value** para indicar si los archivos de instantáneas de la carpeta de instantáneas alternativa están comprimidos en el formato de archivo. cab.  
  
    -   **pre_snapshot_script** -también para **@value** especificar el nombre de archivo y la ruta de acceso completa de un archivo **. SQL** que se ejecutará en el suscriptor durante la inicialización antes de que se aplique la instantánea inicial.  
  
    -   **post_snapshot_script** -también para **@value** especificar el nombre de archivo y la ruta de acceso completa de un archivo **. SQL** que se ejecutará en el suscriptor durante la inicialización después de aplicar la instantánea inicial.  
  
    -   **snapshot_in_defaultfolder** - especifique también el valor **true** o **false** para indicar si la instantánea está disponible únicamente en una ubicación que no es la predeterminada.  
  
2.  (Opcional) En la base de datos de publicación del publicador, ejecute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql). Especifique **@publication** y uno o varios de los parámetros de credenciales de seguridad o de programación que se van a cambiar.  
  
    > [!IMPORTANT]  
    >  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
3.  Ejecute el [Replication Snapshot Agent](../agents/replication-snapshot-agent.md) desde el símbolo del sistema o inicie el trabajo del Agente de instantáneas para generar una nueva instantánea. Para más información, consulte [Crear y aplicar la instantánea inicial](../create-and-apply-the-initial-snapshot.md).  
  
### <a name="to-modify-snapshot-properties-of-an-existing-merge-publication"></a>Para modificar las propiedades de instantánea de una publicación de combinación existente  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql). Especifique un valor de **1** para **@force_invalidate_snapshot** y uno de los siguientes valores para **@property**:  
  
    -   **alt_snapshot_folder** : especifique también una nueva ruta de acceso a la carpeta de **@value**instantáneas alternativa para.  
  
    -   **compress_snapshot** -especifique también el valor **true** o **false** para **@value** para indicar si los archivos de instantáneas de la carpeta de instantáneas alternativa están comprimidos en el formato de archivo. cab.  
  
    -   **pre_snapshot_script** -también para **@value** especificar el nombre de archivo y la ruta de acceso completa de un archivo **. SQL** que se ejecutará en el suscriptor durante la inicialización antes de que se aplique la instantánea inicial.  
  
    -   **post_snapshot_script** -también para **@value** especificar el nombre de archivo y la ruta de acceso completa de un archivo **. SQL** que se ejecutará en el suscriptor durante la inicialización después de aplicar la instantánea inicial.  
  
    -   **snapshot_in_defaultfolder** - especifique también el valor **true** o **false** para indicar si la instantánea está disponible únicamente en una ubicación que no es la predeterminada.  
  
2.  Ejecute el [Replication Snapshot Agent](../agents/replication-snapshot-agent.md) desde el símbolo del sistema o inicie el trabajo del Agente de instantáneas para generar una nueva instantánea. Para más información, consulte [Crear y aplicar la instantánea inicial](../create-and-apply-the-initial-snapshot.md).  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo se crea una publicación que usa una carpeta de instantáneas alternativa y una instantánea comprimida.  
  
 [!code-sql[HowTo#sp_mergealtsnapshot](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubaltsnapshot.sql#sp_mergealtsnapshot)]  
  
## <a name="see-also"></a>Consulte también  
 [Ubicaciones de carpeta de instantáneas alternativas](../alternate-snapshot-folder-locations.md)   
 [Instantáneas comprimidas](../compressed-snapshots.md)   
 [Ejecutar scripts antes y después de aplicar la instantánea](../snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [Transferir instantáneas mediante FTP](../transfer-snapshots-through-ftp.md)   
 [Cambiar las propiedades de la publicación y de los artículos](change-publication-and-article-properties.md)  
  
  
