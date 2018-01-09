---
title: SQL Server Native Client Support for High Availability, Disaster Recovery | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|features
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 2b06186b-4090-4728-b96b-90d6ebd9f66f
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1940375cc3d822d994c673d965e1fb7e23385596
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="sql-server-native-client-support-for-high-availability-disaster-recovery"></a>Compatibilidad de SQL Server Native Client para la alta disponibilidad con recuperación de desastres
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  En este tema se explica la compatibilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (incorporada en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]) con [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Para más información sobre [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], vea [Agentes de escucha de grupo de disponibilidad, conectividad de cliente y conmutación por error de una aplicación &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md), [Creación y configuración de grupos de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md), [Clúster de conmutación por error y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md) y [Secundarias activas: réplicas secundarias legibles &#40;grupos de disponibilidad AlwaysOn&#41;](~/database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
 Puede especificar el agente de escucha del grupo de disponibilidad de un determinado grupo de disponibilidad en la cadena de conexión. Si una aplicación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client se conecta a una base de datos de un grupo de disponibilidad que conmuta por error, la conexión original se interrumpe y la aplicación debe abrir una nueva conexión para continuar el trabajo después de la conmutación por error.  
  
 Si no va a conectarse a un agente de escucha del grupo de disponibilidad y si varias direcciones IP están asociados con un nombre de host, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client iterará secuencialmente a través de todas las direcciones IP asociadas a la entrada DNS. Esto puede llevar mucho tiempo si la primera dirección IP que devuelve el servidor DNS no está enlazada a una tarjeta (NIC) de interfaz de red. Al conectarse a un agente de escucha de un grupo de disponibilidad, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client intenta establecer conexiones a todas las direcciones IP en paralelo y, si algún intento de conexión tiene éxito, el controlador descartará los intentos de conexión pendientes.  
  
> [!NOTE]  
>  El aumento del tiempo de espera de la conexión y la implementación de la lógica de reintento de conexión aumentarán la probabilidad de que una aplicación se conecte a un grupo de disponibilidad. Además, dado que una conexión puede producir un error debido a la conmutación por error de un grupo de disponibilidad, es aconsejable implementar la lógica de reintento de conexión y hacer que una conexión que no se ha podido establecer se reintente hasta que vuelva a conectarse.  
  
## <a name="connecting-with-multisubnetfailover"></a>Conectarse a MultiSubnetFailover  
 Especifique siempre **MultiSubnetFailover=Yes** al conectarse a un agente de escucha de grupo de disponibilidad de SQL Server 2012 o a una instancia de clúster de conmutación por error de SQL Server 2012. **MultiSubnetFailover** permite más rápida conmutación por error para todos los grupos de disponibilidad y clústeres de conmutación por error de la instancia de SQL Server 2012 y reducen significativamente el tiempo de conmutación por error de múltiples subredes siempre en las topologías y. En un clúster de conmutación por error de varias subredes, el cliente intentará conexiones en paralelo. Durante una conmutación por error de subred, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client seguirá reintentando la conexión TCP.  
  
 La propiedad de conexión **MultiSubnetFailover** indica que la aplicación se implementa en un grupo de disponibilidad o una instancia de clúster de conmutación por error, y que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client intentará conectarse a la base de datos en la instancia principal de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] intentando conectarse a todas las direcciones IP. Cuando se especifica **MultiSubnetFailover=Yes** para una conexión, el cliente reintenta la conexión TCP más deprisa que los intervalos de retransmisión TCP predeterminados del sistema operativo. Esto permite una reconexión más rápida después de la conmutación por error de un grupo de disponibilidad AlwaysOn o un siempre en Failover Cluster Instance y es aplicable a único y múltiples subredes grupos de disponibilidad y las instancias de clúster de conmutación por error.  
  
 Para más información sobre las palabras clave de cadena de conexión, vea [Usar palabras clave de cadena de conexión con SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Si se especifica **MultiSubnetFailover=Yes** al conectarse a algo que no sea un agente de escucha de grupo de disponibilidad o una instancia de clúster de conmutación por error, el rendimiento puede verse afectado negativamente y, por ello, no se admite.  
  
 Utilice las siguientes instrucciones para conectarse a un servidor en un grupo de disponibilidad o una instancia de clúster de conmutación por error:  
  
-   Use la propiedad de conexión **MultiSubnetFailover** cuando se conecte a una única subred o a varias subredes, ya que mejorará el rendimiento en ambos casos.  
  
-   Para conectarse a un grupo de disponibilidad, especifique el agente de escucha del grupo de disponibilidad como el servidor en la cadena de conexión.  
  
-   La conexión a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] configurada con más de 64 direcciones IP producirá un error en la conexión.  
  
-   El comportamiento de una aplicación que usa la propiedad de conexión **MultiSubnetFailover** no se ve afectado por el tipo de autenticación: autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], autenticación Kerberos o autenticación de Windows.  
  
