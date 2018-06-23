---
title: Descripción de las transacciones en tablas optimizadas en memoria | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 06075248-705e-4563-9371-b64cd609793c
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: 604e6670d6a28f7b4a700d7a7b8f156cc67d0a54
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197447"
---
# <a name="understanding-transactions-on-memory-optimized-tables"></a>Descripción de las transacciones en tablas con optimización para memoria
  Las transacciones tienen acceso a las tablas optimizadas para memoria mediante control de simultaneidad optimista multiversión. Esto significa que hay versiones diferentes de los datos. Cada transacción opera en su propia versión coherente de forma transaccional de la base de datos, de forma independiente de otras transacciones que se ejecutan simultáneamente. Además, las transacciones operan con la suposición optimista de que no habrá ningún conflicto con otras transacciones simultáneas. Esto evita la necesidad de utilizar bloqueos, pero requiere que el sistema detecte los conflictos y termine una de las transacciones en conflicto. Los conflictos pueden aparecer solo para las transacciones de escritura contra escritura y para las transacciones de lectura contra escritura. Si hay un conflicto de escritura contra escritura, finaliza una transacción de escritura.  
  
 Hay similitudes entre el control de simultaneidad de las tablas optimizadas para memoria y el control de simultaneidad en las tablas basadas en disco para los niveles de aislamiento de transacción READ_COMMITTED_SNAPSHOT y SNAPSHOT. (Para obtener más información acerca de las tablas basadas en disco, consulte [niveles de aislamiento basados en versiones de fila en el motor de base de datos](http://msdn.microsoft.com/library/ms177404\(v=sql.100\).aspx).)  
  
## <a name="topics-in-this-section"></a>Temas de esta sección  
 Esta sección sobre las transacciones en tablas optimizadas para memoria incluye los temas siguientes:  
  
-   [Directrices para los niveles de aislamiento de transacciones con tablas optimizadas en memoria](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
-   [Directrices para la lógica de reintento para las transacciones en tablas optimizadas en memoria](guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)  
  
-   [Transacciones en tablas optimizadas en memoria](transactions-in-memory-optimized-tables.md)  
  
-   [Niveles de aislamiento de transacción](transaction-isolation-levels.md)  
  
-   [Transacciones entre contenedores](cross-container-transactions.md)  
  
 Para saber más, vea [Control de la durabilidad de las transacciones](../relational-databases/logs/control-transaction-durability.md).  
  
## <a name="see-also"></a>Vea también  
 [Tablas con optimización para memoria](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  