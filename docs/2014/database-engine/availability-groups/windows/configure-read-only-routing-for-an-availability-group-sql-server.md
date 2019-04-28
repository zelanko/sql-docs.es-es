---
title: Configurar el enrutamiento de solo lectura para un grupo de disponibilidad (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- read-only routing
- Availability Groups [SQL Server], readable secondary replicas
- Availability Groups [SQL Server], read-only routing
- readable secondary replicas
- Availability Groups [SQL Server], client connectivity
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 7bd89ddd-0403-4930-a5eb-3c78718533d4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a129386b5c88939d68f5d7f23a5fe2b4d8ce7cca
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62789535"
---
# <a name="configure-read-only-routing-for-an-availability-group-sql-server"></a>Configurar el enrutamiento de solo lectura para un grupo de disponibilidad (SQL Server)
  Para configurar el grupo de disponibilidad AlwaysOn para admitir el enrutamiento de solo lectura en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], puede utilizar [!INCLUDE[tsql](../../../includes/tsql-md.md)] o PowerShell. El *enrutamiento de solo lectura* hace referencia a la capacidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de enrutar las solicitudes de conexión de solo lectura a una [réplica secundaria legible](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md) AlwaysOn disponible (es decir, una réplica configurada para permitir cargas de trabajo de solo lectura al ejecutarse en un rol secundario). Para admitir el enrutamiento de solo lectura, el grupo de disponibilidad debe poseer un [agente de escucha de grupo de disponibilidad](../../listeners-client-connectivity-application-failover.md). Los clientes de solo lectura deben dirigir sus solicitudes de conexión a este agente de escucha y las cadenas de conexión del cliente deben especificar el intento de aplicación como de “solo lectura”. Es decir, deben ser *solicitudes de conexión de intento de lectura*.  
  
> [!NOTE]
>  Para obtener información sobre cómo configurar una réplica secundaria legible, vea [Configurar el acceso de solo lectura en una réplica de disponibilidad &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md).  
> 
> 
> 
> [!NOTE]
>  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]no admite la configuración del enrutamiento de solo lectura.  
  

  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   El grupo de disponibilidad debe poseer un agente de escucha de grupo de disponibilidad. Para obtener más información, vea [Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md).  
  
-   Una o varias réplicas de disponibilidad deben configurarse para aceptar solo lectura en el rol secundario (es decir, para ser [réplicas secundarias legibles](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)(AlwaysOn % 20Availability % 20Groups\).md)). Para obtener más información, vea [Configurar el acceso de solo lectura en una réplica de disponibilidad &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md).  
  
-   Debe estar conectado a la instancia del servidor que hospeda la réplica principal actual.  
  
###  <a name="RORReplicaProperties"></a> ¿Qué propiedades de réplica debe configurar para admitir el enrutamiento de solo lectura?  
  
-   Para cada réplica secundaria legible que vaya a admitir el enrutamiento de solo lectura, debe especificar una *dirección URL de enrutamiento de solo lectura*. Esta dirección URL tiene efecto cuando la réplica local se ejecuta en el rol secundario. La dirección URL de enrutamiento de solo lectura debe especificarse réplica a réplica, según sea necesario. Cada dirección URL de solo lectura se usa para enrutar las solicitudes de conexión de intento de lectura a una réplica secundaria legible específica. Normalmente, cada réplica secundaria legible se asigna a una dirección URL de enrutamiento de solo lectura.  
  
     Para obtener información sobre cómo calcular la dirección URL de enrutamiento de solo lectura para una réplica de disponibilidad, vea [Calcular read_only_routing_url para AlwaysOn](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx).  
  
-   Para cada réplica de disponibilidad que desee que admita el enrutamiento de solo lectura cuando sea la réplica principal, debe especificar una *lista de enrutamiento de solo lectura*. Una lista de enrutamiento de solo lectura dada solo tiene efecto cuando la réplica local se ejecuta en el rol principal. Esta lista se debe especificar réplica a réplica, según sea necesario. Normalmente, cada lista de enrutamiento de solo lectura contendría cada dirección URL de enrutamiento de solo lectura con la dirección URL de la réplica local al final de la lista.  
  
    > [!NOTE]  
    >  Las solicitudes de conexión de intento de lectura se enrutan al primer elemento secundario legible disponible en la lista de enrutamiento de solo lectura de la réplica principal actual. No hay equilibrio de carga.  
  
