---
title: MSSQLSERVER_10519 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10519 (Database Engine error)
ms.assetid: 3be393a1-b186-41ae-afb9-a3d07ff354bb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6bb9c6f7fddc9ba0d4430b42ba5472a59c29e3cf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48141085"
---
# <a name="mssqlserver10519"></a>MSSQLSERVER_10519
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|10519|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_INCOMPATIBLE_STMT_AND_HINTS|  
|Texto del mensaje|No se puede crear la Guía de plan ' %. \*ls' porque las sugerencias especificadas en `@hints` no se puede aplicar a la instrucción especificada por `@stmt` o `@statement_start_offset`. Compruebe que las sugerencias pueden aplicarse a la instrucción.|  
  
## <a name="explanation"></a>Explicación  
 Las sugerencias especificadas en `@hints` no se pueden aplicar a la instrucción especificada por `@stmt` o `@statement_start_offset`.  
  
## <a name="user-action"></a>Acción del usuario  
 Especifique sugerencias que puedan aplicarse a la instrucción.  
  
## <a name="see-also"></a>Vea también  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [Guías de plan](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
