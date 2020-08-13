---
title: Niveles de aislamiento (controlador OLE DB) | Microsoft Docs
description: Niveles de aislamiento (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 60fce8b96ff116f1c1e92a75e1335a33207d36d3
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87244106"
---
# <a name="isolation-levels-ole-db"></a>Niveles de aislamiento (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Los clientes [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pueden controlar los niveles de aislamiento de la transacción para una conexión. Para controlar el nivel de aislamiento de las transacciones, el consumidor de OLE DB Driver for SQL Server usa:  
  
-   La propiedad de DBPROPSET_SESSION DBPROP_SESS_AUTOCOMMITISOLEVELS para el modo de confirmación automática predeterminado del controlador OLE DB para SQL Server.  
  
     El valor predeterminado de OLE DB Driver for SQL Server para el nivel es DBPROPVAL_TI_READCOMMITTED.  
  
-   El parámetro *isoLevel* del método **ITransactionLocal::StartTransaction** para las transacciones locales de confirmación manual.  
  
-   El parámetro *isoLevel* del método **ITransactionDispenser::BeginTransaction** para las transacciones distribuidas coordinadas por MS DTC.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite el acceso de solo lectura en el nivel de aislamiento de lectura de datos sucios. Todos los demás niveles restringen la simultaneidad aplicando bloqueos a los objetos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Cuando el cliente requiere niveles de simultaneidad mayores, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aplica mayores restricciones al acceso simultáneo a los datos. Para mantener el mayor nivel de acceso simultáneo a los datos, el consumidor del controlador OLE DB para SQL Server debe controlar inteligentemente sus solicitudes de niveles de simultaneidad específicos.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] presentó el nivel del aislamiento de instantánea. Para obtener más información, vea [Trabajar con aislamiento de instantánea](../../oledb/features/working-with-snapshot-isolation.md).  
  
## <a name="see-also"></a>Consulte también  
 [Transactions](../../oledb/ole-db-transactions/transactions.md)  
  
  
