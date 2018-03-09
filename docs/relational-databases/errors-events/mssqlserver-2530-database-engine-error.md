---
title: MSSQLSERVER_2530 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 5d4be07a-38a5-4b25-819c-4dcb4636cc15
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3235cee13ecfc73cc3a3fee5e83a320c8f25b842
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver2530"></a>MSSQLSERVER_2530
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|2530|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC_INDEX_IS_OFFLINE|  
|Texto del mensaje|El índice "%.*ls"" de la tabla "%.\*ls" está deshabilitado.|  
  
## <a name="explanation"></a>Explicación  
La instrucción DBCC no puede continuar porque el índice especificado está deshabilitado. Cuando se deshabilita un índice, sigue deshabilitado hasta que se vuelve a generar o se quita y se vuelve a crear.  
  
## <a name="user-action"></a>Acción del usuario  
  
1.  Habilite el índice deshabilitado utilizando uno de los métodos siguientes:  
  
    -   Instrucción ALTER INDEX con la cláusula REBUILD  
  
    -   CREATE INDEX con la cláusula DROP_EXISTING  
  
    -   DBCC DBREINDEX  
  
2.  Ejecute de nuevo la instrucción DBCC.  
  
## <a name="see-also"></a>Vea también  
[Habilitar índices y restricciones](~/relational-databases/indexes/enable-indexes-and-constraints.md)  
[ALTER INDEX &#40;Transact-SQL&#41;](~/t-sql/statements/alter-index-transact-sql.md)  
[CREATE INDEX &#40;Transact-SQL&#41;](~/t-sql/statements/create-index-transact-sql.md)  
[DBCC DBREINDEX &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md)  
  
