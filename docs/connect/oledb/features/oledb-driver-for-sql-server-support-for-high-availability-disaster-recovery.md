---
title: Controlador OLE DB para SQL Server Support for High Availability, Disaster Recovery | Documentos de Microsoft
description: Controlador de OLE DB para SQL Server admite alta disponibilidad y recuperación ante desastres
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: c915af2ec748c4b2c15882c9a643c8e200442e98
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="ole-db-driver-for-sql-server-support-for-high-availability-disaster-recovery"></a>Controlador OLE DB para SQL Server Support for High Availability, Disaster Recovery
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Este artículo describe el controlador OLE DB para SQL Server admiten (agregado en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]) para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Para más información sobre [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], vea [Agentes de escucha de grupo de disponibilidad, conectividad de cliente y conmutación por error de una aplicación &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md), [Creación y configuración de grupos de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md), [Clúster de conmutación por error y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md) y [Secundarias activas: réplicas secundarias legibles &#40;grupos de disponibilidad AlwaysOn&#41;](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
 Puede especificar el agente de escucha del grupo de disponibilidad de un determinado grupo de disponibilidad en la cadena de conexión. Si un controlador de OLE DB para la aplicación de SQL Server está conectado a una base de datos en un grupo de disponibilidad que conmuta por error, se pierde la conexión original y la aplicación debe abrir una conexión nueva para seguir trabajando después de la conmutación por error.  
  
 Si no se está conectando a un agente de escucha del grupo de disponibilidad, y si hay varias direcciones IP asociadas con un nombre de host, controlador de OLE DB para SQL Server iterará secuencialmente todas las direcciones IP asociadas a entrada DNS. Esto puede llevar mucho tiempo si la primera dirección IP que devuelve el servidor DNS no está enlazada a una tarjeta (NIC) de interfaz de red. Al conectarse a un agente de escucha del grupo de disponibilidad, el controlador OLE DB para SQL Server intenta establecer conexiones con todas las direcciones IP en paralelo y si un intento de conexión se realiza correctamente, el controlador descartará cualquier intento de conexión pendiente.  
  
> [!NOTE]  
> El aumento del tiempo de espera de la conexión y la implementación de la lógica de reintento de conexión aumentarán la probabilidad de que una aplicación se conecte a un grupo de disponibilidad. Además, dado que una conexión puede producir un error debido a la conmutación por error de un grupo de disponibilidad, es aconsejable implementar la lógica de reintento de conexión y hacer que una conexión que no se ha podido establecer se reintente hasta que vuelva a conectarse.  
  
## <a name="connecting-with-multisubnetfailover"></a>Conectarse a MultiSubnetFailover  
 Especifique siempre **MultiSubnetFailover = Yes** al conectarse a un agente de escucha de SQL Server grupo de disponibilidad AlwaysOn o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instancia de clúster de conmutación por error. **MultiSubnetFailover** permite más rápida conmutación por error para todos los grupos de disponibilidad AlwaysOn y las instancias de clúster de conmutación por error en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]y reducirá significativamente el tiempo de conmutación por error de múltiples subredes siempre en las topologías y. En un clúster de conmutación por error de varias subredes, el cliente intentará conexiones en paralelo. Durante una conmutación por error de subred, el controlador OLE DB para SQL Server volverá a intentar la conexión TCP.  
  
 El **MultiSubnetFailover** propiedad de conexión indica que la aplicación se implementa en un grupo de disponibilidad o una instancia de clúster de conmutación por error, y ese controlador OLE DB para SQL Server intentará conectarse a la base de datos en el principal [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] direcciones de la instancia intenta conectarse a todas las direcciones IP. Cuando se especifica **MultiSubnetFailover=Yes** para una conexión, el cliente reintenta la conexión TCP más deprisa que los intervalos de retransmisión TCP predeterminados del sistema operativo. Esto permite una reconexión más rápida después de la conmutación por error de un grupo de disponibilidad AlwaysOn o una instancia de clúster de conmutación por error y es aplicable a único y múltiples subredes grupos de disponibilidad y las instancias de clúster de conmutación por error.  
  
 Para obtener más información sobre las palabras clave de cadena de conexión, vea [Using Connection String Keywords con controlador OLE DB para SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md).  
  
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
  
