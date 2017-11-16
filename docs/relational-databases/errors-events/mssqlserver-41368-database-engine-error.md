---
title: MSSQLSERVER_41368 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 41368 (Database Engine error)
ms.assetid: abc71559-4c4d-4cce-a08f-3299dd167842
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: cguyer
robots: noindex,nofollow
ms.workload: Inactive
ms.openlocfilehash: acba8b4dd1ffc8d58b88200756eb9a25d1f91b33
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
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
El acceso a tablas optimizadas para memoria con el nivel de aislamiento READ COMMITTED solo se admite para las transacciones de confirmación automática. Para obtener más información, consulte [Transacciones con tablas en memoria y procedimientos](~/relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md).  
  
Al obtener acceso a una tabla optimizada para memoria desde una transacción explícita iniciada con BEGIN TRANSACTION, o desde una transacción implícita, si IMPLICIT_TRANSACTIONS se establece en ON, no se admite el nivel de aislamiento READ COMMITTED.  
  
## <a name="user-action"></a>Acción del usuario  
Utilice SNAPSHOT para tener acceso a una tabla optimizada para memoria desde una transacción READ COMMITTED explícita o implícita. Se puede tener acceso mediante la sugerencia de tabla WITH (SNAPSHOT) (para obtener más información, vea [Transacciones con tablas en memoria y procedimientos](~/relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)) o estableciendo la opción de base de datos MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT en ON (para obtener más información, vea [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql.md)).  
  
## <a name="see-also"></a>Vea también  
[OLTP en memoria &#40;optimización en memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
