---
title: Trabajar con aislamiento de instantánea | Microsoft Docs
description: Trabajar con aislamiento de instantánea en el controlador de OLE DB para SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 81c637192b9702b73a70f3fa2c1aee58c02bc66b
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2018
ms.locfileid: "39109057"
---
# <a name="working-with-snapshot-isolation"></a>Trabajar con aislamiento de instantánea
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introdujo un nuevo nivel de aislamiento de "instantánea" pensado para mejorar la simultaneidad en las aplicaciones de procesamiento de transacciones en línea (OLTP). En versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la simultaneidad se basada únicamente en el bloqueo, lo que podía provocar problemas de bloqueo e interbloqueo en algunas aplicaciones. El aislamiento de instantánea depende de las mejoras de las versiones de fila y está pensado para mejorar el rendimiento evitando situaciones de bloqueo de lectura-escritura.  
  
 Las transacciones que se inician bajo el aislamiento de instantánea leen una instantánea de la base de datos realizada al comenzar la transacción. Los cursores de servidor estáticos, dinámicos y controlados por conjunto de claves, al abrirse dentro de un contexto de transacciones de instantánea, actúan de forma muy similar a los cursores estáticos que se han abierto desde transacciones serializables. Sin embargo, cuando los cursores abiertos en los bloqueos de nivel de aislamiento de instantánea no se utilizan. Este hecho puede reducir el bloqueo en el servidor.  
  
## <a name="ole-db-driver-for-sql-server"></a>Controlador OLE DB para SQL Server  
 El controlador OLE DB para SQL Server incluye mejoras que aprovechan el aislamiento de instantánea que se introdujo en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Estas mejoras incluyen cambios en los conjuntos de propiedades DBPROPSET_SESSION y DBPROPSET_DATASOURCEINFO.  
  
### <a name="dbpropsetdatasourceinfo"></a>DBPROPSET_DATASOURCEINFO  
 El conjunto de propiedades DBPROPSET_DATASOURCEINFO ha cambiado para indicar que se admite el nivel de aislamiento de instantánea mediante la adición del valor DBPROPVAL_TI_SNAPSHOT que se utiliza en la propiedad DBPROP_SUPPORTEDTXNISOLEVELS. Este nuevo valor indica que se admite el nivel del aislamiento de instantánea independientemente de que se haya habilitado o no el control de versiones en la base de datos. En la tabla siguiente se enumera los valores DBPROP_SUPPORTEDTXNISOLEVELS:  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|DBPROP_SUPPORTEDTXNISOLEVELS|Tipo: VT_I4<br /><br /> L/E: de solo lectura<br /><br /> Descripción: una máscara de bits que especifica los niveles de aislamiento de transacción admitidos. Combinación de cero o más de los siguientes elementos:<br /><br /> DBPROPVAL_TI_CHAOS<br /><br /> DBPROPVAL_TI_READUNCOMMITTED<br /><br /> DBPROPVAL_TI_BROWSE<br /><br /> DBPROPVAL_TI_CURSORSTABILITY<br /><br /> DBPROPVAL_TI_READCOMMITTED<br /><br /> DBPROPVAL_TI_REPEATABLEREAD<br /><br /> DBPROPVAL_TI_SERIALIZABLE<br /><br /> DBPROPVAL_TI_ISOLATED<br /><br /> DBPROPVAL_TI_SNAPSHOT|  
  
### <a name="dbpropsetsession"></a>DBPROPSET_SESSION  
 El conjunto de propiedades DBPROPSET_SESSION ha cambiado para indicar que se admite el nivel de aislamiento de instantánea mediante la adición del valor DBPROPVAL_TI_SNAPSHOT que se utiliza en la propiedad DBPROP_SESS_AUTOCOMMITISOLEVELS. Este nuevo valor indica que se admite el nivel del aislamiento de instantánea independientemente de que se haya habilitado o no el control de versiones en la base de datos. A continuación se incluye una tabla con los valores de DBPROP_SESS_AUTOCOMMITISOLEVELS:
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|Tipo: VT_I4<br /><br /> L/E: de solo lectura<br /><br /> Descripción: especifica una máscara de bits que indica el nivel de aislamiento de transacción mientras está activo el modo de confirmación automática. Los valores que se pueden establecer en esta máscara de bits son iguales a los que se pueden establecer para DBPROP_SUPPORTEDTXNISOLEVELS.|  
  
> [!NOTE]  
>  Si se establece DBPROPVAL_TI_SNAPSHOT con las versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], se generan los errores DB_S_ERRORSOCCURRED o DB_E_ERRORSOCCURRED.  
  
 Para obtener información acerca de cómo se admite el aislamiento de instantánea en transacciones, vea [compatibilidad con transacciones locales](../../oledb/ole-db-transactions/supporting-local-transactions.md).  

  
## <a name="see-also"></a>Ver también  
 [Características del controlador OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [Propiedades y comportamientos de conjuntos de filas](../../oledb/ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
  
