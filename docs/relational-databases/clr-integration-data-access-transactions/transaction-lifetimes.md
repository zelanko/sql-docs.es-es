---
title: Duraciones de transacción | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- lifetimes [SQL Server]
- Transact-SQL vs. managed code
ms.assetid: cb076fda-6488-4959-a6a4-7adaccf3f25c
author: rothja
ms.author: jroth
ms.openlocfilehash: 759af22d445bb3c67db1f39ecf69dbeee1b666fe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902477"
---
# <a name="transaction-lifetimes"></a>Período de duración de las transacciones
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Hay una diferencia importante entre las transacciones iniciadas en procedimientos almacenados [!INCLUDE[tsql](../../includes/tsql-md.md)] y las iniciadas en código administrado: el código de Common Language Runtime (CLR) no puede desequilibrar el estado de la transacción al entrar o salir de una invocación CLR. Tenga en cuenta las implicaciones siguientes de esta diferencia:  
  
-   Una transacción iniciada dentro de un marco CLR se debe confirmar o revertir; de otro modo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera un error cuando se sale del marco.  
  
-   Una transacción exterior no se puede confirmar o revertir dentro del código CLR.  
  
-   Un intento para confirmar una transacción no iniciada en el mismo procedimiento produce un error en tiempo de ejecución.  
  
-   Un intento de revertir una transacción no iniciada en el mismo procedimiento hace que la transacción no responda (evitando que ser produzca cualquier otra operación con efectos secundarios). La transacción se interrumpe hasta que el código CLR se sale del ámbito. Tenga en cuenta que esto puede resultar útil cuando detecta un error dentro de su procedimiento y desea asegurarse de que toda la transacción finaliza.  
  
## <a name="see-also"></a>Vea también  
 [Integración CLR y transacciones](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
