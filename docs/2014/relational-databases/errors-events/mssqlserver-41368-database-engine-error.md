---
title: MSSQLSERVER_41368 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 41368 (Database Engine error)
ms.assetid: abc71559-4c4d-4cce-a08f-3299dd167842
caps.latest.revision: 8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8619e3cfb8766caab9d9afbe5ed166761eeeb04f
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37409724"
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
 El acceso a tablas optimizadas para memoria con el nivel de aislamiento READ COMMITTED solo se admite para las transacciones de confirmación automática. Para obtener más información, consulte [Transaction Isolation Levels](../../database-engine/transaction-isolation-levels.md).  
  
 Al obtener acceso a una tabla optimizada para memoria desde una transacción explícita iniciada con BEGIN TRANSACTION, o desde una transacción implícita, si IMPLICIT_TRANSACTIONS se establece en ON, no se admite el nivel de aislamiento READ COMMITTED.  
  
## <a name="user-action"></a>Acción del usuario  
 Utilice SNAPSHOT para tener acceso a una tabla optimizada para memoria desde una transacción READ COMMITTED explícita o implícita. Esto puede lograrse mediante el uso de la sugerencia de tabla WITH (SNAPSHOT) (para obtener más información, consulte [directrices para los niveles de aislamiento de transacciones con tablas optimizadas para memoria](../in-memory-oltp/memory-optimized-tables.md)) o mediante el establecimiento de la base de datos de opción MEMORY_OPTIMIZED_ELEVATE_TO_ INSTANTÁNEA en ON (para obtener más información, consulte [ALTER DATABASE SET Options &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)).  
  
## <a name="see-also"></a>Vea también  
 [OLTP en memoria &#40;optimización en memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
