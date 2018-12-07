---
title: Sincronización web para la replicación de mezcla | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication synchronization [SQL Server replication]
- Internet [SQL Server replication], synchronization
- synchronization [SQL Server replication], Web Synchronization
- Web publishing [SQL Server replication], synchronization
- Web synchronization, about
- Web synchronization
ms.assetid: 84785aba-b2c1-4821-9e9d-a363c73dcb37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f018f3415d0ee99eedb3c086e308a84c61cdc058
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52542897"
---
# <a name="web-synchronization-for-merge-replication"></a>Sincronización web para la replicación de mezcla
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La sincronización web para la replicación de mezcla permite replicar datos utilizando el protocolo HTTPS y es útil en los siguientes escenarios:  
  
-   Sincronizar datos de usuarios móviles a través de Internet  
  
-   Sincronizar datos entre bases de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través de un firewall corporativo  
  
 Por ejemplo, un representante de ventas puede utilizar la sincronización web durante sus viajes. La empresa [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]tiene representantes de ventas que viajan para visitar varias tiendas y proveedores de su región. En viajes más largos, los representantes se hospedan en hoteles y necesitan una manera cómoda de cargar datos de ventas y descargar cualquier actualización de productos al final de cada día.  
  
 El departamento de TI de [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] ha configurado cada equipo portátil con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y ha habilitado la replicación de mezcla para que utilice la sincronización web. El Agente de mezcla de cada equipo portátil tiene una dirección URL de Internet que apunta a los componentes de replicación instalados en un equipo en el que se ejecuta [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS). Estos componentes sincronizan el suscriptor con el publicador. Ahora cada representante se puede conectar a través de cualquier conexión de Internet disponible sin utilizar una conexión remota de acceso telefónico y puede cargar y descargar los datos que desee. La conexión de Internet utiliza SSL (Capa de sockets seguros), por lo que no es necesaria una red privada virtual (VPN).  
  
 Para obtener información sobre cómo configurar los componentes necesarios para la sincronización web, consulte [Configurar sincronización web](../../relational-databases/replication/configure-web-synchronization.md), [Configurar IIS para la sincronización web](../../relational-databases/replication/configure-iis-for-web-synchronization.md) y [Configurar IIS 7 para la sincronización web](../../relational-databases/replication/configure-iis-7-for-web-synchronization.md).  
  
> [!NOTE]  
>  La sincronización web está diseñada para sincronizar datos con equipos portátiles, dispositivos de mano y otros clientes. La sincronización web no está concebida para aplicaciones de servidor a servidor con grandes volúmenes de datos.  
  
## <a name="overview-of-how-web-synchronization-works"></a>Información general sobre el funcionamiento de la sincronización web  
 Cuando se utiliza la sincronización web, las actualizaciones en el suscriptor se empaquetan y envían como un mensaje XML al equipo en el que se ejecuta IIS mediante el protocolo HTTPS. El equipo en el que se ejecuta IIS envía los comandos al publicador en formato binario (normalmente mediante TCP/IP). Las actualizaciones en el publicador se envían al equipo en el que se ejecuta IIS y después se empaquetan como un mensaje XML para su envío al suscriptor.  
  
 En la siguiente ilustración se muestran algunos de los componentes que participan en la sincronización web para la replicación de mezcla.  
  
 ![Flujo de datos y componentes de la sincronización web](../../relational-databases/replication/media/web-sync01.gif "Flujo de datos y componentes de la sincronización web")  
  
 La sincronización web es una opción exclusiva de las suscripciones de extracción, por lo que un Agente de mezcla se ejecutará siempre en el suscriptor. Este Agente de mezcla puede ser el Agente de mezcla estándar, el control ActiveX del Agente de mezcla o de una aplicación que proporcione sincronización a través de Replication Management Objects (RMO). Para especificar la ubicación del equipo en el que se ejecuta IIS, use el parámetro **-InternetUrl** del Agente de mezcla.  
  
 La Escucha de replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Replisapi.dll) se configura en el equipo en el que se ejecuta IIS y es responsable de controlar los mensajes que se envían al servidor desde el publicador y los suscriptores. Cada nodo de la topología controla el flujo de datos XML con el Reconciliador de replicación de mezcla (Replrec.dll).  
  
 Se requiere[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versión posterior para todos los equipos que participen en la sincronización web.  
  
### <a name="synchronization-process"></a>Proceso de sincronización  
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
  
## <a name="see-also"></a>Ver también  
 [Configurar sincronización web](../../relational-databases/replication/configure-web-synchronization.md)   
 [Topologies for Web Synchronization](../../relational-databases/replication/topologies-for-web-synchronization.md)  
  
  
