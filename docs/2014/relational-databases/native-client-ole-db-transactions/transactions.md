---
title: Transacciones | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: dca9b7a3289390b1d1e20e1b0d18c23b44b87617
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63213892"
---
# <a name="transactions"></a>Transacciones
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client implementa la compatibilidad con transacciones locales. El consumidor puede utilizar transacciones distribuidas o coordinadas mediante Microsoft DTC (Coordinador de transacciones distribuidas). En el caso de los consumidores que requieren el control de transacciones que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] abarca varias sesiones, el proveedor de OLE DB de Native Client puede combinar las transacciones iniciadas y mantenidas por MS DTC.  
  
 De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el proveedor de OLE DB de Native Client utiliza un modo de transacción de confirmación automática, donde cada acción discreta de una sesión de consumidor comprende una transacción [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]completa en una instancia de. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] modo de confirmación automática del proveedor de OLE DB de Native Client es local y las transacciones de confirmación automática nunca abarcan más de una sesión.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client expone la interfaz **ITransactionLocal** , lo que permite al consumidor utilizar de forma explícita e implícita transacciones en una única conexión a una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]instancia de. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client no admite transacciones locales anidadas.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Compatibilidad con transacciones locales](supporting-local-transactions.md)  
  
-   [Compatibilidad con transacciones distribuidas](supporting-distributed-transactions.md)  
  
-   [Niveles de aislamiento &#40;OLE DB&#41;](isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
