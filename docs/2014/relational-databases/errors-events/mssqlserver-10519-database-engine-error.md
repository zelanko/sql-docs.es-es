---
title: MSSQLSERVER_10519 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 10519 (Database Engine error)
ms.assetid: 3be393a1-b186-41ae-afb9-a3d07ff354bb
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2ff20cdde06a1ee100d711aeab2612f2ef4625f0
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37422424"
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
  
  
