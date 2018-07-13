---
title: El punto de conexión de creación de reflejo de la base de datos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- database mirroring [SQL Server], endpoint
- endpoints [SQL Server], AlwaysOn Availability Groups
- endpoints [SQL Server], database mirroring
- Availability Groups [SQL Server], endpoint
ms.assetid: 39332dc5-678e-4650-9217-6aa3cdc41635
caps.latest.revision: 44
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e9250860dbdc750bda53e28e52a31bcbe0e038b9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37185175"
---
# <a name="the-database-mirroring-endpoint-sql-server"></a>El extremo de creación de reflejo de la base de datos (SQL Server)
  Para participar en la creación de reflejo de la base de datos o [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] , una instancia de servidor requiere su propio *extremo de creación de reflejo de la base de datos*dedicado. Se trata de un extremo especial que se utiliza exclusivamente para recibir conexiones procedentes de otras instancias de servidor. En una instancia de servidor determinada, todas las conexiones de creación de reflejo de la base de datos o [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] a cualquier otra instancia de servidor utilizan un único extremo de creación de reflejo de la base de datos.  
  
 Los extremos de creación de reflejo de la base de datos utilizan el Protocolo de control de transporte (TCP) para enviar y recibir mensajes entre las instancias del servidor que participan en sesiones de creación de reflejo de la base de datos u hospedan réplicas de disponibilidad. El extremo de creación de reflejo de la base de datos escucha en un número de puerto TCP exclusivo.  
  
> [!NOTE]  
>  Las conexiones de cliente a un servidor principal o una réplica principal no usan el extremo de creación de reflejo de la base de datos.  
  
> [!NOTE]  
>  La característica de creación de reflejo de la base de datos se quitará en una versión futura de Microsoft SQL Server. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente utilizan la creación de reflejo de la base de datos para utilizar [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] en su lugar.  
  
  
##  <a name="ServerNetworkAddress"></a> Dirección de red de servidor  
 La dirección de red de una instancia de servidor (su *dirección de red de servidor* o *dirección URL de punto de conexión*) contiene el número de puerto de su punto de conexión, así como el nombre de sistema y de dominio del equipo host. El número de puerto identifica de forma exclusiva una instancia de servidor específica.  
  
 En la siguiente ilustración se muestra cómo dos instancias de servidor en el mismo servidor se identifican de forma exclusiva. Las direcciones de red de las dos instancias de servidor contienen el mismo nombre de sistema, `MYSYSTEM`, y el mismo nombre de dominio, `Adventure-Works.MyDomain.com`. Para habilitar el sistema de forma que enrute conexiones a una instancia de servidor, una dirección de red de servidor incluye el número de puerto asociado al extremo para la creación de reflejo de una instancia de servidor en particular.  
  
 ![Direcciones de red del servidor de una instancia predeterminada](../media/dbm-2-instances-ports-1-system.gif "Direcciones de red del servidor de una instancia predeterminada")  
  
 De forma predeterminada, una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no contiene un extremo de creación de reflejo de la base de datos. Éstos se deben crear manualmente como parte de la configuración de la sesión de creación de reflejo de la base de datos. El administrador del sistema debe crear un extremo independiente en cada instancia de servidor que participe en la creación del reflejo de la base de datos. Tenga en cuenta que si más de una instancia de servidor en un equipo determinado requiere un extremo de creación de reflejo de la base de datos, debe especificar un número de puerto diferente para cada extremo.  
  
> [!IMPORTANT]  
>  Si el equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dispone de firewall, la configuración de éste debe permitir conexiones entrantes y salientes en el puerto especificado en el extremo.  
  
 Para la creación de reflejo de la base de datos y [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], la autenticación y el cifrado se configuran en el extremo. Para obtener más información, consulte [seguridad de transporte para la creación de reflejo de base de datos y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](transport-security-database-mirroring-always-on-availability.md).  
  
> [!IMPORTANT]  
>  No reconfigure un extremo de creación de reflejo de la base de datos en uso. Las instancias de servidor usan los extremos de todas las demás instancias para conocer el estado de los otros sistemas. Si reconfigura el extremo, podría reiniciarse, lo que podría parecer un error en las otras instancias de servidor. Esto es especialmente importante en el modo de conmutación automática por error, en el que volver a configurar el extremo en un asociado podría dar lugar a una conmutación por error.  
  
  
##  <a name="EndpointAuthenticationTypes"></a> Determinar el tipo de autenticación para un extremo de creación de reflejo de la base de datos  
 Es importante saber que las cuentas de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de las instancias del servidor determinan el tipo de autenticación que se puede usar para los extremos de creación de reflejo de la base de datos, del modo siguiente:  
  
