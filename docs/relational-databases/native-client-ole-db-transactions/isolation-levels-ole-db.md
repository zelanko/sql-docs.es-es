---
title: Niveles de aislamiento (OLE DB) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
ms.assetid: d70ee72c-6e2a-4bcd-9456-4a697a866361
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 3c9bbbcd4c89b46050b5bbca4bc72bc256d8a48e
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39558375"
---
# <a name="isolation-levels-ole-db"></a>Niveles de aislamiento (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Los clientes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden controlar los niveles de aislamiento de la transacción para una conexión. Para controlar el nivel de aislamiento de la transacción, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB proveedor consumidor utiliza:  
  
-   Propiedad DBPROPSET_SESSION corresponderán DBPROP_SESS_AUTOCOMMITISOLEVELS para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] modo de confirmación automática de Native Client OLE DB proveedor predeterminado.  
  
     El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] predeterminado del proveedor Native Client OLE DB para el nivel es DBPROPVAL_TI_READCOMMITTED.  
  
-   El parámetro *isoLevel* del método **ITransactionLocal::StartTransaction** para las transacciones locales de confirmación manual.  
  
-   El parámetro *isoLevel* del método **ITransactionDispenser::BeginTransaction** para las transacciones distribuidas coordinadas por MS DTC.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite el acceso de solo lectura en el nivel de aislamiento de lectura de datos sucios. Todos los demás niveles restringen la simultaneidad aplicando bloqueos a los objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando el cliente requiere niveles de simultaneidad mayores, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplica mayores restricciones al acceso simultáneo a los datos. Para mantener el máximo nivel de acceso simultáneo a los datos, la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor de Native Client OLE DB proveedor inteligente debe controlar sus solicitudes para los niveles de concurrencia específico.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] presentó el nivel del aislamiento de instantánea. Para obtener más información, vea [Trabajar con aislamiento de instantánea](../../relational-databases/native-client/features/working-with-snapshot-isolation.md).  
  
## <a name="see-also"></a>Vea también  
 [Transacciones](../../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  