-   Puede aumentar el valor de **loginTimeout** para tener en cuenta el tiempo de conmutación por error y reducir los reintentos de conexión de la aplicación.  
  
-   No se admiten las transacciones distribuidas.  
  
 Si no está activado el enrutamiento de solo lectura, no se podrá conectar a una ubicación de réplica secundaria en un grupo de disponibilidad en las siguientes situaciones:  
  
1.  Si la ubicación de réplica secundaria no está configurada para aceptar conexiones.  
  
2.  Si una aplicación usa **ApplicationIntent=ReadWrite** (se describe a continuación) y la ubicación de réplica secundaria está configurada para acceso de solo lectura.  
  
 Una conexión producirá un error si una réplica principal está configurada para rechazar cargas de trabajo de solo lectura y la cadena de conexión contiene **ApplicationIntent=ReadOnly**.  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>Actualizar para utilizar clústeres de varias subredes a partir de la creación de reflejo de la base de datos  
 Se producirá un error de conexión si las palabras clave de conexión **MultiSubnetFailover** y **Failover_Partner** se encuentran en la cadena de conexión. También se producirá un error si se usa **MultiSubnetFailover** y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devuelve una respuesta del asociado de conmutación por error que indica que forma parte de un par de creación de reflejo de la base de datos.  
  
 Si actualiza una aplicación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que use actualmente la creación de reflejo de la base de datos en un escenario de varias subredes, debe quitar la propiedad de conexión **Failover_Partner** y reemplazarla con **MultiSubnetFailover** establecida en **Yes** y reemplazar el nombre del servidor en la cadena de conexión con un agente de escucha de grupo de disponibilidad. Si usa una cadena de conexión **Failover_Partner** y **MultiSubnetFailover=Yes**, el controlador generará un error. En cambio, si usa una cadena de conexión **Failover_Partner** y **MultiSubnetFailover=No** (o **ApplicationIntent=ReadWrite**), la aplicación usará la creación de reflejo de la base de datos.  
  
 El controlador devuelve un error si la creación de reflejo de la base de datos se usa en la base de datos principal del grupo de disponibilidad y si **MultiSubnetFailover=Yes** se usa en la cadena de conexión que se conecta a una base de datos principal en lugar de a un agente de escucha de grupo de disponibilidad.  
  
## <a name="specifying-application-intent"></a>Especificar el intento de la aplicación  
 Cuando **ApplicationIntent = ReadOnly**, el cliente solicita una carga de trabajo de lectura al conectarse a una base de datos siempre en habilitado. El servidor aplicará el intento en el momento de la conexión y durante una instrucción de base de datos USE pero solo en una base de datos con habilitada para AlwaysOn.  
  
 La palabra clave **ApplicationIntent** no funciona con bases de datos de solo lectura heredadas.  
  
 Una base de datos puede permitir o denegar cargas de trabajo de lectura en la base de datos de inicio de siempre en destino. (Use la cláusula **ALLOW_CONNECTIONS** de las instrucciones **PRIMARY_ROLE** y **SECONDARY_ROLE**[!INCLUDE[tsql](../../../includes/tsql-md.md)]).  
  
 La palabra clave **ApplicationIntent** se usa para habilitar el enrutamiento de solo lectura.  
  
## <a name="read-only-routing"></a>Enrutamiento de solo lectura  
 El enrutamiento de solo lectura es una característica que puede garantizar la disponibilidad de una réplica de solo lectura de una base de datos. Para habilitar el enrutamiento de solo lectura:  
  
1.  Debe conectarse siempre a un agente de escucha de grupo de disponibilidad Always On.  
  
2.  La palabra clave de cadena de conexión de **ApplicationIntent** debe establecerse en **ReadOnly**.  
  
3.  El administrador de bases de datos debe configurar el grupo de disponibilidad para habilitar el enrutamiento de solo lectura.  
  
 Es posible que varias conexiones con enrutamiento de solo lectura no se conecten todas a la misma réplica de solo lectura. Los cambios en la sincronización de la base de datos o los cambios en la configuración de enrutamiento del servidor pueden producir conexiones de cliente para réplicas de solo lectura diferentes. Para asegurarse de que todas las solicitudes de solo lectura se conectan a la misma réplica de solo lectura, no pase un agente de escucha de grupo de disponibilidad a la palabra clave de cadena de conexión **Server**. En su lugar, especifique el nombre de la instancia de solo lectura.  
  
 El enrutamiento de solo lectura puede tardar más en conectarse al servidor principal porque el enrutamiento de solo lectura se conecta primero al servidor principal y luego busca el mejor secundario legible disponible. Por ello, debe aumentar el tiempo de espera de inicio de sesión.  
  
