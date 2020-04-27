---
title: Entrega de una instantánea mediante FTP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], FTP snapshots
- FTP snapshots [SQL Server replication]
- snapshot replication [SQL Server], FTP
ms.assetid: 99872c4f-40ce-4405-8fd4-44052d3bd827
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d1a8989492c9efb670b00bda00dbfa757c549fca
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62960069"
---
# <a name="deliver-a-snapshot-through-ftp"></a>Entregar una instantánea mediante FTP
  En este tema se describe cómo entregar una instantánea a través de FTP en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
##  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
  
-   El Agente de instantáneas debe tener permisos de escritura para el directorio especificado y el Agente de distribución o de mezcla debe tener permisos de lectura. Si usa suscripciones de extracción, debe especificar un directorio compartido como una ruta de acceso UNC (Convención de nomenclatura universal), por ejemplo, \\\servidorFTP\inicio\instantáneas. Para obtener más información, vea [proteger la carpeta de instantáneas](../security/secure-the-snapshot-folder.md).  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Requisitos previos  
  
-   Para transferir archivos de instantáneas con el Protocolo de transferencia de archivos (FTP), primero debe configurar un servidor de FTP. Para obtener más información, vea la documentación de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Internet Information Services (IIS).  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
 Para contribuir a mejorar la seguridad, se recomienda implementar una red privada virtual (VPN) al utilizar la entrega de instantáneas a través de FTP por Internet. Para más información, vea [Publicar datos a través de Internet mediante VPN](../publish-data-over-the-internet-using-vpn.md).  
  
 Por seguridad, se recomienda no permitir el inicio de sesión anónimo en el servidor de FTP. El Agente de instantáneas debe tener permisos de escritura para el directorio especificado y el Agente de distribución o de mezcla debe tener permisos de lectura. Si usa suscripciones de extracción, debe especificar un directorio compartido como una ruta de acceso UNC (Convención de nomenclatura universal), por ejemplo, \\\servidorFTP\inicio\instantáneas. Para obtener más información, vea [Proteger la carpeta de instantáneas](../security/secure-the-snapshot-folder.md).  
  
 Cuando sea posible, pida a los usuarios que proporcionen sus credenciales en tiempo de ejecución. Si almacena las credenciales en un archivo de script, debe proteger el archivo.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
 Una vez configurado el servidor de FTP, especifique el directorio y la información de seguridad para este servidor en el cuadro de diálogo **Propiedades de la publicación: \<publicación>**. Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-ftp-information"></a>Para especificar la información de FTP  
  
