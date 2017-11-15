---
title: MSSQLSERVER_10532 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 10532 (Database Engine error)
ms.assetid: 01da29ee-bf67-433f-8148-587a7e8d1d76
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: c7160413790d9bc783aac1eb517cb9afd1fa297b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver10532"></a>MSSQLSERVER_10532
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|10532|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_NO_ELIGIBLE_STMT|  
|Texto del mensaje|No se puede crear la guía de plan '%.\*ls' porque el lote o módulo especificado por **@plan_handle** no contiene una instrucción válida para una guía de plan. Especifique un valor distinto para **@plan_handle**.|  
  
## <a name="explanation"></a>Explicación  
El lote o módulo especificado por **@plan_handle** no contiene una instrucción válida para una guía de plan.  
  
## <a name="user-action"></a>Acción del usuario  
Especifique un valor distinto para **@plan_handle**.  
  
## <a name="see-also"></a>Vea también  
[Plan Guides](~/relational-databases/performance/plan-guides.md) (Guías de plan)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