-   Si cada instancia de servidor se ejecuta en una cuenta de servicio de dominio, puede utilizar la autenticación de Windows para los extremos de creación de reflejo de la base de datos. Si las instancias del servidor se ejecutan como la misma cuenta de usuario de dominio, automáticamente existen los inicios de sesión de usuario correctos en ambas bases de datos **maestras** . Esto simplifica la configuración de seguridad de las base de datos de disponibilidad y es recomendable su aplicación.  
  
     Si las instancias de servidor que hospedan las réplicas de disponibilidad para un grupo de disponibilidad se ejecutan como cuentas diferentes, el inicio de sesión de cada cuenta debe crearse en **master** en la otra instancia de servidor. A continuación, deben concederse a ese inicio de sesión permisos CONNECT para conectarse al extremo de creación de reflejo de la base de datos de esa instancia de servidor. Para obtener más información, [configurar inicio de sesión de cuentas para la creación de reflejo de base de datos o grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](set-up-login-accounts-database-mirroring-always-on-availability.md).  
  
     Si las instancias de servidor utilizan la autenticación de Windows, puede crear extremos de creación de reflejo de la base de datos utilizando [!INCLUDE[tsql](../../includes/tsql-md.md)], PowerShell o el Asistente para nuevo grupo de disponibilidad.  
  
    > [!NOTE]  
    >  Si una instancia de servidor que va a hospedar una réplica de disponibilidad no tiene un extremo de creación de reflejo de la base de datos, el Asistente para nuevo grupo de disponibilidad puede crear automáticamente un extremo de creación de reflejo de la base de datos que utilice la autenticación de Windows. Para obtener más información, vea [Usar el Asistente para grupo de disponibilidad &#40;SQL Server Management Studio&#41;](../availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md).  
  
-   Si alguna instancia de servidor se ejecuta en una cuenta integrada (como sistema local, servicio local o servicio de red) o una cuenta que no es de dominio, debe utilizar certificados para la autenticación de extremos. Si utiliza certificados para los extremos de creación de reflejo de la base de datos, el administrador del sistema debe configurar cada instancia del servidor de modo que se utilicen certificados en las conexiones entrantes y salientes.  
  
     No hay ningún método automatizado para configurar la seguridad de creación de reflejo de la base de datos mediante certificados. Deberá usar CREATE ENDPOINT [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción o el `New-SqlHadrEndpoint` cmdlet de PowerShell. Para obtener más información, vea [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql). Para obtener información acerca de cómo habilitar la autenticación de certificados en una instancia del servidor, consulte [usar certificados para un extremo de creación de reflejo de base de datos &#40;Transact-SQL&#41;](use-certificates-for-a-database-mirroring-endpoint-transact-sql.md).  
  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para configurar un extremo de creación del reflejo de la base de datos**  
  
-   [Crear un punto de conexión de creación de reflejo de la base de datos para la autenticación de Windows &#40;Transact-SQL&#41;](create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Usar certificados para un punto de conexión de creación de reflejo de la base de datos &#40;Transact-SQL&#41;](use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
    -   [Permitir que un punto de conexión de creación de reflejo de la base de datos utilice certificados para las conexiones salientes &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-outbound-connections.md)  
  
    -   [Permitir que un punto de conexión de creación de reflejo de la base de datos use certificados para las conexiones entrantes &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [Especificar una dirección de red de servidor &#40;creación de reflejo de la base de datos&#41;](specify-a-server-network-address-database-mirroring.md)  
  
-   [Especificar la dirección URL del punto de conexión al agregar o modificar una réplica de disponibilidad &#40;SQL Server&#41;](../availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [Usar el Asistente para grupo de disponibilidad &#40;SQL Server Management Studio&#41;](../../ssms/sql-server-management-studio-ssms.md)  
  
 **Para ver información acerca del extremo de creación de reflejo de la base de datos**  
  
-   [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)  
  
  
## <a name="see-also"></a>Vea también  
 [Seguridad de transporte para la creación de reflejo de base de datos y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](transport-security-database-mirroring-always-on-availability.md)   
 [Solucionar problemas de configuración de creación de reflejo de la base de datos &#40;SQL Server&#41;](troubleshoot-database-mirroring-configuration-sql-server.md)   
 [Sys.dm_hadr_availability_replica_states &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql)   
 [Sys.dm_db_mirroring_connections &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/database-mirroring-sys-dm-db-mirroring-connections)  
  
  
