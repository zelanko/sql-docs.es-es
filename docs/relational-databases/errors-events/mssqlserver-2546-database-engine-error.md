---
title: MSSQLSERVER_2546 | Microsoft Docs
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
- 2546 (Database Engine error)
ms.assetid: c8f0e1b4-c7c4-45f2-9221-746714172313
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 55278a84ecc717b9668af1b99bd2cf8ec3d5de16
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver2546"></a>MSSQLSERVER_2546
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|2546|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC_INDEX_MARKED_DISABLED|  
|Texto del mensaje|El índice 'INDEX_NAME' de la tabla 'OBJECT_NAME' está marcado como deshabilitado. Genere de nuevo el índice para ponerlo en línea.|  
  
## <a name="explanation"></a>Explicación  
El índice especificado está marcado como sin conexión o está deshabilitado. Por tanto, este índice no se puede comprobar.  
  
## <a name="user-action"></a>Acción del usuario  
Vuelva a generar el índice usando ALTER INDEX.  
  
## <a name="see-also"></a>Vea también  
[ALTER INDEX &#40;Transact-SQL&#41;](~/t-sql/statements/alter-index-transact-sql.md)  
[Reorganizar y volver a generar índices](~/relational-databases/indexes/reorganize-and-rebuild-indexes.md)  
  

