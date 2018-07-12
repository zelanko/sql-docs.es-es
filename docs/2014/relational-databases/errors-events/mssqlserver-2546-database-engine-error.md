---
title: MSSQLSERVER_2546 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 2546 (Database Engine error)
ms.assetid: c8f0e1b4-c7c4-45f2-9221-746714172313
caps.latest.revision: 20
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e9497598b38a7bb13b76e6e54d0b0696cb56990e
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37427084"
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
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [Reorganizar y volver a generar índices](../indexes/indexes.md)  
  
  
