---
title: MSSQLSERVER_8712 | Microsoft Docs
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
- 8712 (Database Engine error)
ms.assetid: 292fb3bc-062e-41e4-a566-b5d3d0b21977
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 65489fa755c5dda3459d7de227631591f821e5bd
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver8712"></a>MSSQLSERVER_8712
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|8712|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|USEPLAN_ERR_NO_INDEX|  
|Texto del mensaje|El índice '%.*ls', especificado en la sugerencia USE PLAN, no existe. Especifique un índice existente o cree un índice con el nombre especificado.|  
  
## <a name="explanation"></a>Explicación  
Uno de los índices que se especifican en la sugerencia USE PLAN no existe.  
  
## <a name="user-action"></a>Acción del usuario  
Asegurarse de que todos los índices que se especifican en la sugerencia USE PLAN existen.  
  
## <a name="see-also"></a>Vea también  
[Sugerencias de consulta &#40;Transact-SQL&#41;](~/t-sql/queries/hints-transact-sql-query.md)  
[Plan Guides](~/relational-databases/performance/plan-guides.md) (Guías de plan)  
  

