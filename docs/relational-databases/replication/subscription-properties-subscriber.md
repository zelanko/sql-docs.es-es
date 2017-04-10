---
title: "Propiedades de suscripci&#243;n: suscriptor | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.subproperties.subscriber.f1"
helpviewer_keywords: 
  - "Propiedades de suscripción, cuadro de diálogo"
ms.assetid: bef66929-3234-4a45-8ec4-3b271519d07a
caps.latest.revision: 25
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 25
---
# Propiedades de suscripci&#243;n: suscriptor
  El cuadro de diálogo **Propiedades de suscripción** del suscriptor le permite ver y establecer las propiedades de las suscripciones de extracción.  
  
 Cada una de las propiedades del cuadro de diálogo **Propiedades de la suscripción** incluye una descripción. Haga clic en una propiedad para mostrar la descripción en la parte inferior del cuadro de diálogo. Este tema ofrece información adicional acerca de varias propiedades. Las propiedades se agrupan en las siguientes categorías:  
  
-   Propiedades que se aplican a todas las suscripciones.  
  
-   Propiedades que se aplican a las suscripciones transaccionales.  
  
-   Propiedades que se aplican a las suscripciones de mezcla.  
  
 Si una opción se muestra como de solo lectura, solamente se puede establecer durante la creación de la suscripción. Si desea establecer opciones que no están disponibles en el Asistente para nueva suscripción, cree la suscripción con los procedimientos almacenados. Para obtener más información, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) y [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
> [!NOTE]  
>  Si aún no ha creado un Agente de distribución o un Agente de mezcla para la suscripción, no se mostrarán muchas de las propiedades de la suscripción. Para crear un trabajo del agente para una suscripción de extracción, ejecute [sp_addpullsubscription_agent & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) (para una suscripción a una publicación transaccional o instantánea) o [sp_addmergepullsubscription_agent & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) (para una suscripción a una publicación de mezcla).  
  
## Opciones para todas las suscripciones  
 **Inicializar datos publicados desde una instantánea**  
 Determina si las suscripciones se inicializan con una instantánea (opción predeterminada) o con otro método. Para obtener más información acerca de cómo inicializar las suscripciones, consulte [inicializar una suscripción](../../relational-databases/replication/initialize-a-subscription.md).  
  
 **Ubicación de la instantánea**  
 Determina la ubicación desde la que se tiene acceso a los archivos de instantáneas durante la inicialización o la reinicialización. La ubicación puede ser uno de los siguientes valores:  
  
-   **Ubicación predeterminada**: muestra la ubicación predeterminada, definida al configurar el distribuidor. Para obtener más información, consulte [especificar la ubicación de instantánea predeterminada & #40; SQL Server Management Studio & #41;](../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md).  
  
-   **Carpeta alternativa**: muestra una ubicación alternativa, que puede especificarse en el cuadro de diálogo **Propiedades de la publicación** . Para más información, consulte [Alternate Snapshot Folder Locations](../../relational-databases/replication/alternate-snapshot-folder-locations.md).  
  
-   **Carpeta de instantáneas dinámicas**: muestra una ubicación de instantáneas para las publicaciones de combinación que utilizan filtros de fila con parámetros. Para más información, consulte [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
-   **Carpeta FTP**: una carpeta accesible para un servidor de protocolo de transferencia de archivos (FTP). Para obtener más información, consulte [Transferir instantáneas mediante FTP](../../relational-databases/replication/transfer-snapshots-through-ftp.md).  
  
 **Carpeta de instantáneas**  
 Si se selecciona cualquier valor distinto de **ubicación predeterminada** para el **ubicación de la instantánea** opción, debe especificar una ruta de acceso a la carpeta de instantáneas.  
  
 **Utilizar el Administrador de sincronización de Windows**  
 Determina si es posible sincronizar la suscripción con el Administrador de sincronización de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 **Seguridad**  
 Haga clic en la **cuenta de proceso del agente** fila y, a continuación, haga clic en el botón de propiedades (**...**) para cambiar la cuenta bajo la que se ejecuta el agente de distribución o el agente de mezcla en el suscriptor. Las opciones de seguridad relativas a las conexiones dependen del tipo de suscripción:  
  
-   Para las suscripciones a una publicación transaccional: para cambiar la cuenta bajo la que el agente de distribución realiza conexiones al distribuidor, haga clic en **conexión del distribuidor**, y, a continuación, haga clic en el botón de propiedades (**...**).  
  
-   Para las suscripciones de actualización inmediata a una publicación transaccional: además de la conexión del distribuidor se ha descrito anteriormente, puede cambiar el método utilizado para propagar los cambios desde el suscriptor al publicador: haga clic en **conexión de publicador**, y, a continuación, haga clic en el botón de propiedades (**...**).  
  
-   Para que las suscripciones a publicaciones de mezcla, haga clic en **conexión de publicador**, y, a continuación, haga clic en el botón de propiedades (**...**).  
  
 Para obtener más información acerca de los permisos necesarios para cada agente, vea [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## Opciones para suscripciones transaccionales  
 **Suscripción actualizable**  
 Determina si los cambios del suscriptor se vuelven a replicar en el publicador.  Es posible replicar los cambios con una actualización en cola o una actualización inmediata. La opción **Método de actualización del suscriptor** determina el método que se debe utilizar. Para más información, consulte [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
## Opciones para suscripciones de mezcla  
 **Definición de partición (HOST_NAME)**  
 Para filtros con parámetros de una publicación que utiliza, la replicación de mezcla evalúa una de dos funciones del sistema (o ambos si el filtro hace referencia a ambas funciones) durante la sincronización para determinar los datos que un suscriptor debe recibir: **SUSER_SNAME ()** o **HOST_NAME ()**. De forma predeterminada, **HOST_NAME ()** devuelve el nombre del equipo en el que está ejecutando el agente de mezcla, pero puede invalidar este valor en el Asistente para nueva suscripción. Para obtener más información sobre filtros con parámetros y reemplazar **HOST_NAME ()**, consulte [filtros de fila parametrizados](../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
 **Tipo de suscripción** y **prioridad**  
 Muestra si la suscripción es una suscripción de cliente o de servidor (no podrá cambiarse una vez creada la suscripción). Las suscripciones de servidor pueden volver a publicar datos en otros suscriptores y es posible asignarles una prioridad para la resolución de conflictos.  
  
 Si ha seleccionado un tipo de suscripción de servidor en el Asistente para nueva suscripción, el suscriptor recibe la prioridad que se usa durante la resolución de conflictos.  
  
 **Solucionar conflictos de manera interactiva**  
 Establece si se va a utilizar la interfaz de usuario Solucionador interactivo para solucionar conflictos durante la sincronización de mezcla. Requiere un valor de **Habilitado** en **Utilizar el Administrador de sincronización de Windows**. Para obtener más información, consulte [Interactive Conflict Resolution](../../relational-databases/replication/merge/interactive-conflict-resolution.md).  
  
 **Sincronización web**  
 **Usar sincronización Web** determina si desea conectarse a un [!INCLUDE[msCoName](../../includes/msconame-md.md)] servidor Internet Information Services (IIS) para sincronizar la suscripción. Esta opción solo está disponible si la sincronización web está habilitada en la publicación. Para más información, consulte [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
 Si selecciona **True** para **Usar sincronización web**:  
  
-   Escriba la dirección completa del servidor IIS en **Dirección de servidor web**.  
  
-   Haga clic en el **conexión de servidor Web** fila y, a continuación, haga clic en el botón de propiedades (**...**) para establecer o cambiar la cuenta bajo la que el suscriptor se conecta al servidor IIS.  
  
-   Si fuese necesario, cambie el **Tiempo de espera del servidor web** . El tiempo de espera es la cantidad de tiempo, en segundos, que transcurre antes de que expire la solicitud de sincronización web.  
  
 Para obtener más información acerca de la configuración, vea [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md).  
  
## Vea también  
 [Ver y modificar las propiedades de una suscripción de extracción](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Ver y modificar las propiedades de una suscripción de inserción](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)  
  
  