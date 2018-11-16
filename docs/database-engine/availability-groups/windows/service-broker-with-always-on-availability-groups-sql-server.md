---
title: Service Broker con grupos de disponibilidad AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Service Broker, AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 881c20e5-1c99-44eb-b393-09fc5ea0f122
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7f544983e1d34073cfe681a614d7d4808b45cd3c
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51607115"
---
# <a name="service-broker-with-always-on-availability-groups-sql-server"></a>Service Broker con grupos de disponibilidad AlwaysOn (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tema contiene información acerca de la configuración de Service Broker para que funcione con [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 **En este tema:**  
  
-   [Requisitos de un servicio en un grupo de disponibilidad para que reciba mensajes remotos](#ReceiveRemoteMessages)  
  
-   [Requisitos para enviar mensajes a un servicio remoto en un grupo de disponibilidad](#SendRemoteMessages)  
  
##  <a name="ReceiveRemoteMessages"></a> Requisitos de un servicio en un grupo de disponibilidad para que reciba mensajes remotos  
  
1.  **Asegúrese de que el grupo de disponibilidad tiene un agente de escucha.**  
  
     Para obtener más información, vea [Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
  
2.  **Asegúrese de que el extremo de Service Broker existe y está correctamente configurado.**  
  
     En cada instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospede una réplica de disponibilidad para el grupo de disponibilidad, configure el extremo de Service Broker del modo siguiente:  
  
    -   Establezca LISTENER_IP en 'ALL'. Este valor permite las conexiones en cualquier dirección IP válida enlazada al agente de escucha del grupo de disponibilidad.  
  
    -   Establezca el valor PORT de Service Broker en el mismo número de puerto en todas las instancias del servidor host.  
  
        > [!TIP]  
        >  Para ver el número de puerto del punto de conexión de Service Broker en una instancia de servidor determinada, consulte la columna **port** de la vista de catálogo [sys.tcp_endpoints](../../../relational-databases/system-catalog-views/sys-tcp-endpoints-transact-sql.md) , donde **type_desc** = 'SERVICE_BROKER'.  
  
     En el ejemplo siguiente se crea un extremo de Service Broker autenticado por Windows que utiliza el puerto predeterminado de Service Broker (4022) y escucha en todas las direcciones IP válidas.  
  
    ```  
    CREATE ENDPOINT [SSBEndpoint]  
        STATE = STARTED  
        AS TCP  (LISTENER_PORT = 4022, LISTENER_IP = ALL )  
        FOR SERVICE_BROKER (AUTHENTICATION = WINDOWS)  
    ```  
  
     Para obtener más información, vea [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-endpoint-transact-sql.md).  

    > [!NOTE]  
    SQL Server Broker no reconoce múltiples subredes. Asegúrese de usar "registerallprovidersip" establecido en 0, y compruebe que no esté usando direcciones IP estáticas en DNS con el permiso necesario para el clúster en el DNS, como se define en https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server. El agente puede retrasar el mensaje con el estado "CONVERSING" al intentar usar la IP deshabilitada.

3.  **Conceda el permiso CONNECT para usar el extremo.**  
  
     Conceda el permiso CONNECT para usar el extremo de Service Broker a PUBLIC o a un inicio de sesión.  
  
     En el siguiente ejemplo se concede la conexión para usar un extremo de Service Broker denominado `broker_endpoint` a PUBLIC.  
  
    ```  
    GRANT CONNECT ON ENDPOINT::[broker_endpoint] TO [PUBLIC]  
    ```  
  
     Para obtener más información, vea [GRANT &#40;Transact-SQL&#41;](../../../t-sql/statements/grant-transact-sql.md).  
  
4.  **Asegúrese de que msdb contiene una ruta AutoCreatedLocal o una ruta al servicio específico.**  
  
    > [!NOTE]  
    >  De forma predeterminada, todas las bases de datos de usuario, incluida **msdb**, contienen la ruta **AutoCreatedLocal**. Esta ruta coincide con cualquier nombre de servicio e instancia de agente, y especifica que el mensaje debe entregarse en la instancia actual. **AutoCreatedLocal** tiene una prioridad menor que las rutas que especifican explícitamente un servicio específico que se comunica con una instancia remota.  
  
     Para obtener más información sobre cómo crear rutas, vea [Ejemplos de enrutamiento de Service Broker](https://msdn.microsoft.com/library/ms166090\(SQL.105\).aspx) (en la versión de Libros en pantalla de [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] ) y [CREATE ROUTE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-route-transact-sql.md).  
  
##  <a name="SendRemoteMessages"></a> Requisitos para enviar mensajes a un servicio remoto en un grupo de disponibilidad  
  
1.  **Cree una ruta al servicio de destino.**  
  
     Configure la ruta del modo siguiente:  
  
    -   Establezca ADDRESS en la dirección IP del agente de escucha del grupo de disponibilidad que hospeda la base de datos de servicio.  
  
    -   Establezca PORT en el puerto especificado en el extremo de Service Broker de cada instancia de SQL Server remota.  
  
     En el ejemplo siguiente se crea una ruta denominada `RouteToTargetService` para el servicio `ISBNLookupRequestService` . La ruta tiene como destino el agente de escucha del grupo de disponibilidad, `MyAgListener`, que utiliza el puerto 4022.  
  
    ```  
    CREATE ROUTE [RouteToTargetService] WITH   
    SERVICE_NAME = 'ISBNLookupRequestService',   
    ADDRESS = 'TCP://MyAgListener:4022';  
  
    ```  
  
     Para obtener más información, vea [CREATE ROUTE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-route-transact-sql.md).  
  
2.  **Asegúrese de que msdb contiene una ruta AutoCreatedLocal o una ruta al servicio específico.** (Para obtener más información, vea [Requisitos de un servicio en un grupo de disponibilidad para que reciba mensajes remotos](#ReceiveRemoteMessages), anteriormente en este tema).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-endpoint-transact-sql.md)  
  
-   [CREATE ROUTE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-route-transact-sql.md)  
  
-   [GRANT &#40;Transact-SQL&#41;](../../../t-sql/statements/grant-transact-sql.md)  
  
-   [Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
  
-   [Creación y configuración de grupos de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)  
  
-   [Configurar cuentas de inicio de sesión para la creación de reflejo de la base de datos o grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md)  
  
## <a name="see-also"></a>Ver también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Agentes de escucha de grupo de disponibilidad, conectividad de cliente y conmutación por error de una aplicación &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)   
 [SQL Server Service Broker](../../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
