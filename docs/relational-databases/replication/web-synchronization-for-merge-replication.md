---
title: "Sincronizaci&#243;n web para la replicaci&#243;n de mezcla | Microsoft Docs"
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
  - "sincronización de replicación de mezcla [replicación de SQL Server]"
  - "Internet [replicación de SQL Server], sincronización"
  - "sincronización [replicación de SQL Server], sincronización web"
  - "publicación Web [replicación de SQL Server], sincronización"
  - "sincronización web, acerca de"
  - "sincronización web"
ms.assetid: 84785aba-b2c1-4821-9e9d-a363c73dcb37
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# Sincronizaci&#243;n web para la replicaci&#243;n de mezcla
  La sincronización web para la replicación de mezcla permite replicar datos utilizando el protocolo HTTPS y es útil en los siguientes escenarios:  
  
-   Sincronizar datos de usuarios móviles a través de Internet  
  
-   Sincronizar datos entre bases de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través de un firewall corporativo  
  
 Por ejemplo, un representante de ventas puede utilizar la sincronización web durante sus viajes. La empresa [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]tiene representantes de ventas que viajan para visitar varias tiendas y proveedores de su región. En viajes más largos, los representantes se hospedan en hoteles y necesitan una manera cómoda de cargar datos de ventas y descargar cualquier actualización de productos al final de cada día.  
  
 El departamento de TI de [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] ha configurado cada equipo portátil con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y ha habilitado la replicación de mezcla para que utilice la sincronización web. El Agente de mezcla de cada equipo portátil tiene una dirección URL de Internet que apunta a los componentes de replicación instalados en un equipo en el que se ejecuta [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS). Estos componentes sincronizan el suscriptor con el publicador. Ahora cada representante se puede conectar a través de cualquier conexión de Internet disponible sin utilizar una conexión remota de acceso telefónico y puede cargar y descargar los datos que desee. La conexión de Internet utiliza SSL (Capa de sockets seguros), por lo que no es necesaria una red privada virtual (VPN).  
  
 Para obtener información acerca de cómo configurar los componentes que son necesarios para la sincronización Web, consulte [Configurar sincronización Web](../../relational-databases/replication/configure-web-synchronization.md), [configurar IIS para la sincronización Web](../../relational-databases/replication/configure-iis-for-web-synchronization.md), y [configurar IIS 7 para la sincronización Web](../../relational-databases/replication/configure-iis-7-for-web-synchronization.md).  
  
> [!NOTE]  
>  La sincronización web está diseñada para sincronizar datos con equipos portátiles, dispositivos de mano y otros clientes. La sincronización web no está concebida para aplicaciones de servidor a servidor con grandes volúmenes de datos.  
  
## Información general sobre el funcionamiento de la sincronización web  
 Cuando se utiliza la sincronización web, las actualizaciones en el suscriptor se empaquetan y envían como un mensaje XML al equipo en el que se ejecuta IIS mediante el protocolo HTTPS. El equipo en el que se ejecuta IIS envía los comandos al publicador en formato binario (normalmente mediante TCP/IP). Las actualizaciones en el publicador se envían al equipo en el que se ejecuta IIS y después se empaquetan como un mensaje XML para su envío al suscriptor.  
  
 En la siguiente ilustración se muestran algunos de los componentes que participan en la sincronización web para la replicación de mezcla.  
  
 ![Componentes y flujo de datos de sincronización web](../../relational-databases/replication/media/web-sync01.gif "Componentes y flujo de datos de sincronización web")  
  
 La sincronización web es una opción exclusiva de las suscripciones de extracción, por lo que un Agente de mezcla se ejecutará siempre en el suscriptor. Este Agente de mezcla puede ser el Agente de mezcla estándar, el control ActiveX del Agente de mezcla o de una aplicación que proporcione sincronización a través de Replication Management Objects (RMO). Para especificar la ubicación del equipo en el que se ejecuta IIS, utilice el parámetro **–InternetUrl** del Agente de mezcla.  
  
 La Escucha de replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Replisapi.dll) se configura en el equipo en el que se ejecuta IIS y es responsable de controlar los mensajes que se envían al servidor desde el publicador y los suscriptores. Cada nodo de la topología controla el flujo de datos XML con el Reconciliador de replicación de mezcla (Replrec.dll).  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versión posterior para todos los equipos que participen en la sincronización web.  
  
### Proceso de sincronización  
 Durante la sincronización se llevan a cabo los siguientes pasos:  
  
1.  El Agente de mezcla se inicia en el suscriptor. El agente realiza las tareas siguientes:  
  
    1.  Establece una conexión SQL con la base de datos de suscripciones.  
  
    2.  Extrae cualquier cambio de la base de datos.  
  
    3.  Realiza una solicitud HTTPS al equipo en el que se ejecuta IIS.  
  
    4.  Carga los cambios en los datos como un mensaje XML.  
  
2.  El Reconciliador de replicación de mezcla y la Escucha de replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hospedados en el equipo en el que se ejecuta IIS realizan lo siguiente:  
  
    1.  Responden a la solicitud HTTPS.  
  
    2.  Establecen una conexión SQL con la base de datos de publicación.  
  
    3.  Aplican los cambios de carga en la base de datos de publicación.  
  
    4.  Extraen los cambios de descarga para el suscriptor.  
  
    5.  Devuelven una respuesta HTTPS al Agente de mezcla.  
  
3.  A continuación, el Agente de mezcla en el suscriptor acepta la respuesta HTTPS y aplica los cambios de descarga a la base de datos de suscripciones.  
  
## Vea también  
 [Configurar sincronización web](../../relational-databases/replication/configure-web-synchronization.md)   
 [Topologías para sincronización web](../../relational-databases/replication/topologies-for-web-synchronization.md)  
  
  