Si actualiza un controlador OLE DB para la aplicación de SQL Server que usa actualmente creación de reflejo de base de datos a un escenario de múltiples subredes, debe quitar la **Failover_Partner** propiedad de conexión y reemplazarla con  **MultiSubnetFailover** establecido en **Sí** y reemplace el nombre del servidor en la cadena de conexión con un agente de escucha del grupo de disponibilidad. Si usa una cadena de conexión **Failover_Partner** y **MultiSubnetFailover=Yes**, el controlador generará un error. En cambio, si usa una cadena de conexión **Failover_Partner** y **MultiSubnetFailover=No** (o **ApplicationIntent=ReadWrite**), la aplicación usará la creación de reflejo de la base de datos.  
  
El controlador devuelve un error si la creación de reflejo de la base de datos se usa en la base de datos principal del grupo de disponibilidad y si **MultiSubnetFailover=Yes** se usa en la cadena de conexión que se conecta a una base de datos principal en lugar de a un agente de escucha de grupo de disponibilidad.  
  
## <a name="specifying-application-intent"></a>Especificar el intento de la aplicación  
Cuando **ApplicationIntent = ReadOnly**, el cliente solicita una carga de trabajo de lectura al conectarse a una base de datos siempre en habilitado. El servidor aplicará la intención en el momento de la conexión y durante un `USE` instrucción pero solo a una base de datos siempre habilitado en la base de datos.  
  
La palabra clave **ApplicationIntent** no funciona con bases de datos de solo lectura heredadas.  
  
Una base de datos puede permitir o denegar cargas de trabajo de lectura en la base de datos de inicio de siempre en destino. (Use la cláusula **ALLOW_CONNECTIONS** de las instrucciones **PRIMARY_ROLE** y **SECONDARY_ROLE**[!INCLUDE[tsql](../../../includes/tsql-md.md)]).  
  
La palabra clave **ApplicationIntent** se usa para habilitar el enrutamiento de solo lectura.  
  
## <a name="read-only-routing"></a>Enrutamiento de solo lectura  
El enrutamiento de solo lectura es una característica que puede asegurar la disponibilidad de una réplica de solo lectura de una base de datos. Para habilitar el enrutamiento de solo lectura:  
  
1.  Debe conectarse siempre a un agente de escucha de grupo de disponibilidad Always On.  
  
2.  La palabra clave de cadena de conexión de **ApplicationIntent** debe establecerse en **ReadOnly**.  
  
3.  El grupo de disponibilidad AlwaysOn debe configurarse por el Administrador de base de datos para habilitar el enrutamiento de solo lectura.  
  
Es posible que varias conexiones con enrutamiento de solo lectura no se conecten todas a la misma réplica de solo lectura. Los cambios en la sincronización de la base de datos o los cambios en la configuración de enrutamiento del servidor pueden producir conexiones de cliente para réplicas de solo lectura diferentes. Para asegurarse de que todas las solicitudes de solo lectura se conectan a la misma réplica de solo lectura, no pase un agente de escucha de grupo de disponibilidad AlwaysOn para la **Server** palabra clave de cadena de conexión. En su lugar, especifique el nombre de la instancia de solo lectura.  
  
El enrutamiento de solo lectura puede tardar más tiempo que la conexión a la réplica principal, ya que primero se conecta a la réplica principal y después busca la mejor réplica secundaria legible disponible. Por ello, debe aumentar el tiempo de espera de inicio de sesión.  
  
## <a name="ole-db"></a>OLE DB  
El controlador OLE DB para SQL Server admite tanto la **ApplicationIntent** y **MultiSubnetFailover** palabras clave.   
  
