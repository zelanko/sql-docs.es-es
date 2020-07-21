---
title: MSSQLSERVER_41368 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41368 (Database Engine error)
ms.assetid: abc71559-4c4d-4cce-a08f-3299dd167842
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 18b9ccb8a91d1fa8df1d6f39bf9c47636ae33d4e
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551378"
---
# <a name="mssqlserver_41368"></a>MSSQLSERVER_41368
    
## <a name="details"></a>Detalles  
  
|Atributo|Value|  
|-|-|  
|Nombre de producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Id. de evento|41368|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQL_IMPLICIT_AND_EXPLICIT_TX_NOT_SUPPORTED|  
|Texto del mensaje|El acceso a las tablas optimizadas en memoria con el nivel de aislamiento READ COMMITTED se admite solo para las transacciones de confirmación automática. No se admite para las transacciones explícitas o implícitas. Proporciona un nivel de aislamiento admitido para la tabla optimizada en memoria mediante una sugerencia de tabla, como WITH (SNAPSHOT).|  
  
## <a name="explanation"></a>Explicación  
 El acceso a tablas optimizadas para memoria con el nivel de aislamiento READ COMMITTED solo se admite para las transacciones de confirmación automática. Para obtener más información, consulte [Transaction Isolation Levels](../../database-engine/transaction-isolation-levels.md).  
  
 Al obtener acceso a una tabla optimizada para memoria desde una transacción explícita iniciada con BEGIN TRANSACTION, o desde una transacción implícita, si IMPLICIT_TRANSACTIONS se establece en ON, no se admite el nivel de aislamiento READ COMMITTED.  
  
## <a name="user-action"></a>Acción del usuario  
 Utilice SNAPSHOT para tener acceso a una tabla optimizada para memoria desde una transacción READ COMMITTED explícita o implícita. Esto puede lograrse mediante el uso de la sugerencia de tabla WITH (SNAPSHOT) (para obtener más información, vea [instrucciones para los niveles de aislamiento de transacción con tablas optimizadas para memoria](../in-memory-oltp/memory-optimized-tables.md)) o estableciendo la opción de base de datos MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT en ON (para obtener más información, vea [Opciones de ALTER DATABASE Set &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)).  
  
## <a name="see-also"></a>Consulte también  
 [OLTP en memoria &#40;optimización en memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
