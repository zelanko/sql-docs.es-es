---
title: MSSQLSERVER_10502 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10502 (Database Engine error)
ms.assetid: 26d9b64d-4299-4b55-92d0-0a32a3688c0a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 42b4a39678e4b85e581bca7e1b9e085c6f4620f2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48089115"
---
# <a name="mssqlserver10502"></a>MSSQLSERVER_10502
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|10502|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_DUP_FOUND|  
|Texto del mensaje|No se puede crear la guía de plan '%.*ls' porque la instrucción especificada por @stmt y @module_or_batch, o por @plan_handle y @statement_start_offset, coincide con la guía de plan '%.\*ls' existente en la base de datos. Quite la guía de plan existente antes de crear la nueva.|  
  
## <a name="explanation"></a>Explicación  
 Existe una guía de plan para la instrucción especificada.  
  
## <a name="user-action"></a>Acción del usuario  
 Quite la guía de plan existente antes de crear la nueva.  
  
## <a name="see-also"></a>Vea también  
 [Guías de plan](../performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