Las dos palabras clave de cadena de conexión de OLE DB se agregaron para admitir [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en el controlador OLE DB para SQL Server:  
  
-   **ApplicationIntent** 
-   **MultiSubnetFailover**  
  
 Para obtener más información sobre las palabras clave de cadena de conexión en el controlador de OLE DB para SQL Server, vea [Using Connection String Keywords con controlador OLE DB para SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md).  

### <a name="application-intent"></a>Intención de aplicaciones 

Las propiedades de conexión equivalentes son:  
  
-   **SSPROP_INIT_APPLICATIONINTENT**  
  
-   **DBPROP_INIT_PROVIDERSTRING**  
  
Un controlador de OLE DB para la aplicación de SQL Server puede utilizar uno de los métodos para especificar la intención de aplicación:  
  
 -   **IDBInitialize:: Initialize**  
 **IDBInitialize::Initialize** usa el conjunto de propiedades previamente configurado para inicializar el origen de datos y crear el objeto de origen de datos. Especifique la intención de aplicaciones como una propiedad del proveedor o como parte de la cadena de propiedades extendidas.  
  
 -   **IDataInitialize:: GetDatasource**  
 **IDataInitialize::GetDataSource** toma una cadena de conexión de entrada que puede contener la palabra clave **Application Intent**.  
  
 -   **IDBProperties::SetProperties**  
 Para establecer el valor de la propiedad **ApplicationIntent**, llame a **IDBProperties::SetProperties** pasando la propiedad **SSPROP_INIT_APPLICATIONINTENT** con valor "**ReadWrite**" o "**ReadOnly**" o la propiedad **DBPROP_INIT_PROVIDERSTRING** con el valor que contiene "**ApplicationIntent=ReadOnly**" o "**ApplicationIntent=ReadWrite**".  
  
Puede especificar la intención de aplicaciones en el campo Propiedades de intención de aplicaciones de la pestaña Todo del cuadro de diálogo **Propiedades de vínculo de datos**.  
  
Cuando se establezcan conexiones implícitas, estas usarán la configuración de la intención de aplicaciones de la conexión primaria. De forma similar, cuando se creen varias sesiones con el mismo origen de datos estas heredarán la configuración de la intención de aplicaciones del origen de datos.  
  
### <a name="multisubnetfailover"></a>MultiSubnetFailover

Las propiedades de conexión equivalentes son:  
  
-   **SSPROP_INIT_MULTISUBNETFAILOVER**  
  
-   **DBPROP_INIT_PROVIDERSTRING**  

Un controlador de OLE DB para la aplicación de SQL Server puede utilizar uno de los métodos siguientes para establecer la opción MultiSubnetFailover:  

 -   **IDBInitialize:: Initialize**  
 **IDBInitialize::Initialize** usa el conjunto de propiedades previamente configurado para inicializar el origen de datos y crear el objeto de origen de datos. Especifique la intención de aplicaciones como una propiedad del proveedor o como parte de la cadena de propiedades extendidas.  
  
 -   **IDataInitialize:: GetDatasource**  
 **IDataInitialize:: GetDatasource** toma una cadena de conexión de entrada que puede contener el **MultiSubnetFailover** palabra clave.  

-   **IDBProperties::SetProperties**  
Para establecer el **MultiSubnetFailover** valor de propiedad, llamada **IDBProperties:: SetProperties** pasando el **SSPROP_INIT_MULTISUBNETFAILOVER** propiedad con el valor  **VARIANT_TRUE** o **VARIANT_FALSE** o **DBPROP_INIT_PROVIDERSTRING** propiedad con el valor "**MultiSubnetFailover = Yes** "o"**MultiSubnetFailover = No**".

#### <a name="example"></a>Ejemplo

```
DBPROP rgPropMultisubnet;

rgPropMultisubnet.dwPropertyID = SSPROP_INIT_MULTISUBNETFAILOVER;
rgPropMultisubnet.dwOptions = DBPROPOPTIONS_REQUIRED;
rgPropMultisubnet.dwStatus = DBPROPSTATUS_OK;
rgPropMultisubnet.colid = DB_NULLID;
V_VT(&(rgPropMultisubnet.vValue)) = VT_BOOL;
V_BOOL(&(rgPropMultisubnet.vValue)) = VARIANT_TRUE;

DBPROPSET PropSet;

PropSet.rgProperties = &rgPropMultisubnet;
PropSet.cProperties = 1;
PropSet.guidPropertySet = DBPROPSET_SQLSERVERDBINIT;
IDBProperties* pIDBProperties = NULL;
hr = pIDBInitialize->QueryInterface(IID_IDBProperties, (void **)&pIDBProperties);
pIDBProperties->SetProperties(1, &PropSet);
```

## <a name="see-also"></a>Vea también  
 [Controlador OLE DB para características de SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [Uso de palabras clave de cadena de conexión con el controlador OLE DB para SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)  
  
  
