---
title: MSSQLSERVER_10534 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 10534 (Database Engine error)
ms.assetid: e65bb118-99d5-4fdb-b1d5-0ec70f0a677b
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 153227c6d24d6c73e89f09820110b514192c2736
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver10534"></a>MSSQLSERVER_10534
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|10534|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_INVALID_PARAMS|  
|Texto del mensaje|No se puede crear la guía de plan '%.\*ls' porque el valor especificado para **@params** no es válido. Especifique el valor con la sintaxis *parameter_name parameter_type*, o especifique NULL.|  
  
## <a name="explanation"></a>Explicación  
El valor especificado para **@params** no es válido.  
  
## <a name="user-action"></a>Acción del usuario  
Especifique el valor con la sintaxis *parameter_name parameter_type*, o especifique NULL.  
  
## <a name="see-also"></a>Vea también  
[Plan Guides](~/relational-databases/performance/plan-guides.md) (Guías de plan)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
