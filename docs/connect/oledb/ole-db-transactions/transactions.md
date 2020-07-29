---
title: Transacciones | Microsoft Docs
description: Transacciones en el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 64a05f57c40027a4db448a987d32f77d62f0a837
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86011237"
---
# <a name="transactions"></a>Transacciones
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server implementa la compatibilidad con transacciones locales. El consumidor puede utilizar transacciones distribuidas o coordinadas mediante Microsoft DTC (Coordinador de transacciones distribuidas). Para los consumidores que requieren un control de las transacciones que abarque varias sesiones, el controlador OLE DB para SQL Server puede combinar las transacciones que inicia y mantiene MS DTC.  
  
 De forma predeterminada, el controlador OLE DB para SQL Server usa un modo de transacción con confirmación automática, donde cada acción específica en una sesión del consumidor comprende una transacción completa en una sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El modo de confirmación automática del controlador OLE DB para SQL Server es local y las transacciones con confirmación automática nunca abarcan más de una única sesión.  
  
 El controlador OLE DB para SQL Server expone la interfaz **ITransactionLocal**, que permite al consumidor iniciar transacciones de forma explícita e implícita en una conexión única a una sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. OLE DB Driver for SQL Server no admite transacciones locales anidadas.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Compatibilidad con transacciones locales](../../oledb/ole-db-transactions/supporting-local-transactions.md)  
  
-   [Compatibilidad con transacciones distribuidas](../../oledb/ole-db-transactions/supporting-distributed-transactions.md)  
  
-   [Niveles de aislamiento &#40;OLE DB&#41;](../../oledb/ole-db-transactions/isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>Consulte también  
 [Programación del controlador OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
