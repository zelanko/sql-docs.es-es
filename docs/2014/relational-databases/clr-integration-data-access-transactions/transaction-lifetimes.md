---
title: Duraciones de transacción | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- lifetimes [SQL Server]
- Transact-SQL vs. managed code
ms.assetid: cb076fda-6488-4959-a6a4-7adaccf3f25c
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c56a98e5cd9670f8dd3a86265aa50a7f0f57b5af
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198935"
---
# <a name="transaction-lifetimes"></a>Período de duración de las transacciones
  Hay una diferencia importante entre las transacciones iniciadas en procedimientos almacenados [!INCLUDE[tsql](../../includes/tsql-md.md)] y las iniciadas en código administrado: el código de Common Language Runtime (CLR) no puede desequilibrar el estado de la transacción al entrar o salir de una invocación CLR. Tenga en cuenta las implicaciones siguientes de esta diferencia:  
  
-   Una transacción iniciada dentro de un marco CLR se debe confirmar o revertir; de otro modo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera un error cuando se sale del marco.  
  
-   Una transacción exterior no se puede confirmar o revertir dentro del código CLR.  
  
-   Un intento para confirmar una transacción no iniciada en el mismo procedimiento produce un error en tiempo de ejecución.  
  
-   Un intento de revertir una transacción no iniciada en el mismo procedimiento hace que la transacción no responda (evitando que ser produzca cualquier otra operación con efectos secundarios). La transacción se interrumpe hasta que el código CLR se sale del ámbito. Tenga en cuenta que esto puede resultar útil cuando detecta un error dentro de su procedimiento y desea asegurarse de que toda la transacción finaliza.  
  
## <a name="see-also"></a>Vea también  
 [Integración CLR y transacciones](../native-client-ole-db-transactions/transactions.md)  
  
  