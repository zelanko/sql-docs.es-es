---
title: Niveles de aislamiento (OLE DB) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d1870c4f9f348c9d1b2ca52b94ee38a3e5d38190
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2018
ms.locfileid: "35698076"
---
# <a name="isolation-levels-ole-db"></a>Niveles de aislamiento (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Los clientes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden controlar los niveles de aislamiento de la transacción para una conexión. Para controlar el nivel de aislamiento de transacción, la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usos de consumidor de proveedor OLE DB de Native Client:  
  
-   Propiedad de DBPROPSET_SESSION DBPROP_SESS_AUTOCOMMITISOLEVELS para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] modo de confirmación automática de Native Client OLE DB proveedor predeterminado.  
  
     El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] predeterminado del proveedor OLE DB de Native Client para el nivel es DBPROPVAL_TI_READCOMMITTED.  
  
-   El *isoLevel* parámetro de la **ITransactionLocal:: StartTransaction** método para realizar transacciones locales de confirmación manual.  
  
-   El *isoLevel* parámetro de la **ITransactionDispenser:: BeginTransaction** transacciones distribuidas de método para coordinada con MS DTC.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite el acceso de solo lectura en el nivel de aislamiento de lectura de datos sucios. Todos los demás niveles restringen la simultaneidad aplicando bloqueos a los objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando el cliente requiere niveles de simultaneidad mayores, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplica mayores restricciones al acceso simultáneo a los datos. Para mantener el nivel más alto de acceso simultáneo a los datos, la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor del proveedor OLE DB de Native Client debe controlar inteligentemente sus solicitudes para los niveles de simultaneidad específicos.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] presentó el nivel del aislamiento de instantánea. Para obtener más información, consulte [trabajar con aislamiento de instantánea](../../relational-databases/native-client/features/working-with-snapshot-isolation.md).  
  
## <a name="see-also"></a>Vea también  
 [Transacciones](../../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  
