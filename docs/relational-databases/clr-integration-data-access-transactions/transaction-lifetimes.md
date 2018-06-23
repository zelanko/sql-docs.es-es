---
title: Duraciones de transacción | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: reference
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- lifetimes [SQL Server]
- Transact-SQL vs. managed code
ms.assetid: cb076fda-6488-4959-a6a4-7adaccf3f25c
caps.latest.revision: 10
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ee3f55fea7f08aa38257558e673adbf090ea1d0a
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2018
ms.locfileid: "35695246"
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
  
  
