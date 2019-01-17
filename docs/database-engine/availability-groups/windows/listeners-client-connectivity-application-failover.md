---
title: Conexión a un agente de escucha del grupo de disponibilidad
description: Contiene información sobre cómo conectarse a un agente de escucha del grupo de disponibilidad Always On, antes y después de la conmutación por error.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- read-only routing
- read-intent connections [AlwaysOn Availability Groups]
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], read-only routing
- Availability Groups [SQL Server], client connectivity
ms.assetid: 76fb3eca-6b08-4610-8d79-64019dd56c44
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 23321c9c8208cf4a78909ab5cedcd921184f7b0b
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53214706"
---
# <a name="connect-to-an-always-on-availability-group-listener"></a>Conexión a un agente de escucha del grupo de disponibilidad Always On 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tema contiene información acerca de las consideraciones de conectividad del cliente de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] y la funcionalidad de conmutación por error de aplicaciones.  
  
> [!NOTE]  
>  Para la mayoría de las configuraciones habituales de agente de escucha, puede crear el primer agente de escucha del grupo de disponibilidad utilizando simplemente instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)] o cmdlets de PowerShell. Para obtener más información, vea [Tareas relacionadas](#RelatedTasks), más adelante en este mismo tema.  
  
 **En este tema:**  
  
-   [Agentes de escucha del grupo de disponibilidad](#AGlisteners)  
  
-   [Usar un agente de escucha para conectarse a la réplica principal](#ConnectToPrimary)  
  
-   [Usar un agente de escucha para conectarse a una réplica secundaria de solo lectura (enrutamiento de solo lectura)](#ConnectToSecondary)  
  
    -   [Para configurar réplicas de disponibilidad para el enrutamiento de solo lectura](#ConfigureARsForROR)  
  
    -   [Intención de aplicación de solo lectura y enrutamiento de solo lectura](#ReadOnlyAppIntent)  
  
-   [Omitir agentes de escucha del grupo de disponibilidad](#BypassAGl)  
  
-   [Comportamiento de conexiones de cliente en la conmutación por error](#CCBehaviorOnFailover)  
  
-   [Compatibilidad con clústeres de conmutación por error de varias subredes de grupo de disponibilidad](#SupportAgMultiSubnetFailover)  
  
-   [Agentes de escucha del grupo de disponibilidad y certificados SSL](#SSLcertificates)  
  
-   [Agentes de escucha del grupo de disponibilidad y nombres principales de servidor (SPN)](#SPNs)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
-   [Contenido relacionado](#RelatedContent)  
  
##  <a name="AGlisteners"></a> Agentes de escucha del grupo de disponibilidad  
 Puede proporcionar conectividad de cliente a la base de datos de un grupo de disponibilidad determinado mediante la creación de un agente de escucha del grupo de disponibilidad. Un agente de escucha de grupo de disponibilidad es un nombre de red virtual (VNN) al que los clientes pueden conectarse para tener acceso a una base de datos situada en una réplica principal o secundaria de un grupo de disponibilidad AlwaysOn. Los agentes de escucha del grupo de disponibilidad permiten a los clientes conectarse a una réplica de disponibilidad sin conocer el nombre de la instancia física de SQL Server a la que se están conectando.  No hay necesidad de modificar la cadena de conexión del cliente para conectarse a la ubicación actual de la réplica principal.  
  
 Un agente de escucha de grupo de disponibilidad se compone de un nombre de agente de escucha del Sistema de nombres de dominio (DNS), de una designación de puerto de agente de escucha y de una o varias direcciones IP. Solo el protocolo TCP es compatible con el agente de escucha del grupo de disponibilidad.  El nombre DNS del agente de escucha también debe ser único en el dominio y en NetBIOS.  Cuando se crea un nuevo agente de escucha del grupo de disponibilidad, se convierte en un recurso en un clúster con un nombre de red virtual (VNN), una dirección IP virtual (VIP) y una dependencia de grupo de disponibilidad asociados. Un cliente utiliza DNS para resolver VNN en varias direcciones IP y después intenta conectarse a cada dirección hasta que una solicitud de conexión tiene éxito o hasta que se agota el tiempo de espera de las solicitudes de conexión.  
  
 Si el enrutamiento de solo lectura se configura para una o varias [réplicas secundarias legibles](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md), las conexiones de cliente de intento de lectura dirigidas a la réplica principal se redirigen a una réplica secundaria legible. Asimismo, si la réplica principal se queda sin conexión en una instancia de SQL Server y se pone en línea una nueva réplica principal en otra instancia de SQL Server, el agente de escucha del grupo de disponibilidad permite a los clientes conectarse a la nueva réplica principal.  
  
 Para obtener información esencial sobre los agentes de escucha del grupo de disponibilidad, vea [Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
  
 **En esta sección:**  
  
-   [Configuración de agentes de escucha del grupo de disponibilidad](#AGlConfig)  
  
-   [Seleccionar un puerto de agentes de escucha del grupo de disponibilidad](#SelectListenerPort)  
  
###  <a name="AGlConfig"></a> Configuración de agentes de escucha del grupo de disponibilidad  
 Un agente de escucha del grupo de disponibilidad se define por lo siguiente:  
  
 Nombre DNS único  
 Esto también se conoce como Nombre de red virtual (VNN). Se aplican las reglas de nomenclatura de Active Directory para los nombres de host DNS. Para obtener más información, vea el artículo de KB [Convenciones de nomenclatura en Active Directory para equipos, dominios, sitios y unidades organizativas](https://support.microsoft.com/kb/909264) .  
  
 Una o varias direcciones IP virtuales (VIP)  
 Las direcciones VIP se configuran para una o varias subredes en las que el grupo de disponibilidad puede realizar la conmutación por error.  
  
 Configuración de dirección IP  
 Para un agente de escucha determinado del grupo de disponibilidad, la dirección IP usa el Protocolo de configuración dinámica de host (DHCP) o una o varias direcciones IP estáticas.  
  
-   Protocolo de configuración dinámica de host (DHCP)  
  
     Si un grupo de disponibilidad reside en una sola subred, puede configurar todas las direcciones IP del agente de escucha del grupo de disponibilidad para usar DHCP. En los entornos de preproducción, DHCP proporciona una instalación fácil para un grupo de disponibilidad que no requiera recuperación ante desastres en un sitio remoto en una subred independiente. Sin embargo, no se debe usar DHCP junto con un agente de escucha del grupo de disponibilidad en un entorno de producción. Esto se debe a que, en caso de tiempo de inactividad, si expira el tiempo de concesión de la dirección de IP de DHCP, se necesitará un tiempo adicional para volver a registrar la nueva dirección IP de DHCP asociada al nombre DNS del agente de escucha. El tiempo adicional producirá un error de conexión del cliente.  
  
-   Direcciones IP estáticas  
  
     En los entornos de producción, se recomienda que los agentes de escucha del grupo de disponibilidad usen direcciones IP estáticas. Además, en los casos donde los grupos de disponibilidad se extienden a través de subredes en un dominio de varias subredes, un agente de escucha del grupo de disponibilidad debe usar direcciones IP estáticas.  
  
 Las configuraciones de red híbridas y DHCP en subredes no se admiten para los agentes de escucha del grupo de disponibilidad. Esto se debe a que cuando se produce una conmutación por error, una dirección IP dinámica puede expirar o lanzarse, con lo que se compromete la alta disponibilidad total.  
  
###  <a name="SelectListenerPort"></a> Seleccionar un puerto de agentes de escucha del grupo de disponibilidad  
 Al configurar un agente de escucha del grupo de disponibilidad, debe designar un puerto.  Puede configurar el puerto predeterminado en 1433 para permitir la sencillez de las cadenas de conexión de cliente. Si utiliza 1433, no necesita indicar un número de puerto en una cadena de conexión.   Además, puesto que cada agente de escucha del grupo de disponibilidad tendrá un nombre de red virtual independiente, cada agente de escucha del grupo de disponibilidad configurado en un único WSFC se puede configurar para hacer referencia al mismo puerto predeterminado 1433.  
  
 También puede diseñar un puerto de agente de escucha no estándar, aunque esto significa que también necesitará especificar explícitamente un puerto de destino en la cadena de conexión cada vez que se conecte al agente de escucha del grupo de disponibilidad.  También necesitará abrir permiso en el firewall para el puerto no estándar.  
  
 Si utiliza el puerto predeterminado 1433 para los VNN del agente de escucha del grupo de disponibilidad, seguirá siendo necesario asegurarse de que ningún otro servicio en el nodo de clúster esté utilizando este puerto; de lo contrario, se produciría un conflicto de puerto.  
  
 Si una de las instancias de SQL Server ya está escuchando en el puerto TCP 1433 a través del agente de escucha de la instancia y no hay otros servicios (incluidas las instancias adicionales de SQL Server) en el equipo que escuchen en el puerto 1433, no se producirá un conflicto de puerto con el agente de escucha del grupo de disponibilidad.  Esto se debe a que el agente de escucha del grupo de disponibilidad puede compartir el mismo puerto TCP en el mismo proceso del servicio.  Sin embargo, no se deben configurar varias instancias de SQL Server (en paralelo) para escuchar en el mismo puerto.  
  
##  <a name="ConnectToPrimary"></a> Usar un agente de escucha para conectarse a la réplica principal  
 Para usar un agente de escucha del grupo de disponibilidad y conectarse a la réplica principal para acceso de lectura/escritura, la cadena de conexión especifica el nombre DNS del agente de escucha del grupo de disponibilidad.  Si una réplica principal del grupo de disponibilidad cambia a una nueva réplica, las conexiones existentes que usan un nombre de red del agente de escucha del grupo de disponibilidad se desconectarán.  Las nuevas conexiones al agente de escucha del grupo de disponibilidad se dirigen a la nueva réplica principal. El siguiente es un ejemplo de una cadena de conexión básica para el proveedor ADO.NET (System.Data.SqlClient):  
  
```  
Server=tcp: AGListener,1433;Database=MyDB;IntegratedSecurity=SSPI  
```  
  
 Puede seguir eligiendo hacer referencia directamente a la instancia de SQL Server de las réplicas principal o secundaria en lugar de utilizar el nombre del servidor del agente de escucha del grupo de disponibilidad; sin embargo, si decide realizar esta acción, perderá la ventaja que supone dirigir automáticamente las nuevas conexiones a la réplica principal actual.  También perderá la ventaja del enrutamiento de solo lectura.  
  
##  <a name="ConnectToSecondary"></a> Usar un agente de escucha para conectarse a una réplica secundaria de solo lectura (enrutamiento de solo lectura)  
 El*enrutamiento de solo lectura* se refiere a la capacidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de enrutar las conexiones entrantes a un agente de escucha de grupo de disponibilidad a una réplica secundaria configurada para permitir las cargas de trabajo de solo lectura. Una conexión entrante que hace referencia al nombre de un agente de escucha del grupo de disponibilidad se puede enrutar automáticamente a una réplica de solo lectura si se cumple lo siguiente:  
  
-   Al menos una réplica secundaria se establece para acceso de solo lectura, y cada réplica secundaria de solo lectura y la réplica principal se configuran para admitir el enrutamiento de solo lectura. Para obtener más información, vea [Para configurar réplicas de disponibilidad para el enrutamiento de solo lectura](#ConfigureARsForROR), más adelante en esta sección.  

-   La cadena de conexión hace referencia a una base de datos implicada en el grupo de disponibilidad. Una alternativa para esto sería que el inicio de sesión usado en la conexión tenga la base de datos configurada como su base de datos predeterminada. Para más información, vea [Calculating read_only_routing_url for Always On](https://blogs.msdn.microsoft.com/mattn/2012/04/25/calculating-read_only_routing_url-for-alwayson/) (Calcular read_only_routing_url para Always On).

-   La cadena de conexión hace referencia a un agente de escucha de grupo de disponibilidad y la intención de aplicaciones de la conexión entrante se establece en solo lectura (por ejemplo, al usar la palabra clave **Application Intent=ReadOnly** en las cadenas de conexión, los atributos de conexión o las propiedades de ODBC u OLEDB). Para obtener más información, vea [Intención de aplicación de solo lectura y enrutamiento de solo lectura](#ReadOnlyAppIntent), más adelante en esta sección.  
  
###  <a name="ConfigureARsForROR"></a> Para configurar réplicas de disponibilidad para el enrutamiento de solo lectura  
 Un administrador de base de datos debe configurar las réplicas de disponibilidad del siguiente modo:  
  
1.  Para cada réplica de disponibilidad que desee configurar como réplica secundaria legible, un administrador de base de datos debe configurar los valores siguientes, que tienen efecto solo en el rol secundario:  
  
    -   El acceso de conexión debe establecerse en "todo" o "solo lectura".  
  
    -   Se debe especificar la dirección URL de enrutamiento de solo lectura.  
  
2.  Para cada una de estas réplicas, se debe especificar una lista de enrutamiento de solo lectura para el rol principal. Especifique uno o varios nombres de servidor como destinos de enrutamiento.  
  
####  <a name="RelatedTasksROR"></a> Tareas relacionadas  
  
-   [Configurar el acceso de solo lectura en una réplica de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Configurar el enrutamiento de solo lectura para un grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
###  <a name="ReadOnlyAppIntent"></a> Intención de aplicación de solo lectura y enrutamiento de solo lectura  
 La propiedad de la cadena de conexión de la intención de aplicación expresa la solicitud de la aplicación cliente de ser dirigida a una versión de lectura y escritura, o de solo lectura, de una base de datos del grupo de disponibilidad. Para utilizar el enrutamiento de solo lectura, un cliente debe utilizar un intento de aplicación de solo lectura en la cadena de conexión al conectarse al agente de escucha del grupo de disponibilidad. Sin el intento de aplicación de solo lectura, las conexiones al agente de escucha del grupo de disponibilidad se dirigen a la base de datos en la réplica principal.  
  
 El atributo de la intención de aplicación se almacena en la sesión de cliente durante el inicio de sesión y, después, la instancia de SQL Server procesará esta intención y determinará lo que debe hacer de acuerdo con la configuración del grupo de disponibilidad y el estado de lectura y escritura actual de la base de datos de destino en la réplica secundaria.  
  
 El siguiente es un ejemplo de una cadena de conexión para el proveedor ADO.NET (System.Data.SqlClient) que designa el intento de solo lectura de la aplicación:  
  
```  
Server=tcp:AGListener,1433;Database=AdventureWorks;IntegratedSecurity=SSPI;ApplicationIntent=ReadOnly  
```  
  
 En este ejemplo de cadena de comparación, el cliente intenta conectarse a la base de datos AdventureWorks mediante un agente de escucha del grupo de disponibilidad denominado `AGListener` en el puerto 1433 (también puede omitir el puerto si el agente de escucha del grupo de disponibilidad escucha en 1433).  La cadena de conexión tiene la propiedad **ApplicationIntent** establecida en **ReadOnly**, lo que la convierte en una *cadena de conexión de intención de lectura*.  Sin este valor, el servidor no habría intentado un enrutamiento de solo lectura de la conexión.  
  
 La base de datos principal del grupo de disponibilidad procesa la solicitud de enrutamiento de solo lectura entrante e intenta localizar una réplica en línea de solo lectura que esté unida a la réplica principal y esté configurada para el enrutamiento de solo lectura.  El cliente recibe información de conexión del servidor de réplica principal y se conecta a la réplica de solo lectura identificada.  
  
 Observe que el intento de aplicación se puede enviar de un controlador de cliente a una instancia de nivel inferior de SQL Server.  En este caso, el intento de aplicación de solo lectura se omite y la conexión continúa normalmente.  
  
 Puede omitir el enrutamiento de solo lectura si no establece la propiedad de conexión de intención de aplicaciones en **ReadOnly** (cuando no está designada, el valor predeterminado es **ReadWrite** durante el inicio de sesión) o si se conecta directamente a la instancia de réplica principal de SQL Server en lugar de usar el nombre del agente de escucha de grupo de disponibilidad.  El enrutamiento de solo lectura tampoco se producirá si se conecta directamente a una réplica de solo lectura.  
  
####  <a name="RelatedTasksApps"></a> Tareas relacionadas  
  
-   [Compatibilidad de SQL Server Native Client para la alta disponibilidad con recuperación de desastres](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [Usar palabras clave de cadena de conexión con SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
##  <a name="BypassAGl"></a> Omitir agentes de escucha del grupo de disponibilidad  
 Mientras los agentes de escucha del grupo de disponibilidad habilitan la compatibilidad con la redirección de conmutación por error y el enrutamiento de solo lectura, las conexiones de cliente no requieren utilizarlos. Una conexión de cliente puede hacer referencia directamente a la instancia de SQL Server en lugar de conectarse al agente de escucha del grupo de disponibilidad.  
  
 Para la instancia de SQL Server, es irrelevante si una conexión inicia una sesión utilizando el agente de escucha del grupo de disponibilidad o utilizando otro extremo de la instancia.  La instancia de SQL Server comprobará el estado de la base de datos de destino y permitirá o denegará la conectividad basada en la configuración del grupo de disponibilidad y el estado actual de la base de datos de la instancia.  Por ejemplo, si una aplicación cliente se conecta directamente a una instancia de puerto de SQL Server y se conecta a una base de datos de destino hospedada en un grupo de disponibilidad, y la base de datos de destino está en estado principal y en línea, la conectividad se realizará correctamente.  Si la base de datos de destino está sin conexión o en estado transitorio, la conectividad a la base de datos producirá un error.  
  
 Alternativamente, en la migración de creación de reflejo de la base de datos a [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], las aplicaciones pueden especificar la cadena de conexión de creación de reflejo de la base de datos mientras solo exista una réplica secundaria y no permita conexiones de usuario. Para obtener más información, vea [Usar cadenas de conexión de creación de reflejo de la base de datos con grupos de disponibilidad](#DbmConnectionString), más adelante en esta sección.  
  
###  <a name="DbmConnectionString"></a> Usar cadenas de conexión de creación de reflejo de la base de datos con grupos de disponibilidad  
 Si un grupo de disponibilidad posee solo una réplica secundaria y está configurado con ALLOW_CONNECTIONS = READ_ONLY o con ALLOW_CONNECTIONS = NONE en la réplica secundaria, los clientes pueden conectarse a la réplica de disponibilidad principal a través de una cadena de conexión de creación de reflejo de la base de datos. Este enfoque puede ser útil cuando se migra una aplicación existente de creación de reflejo de la base de datos a un grupo de disponibilidad, siempre que se limite el grupo de disponibilidad a dos réplicas de disponibilidad (una réplica principal y una réplica secundaria). Si agrega réplicas secundarias adicionales, deberá crear un agente de escucha del grupo de disponibilidad y actualizar sus aplicaciones para que se utilice el nombre DNS del agente de escucha del grupo de disponibilidad.  
  
 Cuando se utilizan cadenas de conexión de creación de reflejo de la base de datos, el cliente puede usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client o el proveedor de datos de .NET Framework para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. La cadena de conexión proporcionada por un cliente debe proporcionar como mínimo el nombre de una instancia del servidor, el *nombre del asociado inicial*, para identificar la instancia del servidor que hospeda inicialmente la réplica de disponibilidad con la que se desea establecer conexión. Opcionalmente, la cadena de conexión también puede proporcionar el nombre de otra instancia del servidor, *nombre del asociado de conmutación por error*, para identificar la instancia del servidor que hospeda inicialmente la réplica secundaria como nombre del asociado de conmutación por error.  
  
 Para obtener más información sobre las cadenas de conexión de creación de reflejo de la base de datos, vea [Conectar clientes a una sesión de creación de reflejo de la base de datos &#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md).  
  
##  <a name="CCBehaviorOnFailover"></a> Comportamiento de conexiones de cliente en la conmutación por error  
 Cuando se produce una conmutación por error de grupo de disponibilidad, las conexiones persistentes existentes al grupo de disponibilidad se terminan y el cliente debe establecer una nueva conexión para continuar trabajando con la misma base de datos principal o una base de datos secundaria de solo lectura.  Mientras una conmutación por error se produce en el servidor, la conectividad al grupo de disponibilidad puede sufrir un error, forzando a la aplicación cliente a volver a intentar la conexión hasta que el servidor principal vuelve a ponerse totalmente en línea.  
  
 Si el grupo de disponibilidad vuelve a ponerse en línea durante el intento de conexión de una aplicación cliente pero antes del tiempo de espera de conexión, el controlador cliente puede conectarse correctamente durante uno de los intentos internos de reintento y no se producirá ningún error en la aplicación en este caso.  
  
##  <a name="SupportAgMultiSubnetFailover"></a> Compatibilidad con clústeres de conmutación por error de varias subredes de grupo de disponibilidad  
 Si usa bibliotecas cliente que admiten la opción de conexión MultiSubnetFailover en la cadena de conexión, puede optimizar la conmutación por error del grupo de disponibilidad a otra subred si establece MultiSubnetFailover en "True" o "Yes", en función de la sintaxis del proveedor que use.  
  
> [!NOTE]  
>  Se recomienda esta configuración para las conexiones de una red y de varias subredes a los agentes de escucha del grupo de disponibilidad y a los nombres de instancia de clúster de conmutación por error de SQL Server.  La habilitación de esta opción agrega optimizaciones adicionales, incluso en escenarios de una sola subred.  
  
 La opción de conexión **MultiSubnetFailover** funciona únicamente con el protocolo de red TCP y solo se admite en la conexión a un agente de escucha del grupo de disponibilidad y para cualquier nombre de red virtual que se conecta a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 El siguiente es un ejemplo de cadena de conexión del proveedor ADO.NET (System.Data.SqlClient) que habilita la conmutación por error de varias subredes:  
  
```  
Server=tcp:AGListener,1433;Database=AdventureWorks;IntegratedSecurity=SSPI; MultiSubnetFailover=True  
```  
  
 La opción de conexión **MultiSubnetFailover** debe establecerse en **True** aunque el grupo de disponibilidad solo abarque una única subred.  Esto permite preconfigurar nuevos clientes que puedan abarca en el futuro subredes sin necesidad de los cambios en la cadena de conexión de cliente y también optimiza el rendimiento de conmutación por error para conmutaciones por error de las subredes.  Cuando la opción de conexión **MultiSubnetFailover** no es necesaria, proporciona la ventaja de una conmutación por error más rápida de la subred.  Esto se debe a que el controlador cliente intentará abrir un socket de TCP para cada dirección IP en paralelo asociada al grupo de disponibilidad.  El controlador cliente esperará que la primera dirección IP responda y, una vez que lo haga, la utilizará para la conexión.  
  
##  <a name="SSLcertificates"></a> Agentes de escucha del grupo de disponibilidad y certificados SSL  
 Al conectarse a un agente de escucha del grupo de disponibilidad, si las instancias participantes de SQL Server utilizan certificados SSL junto con cifrado de sesión, el controlador cliente de conexión deberá admitir el nombre alternativo del asunto del certificado SSL para forzar el cifrado.  La compatibilidad del controlador de SQL Server con el nombre alternativo del asunto del certificado está previsto para ADO.NET (SqlClient), Microsoft JDBC y SQL Native Client (SNAC).  
  
 Se debe configurar un certificado X.509 para cada nodo de servidor participante en el clúster de conmutación por error con una lista de todos los agentes de escucha del grupo de disponibilidad establecidos en el nombre alternativo del asunto del certificado.  
  
 Por ejemplo, si el WSFC tiene tres agentes de escucha del grupo de disponibilidad con los nombres `AG1_listener.Adventure-Works.com`, `AG2_listener.Adventure-Works.com`y `AG3_listener.Adventure-Works.com`, el nombre alternativo del asunto del certificado debe establecerse del modo siguiente:  
  
```  
CN = ServerFQDN  
SAN = ServerFQDN,AG1_listener.Adventure-Works.com, AG2_listener.Adventure-Works.com, AG3_listener.Adventure-Works.com  
```  
  
##  <a name="SPNs"></a> Agentes de escucha del grupo de disponibilidad y nombres principales de servidor (SPN)  
 Un nombre principal del servidor debe ser configurado en Active Directory por un administrador de dominio para cada nombre de agente de escucha del grupo de disponibilidad con el fin de habilitar Kerberos para la conexión de cliente con el agente de escucha del grupo de disponibilidad. Al registrar el SPN, debe usar la cuenta de servicio de la instancia del servidor que hospeda la réplica de disponibilidad.  Para que el SPN funcione en todas las réplicas, debe utilizarse la misma cuenta de servicio para todas las instancias del clúster de WSFC que hospeda el grupo de disponibilidad.  
  
 Utilice la herramienta de línea de comandos de Windows **setspn** para configurar el SPN.  Por ejemplo, para configurar un SPN para un grupo de disponibilidad denominado `AG1listener.Adventure-Works.com` hospedado en un conjunto de instancias de SQL Server configuradas para ejecutarse en la cuenta de dominio `corp/svclogin2`:  
  
```  
setspn -A MSSQLSvc/AG1listener.Adventure-Works.com:1433 corp/svclogin2  
```  
  
 Para obtener más información acerca del registro manual de un SPN para SQL Server, vea [Registrar un nombre de entidad de seguridad de servicio para las conexiones con Kerberos](../../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Conectividad de cliente de AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)  
  
-   [Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Ver las propiedades del agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)  
  
-   [Quitar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-listener-sql-server.md)  
  
-   [Configurar el acceso de solo lectura en una réplica de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Configurar el enrutamiento de solo lectura para un grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   [Guía de soluciones AlwaysOn de Microsoft SQL Server para lograr alta disponibilidad y recuperación ante desastres](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [Introducción al agente de escucha de grupo de disponibilidad](https://blogs.msdn.microsoft.com/sqlalwayson/2012/01/16/introduction-to-the-availability-group-listener/) (un blog del equipo de SQL Server AlwaysOn)  
  
-   [Blog del equipo Always On de SQL Server: el blog oficial del equipo de Always On de SQL Server](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
## <a name="see-also"></a>Consulte también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Conectividad de cliente de AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)   
 [Acerca del acceso de conexión de cliente a réplicas de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)   
 [Secundarias activas: réplicas secundarias legibles &#40;grupos de disponibilidad Always On&#41;](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Conectar clientes a una sesión de creación de reflejo de la base de datos &#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)  
  
  
