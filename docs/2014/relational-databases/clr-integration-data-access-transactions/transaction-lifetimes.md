---
title: Duraciones de transacción | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- lifetimes [SQL Server]
- Transact-SQL vs. managed code
ms.assetid: cb076fda-6488-4959-a6a4-7adaccf3f25c
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 290d4c43767ba7e1c6f784c84473e9a05503af54
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62920071"
---
# <a name="transaction-lifetimes"></a>Período de duración de las transacciones
  Hay una diferencia importante entre las transacciones iniciadas en procedimientos almacenados [!INCLUDE[tsql](../../includes/tsql-md.md)] y las iniciadas en código administrado: el código de Common Language Runtime (CLR) no puede desequilibrar el estado de la transacción al entrar o salir de una invocación CLR. Tenga en cuenta las implicaciones siguientes de esta diferencia:  
  
-   Una transacción iniciada dentro de un marco CLR se debe confirmar o revertir; de otro modo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera un error cuando se sale del marco.  
  
-   Una transacción exterior no se puede confirmar o revertir dentro del código CLR.  
  
-   Un intento para confirmar una transacción no iniciada en el mismo procedimiento produce un error en tiempo de ejecución.  
  
-   Un intento de revertir una transacción no iniciada en el mismo procedimiento hace que la transacción no responda (evitando que ser produzca cualquier otra operación con efectos secundarios). La transacción se interrumpe hasta que el código CLR se sale del ámbito. Tenga en cuenta que esto puede resultar útil cuando detecta un error dentro de su procedimiento y desea asegurarse de que toda la transacción finaliza.  
  
## <a name="see-also"></a>Vea también  
 [Integración CLR y transacciones](../native-client-ole-db-transactions/transactions.md)  
  
  
