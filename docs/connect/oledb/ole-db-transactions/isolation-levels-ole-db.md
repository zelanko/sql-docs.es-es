---
title: Niveles de aislamiento (OLE DB) | Documentos de Microsoft
description: Niveles de aislamiento (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-transactions
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: b015a27fccfdad7b9f20bdac16a3a587f0c026a5
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/16/2018
ms.locfileid: "35690018"
---
# <a name="isolation-levels-ole-db"></a>Niveles de aislamiento (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Los clientes [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pueden controlar los niveles de aislamiento de la transacción para una conexión. Para controlar el nivel de aislamiento de transacción, se utiliza el controlador OLE DB para el consumidor de SQL Server:  
  
-   Propiedad de DBPROPSET_SESSION DBPROP_SESS_AUTOCOMMITISOLEVELS para el controlador OLE DB para el modo de confirmación automática predeterminada de SQL Server.  
  
     El controlador OLE DB para el valor predeterminado de SQL Server para el nivel es DBPROPVAL_TI_READCOMMITTED.  
  
-   El *isoLevel* parámetro de la **ITransactionLocal:: StartTransaction** método para realizar transacciones locales de confirmación manual.  
  
-   El *isoLevel* parámetro de la **ITransactionDispenser:: BeginTransaction** transacciones distribuidas de método para coordinada con MS DTC.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite el acceso de solo lectura en el nivel de aislamiento de lectura de datos sucios. Todos los demás niveles restringen la simultaneidad aplicando bloqueos a los objetos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Cuando el cliente requiere niveles de simultaneidad mayores, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aplica mayores restricciones al acceso simultáneo a los datos. Para mantener el nivel más alto de acceso simultáneo a los datos, el controlador OLE DB para el consumidor de SQL Server debe controlar inteligentemente sus solicitudes para los niveles de simultaneidad específicos.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] presentó el nivel del aislamiento de instantánea. Para obtener más información, consulte [trabajar con aislamiento de instantánea](../../oledb/features/working-with-snapshot-isolation.md).  
  
## <a name="see-also"></a>Vea también  
 [Transacciones](../../oledb/ole-db-transactions/transactions.md)  
  
  
