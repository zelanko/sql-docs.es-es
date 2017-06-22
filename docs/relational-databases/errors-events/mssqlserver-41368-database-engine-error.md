---
title: MSSQLSERVER_41368 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 41368 (Database Engine error)
ms.assetid: abc71559-4c4d-4cce-a08f-3299dd167842
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
robots: noindex,nofollow
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9161b32ff6c9c2e2ee03b5909ee69db1594bbd9d
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver41368"></a>MSSQLSERVER_41368
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Identificador del evento|41368|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQL_IMPLICIT_AND_EXPLICIT_TX_NOT_SUPPORTED|  
|Texto del mensaje|El acceso a las tablas optimizadas en memoria con el nivel de aislamiento READ COMMITTED se admite solo para las transacciones de confirmación automática. No se admite para las transacciones explícitas o implícitas. Proporciona un nivel de aislamiento admitido para la tabla optimizada en memoria mediante una sugerencia de tabla, como WITH (SNAPSHOT).|  
  
## <a name="explanation"></a>Explicación  
El acceso a tablas con optimización para memoria con el nivel de aislamiento READ COMMITTED solo se admite para las transacciones de confirmación automática. Para obtener más información, consulte [Transacciones con tablas en memoria y procedimientos](~/relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md).  
  
Al obtener acceso a una tabla con optimización para memoria desde una transacción explícita iniciada con BEGIN TRANSACTION, o desde una transacción implícita, si IMPLICIT_TRANSACTIONS se establece en ON, no se admite el nivel de aislamiento READ COMMITTED.  
  
## <a name="user-action"></a>Acción del usuario  
Utilice SNAPSHOT para tener acceso a una tabla con optimización para memoria desde una transacción READ COMMITTED explícita o implícita. Se puede tener acceso mediante la sugerencia de tabla WITH (SNAPSHOT) (para obtener más información, vea [Transacciones con tablas en memoria y procedimientos](~/relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)) o estableciendo la opción de base de datos MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT en ON (para obtener más información, vea [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql.md)).  
  
## <a name="see-also"></a>Vea también  
[OLTP en memoria &#40;optimización en memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  