1.  En el cuadro de diálogo **Propiedades de la publicación: \<publicación>**, seleccione **Permitir a los suscriptores descargar archivos de instantánea usando FTP (Protocolo de transferencia de archivos)** en una de las páginas siguientes:   
    -   La página **Instantánea de FTP**, para las publicaciones transaccionales y de instantáneas, y las publicaciones de combinación para los publicadores que ejecuten versiones anteriores a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].    
    -   La página **Instantánea de FTP e Internet** , para las publicaciones de combinación de los publicadores que ejecuten [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o posterior.    
2.  Especifique valores para **Nombre del servidor FTP**, **Número de puerto**, **Ruta de acceso de la carpeta raíz del servidor FTP**, **Inicio de sesión**y **Contraseña**.    
     Por ejemplo, si el directorio raíz del servidor de FTP es \\\servidorFTP\inicio y desea almacenar las instantáneas en \\\servidorFTP\inicio\instantáneas, especifique \instantáneas\ftp para la propiedad **Ruta de acceso de la carpeta raíz del servidor FTP** (la replicación adjunta 'ftp' a la ruta de acceso de la carpeta de instantáneas al crear los archivos de instantáneas).    
3.  Especifique que el Agente de instantáneas copie los archivos de instantáneas en el directorio especificado en el paso 2. Por ejemplo, para que el Agente de instantáneas copie los archivos de instantáneas en \\\servidorFTP\inicio\instantáneas\ftp, debe especificar la ruta de acceso \\\servidorFTP\inicio\instantáneas en uno de estos dos lugares:    
    -   La ubicación de instantáneas predeterminada en el distribuidor asociado con esta publicación.    
         Para obtener más información sobre cómo especificar la ubicación de instantáneas predeterminada, vea [especificar la ubicación de instantáneas predeterminada](../snapshot-options.md#snapshot-folder-locations).    
    -   Una carpeta de instantáneas alternativa para esta publicación. Se necesita una ubicación alternativa si la instantánea está comprimida.    
         Escriba la ruta de acceso en el cuadro de texto **Poner los archivos en la siguiente carpeta**, situado en la página Instantánea del cuadro de diálogo **Propiedades de la publicación: \<publicación>**.   
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
 Se puede establecer la opción para que los archivos de instantáneas estén disponibles en un servidor FTP y se puede modificar esta configuración mediante programación empleando los procedimientos almacenados de replicación. El procedimiento usado depende del tipo de publicación. La entrega de instantáneas a través de FTP solamente se usa con suscripciones de extracción.  
  
#### <a name="to-enable-ftp-snapshot-delivery-for-a-snapshot-or-transactional-publication"></a>Para habilitar la entrega de instantáneas a través de FTP para una publicación transaccional o de instantáneas  
  
1.  En la base de datos de publicación del Publicador, ejecute [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql). Especifique **@publication**, un valor de `true` para **@enabled_for_internet**y los valores adecuados para los parámetros siguientes:    
    -   **@ftp_address**: la dirección del servidor FTP que se usa para proporcionar la instantánea.    
    -   Opta **@ftp_port** : el puerto usado por el servidor FTP.    
    -   Opta **@ftp_subdirectory** : el subdirectorio del directorio FTP predeterminado asignado a un inicio de sesión FTP. Por ejemplo, si la raíz del servidor FTP \\es \servidorftp\inicio y desea que las instantáneas se almacenen en \\\ftpserver\home\snapshots, especifique **@ftp_subdirectory** **\snapshots\ftp** para (la replicación anexa ' ftp ' a la ruta de acceso de la carpeta de instantáneas al crear archivos de instantáneas).    
    -   Opta **@ftp_login** : una cuenta de inicio de sesión que se usa al conectarse al servidor FTP.    
    -   Opta **@ftp_password** -la contraseña para el inicio de sesión de FTP.  
  
     Esto crea una publicación que usa FTP. Para obtener más información, vea [crear una publicación](create-a-publication.md).  
  
#### <a name="to-enable-ftp-snapshot-delivery-for-a-merge-publication"></a>Para habilitar la entrega de instantáneas a través de FTP para una publicación de combinación  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql). Especifique **@publication**, un valor de `true` para **@enabled_for_internet** y los valores adecuados para los parámetros siguientes:  
  
    -   **@ftp_address**: la dirección del servidor FTP que se usa para proporcionar la instantánea.    
    -   Opta **@ftp_port** : el puerto usado por el servidor FTP.    
    -   Opta **@ftp_subdirectory** : el subdirectorio del directorio FTP predeterminado asignado a un inicio de sesión FTP. Por ejemplo, si la raíz del servidor FTP \\es \servidorftp\inicio y desea que las instantáneas se almacenen en \\\ftpserver\home\snapshots, especifique **@ftp_subdirectory** **\snapshots\ftp** para (la replicación anexa ' ftp ' a la ruta de acceso de la carpeta de instantáneas al crear archivos de instantáneas).    
    -   Opta **@ftp_login** : una cuenta de inicio de sesión que se usa al conectarse al servidor FTP.    
    -   Opta **@ftp_password** -la contraseña para el inicio de sesión de FTP.  
  
     Esto crea una publicación que usa FTP. Para obtener más información, vea [crear una publicación](create-a-publication.md).  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication-that-uses-ftp-snapshot-delivery"></a>Para crear una suscripción de extracción a una publicación transaccional o de instantáneas que usa la entrega de instantáneas a través de FTP  
  
1.  En el publicador de la base de datos de suscripciones, ejecute [sp_addpullsubscription](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql). Especifique **@publisher** y **@publication**.  
  
    -   En el suscriptor de la base de datos de suscripciones, ejecute [sp_addpullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql). Especifique **@publisher**, **@publisher_db**, **@publication**, las [!INCLUDE[msCoName](../../../includes/msconame-md.md)] credenciales de Windows con las que se ejecuta el agente de distribución en **@job_login** el **@job_password**suscriptor para y, `true` y **@use_ftp**un valor de para.  
  
2.  En la base de datos de publicación del publicador, ejecute [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) para registrar la suscripción de extracción. Para obtener más información, consulte [Create a Pull Subscription](../create-a-pull-subscription.md).  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication-that-uses-ftp-snapshot-delivery"></a>Para crear una suscripción de extracción a una publicación de combinación que use la entrega de instantáneas a través de FTP  
  
1.  En la base de datos de suscripciones del suscriptor, ejecute [sp_addmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql). Especifique **@publisher** y **@publication**.   
2.  En el suscriptor de la base de datos de suscripciones, ejecute [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql). Especifique **@publisher**, **@publisher_db**, **@publication**, las credenciales de Windows con las que se ejecuta el agente de distribución en **@job_login** el **@job_password**suscriptor para y, `true` y **@use_ftp**un valor de para.    
3.  En la base de datos de publicación del publicador, ejecute [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql) para registrar la suscripción de extracción. Para obtener más información, consulte [Create a Pull Subscription](../create-a-pull-subscription.md).  
  
#### <a name="to-change-one-or-more-ftp-snapshot-delivery-settings-for-a-snapshot-or-transactional-publication"></a>Para cambiar una o más configuraciones de entrega de instantáneas a través de FTP para una publicación transaccional o de instantáneas  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql). Especifique uno de los valores siguientes para **@property** y un nuevo valor de esta configuración para **@value**:    
    -   `ftp_address`: la dirección del servidor FTP usada para entregar la instantánea    
    -   `ftp_port`: el puerto usado por el servidor FTP    
    -   `ftp_subdirectory`: el subdirectorio del directorio FTP predeterminado usado para la instantánea de FTP    
    -   `ftp_login`: un inicio de sesión para conectar al servidor de FTP    
    -   `ftp_password`: la contraseña del inicio de sesión de FTP  
  
2.  (Opcional) Repita el paso 1 para cada configuración de FTP que se está cambiando.    
3.  (Opcional) Para deshabilitar la entrega de instantáneas a través de FTP, ejecute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql) en el Publicador de la base de datos de publicación. Especifique un valor de `enabled_for_internet` para **@property** y un valor de `false` para **@value**.  
  
#### <a name="to-change-ftp-snapshot-delivery-settings-for-a-merge-publication"></a>Para cambiar la configuración de entrega de instantáneas a través de FTP para una publicación de combinación  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql). Especifique uno de los valores siguientes para **@property** y un nuevo valor de esta configuración para **@value**:  
  
    -   `ftp_address`: la dirección del servidor FTP usada para entregar la instantánea    
    -   `ftp_port`: el puerto usado por el servidor FTP    
    -   `ftp_subdirectory`: el subdirectorio del directorio FTP predeterminado usado para la instantánea de FTP   
    -   `ftp_login`: un inicio de sesión para conectar al servidor de FTP    
    -   `ftp_password`: la contraseña del inicio de sesión de FTP    
2.  (Opcional) Repita el paso 1 para cada configuración de FTP que se está cambiando.    
3.  (Opcional) Para deshabilitar la entrega de instantáneas a través de FTP, ejecute [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql) en el Publicador de la base de datos de publicación. Especifique un valor de `enabled_for_internet` para **@property** y un valor de `false` para **@value**.  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a>Ejemplos (Transact-SQL)  
 El ejemplo siguiente crea una publicación de combinación que permite a los Suscriptores tener acceso a los datos de instantánea usando FTP. El suscriptor debe usar una conexión VPN segura al obtener acceso al recurso compartido de FTP. Las variables de scripting de**sqlcmd** se usan para proporcionar valores de inicio de sesión y de contraseña. Para obtener más información, vea [Usar sqlcmd con variables de script](../../scripting/sqlcmd-use-with-scripting-variables.md).  
  
 [!code-sql[HowTo#sp_createmergepub_ftp](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubftp.sql#sp_createmergepub_ftp)]  
  
 El ejemplo siguiente crea una suscripción a una publicación de combinación, donde el Suscriptor obtiene la instantánea mediante FTP. El suscriptor debe usar una conexión VPN segura al obtener acceso al recurso compartido de FTP. Las variables de scripting de**sqlcmd** se usan para proporcionar valores de inicio de sesión y de contraseña. Para obtener más información, vea [Usar sqlcmd con variables de script](../../scripting/sqlcmd-use-with-scripting-variables.md).  
  
 [!code-sql[HowTo#sp_createmergepullsub_ftp](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepullsubftp.sql#sp_createmergepullsub_ftp)]  
  
 [!code-sql[HowTo#sp_createmergepullsubagent_ftp](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepullsubftp.sql#sp_createmergepullsubagent_ftp)]  
  
## <a name="see-also"></a>Consulte también  
 [Conceptos de procedimientos almacenados del sistema de replicación](../concepts/replication-system-stored-procedures-concepts.md)   
 [Transferir instantáneas a través de FTP](../transfer-snapshots-through-ftp.md)   
 [Cambiar las propiedades de la publicación y del artículo](change-publication-and-article-properties.md)   
 [Inicializar una suscripción con una instantánea](../initialize-a-subscription-with-a-snapshot.md)  
  
  
