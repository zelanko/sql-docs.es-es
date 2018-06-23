---
title: Las transacciones | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
ms.assetid: 3b41e33a-c1ca-4b2a-9464-312b0ed3ca89
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: dae1a7fc812e28c9ac51c1a2dc3f404ce8c420b3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103529"
---
# <a name="transactions"></a>Transactions
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client implementa compatibilidad con transacciones locales. El consumidor puede utilizar transacciones distribuidas o coordinadas mediante Microsoft DTC (Coordinador de transacciones distribuidas). Para los consumidores que requieren control de transacciones que abarque varias sesiones, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client puede combinar las transacciones que inicia y mantiene MS DTC.  
  
 De forma predeterminada, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client utiliza un modo de transacción de confirmación automática, donde cada acción discreta en una sesión del consumidor comprende una transacción completa en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el modo de confirmación automática del proveedor de OLE DB de Native Client es local, y transacciones de confirmación automática nunca abarcan más de una sola sesión.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client expone la **ITransactionLocal** interfaz, lo que permite al consumidor de forma explícita e implícitamente iniciar transacciones en una sola conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client no admite las transacciones locales anidadas.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Compatibilidad con transacciones locales](supporting-local-transactions.md)  
  
-   [Compatibilidad con transacciones distribuidas](supporting-distributed-transactions.md)  
  
-   [Niveles de aislamiento &#40;OLE DB&#41;](isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  