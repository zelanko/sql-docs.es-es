---
title: Transacciones | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
ms.assetid: 3b41e33a-c1ca-4b2a-9464-312b0ed3ca89
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d54dbe8e3df6e930ebd026e638d0a21f2f88f32e
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73772557"
---
# <a name="transactions"></a>Transacciones
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client implementa la compatibilidad con transacciones locales. El consumidor puede utilizar transacciones distribuidas o coordinadas mediante Microsoft DTC (Coordinador de transacciones distribuidas). En el caso de los consumidores que requieren el control de transacciones que abarca varias sesiones, el proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB puede combinar las transacciones iniciadas y mantenidas por MS DTC.  
  
 De forma predeterminada, el proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client utiliza un modo de transacción de confirmación automática, donde cada acción discreta de una sesión de consumidor comprende una transacción completa en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El modo de confirmación automática del proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client es local y las transacciones de confirmación automática nunca abarcan más de una sesión.  
  
 El proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client expone la interfaz **ITransactionLocal** , lo que permite al consumidor utilizar de forma explícita e implícita transacciones en una única conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client no admite transacciones locales anidadas.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Compatibilidad con transacciones locales](../../relational-databases/native-client-ole-db-transactions/supporting-local-transactions.md)  
  
-   [Compatibilidad con transacciones distribuidas](../../relational-databases/native-client-ole-db-transactions/supporting-distributed-transactions.md)  
  
-   [Niveles &#40;de aislamiento OLE DB&#41;](../../relational-databases/native-client-ole-db-transactions/isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
