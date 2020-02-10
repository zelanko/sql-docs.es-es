---
title: MSSQLSERVER_2546 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2546 (Database Engine error)
ms.assetid: c8f0e1b4-c7c4-45f2-9221-746714172313
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ca1a8af843d0183acd46a8b11e00427738d59d0e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62868856"
---
# <a name="mssqlserver_2546"></a>MSSQLSERVER_2546
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|2546|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC_INDEX_MARKED_DISABLED|  
|Texto del mensaje|El índice 'INDEX_NAME' de la tabla 'OBJECT_NAME' está marcado como deshabilitado. Genere de nuevo el índice para ponerlo en línea.|  
  
## <a name="explanation"></a>Explicación  
 El índice especificado está marcado como sin conexión o está deshabilitado. Por tanto, este índice no se puede comprobar.  
  
## <a name="user-action"></a>Acción del usuario  
 Vuelva a generar el índice usando ALTER INDEX.  
  
## <a name="see-also"></a>Consulte también  
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [Reorganizar y volver a generar índices](../indexes/indexes.md)  
  
  
