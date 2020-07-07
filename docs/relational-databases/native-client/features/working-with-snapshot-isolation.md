---
title: Trabajo con aislamiento de instantánea | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], snapshot isolation
- SQLNCLI, snapshot isolation
- isolation levels [SQL Server], snapshot
- DBPROPSET_SESSION property set
- DBDROPSET_DATASOURCEINFO property set
- snapshot isolation [SQL Server Native Client]
- SQL Server Native Client OLE DB provider, snapshot isolation
- SQL Server Native Client ODBC driver, snapshot isolation
- SQL Server Native Client, snapshot isolation
- SQLGetInfo function
- concurrency [SQL Server Native Client]
- SQLSetConnectAttr function
ms.assetid: 39e87eb1-677e-45dd-bc61-83a4025a7756
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 196ddb0db1d988f3f81c6f34a53973a4ac0123ce
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86009811"
---
# <a name="working-with-snapshot-isolation"></a>Trabajar con aislamiento de instantánea
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introdujo un nuevo nivel de aislamiento de "instantánea" pensado para mejorar la simultaneidad en las aplicaciones de procesamiento de transacciones en línea (OLTP). En versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la simultaneidad se basada únicamente en el bloqueo, lo que podía provocar problemas de bloqueo e interbloqueo en algunas aplicaciones. El aislamiento de instantánea depende de las mejoras de las versiones de fila y está pensado para mejorar el rendimiento evitando situaciones de bloqueo de lectura-escritura.  
  
 Las transacciones que se inician bajo el aislamiento de instantánea leen una instantánea de la base de datos realizada al comenzar la transacción. Un resultado de esta acción es que los cursores estáticos, dinámicos y controlados por conjunto de claves, al abrirse dentro de un contexto de transacciones de instantánea, actúan de forma muy similar a los cursores estáticos que se abren desde transacciones serializables. Sin embargo, cuando los cursores se abren bajo el nivel de aislamiento de instantánea no se toman bloqueos, lo que puede reducir el bloqueo en el servidor.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Proveedor OLE DB de SQL Server Native Client  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client tiene mejoras que aprovechan el aislamiento de instantánea introducido en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] . Estas mejoras incluyen cambios en los conjuntos de propiedades DBPROPSET_SESSION y DBPROPSET_DATASOURCEINFO.  
  
### <a name="dbpropset_datasourceinfo"></a>DBPROPSET_DATASOURCEINFO  
 El conjunto de propiedades DBPROPSET_DATASOURCEINFO ha cambiado para indicar que se admite el nivel de aislamiento de instantánea mediante la adición del valor DBPROPVAL_TI_SNAPSHOT que se utiliza en la propiedad DBPROP_SUPPORTEDTXNISOLEVELS. Este nuevo valor indica que se admite el nivel del aislamiento de instantánea independientemente de que se haya habilitado o no el control de versiones en la base de datos. A continuación se incluye una lista de los valores de DBPROP_SUPPORTEDTXNISOLEVELS:  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|DBPROP_SUPPORTEDTXNISOLEVELS|Tipo: VT_I4<br /><br /> L/E: de solo lectura<br /><br /> Descripción: una máscara de bits que especifica los niveles de aislamiento de transacción admitidos. Combinación de cero o más de los siguientes elementos:<br /><br /> DBPROPVAL_TI_CHAOS<br /><br /> DBPROPVAL_TI_READUNCOMMITTED<br /><br /> DBPROPVAL_TI_BROWSE<br /><br /> DBPROPVAL_TI_CURSORSTABILITY<br /><br /> DBPROPVAL_TI_READCOMMITTED<br /><br /> DBPROPVAL_TI_REPEATABLEREAD<br /><br /> DBPROPVAL_TI_SERIALIZABLE<br /><br /> DBPROPVAL_TI_ISOLATED<br /><br /> DBPROPVAL_TI_SNAPSHOT|  
  
### <a name="dbpropset_session"></a>DBPROPSET_SESSION  
 El conjunto de propiedades DBPROPSET_SESSION ha cambiado para indicar que se admite el nivel de aislamiento de instantánea mediante la adición del valor DBPROPVAL_TI_SNAPSHOT que se utiliza en la propiedad DBPROP_SESS_AUTOCOMMITISOLEVELS. Este nuevo valor indica que se admite el nivel del aislamiento de instantánea independientemente de que se haya habilitado o no el control de versiones en la base de datos. A continuación se incluye una lista de los valores de DBPROP_SESS_AUTOCOMMITISOLEVELS:  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|Tipo: VT_I4<br /><br /> L/E: de solo lectura<br /><br /> Descripción: especifica una máscara de bits que indica el nivel de aislamiento de transacción mientras está activo el modo de confirmación automática. Los valores que se pueden establecer en esta máscara de bits son iguales a los que se pueden establecer para DBPROP_SUPPORTEDTXNISOLEVELS.|  
  
> [!NOTE]  
>  Si se establece DBPROPVAL_TI_SNAPSHOT con las versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], se generan los errores DB_S_ERRORSOCCURRED o DB_E_ERRORSOCCURRED.  
  
 Para más información sobre cómo se admite el aislamiento de instantánea en transacciones, consulte [Compatibilidad con transacciones locales](../../../relational-databases/native-client-ole-db-transactions/supporting-local-transactions.md).  
  
## <a name="sql-server-native-client-odbc-driver"></a>Controlador ODBC de SQL Server Native Client  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client proporciona compatibilidad para el aislamiento de instantáneas a través de las mejoras realizadas en las funciones [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) y [SQLGetInfo](../../../relational-databases/native-client-odbc-api/sqlgetinfo.md) .  
  
### <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 La función **SQLSetConnectAttr** admite ahora el uso del atributo SQL_COPT_SS_TXN_ISOLATION. Si SQL_COPT_SS_TXN_ISOLATION se establece en SQL_TXN_SS_SNAPSHOT, significa que la transacción tendrá lugar en el nivel de aislamiento de instantáneas.  
  
### <a name="sqlgetinfo"></a>SQLGetInfo  
 La función [SQLGetInfo](../../../relational-databases/native-client-odbc-api/sqlgetinfo.md) admite ahora el valor SQL_TXN_SS_SNAPSHOT que se ha agregado al tipo de información SQL_TXN_ISOLATION_OPTION.  
  
 Para obtener información sobre cómo se admite el aislamiento de instantáneas en transacciones, vea [cursor TRANSACTION ISOLATION LEVEL](../../../relational-databases/native-client-odbc-cursors/properties/cursor-transaction-isolation-level.md).  
  
## <a name="see-also"></a>Consulte también  
 [Características de SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Propiedades y comportamientos de conjuntos de filas](../../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
  
