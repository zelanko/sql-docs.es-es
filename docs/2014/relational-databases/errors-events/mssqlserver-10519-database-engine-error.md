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
ms.openlocfilehash: 0ec584649842f787b1de9d2ea6d161aea6970250
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84947775"
---
# <a name="mssqlserver_10519"></a>MSSQLSERVER_10519
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|10519|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_INCOMPATIBLE_STMT_AND_HINTS|  
|Texto del mensaje|No se puede crear la guía de plan '%.\*ls' porque las sugerencias especificadas en `@hints` no se pueden aplicar a la instrucción especificada por `@stmt` o `@statement_start_offset`. Compruebe que las sugerencias pueden aplicarse a la instrucción.|  
  
## <a name="explanation"></a>Explicación  
 Las sugerencias especificadas en `@hints` no se pueden aplicar a la instrucción especificada por `@stmt` o `@statement_start_offset`.  
  
## <a name="user-action"></a>Acción del usuario  
 Especifique sugerencias que puedan aplicarse a la instrucción.  
  
## <a name="see-also"></a>Consulte también  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [Guías de plan](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