## <a name="odbc"></a>ODBC  
 Se han agregado dos palabras clave de cadena de conexión ODBC para ser compatible con [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client:  
  
-   **Intención de aplicaciones**  
  
-   **MultiSubnetFailover**  
  
 Para más información sobre las palabras clave de cadena de conexión ODBC en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, vea [Usar palabras clave de cadena de conexión con SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Las propiedades de conexión equivalentes son:  
  
-   **SQL_COPT_SS_APPLICATION_INTENT**  
  
-   **SQL_COPT_SS_MULTISUBNET_FAILOVER**  
  
 Para más información sobre las propiedades de conexión ODBC en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, vea [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md).  
  
 La funcionalidad de las palabras clave **ApplicationIntent** y **MultiSubnetFailover** se expondrá en el Administrador de orígenes de datos ODBC para los DSN que usan el controlador de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client a partir de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 Una aplicación ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client puede utilizar una de estas tres funciones para realizar la conexión:  
  
|Función|Description|  
|--------------|-----------------|  
|[SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)|La lista de servidores devuelta por **SQLBrowseConnect** no incluirá los VNN. Solo verá una lista de servidores que no indica si el servidor es un servidor independiente, o un servidor principal o secundario de un clúster de clústeres de conmutación por error de Windows Server (WSFC) que contiene dos o más instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] habilitadas para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Si se conecta a un servidor y obtiene un error, puede deberse a que se ha conectado a un servidor y el valor de **ApplicationIntent** no es compatible con la configuración del servidor.<br /><br /> Dado que **SQLBrowseConnect** no reconoce los servidores de un clúster de clústeres de conmutación por error de Windows Server (WSFC) que contiene dos o más instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] habilitadas para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], **SQLBrowseConnect** omite la palabra clave de cadena de conexión **MultiSubnetFailover**.|  
|[SQLConnect](../../../relational-databases/native-client-odbc-api/sqlconnect.md)|**SQLConnect** admite **ApplicationIntent** y **MultiSubnetFailover** mediante un nombre de origen de datos (DSN) o propiedades de conexión.|  
|[SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)|**SQLDriverConnect** admite **ApplicationIntent** y **MultiSubnetFailover** mediante palabras clave de cadena de conexión, propiedades de conexión o DSN.|  
  
## <a name="ole-db"></a>OLE DB  
 OLE DB en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no admite la palabra clave **MultiSubnetFailover**.  
  
 OLE DB en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admitirá la intención de aplicaciones. La intención de aplicaciones se comportará igual para las aplicaciones OLE DB que para las aplicaciones ODBC (vea el párrafo anterior).  
  
 Se ha agregado una palabra clave de cadena de conexión OLE DB para admitir [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client:  
  
-   **Intento de aplicación**  
  
 Para más información sobre las palabras clave de cadena de conexión en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, vea [Usar palabras clave de cadena de conexión con SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Las propiedades de conexión equivalentes son:  
  
-   **SSPROP_INIT_APPLICATIONINTENT**  
  
-   **DBPROP_INIT_PROVIDERSTRING**  
  
 Una aplicación OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client puede utilizar uno de los métodos siguientes para especificar la intención de aplicaciones:  
  
 **IDBInitialize:: Initialize**  
 **IDBInitialize::Initialize** usa el conjunto de propiedades previamente configurado para inicializar el origen de datos y crear el objeto de origen de datos. Especifique la intención de aplicaciones como una propiedad del proveedor o como parte de la cadena de propiedades extendidas.  
  
 **IDataInitialize:: GetDatasource**  
 **IDataInitialize::GetDataSource** toma una cadena de conexión de entrada que puede contener la palabra clave **Application Intent**.  
  
 **IDBProperties::GetProperties**  
 **IDBProperties::GetProperties** recupera el valor de la propiedad que está establecida actualmente en el origen de datos.  Puede recuperar el valor de **Application Intent** a través de la propiedad DBPROP_INIT_PROVIDERSTRING y la propiedad SSPROP_INIT_APPLICATIONINTENT.  
  
 **IDBProperties:: SetProperties**  
 Para establecer el valor de la propiedad **ApplicationIntent**, llame a **IDBProperties::SetProperties** pasando la propiedad **SSPROP_INIT_APPLICATIONINTENT** con valor "**ReadWrite**" o "**ReadOnly**" o la propiedad **DBPROP_INIT_PROVIDERSTRING** con el valor que contiene "**ApplicationIntent=ReadOnly**" o "**ApplicationIntent=ReadWrite**".  
  
 Puede especificar la intención de aplicaciones en el campo Propiedades de intención de aplicaciones de la pestaña Todo del cuadro de diálogo **Propiedades de vínculo de datos**.  
  
 Cuando se establezcan conexiones implícitas, estas usarán la configuración de la intención de aplicaciones de la conexión primaria. De forma similar, cuando se creen varias sesiones con el mismo origen de datos estas heredarán la configuración de la intención de aplicaciones del origen de datos.  
  
## <a name="see-also"></a>Vea también  
 [Características de SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Usar palabras clave de cadena de conexión con SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
  
