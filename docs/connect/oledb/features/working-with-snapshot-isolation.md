---
title: Trabajo con aislamiento de instantánea | Microsoft Docs
description: Trabajo con aislamiento de instantáneas en OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], snapshot isolation
- MSOLEDBSQL, snapshot isolation
- isolation levels [SQL Server], snapshot
- DBPROPSET_SESSION property set
- DBDROPSET_DATASOURCEINFO property set
- snapshot isolation [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, snapshot isolation
- SQLGetInfo function
- concurrency [OLE DB Driver for SQL Server]
- SQLSetConnectAttr function
author: pmasl
ms.author: pelopes
ms.openlocfilehash: acbb39726ede983d3c0909235d1fb2ddb588d65b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "85986833"
---
# <a name="working-with-snapshot-isolation"></a>Trabajar con aislamiento de instantánea
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introdujo un nuevo nivel de aislamiento de "instantánea" pensado para mejorar la simultaneidad en las aplicaciones de procesamiento de transacciones en línea (OLTP). En versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la simultaneidad se basada únicamente en el bloqueo, lo que podía provocar problemas de bloqueo e interbloqueo en algunas aplicaciones. El aislamiento de instantánea depende de las mejoras de las versiones de fila y está pensado para mejorar el rendimiento evitando situaciones de bloqueo de lectura-escritura.  
  
 Las transacciones que se inician bajo el aislamiento de instantánea leen una instantánea de la base de datos realizada al comenzar la transacción. Los cursores de servidor estáticos, dinámicos y controlados por conjunto de claves, al abrirse dentro de un contexto de transacciones de instantánea, actúan de forma muy similar a los cursores estáticos que se han abierto desde transacciones serializables. Sin embargo, cuando los cursores se abren bajo el nivel de aislamiento de instantánea no se toman bloqueos, lo que puede reducir el bloqueo en el servidor.  
  
## <a name="ole-db-driver-for-sql-server"></a>Controlador OLE DB para SQL Server  
 El proveedor OLE DB Driver for SQL Server incluye mejoras que aprovechan el aislamiento de instantánea presentado en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Estas mejoras incluyen cambios en los conjuntos de propiedades DBPROPSET_SESSION y DBPROPSET_DATASOURCEINFO.  
  
### <a name="dbpropset_datasourceinfo"></a>DBPROPSET_DATASOURCEINFO  
 El conjunto de propiedades DBPROPSET_DATASOURCEINFO ha cambiado para indicar que se admite el nivel de aislamiento de instantánea mediante la adición del valor DBPROPVAL_TI_SNAPSHOT que se utiliza en la propiedad DBPROP_SUPPORTEDTXNISOLEVELS. Este nuevo valor indica que se admite el nivel del aislamiento de instantánea independientemente de que se haya habilitado o no el control de versiones en la base de datos. En la tabla siguiente se incluye una lista de los valores de DBPROP_SUPPORTEDTXNISOLEVELS:  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|DBPROP_SUPPORTEDTXNISOLEVELS|Tipo: VT_I4<br /><br /> L/E: de solo lectura<br /><br /> Descripción: una máscara de bits que especifica los niveles de aislamiento de transacción admitidos. Combinación de cero o más de los siguientes elementos:<br /><br /> DBPROPVAL_TI_CHAOS<br /><br /> DBPROPVAL_TI_READUNCOMMITTED<br /><br /> DBPROPVAL_TI_BROWSE<br /><br /> DBPROPVAL_TI_CURSORSTABILITY<br /><br /> DBPROPVAL_TI_READCOMMITTED<br /><br /> DBPROPVAL_TI_REPEATABLEREAD<br /><br /> DBPROPVAL_TI_SERIALIZABLE<br /><br /> DBPROPVAL_TI_ISOLATED<br /><br /> DBPROPVAL_TI_SNAPSHOT|  
  
### <a name="dbpropset_session"></a>DBPROPSET_SESSION  
 El conjunto de propiedades DBPROPSET_SESSION ha cambiado para indicar que se admite el nivel de aislamiento de instantánea mediante la adición del valor DBPROPVAL_TI_SNAPSHOT que se utiliza en la propiedad DBPROP_SESS_AUTOCOMMITISOLEVELS. Este nuevo valor indica que se admite el nivel del aislamiento de instantánea independientemente de que se haya habilitado o no el control de versiones en la base de datos. A continuación se incluye una tabla con los valores de DBPROP_SESS_AUTOCOMMITISOLEVELS:
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|Tipo: VT_I4<br /><br /> L/E: de solo lectura<br /><br /> Descripción: especifica una máscara de bits que indica el nivel de aislamiento de transacción mientras está activo el modo de confirmación automática. Los valores que se pueden establecer en esta máscara de bits son iguales a los que se pueden establecer para DBPROP_SUPPORTEDTXNISOLEVELS.|  
  
> [!NOTE]  
>  Si se establece DBPROPVAL_TI_SNAPSHOT con las versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], se generan los errores DB_S_ERRORSOCCURRED o DB_E_ERRORSOCCURRED.  
  
 Para más información sobre cómo se admite el aislamiento de instantánea en transacciones, consulte [Compatibilidad con transacciones locales](../../oledb/ole-db-transactions/supporting-local-transactions.md).  

  
## <a name="see-also"></a>Consulte también  
 [Características del controlador OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [Propiedades y comportamientos de conjuntos de filas](../../oledb/ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
  