> [!NOTE]  
>  Para obtener información sobre los agentes de escucha de grupo de disponibilidad y obtener más información sobre el enrutamiento de solo lectura, vea [Agentes de escucha de grupo de disponibilidad, conectividad de cliente y conmutación por error de una aplicación &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
  
|Tarea|Permisos|  
|----------|-----------------|  
|Para configurar réplicas al crear un grupo de disponibilidad|Se requiere la pertenencia al rol fijo de servidor **sysadmin** y el permiso de servidor CREATE AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.|  
|Para modificar una réplica de disponibilidad|Se requiere el permiso ALTER AVAILABILITY GROUP en el grupo de disponibilidad, el permiso CONTROL AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.|  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para configurar el enrutamiento de solo lectura**  
  
> [!NOTE]  
>  Para obtener un ejemplo de código, vea [Ejemplo (Transact-SQL)](#TsqlExample), más adelante en esta sección.  
  
1.  Conéctese a la instancia del servidor que hospeda la réplica principal.  
  
2.  Si va a especificar una réplica para un nuevo grupo de disponibilidad, use la instrucción [CREATE AVAILABILITY GROUP](/sql/t-sql/statements/create-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] . Si va a agregar o modificar una réplica para un grupo de disponibilidad existente, use la instrucción [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
    -   Para configurar el acceso de solo lectura para el rol secundario, en la cláusula ADD REPLICA o MODIFY REPLICA WITH, especifique la opción SECONDARY_ROLE, del siguiente modo:  
  
         SECONDARY_ROLE **(** READ_ONLY_ROUTING_URL **='** TCP **://*`system-address`*:*`port`*')**  
  
         Los parámetros de la dirección URL de enrutamiento de solo lectura son los siguientes:  
  
         *system-address*  
         Es una cadena, como un nombre de sistema, un nombre de dominio completo o una dirección IP, que identifica sin ambigüedad el equipo de destino.  
  
         *port*  
         Es un número de puerto que usa el motor de base de datos de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
         Por ejemplo:   `SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER01.contoso.com:1433')`  
  
         En una cláusula MODIFY REPLICA el ALLOW_CONNECTIONS es opcional si la réplica ya está configurada para permitir conexiones de solo lectura.  
  
         Para obtener más información, vea [Calcular read_only_routing_url para AlwaysOn](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx).  
  
    -   Para configurar el enrutamiento de solo lectura para el rol principal, en la cláusula ADD REPLICA o MODIFY REPLICA WITH, especifique la opción PRIMARY_ROLE, del siguiente modo:  
  
         PRIMARY_ROLE **(** READ_ONLY_ROUTING_LIST **= ('*`server`*'** [ **,**... *n* ] **))**  
  
         donde *server* identifica una instancia del servidor que hospeda una réplica secundaria de solo lectura en el grupo de disponibilidad.  
  
         Por ejemplo:   `PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('Server1','Server2'))`  
  
        > [!NOTE]  
        >  Debe establecer la dirección URL de enrutamiento de solo lectura antes de configurar la lista de enrutamiento de solo lectura.  
  
###  <a name="TsqlExample"></a> Ejemplo (Transact-SQL)  
 En el ejemplo siguiente se modifica la disponibilidad de las dos réplicas de un grupo de disponibilidad existente, `AG1` para admitir el enrutamiento de solo lectura, si una de las réplicas posee actualmente el rol principal. Para identificar las instancias de servidor que hospedan la réplica de disponibilidad, este ejemplo especifica los nombres de instancia `COMPUTER01` y `COMPUTER02`.  
  
```  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER01' WITH   
(SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY));  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER01' WITH   
(SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER01.contoso.com:1433'));  
  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER02' WITH   
(SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY));  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER02' WITH   
(SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER02.contoso.com:1433'));  
  
ALTER AVAILABILITY GROUP [AG1]   
MODIFY REPLICA ON  
N'COMPUTER01' WITH   
(PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('COMPUTER02','COMPUTER01')));  
  
ALTER AVAILABILITY GROUP [AG1]   
MODIFY REPLICA ON  
N'COMPUTER02' WITH   
(PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('COMPUTER01','COMPUTER02')));  
GO  
  
```  
  
##  <a name="PowerShellProcedure"></a> Usar PowerShell  
 **Para configurar el enrutamiento de solo lectura**  
  
> [!NOTE]  
>  Para obtener un ejemplo de código, vea [Ejemplo (PowerShell)](#PSExample), más adelante en esta sección.  
  
1.  Establezca el valor predeterminado (`cd`) en la instancia del servidor que hospeda la réplica de disponibilidad principal.  
  
2.  Para agregar una réplica de disponibilidad a un grupo de disponibilidad, use el cmdlet `New-SqlAvailabilityReplica`. Para modificar una réplica de disponibilidad existente, use el cmdlet `Set-SqlAvailabilityReplica`. Los parámetros pertinentes son los siguientes:  
  
    -   Para configurar el enrutamiento de solo lectura para el rol secundario, especifique el **ReadonlyRoutingConnectionUrl "*`url`*"** parámetro.  
  
         donde, *url* es el nombre de dominio completo (FQDN) y puerto que se usa para el enrutamiento de la réplica para las conexiones de solo lectura. Por ejemplo:  `-ReadonlyRoutingConnectionUrl "TCP://DBSERVER8.manufacturing.Adventure-Works.com:7024"`  
  
         Para obtener más información, vea [Calcular read_only_routing_url para AlwaysOn](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx).  
  
    -   Para configurar el acceso de conexión para el rol principal, especifique **ReadonlyRoutingList "*`server`*"** [ **,**... *n* ], donde *server* identifica una instancia del servidor que hospeda una réplica secundaria de solo lectura en el grupo de disponibilidad. Por ejemplo:  `-ReadOnlyRoutingList "SecondaryServer","PrimaryServer"`  
  
        > [!NOTE]  
        >  Debe establecer la dirección URL de enrutamiento de solo lectura de la réplica antes de configurar su lista de enrutamiento de solo lectura.  
  
    > [!NOTE]  
    >  Para ver la sintaxis de un cmdlet, use el cmdlet `Get-Help` en el entorno de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para más información, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Para configurar y usar el proveedor de SQL Server PowerShell**  
  
-   [Proveedor de SQL Server PowerShell Provider](../../../powershell/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)  
  
###  <a name="PSExample"></a> Ejemplo (PowerShell)  
 En el ejemplo siguiente se configura la réplica principal y una réplica secundaria en un grupo de disponibilidad para el enrutamiento de solo lectura. Primero, en el el ejemplo se asigna una dirección URL de solo lectura de enrutamiento a cada réplica. Después, establece la lista de enrutamiento de solo lectura en la réplica principal. Las conexiones con la propiedad "ReadOnly" establecida en la cadena de conexión se redirigirán a la réplica secundaria. Si esta réplica secundaria no es legible (según lo determinado por la opción de configuración `ConnectionModeInSecondaryRole`), la conexión se dirigirá de nuevo a la réplica principal.  
  
```  
Set-Location SQLSERVER:\SQL\PrimaryServer\default\AvailabilityGroups\MyAg  
$primaryReplica = Get-Item "AvailabilityReplicas\PrimaryServer"  
$secondaryReplica = Get-Item "AvailabilityReplicas\SecondaryServer"  
  
Set-SqlAvailabilityReplica -ReadOnlyRoutingConnectionUrl "TCP://PrimaryServer.domain.com:1433" -InputObject $primaryReplica  
Set-SqlAvailabilityReplica -ReadOnlyRoutingConnectionUrl "TCP://SecondaryServer.domain.com:1433" -InputObject $secondaryReplica  
Set-SqlAvailabilityReplica -ReadOnlyRoutingList "SecondaryServer","PrimaryServer" -InputObject $primaryReplica  
```  
  
##  <a name="FollowUp"></a> Seguimiento: después de configurar el enrutamiento de solo lectura  
 Una vez que la réplica principal actual y las réplicas secundarias legibles están configuradas para admitir el enrutamiento de solo lectura en ambos roles, las réplicas secundarias legibles pueden recibir solicitudes de intentos de conexión de lectura de los clientes que se conectan mediante el agente de escucha de grupo de disponibilidad.  
  
> [!TIP]  
>  Cuando se usa el [bcp (utilidad)](../../../tools/bcp-utility.md) o [utilidad sqlcmd](../../../tools/sqlcmd-utility.md), puede especificar el acceso de solo lectura a cualquier réplica secundaria que está habilitada para el acceso de solo lectura mediante el `-K ReadOnly` cambie.  
  
###  <a name="ConnStringReqsRecs"></a> Requisitos y recomendaciones para las cadenas de conexión de cliente  
 Para que una aplicación cliente use el enrutamiento de solo lectura, la cadena de conexión debe cumplir los requisitos siguientes:  
  
-   Usar el protocolo TCP.  
  
-   Establecer el atributo o propiedad para el intento de aplicaciones de solo lectura.  
  
-   Hacer referencia al agente de escucha de un grupo de disponibilidad que se configura para admitir el enrutamiento de solo lectura.  
  
-   Hacer referencia a una base de datos en ese grupo de disponibilidad.  
  
 Además, se recomienda que las cadenas de conexión habiliten la conmutación por error de múltiples subredes, que admite un subproceso de cliente paralelo para cada réplica en cada subred. Esto reduce el tiempo de reconexión de cliente después de una conmutación por error.  
  
 La sintaxis para una cadena de conexión depende del proveedor de SQL Server que una aplicación está utilizando. El siguiente ejemplo de cadena de conexión para el proveedor de datos de .NET Framework 4.0.2 para SQL Server, muestra las partes de una cadena de conexión necesarias y que se recomiendan para que funcionen con el enrutamiento de solo lectura.  
  
```  
Server=tcp:MyAgListener,1433;Database=Db1;IntegratedSecurity=SSPI;ApplicationIntent=ReadOnly;MultiSubnetFailover=True  
```  
  
 Para obtener más información sobre el intento de aplicación de solo lectura y el enrutamiento de solo lectura, vea [Agentes de escucha de grupo de disponibilidad, conectividad de cliente y conmutación por error de una aplicación &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md).  
  
### <a name="if-read-only-routing-is-not-working-correctly"></a>Si el enrutamiento de solo lectura no funciona correctamente  
 Para obtener información sobre la solución de problemas de una configuración de enrutamiento de solo lectura, vea [El enrutamiento de solo lectura no funciona correctamente](troubleshoot-always-on-availability-groups-configuration-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para ver las configuraciones del enrutamiento de solo lectura**  
  
-   [sys.availability_read_only_routing_lists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql)  
  
-   [sys.availability_replicas &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql) (columna **read_only_routing_url**)  
  
 **Para configurar el acceso de la conexión de cliente**  
  
-   [Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Configurar el acceso de solo lectura en una réplica de disponibilidad &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
 **Para usar las cadenas de conexión en aplicaciones**  
  
-   [Compatibilidad de SQL Server Native Client para la alta disponibilidad con recuperación de desastres](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [Usar palabras clave de cadena de conexión con SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   **Blogs:**  
  
     [Calcular read_only_routing_url para AlwaysOn](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx)  
  
     [Blogs del equipo de AlwaysOn SQL Server: El blog del equipo de AlwaysOn oficial SQL Server](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [Blogs de los ingenieros de SQL Server de CSS](https://blogs.msdn.com/b/psssql/)  
  
-   **Notas del producto:**  
  
     [Notas del producto de Microsoft para SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Notas del producto del equipo de asesoramiento al cliente de SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>Vea también  
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Secundarias activas: Réplicas secundarias legibles (grupos de disponibilidad AlwaysOn)](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Acerca del acceso de conexión de cliente a réplicas de disponibilidad &#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md)   
 [Agentes de escucha de grupo de disponibilidad, conectividad de cliente y conmutación por error de una aplicación &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)  
  
  
