---
title: "Entregar una instant&#225;nea mediante FTP | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "instantáneas [replicación de SQL Server], instantáneas de FTP"
  - "instantáneas de FTP [replicación de SQL Server]"
  - "replicación de instantáneas [SQL Server], FTP"
ms.assetid: 99872c4f-40ce-4405-8fd4-44052d3bd827
caps.latest.revision: 47
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 47
---
# Entregar una instant&#225;nea mediante FTP
  En este tema se describe cómo entregar una instantánea a través de FTP en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Requisitos previos](#Prerequisites)  
  
     [Seguridad](#Security)  
  
-   **Para entregar una instantánea mediante FTP con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   El Agente de instantáneas debe tener permisos de escritura para el directorio especificado y el Agente de distribución o de mezcla debe tener permisos de lectura. Si utiliza suscripciones de extracción, debe especificar un directorio compartido como una ruta de nomenclatura universal (UNC) de la convención, como \\\ftpserver\home\snapshots. Para obtener más información, consulte [proteger la carpeta de instantáneas](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   Para transferir archivos de instantáneas con el Protocolo de transferencia de archivos (FTP), primero debe configurar un servidor de FTP. Para obtener más información, vea la documentación de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Internet Information Services (IIS).  
  
###  <a name="Security"></a> Seguridad  
 Para contribuir a mejorar la seguridad, se recomienda implementar una red privada virtual (VPN) al utilizar la entrega de instantáneas a través de FTP por Internet. Para obtener más información, consulte [publicar datos por Internet mediante VPN](../../../relational-databases/replication/publish-data-over-the-internet-using-vpn.md).  
  
 Por seguridad, se recomienda no permitir el inicio de sesión anónimo en el servidor de FTP. El Agente de instantáneas debe tener permisos de escritura para el directorio especificado y el Agente de distribución o de mezcla debe tener permisos de lectura. Si utiliza suscripciones de extracción, debe especificar un directorio compartido como una ruta de nomenclatura universal (UNC) de la convención, como \\\ftpserver\home\snapshots. Para obtener más información, consulte [proteger la carpeta de instantáneas](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
 Cuando sea posible, pida a los usuarios que proporcionen sus credenciales en tiempo de ejecución. Si almacena las credenciales en un archivo de script, debe proteger el archivo.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Después de configura el servidor FTP, especifique la información de directorio y la seguridad para este servidor en la **Propiedades de la publicación \< publicación>** cuadro de diálogo. Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para especificar la información de FTP  
  
1.  En la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, seleccione **Permitir a los suscriptores descargar archivos de instantáneas mediante FTP** de una de las siguientes páginas:  
  
    -   La página **Instantánea de FTP** , para las publicaciones transaccionales y de instantáneas, y las publicaciones de combinación para los publicadores que ejecuten versiones anteriores a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
    -   La página **Instantánea de FTP e Internet** , para las publicaciones de combinación de los publicadores que ejecuten [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o posterior.  
  
2.  Especifique valores para **Nombre del servidor FTP**, **Número de puerto**, **Ruta de acceso de la carpeta raíz del servidor FTP**, **Inicio de sesión**y **Contraseña**.  
  
     Por ejemplo, si la raíz del servidor FTP es \\\ftpserver\home y desea que las instantáneas se encuentran en \\\ftpserver\home\snapshots, especifique \snapshots\ftp para la propiedad **ruta de acceso de la carpeta raíz FTP** (replicación anexa 'ftp' a la ruta de la carpeta de instantáneas al crear los archivos de instantáneas).  
  
3.  Especifique que el Agente de instantáneas copie los archivos de instantáneas en el directorio especificado en el paso 2. Por ejemplo, la instantánea agente escribir los archivos de instantáneas a \\\ftpserver\home\snapshots\ftp, debe especificar la ruta de acceso \\\ftpserver\home\snapshots en uno de dos lugares:  
  
    -   La ubicación de instantáneas predeterminada en el distribuidor asociado con esta publicación.  
  
         Para obtener más información acerca de cómo especificar la ubicación predeterminada de instantáneas, consulte [especificar la ubicación predeterminada de instantáneas & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md).  
  
    -   Una carpeta de instantáneas alternativa para esta publicación. Se necesita una ubicación alternativa si la instantánea está comprimida.  
  
         Escriba la ruta de acceso en la **colocar los archivos en la siguiente carpeta** cuadro de texto en la página instantánea de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo. Para obtener más información acerca de las ubicaciones alternativas para la carpeta de instantáneas, vea [Alternate Snapshot Folder Locations](../../../relational-databases/replication/alternate-snapshot-folder-locations.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Se puede establecer la opción para que los archivos de instantáneas estén disponibles en un servidor FTP y se puede modificar esta configuración mediante programación empleando los procedimientos almacenados de replicación. El procedimiento usado depende del tipo de publicación. La entrega de instantáneas a través de FTP solamente se usa con suscripciones de extracción.  
  
#### Para habilitar la entrega de instantáneas a través de FTP para una publicación transaccional o de instantáneas  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md). Especifique **@publication**, un valor de **true** para **@enabled_for_internet**, y los valores adecuados para los parámetros siguientes:  
  
    -   **@ftp_address** -la dirección del servidor FTP usada para entregar la instantánea.  
  
    -   (Opcional) **@ftp_port** -el puerto utilizado por el servidor FTP.  
  
    -   (Opcional) **@ftp_subdirectory** -el subdirectorio del directorio FTP predeterminado asignado a un inicio de sesión FTP. Por ejemplo, si la raíz del servidor FTP es \\\ftpserver\home y desea que las instantáneas se encuentran en \\\ftpserver\home\snapshots, especifique **\snapshots\ftp** de **@ftp_subdirectory** (replicación anexa 'ftp' a la ruta de la carpeta de instantáneas al crear los archivos de instantáneas).  
  
    -   (Opcional) **@ftp_login** -una cuenta de inicio de sesión utilizada al conectarse al servidor FTP.  
  
    -   (Opcional) **@ftp_password** -la contraseña para el inicio de sesión FTP.  
  
     Esto crea una publicación que usa FTP. Para obtener más información, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### Para habilitar la entrega de instantáneas a través de FTP para una publicación de combinación  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Especifique **@publication**, un valor de **true** para **@enabled_for_internet** y los valores adecuados para los parámetros siguientes:  
  
    -   **@ftp_address** -la dirección del servidor FTP usada para entregar la instantánea.  
  
    -   (Opcional) **@ftp_port** -el puerto utilizado por el servidor FTP.  
  
    -   (Opcional) **@ftp_subdirectory** -el subdirectorio del directorio FTP predeterminado asignado a un inicio de sesión FTP. Por ejemplo, si la raíz del servidor FTP es \\\ftpserver\home y desea que las instantáneas se encuentran en \\\ftpserver\home\snapshots, especifique **\snapshots\ftp** de **@ftp_subdirectory** (replicación anexa 'ftp' a la ruta de la carpeta de instantáneas al crear los archivos de instantáneas).  
  
    -   (Opcional) **@ftp_login** -una cuenta de inicio de sesión utilizada al conectarse al servidor FTP.  
  
    -   (Opcional) **@ftp_password** -la contraseña para el inicio de sesión FTP.  
  
     Esto crea una publicación que usa FTP. Para obtener más información, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### Para crear una suscripción de extracción a una publicación transaccional o de instantáneas que usa la entrega de instantáneas a través de FTP  
  
1.  En el suscriptor en la base de datos de suscripción, ejecute [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md). Especifique **@publisher** y **@publication**.  
  
    -   En el suscriptor en la base de datos de suscripción, ejecute [sp_addpullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Especifique **@publisher**, **@publisher_db**, **@publication**, la [!INCLUDE[msCoName](../../../includes/msconame-md.md)] las credenciales de Windows en la que se ejecuta el agente de distribución en el suscriptor para **@job_login** y **@job_password**, y un valor de **true** para **@use_ftp**.  
  
2.  En el publicador de la base de datos de publicación, ejecute [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) para registrar la suscripción de extracción. Para más información, consulte [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
#### Para crear una suscripción de extracción a una publicación de combinación que use la entrega de instantáneas a través de FTP  
  
1.  En el suscriptor en la base de datos de suscripción, ejecute [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Especifique **@publisher** y **@publication**.  
  
2.  En el suscriptor en la base de datos de suscripción, ejecute [sp_addmergepullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md). Especifique **@publisher**, **@publisher_db**, **@publication**, las credenciales de Windows en la que se ejecuta el agente de distribución en el suscriptor para **@job_login** y **@job_password**, y un valor de **true** para **@use_ftp**.  
  
3.  En el publicador de la base de datos de publicación, ejecute [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md) para registrar la suscripción de extracción. Para más información, consulte [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
#### Para cambiar una o más configuraciones de entrega de instantáneas a través de FTP para una publicación transaccional o de instantáneas  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md). Especifique uno de los siguientes valores para **@property** y un nuevo valor de esta configuración para **@value**:  
  
    -   **ftp_address** -la dirección del servidor FTP usada para entregar la instantánea.  
  
    -   **ftp_port** -el puerto utilizado por el servidor FTP.  
  
    -   **ftp_subdirectory** -el subdirectorio del directorio FTP predeterminado usado para la instantánea FTP.  
  
    -   **ftp_login** -un inicio de sesión utilizado para conectarse al servidor FTP.  
  
    -   **ftp_password** -la contraseña para el inicio de sesión FTP.  
  
2.  (Opcional) Repita el paso 1 para cada configuración de FTP que se está cambiando.  
  
3.  (Opcional) Para deshabilitar la entrega de instantánea FTP, ejecute [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) en el publicador de la base de datos de publicación. Especifique un valor de **enabled_for_internet** para **@property** y un valor de **false** para **@value**.  
  
#### Para cambiar la configuración de entrega de instantáneas a través de FTP para una publicación de combinación  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md). Especifique uno de los siguientes valores para **@property** y un nuevo valor de esta configuración para **@value**:  
  
    -   **ftp_address** -la dirección del servidor FTP usada para entregar la instantánea.  
  
    -   **ftp_port** -el puerto utilizado por el servidor FTP.  
  
    -   **ftp_subdirectory** -el subdirectorio del directorio FTP predeterminado usado para la instantánea FTP.  
  
    -   **ftp_login** -un inicio de sesión utilizado para conectarse al servidor FTP.  
  
    -   **ftp_password** -la contraseña para el inicio de sesión FTP.  
  
2.  (Opcional) Repita el paso 1 para cada configuración de FTP que se está cambiando.  
  
3.  (Opcional) Para deshabilitar la entrega de instantánea FTP, ejecute [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) en el publicador de la base de datos de publicación. Especifique un valor de **enabled_for_internet** para **@property** y un valor de **false** para **@value**.  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 El ejemplo siguiente crea una publicación de combinación que permite a los Suscriptores tener acceso a los datos de instantánea usando FTP. El suscriptor debe usar una conexión VPN segura al obtener acceso al recurso compartido de FTP. Las variables de scripting de**sqlcmd** se usan para proporcionar valores de inicio de sesión y de contraseña. Para obtener más información, consulte [usar sqlcmd con Variables de secuencias de comandos](../../../relational-databases/scripting/use-sqlcmd-with-scripting-variables.md).  
  
 [!code-sql[HowTo#sp_createmergepub_ftp](../../../relational-databases/replication/codesnippet/tsql/deliver-a-snapshot-throu_1.sql)]  
  
 El ejemplo siguiente crea una suscripción a una publicación de combinación, donde el Suscriptor obtiene la instantánea mediante FTP. El suscriptor debe usar una conexión VPN segura al obtener acceso al recurso compartido de FTP. Las variables de scripting de**sqlcmd** se usan para proporcionar valores de inicio de sesión y de contraseña. Para obtener más información, consulte [usar sqlcmd con Variables de secuencias de comandos](../../../relational-databases/scripting/use-sqlcmd-with-scripting-variables.md).  
  
 [!code-sql[HowTo#sp_createmergepullsub_ftp](../../../relational-databases/replication/codesnippet/tsql/deliver-a-snapshot-throu_2.sql)]  
  
 [!code-sql[HowTo#sp_createmergepullsubagent_ftp](../../../relational-databases/replication/codesnippet/tsql/deliver-a-snapshot-throu_3.sql)]  
  
## Vea también  
 [Conceptos sobre los procedimientos almacenados del sistema de replicación](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Transferir instantáneas mediante FTP](../../../relational-databases/replication/transfer-snapshots-through-ftp.md)   
 [Cambiar las propiedades de la publicación y de los artículos](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Inicializar una suscripción con una instantánea](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  