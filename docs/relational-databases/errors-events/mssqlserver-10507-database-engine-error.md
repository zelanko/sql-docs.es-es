---
title: MSSQLSERVER_10507 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 10507 (Database Engine error)
ms.assetid: cd83fa81-ac37-4eda-a3c3-17610b051de2
caps.latest.revision: 9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 90d22a2b85d2f6257af927158484af8927a4ce11
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver10507"></a>MSSQLSERVER_10507
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|10507|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_STMT_DOES_NOT_MATCH|  
|Texto del mensaje|No se puede crear la guía de plan '%.\*ls' porque la instrucción especificada por **@stmt** y **@module_or_batch**, o por **@plan_handle** y **@statement_start_offset**, no coincide con ninguna instrucción del módulo o lote especificado. Modifique los valores para que coincidan con una instrucción del módulo o lote.|  
  
## <a name="explanation"></a>Explicación  
Una instrucción en el módulo o lote especificado no se pudo hacer coincidir con la instrucción o valor de desplazamiento de instrucción especificados.  
  
## <a name="user-action"></a>Acción del usuario  
Modifique los valores de los parámetros especificados para que coincidan con una instrucción del módulo o lote.  
  
## <a name="see-also"></a>Ver también  
[Guías de plan](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
