---
title: Mediante la creación de reflejo de base de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client|features
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- SQL Server Native Client, database mirroring
- data access [SQL Server Native Client], database mirroring
- database mirroring [SQL Server], connecting clients to
- SQLNCLI, database mirroring
- SQL Server Native Client ODBC driver, database mirroring
- SQL Server Native Client OLE DB provider, database mirroring
ms.assetid: 71b15712-7972-4465-9274-e0ddc271eedc
caps.latest.revision: 55
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5b7bdad805cf9ebcfead0df42cd847db741f41ce
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="using-database-mirroring"></a>Usar la creación de reflejo de bases de datos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]Use [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en su lugar.  
  
 La creación de reflejo de la base de datos, introducida en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], es una solución de software para aumentar la disponibilidad de la base de datos y la redundancia de datos. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client proporciona compatibilidad implícita con creación de reflejo de base de datos, por lo que el desarrollador no necesita escribir ningún código ni realizar ninguna otra acción una vez que se ha configurado para la base de datos.  
  
 La creación de reflejo, que se implementa en una base de cada base de datos, conserva una copia de un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] base de datos de producción en un servidor en espera. Este servidor puede ser un servidor en estado de espera activa o semiactiva, dependiendo de la configuración y del estado de la sesión de creación de reflejo de la base de datos. Un servidor en estado de espera activa admite la conmutación por error rápida sin pérdida de las transacciones confirmadas, mientras que un servidor en estado de espera semiactiva admite la acción de forzar el servicio (con posible pérdida de datos).  
  
 La base de datos de producción se llama el *base de datos principal*, y se llama a la copia en espera la *base de datos reflejada*. La base de datos principal y la base de datos reflejada deben residir en instancias independientes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (instancias de servidor), y debe residir en equipos distintos si es posible.  
  
 La instancia de servidor de producción, llamada a la *servidor principal*, se comunica con la instancia de servidor en espera, llamada a la *servidor reflejado*. Los servidores principal y reflejado actúan como asociados en una creación de reflejo de base de datos *sesión*. Si se produce un error en el servidor principal, el servidor reflejado puede convertir su base de datos en la base de datos principal mediante un proceso denominado *conmutación por error*. Por ejemplo, Partner_A y Partner_B son dos servidores asociados, con la base de datos principal inicialmente en Partner_A como servidor principal y la base de datos reflejada en Partner_B como servidor reflejado. Si Partner_A se queda sin conexión, la base de datos de Partner_B puede realizar la conmutación por error para convertirse en la base de datos principal actual. Cuando Partner_A se vuelve a unir a la sesión de creación de reflejo, se convierte en el servidor reflejado y su base de datos pasa a ser la base de datos reflejada.  
  
 Las configuraciones alternativas de creación de reflejo de la base de datos proporcionan diferentes niveles de rendimiento y de seguridad de los datos, y admiten varias formas de conmutación por error. Para obtener más información, vea [Creación de reflejo de la base de datos &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
 Se puede utilizar un alias al especificar el nombre de la base de datos reflejada.  
  
> [!NOTE]  
>  Para obtener información acerca de los intentos de conexión inicial y los intentos de reconexión a una base de datos reflejada, vea [conectar clientes a una sesión de creación de reflejo de base de datos &#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md).  
  
## <a name="programming-considerations"></a>Consideraciones de programación  
 Cuando el servidor principal genera un error, la aplicación cliente recibe mensajes de error como respuesta a las llamadas a la API que indican que se ha perdido la conexión a la base de datos. Cuando esto sucede, se pierde cualquier cambio no confirmado en la base de datos y se revierte la transacción actual. Si esto se produce, la aplicación debe cerrar la conexión (o liberar el objeto de origen de datos) y volverla a abrir. La conexión se redirige de forma transparente a la base de datos reflejada, que ahora actúa como servidor principal.  
  
 Cuando se establece una conexión, el servidor principal envía la identidad de su asociado de conmutación por error al cliente que se va a utilizar cuando se produzca la conmutación por error. Si una aplicación intenta establecer una conexión después de producirse un error en el servidor principal, el cliente no conocerá la identidad del asociado de conmutación por error. Para que los clientes tengan la oportunidad de solucionar esta situación, una propiedad de inicialización y una palabra clave de cadena de conexión asociada permiten al cliente especificar por sí solo la identidad del asociado de conmutación por error. El atributo de cliente solamente se utiliza en esta situación; si el servidor principal está disponible, no se utiliza. Si el servidor asociado de conmutación por error proporcionado por el cliente no corresponde a un servidor que actúa como asociado de conmutación por error, el servidor rechaza la conexión. Para que las aplicaciones puedan adaptarse a los cambios de configuración, se puede determinar la identidad del asociado de conmutación por error real inspeccionando el atributo una vez establecida la conexión. Conviene almacenar en la memoria caché la información del asociado para actualizar la cadena de conexión o concebir una estrategia de reintento en caso de que no se consiga establecer una conexión en el primer intento.   
  
> [!NOTE]  
>  Debe especificar explícitamente la base de datos que va a ser utilizada por una conexión si desea usar esta característica en un nombre del origen de datos (DSN), una cadena de conexión, o un atributo o propiedad de conexión. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no intentará realizar la conmutación por error a la base de datos asociada si no se hace esto.  
>   
>  La creación de reflejo es una característica de la base de datos. Puede darse el caso de que las aplicaciones que utilizan varias bases de datos no puedan utilizar esta característica.  
>   
>  Además, los nombres de servidor no distinguen mayúsculas de minúsculas, pero los nombres de base de datos sí lo hacen. Debe asegurarse, por lo tanto, de utilizar la misma grafía en los nombres de origen de datos (DSN) y en las cadenas de conexión.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Proveedor OLE DB de SQL Server Native Client  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB admite la creación de reflejo de base de datos a través de la conexión y los atributos de cadena de conexión. Se ha agregado la propiedad ssprop_init_failoverpartner al conjunto de propiedades DBPROPSET_SQLSERVERDBINIT y el **FailoverPartner** palabra clave es un nuevo atributo de cadena de conexión para DBPROP_INIT_PROVIDERSTRING. Para obtener más información, consulte [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 La caché de conmutación por error se mantiene mientras se carga el proveedor, que es hasta **CoUninitialize** se llama o siempre que la aplicación tiene una referencia a un objeto administrado por el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB como un objeto de origen de datos.  
  
 Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] compatibilidad del proveedor OLE DB de Native Client con creación de reflejo de base de datos, vea [propiedades de inicialización y autorización](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
## <a name="sql-server-native-client-odbc-driver"></a>Controlador ODBC de SQL Server Native Client  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC Native Client admite la creación de reflejo de base de datos a través de la conexión y los atributos de cadena de conexión. En concreto, se ha agregado el atributo SQL_COPT_SS_FAILOVER_PARTNER para su uso con el [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) y [SQLGetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) funciones; y la **Failover_Partner** se ha agregado la palabra clave como un nuevo atributo de cadena de conexión.  
  
 La memoria caché de conmutación por error se mantiene mientras la aplicación tiene asignado por lo menos un identificador de entorno. En cambio, se pierde cuando se cancela la asignación del último identificador de entorno.  
  
> [!NOTE]  
>  El Administrador de controladores ODBC se ha mejorado para admitir la especificación del nombre del servidor de conmutación por error.  
  
## <a name="see-also"></a>Vea también  
 [Características SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Conectar clientes a una sesión de creación de reflejo de la base de datos &#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)   
 [Creación de reflejo de la base de datos &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
