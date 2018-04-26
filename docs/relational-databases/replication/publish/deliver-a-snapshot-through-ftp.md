---
title: Entrega de una instantánea mediante FTP | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], FTP snapshots
- FTP snapshots [SQL Server replication]
- snapshot replication [SQL Server], FTP
ms.assetid: 99872c4f-40ce-4405-8fd4-44052d3bd827
caps.latest.revision: 47
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 207a9bcdce9192deb91a02e579978468d541404b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="deliver-a-snapshot-through-ftp"></a>Entregar una instantánea mediante FTP
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo entregar una instantánea a través de FTP en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Requisitos previos](#Prerequisites)  
  
     [Seguridad](#Security)  
  
-   **Para entregar una instantánea mediante FTP con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   El Agente de instantáneas debe tener permisos de escritura para el directorio especificado y el Agente de distribución o de mezcla debe tener permisos de lectura. Si usa suscripciones de extracción, debe especificar un directorio compartido como una ruta de acceso UNC (Convención de nomenclatura universal), por ejemplo, \\\servidorFTP\inicio\instantáneas. Para obtener más información, vea [Proteger la carpeta de instantáneas](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   Para transferir archivos de instantáneas con el Protocolo de transferencia de archivos (FTP), primero debe configurar un servidor de FTP. Para obtener más información, vea la documentación de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Internet Information Services (IIS).  
  
###  <a name="Security"></a> Seguridad  
 Para contribuir a mejorar la seguridad, se recomienda implementar una red privada virtual (VPN) al utilizar la entrega de instantáneas a través de FTP por Internet. Para obtener más información, vea [Publish Data over the Internet Using VPN](../../../relational-databases/replication/publish-data-over-the-internet-using-vpn.md) (Publicar datos a través de Internet mediante VPN).  
  
 Por seguridad, se recomienda no permitir el inicio de sesión anónimo en el servidor de FTP. El Agente de instantáneas debe tener permisos de escritura para el directorio especificado y el Agente de distribución o de mezcla debe tener permisos de lectura. Si usa suscripciones de extracción, debe especificar un directorio compartido como una ruta de acceso UNC (Convención de nomenclatura universal), por ejemplo, \\\servidorFTP\inicio\instantáneas. Para obtener más información, vea [Proteger la carpeta de instantáneas](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
 Cuando sea posible, pida a los usuarios que proporcionen sus credenciales en tiempo de ejecución. Si almacena las credenciales en un archivo de script, debe proteger el archivo.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Una vez configurado el servidor de FTP, especifique el directorio y la información de seguridad para este servidor en el cuadro de diálogo **Propiedades de la publicación: \<publicación>**. Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-ftp-information"></a>Para especificar la información de FTP  
  
1.  En el cuadro de diálogo **Propiedades de la publicación: \<publicación>**, seleccione **Permitir a los suscriptores descargar archivos de instantánea usando FTP (Protocolo de transferencia de archivos)** en una de las páginas siguientes:  
  
    -   La página **Instantánea de FTP** , para las publicaciones transaccionales y de instantáneas, y las publicaciones de combinación para los publicadores que ejecuten versiones anteriores a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
    -   La página **Instantánea de FTP e Internet** , para las publicaciones de combinación de los publicadores que ejecuten [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o posterior.  
  
2.  Especifique valores para **Nombre del servidor FTP**, **Número de puerto**, **Ruta de acceso de la carpeta raíz del servidor FTP**, **Inicio de sesión**y **Contraseña**.  
  
     Por ejemplo, si el directorio raíz del servidor de FTP es \\\servidorFTP\inicio y desea almacenar las instantáneas en \\\servidorFTP\inicio\instantáneas, especifique \instantáneas\ftp para la propiedad **Ruta de acceso de la carpeta raíz del servidor FTP** (la replicación adjunta 'ftp' a la ruta de acceso de la carpeta de instantáneas al crear los archivos de instantáneas).  
  
3.  Especifique que el Agente de instantáneas copie los archivos de instantáneas en el directorio especificado en el paso 2. Por ejemplo, para que el Agente de instantáneas copie los archivos de instantáneas en \\\servidorFTP\inicio\instantáneas\ftp, debe especificar la ruta de acceso \\\servidorFTP\inicio\instantáneas en uno de estos dos lugares:  
  
    -   La ubicación de instantáneas predeterminada en el distribuidor asociado con esta publicación.  
  
         Para obtener más información sobre cómo especificar la ubicación de las instantáneas predeterminada, vea [Especificar la ubicación predeterminada de instantáneas &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md) (Especificar la ubicación predeterminada de instantáneas &#40;SQL Server Management Studio&#41;).  
  
    -   Una carpeta de instantáneas alternativa para esta publicación. Se necesita una ubicación alternativa si la instantánea está comprimida.  
  
         Escriba la ruta de acceso en el cuadro de texto **Poner los archivos en la siguiente carpeta**, situado en la página Instantánea del cuadro de diálogo **Propiedades de la publicación: \<publicación>**. Para obtener más información acerca de las ubicaciones alternativas para la carpeta de instantáneas, vea [Alternate Snapshot Folder Locations](../../../relational-databases/replication/alternate-snapshot-folder-locations.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Se puede establecer la opción para que los archivos de instantáneas estén disponibles en un servidor FTP y se puede modificar esta configuración mediante programación empleando los procedimientos almacenados de replicación. El procedimiento usado depende del tipo de publicación. La entrega de instantáneas a través de FTP solamente se usa con suscripciones de extracción.  
  
#### <a name="to-enable-ftp-snapshot-delivery-for-a-snapshot-or-transactional-publication"></a>Para habilitar la entrega de instantáneas a través de FTP para una publicación transaccional o de instantáneas  
  
1.  En la base de datos de publicación del Publicador, ejecute [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md). Especifique **@publication**, un valor de **true** para **@enabled_for_internet**y los valores adecuados para los parámetros siguientes:  
  
    -   **@ftp_address** : la dirección del servidor FTP usada para entregar la instantánea  
  
    -   (Opcional) **@ftp_port** : el puerto usado por el servidor FTP  
  
    -   (Opcional) **@ftp_subdirectory** : el subdirectorio del directorio FTP predeterminado asignado a un inicio de sesión de FTP. Por ejemplo, si el directorio raíz del servidor de FTP es \\\servidorFTP\inicio y desea almacenar las instantáneas en \\\servidorFTP\inicio\instantáneas, especifique **\instantáneas\ftp** para **@ftp_subdirectory** (la replicación anexa "ftp" a la ruta de acceso de la carpeta de instantáneas al crear los archivos de instantáneas).  
  
    -   (Opcional) **@ftp_login** : una cuenta de inicio de sesión usada al conectar al servidor FTP  
  
    -   (Opcional) **@ftp_password** : la contraseña para el inicio de sesión de FTP  
  
     Esto crea una publicación que usa FTP. Para obtener más información, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### <a name="to-enable-ftp-snapshot-delivery-for-a-merge-publication"></a>Para habilitar la entrega de instantáneas a través de FTP para una publicación de combinación  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Especifique **@publication**, un valor de **true** para **@enabled_for_internet** y los valores adecuados para los parámetros siguientes:  
  
    -   **@ftp_address** : la dirección del servidor FTP usada para entregar la instantánea  
  
    -   (Opcional) **@ftp_port** : el puerto usado por el servidor FTP  
  
    -   (Opcional) **@ftp_subdirectory** : el subdirectorio del directorio FTP predeterminado asignado a un inicio de sesión de FTP. Por ejemplo, si el directorio raíz del servidor de FTP es \\\servidorFTP\inicio y desea almacenar las instantáneas en \\\servidorFTP\inicio\instantáneas, especifique **\instantáneas\ftp** para **@ftp_subdirectory** (la replicación anexa "ftp" a la ruta de acceso de la carpeta de instantáneas al crear los archivos de instantáneas).  
  
    -   (Opcional) **@ftp_login** : una cuenta de inicio de sesión usada al conectar al servidor FTP  
  
    -   (Opcional) **@ftp_password** : la contraseña para el inicio de sesión de FTP  
  
     Esto crea una publicación que usa FTP. Para obtener más información, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication-that-uses-ftp-snapshot-delivery"></a>Para crear una suscripción de extracción a una publicación transaccional o de instantáneas que usa la entrega de instantáneas a través de FTP  
  
1.  En el publicador de la base de datos de suscripciones, ejecute [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md). Especifique **@publisher** y **@publication**.  
  
    -   En el suscriptor de la base de datos de suscripciones, ejecute [sp_addpullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Especifique **@publisher**, **@publisher_db**, **@publication**, las credenciales de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows con las que se ejecuta el Agente de distribución en el suscriptor para **@job_login** y **@job_password**y un valor de **true** para **@use_ftp**.  
  
2.  En la base de datos de publicación del publicador, ejecute [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) para registrar la suscripción de extracción. Para obtener más información, consulte [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication-that-uses-ftp-snapshot-delivery"></a>Para crear una suscripción de extracción a una publicación de combinación que use la entrega de instantáneas a través de FTP  
  
1.  En la base de datos de suscripciones del suscriptor, ejecute [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Especifique **@publisher** y **@publication**.  
  
2.  En el suscriptor de la base de datos de suscripciones, ejecute [sp_addmergepullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md). Especifique **@publisher**, **@publisher_db**, **@publication**, las credenciales de Windows con las que se ejecuta el Agente de distribución en el suscriptor para **@job_login** y **@job_password**y un valor de **true** para **@use_ftp**.  
  
3.  En la base de datos de publicación del publicador, ejecute [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md) para registrar la suscripción de extracción. Para obtener más información, consulte [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
#### <a name="to-change-one-or-more-ftp-snapshot-delivery-settings-for-a-snapshot-or-transactional-publication"></a>Para cambiar una o más configuraciones de entrega de instantáneas a través de FTP para una publicación transaccional o de instantáneas  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md). Especifique uno de los siguientes valores para **@property** y un nuevo valor de esta configuración para **@value**:  
  
    -   **ftp_address** : la dirección del servidor FTP usada para entregar la instantánea  
  
    -   **ftp_port** : el puerto usado por el servidor FTP  
  
    -   **ftp_subdirectory** : el subdirectorio del directorio FTP predeterminado usado para la instantánea de FTP  
  
    -   **ftp_login** : un inicio de sesión para conectar al servidor de FTP  
  
    -   **ftp_password** : la contraseña del inicio de sesión de FTP  
  
2.  (Opcional) Repita el paso 1 para cada configuración de FTP que se está cambiando.  
  
3.  (Opcional) Para deshabilitar la entrega de instantáneas a través de FTP, ejecute [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) en el Publicador de la base de datos de publicación. Especifique un valor de **enabled_for_internet** para **@property** y un valor de **false** para **@value**.  
  
#### <a name="to-change-ftp-snapshot-delivery-settings-for-a-merge-publication"></a>Para cambiar la configuración de entrega de instantáneas a través de FTP para una publicación de combinación  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md). Especifique uno de los siguientes valores para **@property** y un nuevo valor de esta configuración para **@value**:  
  
    -   **ftp_address** : la dirección del servidor FTP usada para entregar la instantánea  
  
    -   **ftp_port** : el puerto usado por el servidor FTP  
  
    -   **ftp_subdirectory** : el subdirectorio del directorio FTP predeterminado usado para la instantánea de FTP  
  
    -   **ftp_login** : un inicio de sesión para conectar al servidor de FTP  
  
    -   **ftp_password** : la contraseña del inicio de sesión de FTP  
  
2.  (Opcional) Repita el paso 1 para cada configuración de FTP que se está cambiando.  
  
3.  (Opcional) Para deshabilitar la entrega de instantáneas a través de FTP, ejecute [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) en el Publicador de la base de datos de publicación. Especifique un valor de **enabled_for_internet** para **@property** y un valor de **false** para **@value**.  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 El ejemplo siguiente crea una publicación de combinación que permite a los Suscriptores tener acceso a los datos de instantánea usando FTP. El suscriptor debe usar una conexión VPN segura al obtener acceso al recurso compartido de FTP. Las variables de scripting de**sqlcmd** se usan para proporcionar valores de inicio de sesión y de contraseña. Para obtener más información, vea [Usar sqlcmd con variables de script](../../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md).  
  
 [!code-sql[HowTo#sp_createmergepub_ftp](../../../relational-databases/replication/codesnippet/tsql/deliver-a-snapshot-throu_1.sql)]  
  
 El ejemplo siguiente crea una suscripción a una publicación de combinación, donde el Suscriptor obtiene la instantánea mediante FTP. El suscriptor debe usar una conexión VPN segura al obtener acceso al recurso compartido de FTP. Las variables de scripting de**sqlcmd** se usan para proporcionar valores de inicio de sesión y de contraseña. Para obtener más información, vea [Usar sqlcmd con variables de script](../../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md).  
  
 [!code-sql[HowTo#sp_createmergepullsub_ftp](../../../relational-databases/replication/codesnippet/tsql/deliver-a-snapshot-throu_2.sql)]  
  
 [!code-sql[HowTo#sp_createmergepullsubagent_ftp](../../../relational-databases/replication/codesnippet/tsql/deliver-a-snapshot-throu_3.sql)]  
  
## <a name="see-also"></a>Ver también  
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Transferir instantáneas mediante FTP](../../../relational-databases/replication/transfer-snapshots-through-ftp.md)   
 [Cambiar las propiedades de la publicación y de los artículos](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Inicializar una suscripción con una instantánea](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
