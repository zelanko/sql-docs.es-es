---
title: Niveles de aislamiento (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
ms.assetid: d70ee72c-6e2a-4bcd-9456-4a697a866361
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4ddfe4bd9d8760fa561e7b0221f61413b3c6d111
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761616"
---
# <a name="isolation-levels-ole-db"></a>Niveles de aislamiento (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Los clientes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden controlar los niveles de aislamiento de la transacción para una conexión. Para controlar el nivel de aislamiento de transacciones, el consumidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB Native Client utiliza:  
  
-   DBPROPSET_SESSION propiedad DBPROP_SESS_AUTOCOMMITISOLEVELS para el modo de confirmación automática del proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
     El valor predeterminado del proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para el nivel es DBPROPVAL_TI_READCOMMITTED.  
  
-   El parámetro *isoLevel* del método **ITransactionLocal::StartTransaction** para las transacciones locales de confirmación manual.  
  
-   El parámetro *isoLevel* del método **ITransactionDispenser::BeginTransaction** para las transacciones distribuidas coordinadas por MS DTC.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite el acceso de solo lectura en el nivel de aislamiento de lectura de datos sucios. Todos los demás niveles restringen la simultaneidad aplicando bloqueos a los objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando el cliente requiere niveles de simultaneidad mayores, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplica mayores restricciones al acceso simultáneo a los datos. Para mantener el máximo nivel de acceso simultáneo a los datos, el consumidor del proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB debe controlar de forma inteligente sus solicitudes de niveles de simultaneidad específicos.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] presentó el nivel del aislamiento de instantánea. Para obtener más información, vea [Working with Snapshot Isolation](../../relational-databases/native-client/features/working-with-snapshot-isolation.md).  
  
## <a name="see-also"></a>Vea también  
 [Transactions](../../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  
