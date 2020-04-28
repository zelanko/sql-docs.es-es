---
title: Alta disponibilidad, recuperación
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 2b06186b-4090-4728-b96b-90d6ebd9f66f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f940302db497dd02b3fc5ef89056aef29a6b64a7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81388431"
---
# <a name="sql-server-native-client-support-for-high-availability-disaster-recovery"></a>Compatibilidad de SQL Server Native Client para la alta disponibilidad con recuperación de desastres
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  En este tema se explica la compatibilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (incorporada en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]) con [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Para más información sobre [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], vea [Agentes de escucha de grupo de disponibilidad, conectividad de cliente y conmutación por error de una aplicación &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md), [Creación y configuración de grupos de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md), [Clúster de conmutación por error y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md) y [Secundarias activas: réplicas secundarias legibles &#40;grupos de disponibilidad AlwaysOn&#41;](~/database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
 Puede especificar el agente de escucha del grupo de disponibilidad de un determinado grupo de disponibilidad en la cadena de conexión. Si una aplicación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client se conecta a una base de datos de un grupo de disponibilidad que conmuta por error, la conexión original se interrumpe y la aplicación debe abrir una nueva conexión para continuar el trabajo después de la conmutación por error.  
  
 Si no va a conectarse a un agente de escucha del grupo de disponibilidad y si varias direcciones IP están asociados con un nombre de host, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client iterará secuencialmente a través de todas las direcciones IP asociadas a la entrada DNS. Esto puede llevar mucho tiempo si la primera dirección IP que devuelve el servidor DNS no está enlazada a una tarjeta (NIC) de interfaz de red. Al conectarse a un agente de escucha de un grupo de disponibilidad, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client intenta establecer conexiones a todas las direcciones IP en paralelo y, si algún intento de conexión tiene éxito, el controlador descartará los intentos de conexión pendientes.  
  
> [!NOTE]  
>  El aumento del tiempo de espera de la conexión y la implementación de la lógica de reintento de conexión aumentarán la probabilidad de que una aplicación se conecte a un grupo de disponibilidad. Además, dado que una conexión puede producir un error debido a la conmutación por error de un grupo de disponibilidad, es aconsejable implementar la lógica de reintento de conexión y hacer que una conexión que no se ha podido establecer se reintente hasta que vuelva a conectarse.  
  
## <a name="connecting-with-multisubnetfailover"></a>Conectarse a MultiSubnetFailover  
 Especifique siempre **MultiSubnetFailover=Yes** al conectarse a un agente de escucha de grupo de disponibilidad de SQL Server 2012 o a una instancia de clúster de conmutación por error de SQL Server 2012. **MultiSubnetFailover** permite una conmutación por error más rápida para todos los grupos de disponibilidad y la instancia de clúster de conmutación por error en SQL Server 2012 y reducirá significativamente el tiempo de conmutación por error para topologías de Always on de una y varias subredes. En un clúster de conmutación por error de varias subredes, el cliente intentará conexiones en paralelo. Durante una conmutación por error de subred, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client seguirá reintentando la conexión TCP.  
  
 La propiedad de conexión **MultiSubnetFailover** indica que la aplicación se implementa en un grupo de disponibilidad o una instancia de clúster de conmutación por error, y que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client intentará conectarse a la base de datos en la instancia principal de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] intentando conectarse a todas las direcciones IP. Cuando se especifica **MultiSubnetFailover=Yes** para una conexión, el cliente reintenta la conexión TCP más deprisa que los intervalos de retransmisión TCP predeterminados del sistema operativo. Esto permite una reconexión más rápida después de la conmutación por error de un grupo de disponibilidad de Always On o una instancia de clúster de conmutación por error Always On, y es aplicable a las instancias de clúster de conmutación por error y grupos de disponibilidad de una y varias subredes.  
  
 Para más información sobre las palabras clave de cadena de conexión, vea [Usar palabras clave de cadena de conexión con SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Si se especifica **MultiSubnetFailover=Yes** al conectarse a algo que no sea un agente de escucha de grupo de disponibilidad o una instancia de clúster de conmutación por error, el rendimiento puede verse afectado negativamente y, por ello, no se admite.  
  
 Utilice las siguientes instrucciones para conectarse a un servidor en un grupo de disponibilidad o una instancia de clúster de conmutación por error:  
  
-   Use la propiedad de conexión **MultiSubnetFailover** cuando se conecte a una única subred o a varias subredes. mejorará el rendimiento de ambos.  
  
-   Para conectarse a un grupo de disponibilidad, especifique el agente de escucha del grupo de disponibilidad como el servidor en la cadena de conexión.  
  
-   La conexión a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] configurada con más de 64 direcciones IP producirá un error en la conexión.  
  
-   El comportamiento de una aplicación que usa la propiedad de conexión **MultiSubnetFailover** no se ve afectado en función del tipo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de autenticación: autenticación de, autenticación Kerberos o autenticación de Windows.  
  
-   Puede aumentar el valor de **loginTimeout** para tener en cuenta el tiempo de conmutación por error y reducir los reintentos de conexión de la aplicación.  
  
-   No se admiten las transacciones distribuidas.  
  
 Si no está activado el enrutamiento de solo lectura, no se podrá conectar a una ubicación de réplica secundaria en un grupo de disponibilidad en las siguientes situaciones:  
  
1.  Si la ubicación de réplica secundaria no está configurada para aceptar conexiones.  
  
2.  Si una aplicación utiliza **ApplicationIntent = ReadWrite** (se describe a continuación) y la ubicación de la réplica secundaria está configurada para acceso de solo lectura.  
  
 Una conexión producirá un error si una réplica principal está configurada para rechazar cargas de trabajo de solo lectura y la cadena de conexión contiene **ApplicationIntent=ReadOnly**.  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>Actualizar para utilizar clústeres de varias subredes a partir de la creación de reflejo de la base de datos  
 Se producirá un error de conexión si las palabras clave de conexión **MultiSubnetFailover** y **Failover_Partner** se encuentran en la cadena de conexión. También se producirá un error si se usa **MultiSubnetFailover** y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devuelve una respuesta del asociado de conmutación por error que indica que forma parte de un par de creación de reflejo de la base de datos.  
  
 Si actualiza una aplicación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que use actualmente la creación de reflejo de la base de datos en un escenario de varias subredes, debe quitar la propiedad de conexión **Failover_Partner** y reemplazarla con **MultiSubnetFailover** establecida en **Yes** y reemplazar el nombre del servidor en la cadena de conexión con un agente de escucha de grupo de disponibilidad. Si usa una cadena de conexión **Failover_Partner** y **MultiSubnetFailover=Yes**, el controlador generará un error. En cambio, si usa una cadena de conexión **Failover_Partner** y **MultiSubnetFailover=No** (o **ApplicationIntent=ReadWrite**), la aplicación usará la creación de reflejo de la base de datos.  
  
 El controlador devuelve un error si la creación de reflejo de la base de datos se usa en la base de datos principal del grupo de disponibilidad y si **MultiSubnetFailover=Yes** se usa en la cadena de conexión que se conecta a una base de datos principal en lugar de a un agente de escucha de grupo de disponibilidad.  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="odbc"></a>ODBC  
 Se han agregado dos palabras clave de cadena de conexión ODBC para ser compatible con [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client:  
  
-   **ApplicationIntent**  
  
-   **MultiSubnetFailover**  
  
 Para más información sobre las palabras clave de cadena de conexión ODBC en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, vea [Usar palabras clave de cadena de conexión con SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Las propiedades de conexión equivalentes son:  
  
-   **SQL_COPT_SS_APPLICATION_INTENT**  
  
-   **SQL_COPT_SS_MULTISUBNET_FAILOVER**  
  
 Para más información sobre las propiedades de conexión ODBC en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, vea [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md).  
  
 La funcionalidad de las palabras clave **ApplicationIntent** y **MultiSubnetFailover** se expondrá en el Administrador de orígenes de datos ODBC para los DSN que usan el controlador de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client a partir de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 Una aplicación ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client puede utilizar una de estas tres funciones para realizar la conexión:  
  
|Función|Descripción|  
|--------------|-----------------|  
|[SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)|La lista de servidores devuelta por **SQLBrowseConnect** no incluirá los VNN. Solo verá una lista de servidores que no indica si el servidor es un servidor independiente, o un servidor principal o secundario de un clúster de clústeres de conmutación por error de Windows Server (WSFC) que contiene dos o más instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] habilitadas para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Si se conecta a un servidor y obtiene un error, puede deberse a que se ha conectado a un servidor y el valor de **ApplicationIntent** no es compatible con la configuración del servidor.<br /><br /> Dado que **SQLBrowseConnect** no reconoce los servidores de un clúster de clústeres de conmutación por error de Windows Server (WSFC) que contiene dos o más instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] habilitadas para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], **SQLBrowseConnect** omite la palabra clave de cadena de conexión **MultiSubnetFailover**.|  
|[SQLConnect](../../../relational-databases/native-client-odbc-api/sqlconnect.md)|**SQLConnect** admite **ApplicationIntent** y **MultiSubnetFailover** mediante un nombre de origen de datos (DSN) o propiedades de conexión.|  
|[SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)|**SQLDriverConnect** admite **ApplicationIntent** y **MultiSubnetFailover** mediante palabras clave de cadena de conexión, propiedades de conexión o DSN.|  
  
## <a name="ole-db"></a>OLE DB  
 OLE DB en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no admite la palabra clave **MultiSubnetFailover**.  
  
 OLE DB en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admitirá la intención de aplicaciones. La intención de aplicaciones se comportará igual para las aplicaciones OLE DB que para las aplicaciones ODBC (vea el párrafo anterior).  
  
 Se ha agregado una palabra clave de cadena de conexión OLE DB para admitir [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client:  
  
-   **Application Intent**  
  
 Para más información sobre las palabras clave de cadena de conexión en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, vea [Usar palabras clave de cadena de conexión con SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Las propiedades de conexión equivalentes son:  
  
-   **SSPROP_INIT_APPLICATIONINTENT**  
  
-   **DBPROP_INIT_PROVIDERSTRING**  
  
 Una aplicación OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client puede utilizar uno de los métodos siguientes para especificar la intención de aplicaciones:  
  
 **IDBInitialize::Initialize**  
 **IDBInitialize::Initialize** usa el conjunto de propiedades previamente configurado para inicializar el origen de datos y crear el objeto de origen de datos. Especifique la intención de aplicaciones como una propiedad del proveedor o como parte de la cadena de propiedades extendidas.  
  
 **IDataInitialize::GetDataSource**  
 **IDataInitialize::GetDataSource** toma una cadena de conexión de entrada que puede contener la palabra clave **Application Intent**.  
  
 **IDBProperties::GetProperties**  
 **IDBProperties::GetProperties** recupera el valor de la propiedad que está establecida actualmente en el origen de datos.  Puede recuperar el valor de **Application Intent** a través de la propiedad DBPROP_INIT_PROVIDERSTRING y la propiedad SSPROP_INIT_APPLICATIONINTENT.  
  
 **IDBProperties::SetProperties**  
 Para establecer el valor de la propiedad **ApplicationIntent**, llame a **IDBProperties::SetProperties** pasando la propiedad **SSPROP_INIT_APPLICATIONINTENT** con valor "**ReadWrite**" o "**ReadOnly**" o la propiedad **DBPROP_INIT_PROVIDERSTRING** con el valor que contiene "**ApplicationIntent=ReadOnly**" o "**ApplicationIntent=ReadWrite**".  
  
 Puede especificar la intención de aplicaciones en el campo Propiedades de intención de aplicaciones de la pestaña Todo del cuadro de diálogo **Propiedades de vínculo de datos**.  
  
 Cuando se establezcan conexiones implícitas, estas usarán la configuración de la intención de aplicaciones de la conexión primaria. De forma similar, cuando se creen varias sesiones con el mismo origen de datos estas heredarán la configuración de la intención de aplicaciones del origen de datos.  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Native Client características](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Usar palabras clave de cadena de conexión con SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
  
