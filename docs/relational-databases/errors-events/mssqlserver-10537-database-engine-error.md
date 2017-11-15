---
title: MSSQLSERVER_10537 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 10537 (Database Engine error)
ms.assetid: 728469a4-6523-4a37-925f-a950d75420fa
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: c06cdb313b6b5872d244620042d61b9a23ec0161
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver10537"></a>MSSQLSERVER_10537
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|10537|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_DUP_ENABLED|  
|Texto del mensaje|No se puede habilitar la guía de plan '%.*ls' porque la guía de plan habilitada '%.\*ls' contiene el mismo ámbito y el mismo valor de desplazamiento de inicio que la instrucción. Deshabilite la guía de plan existente antes de habilitar la especificada.|  
  
## <a name="explanation"></a>Explicación  
Una guía de plan existente contiene el mismo ámbito y el mismo valor de desplazamiento de inicio que la instrucción de la guía de plan especificada.  
  
## <a name="user-action"></a>Acción del usuario  
Deshabilite la guía de plan existente antes de habilitar la especificada.  
  
## <a name="see-also"></a>Vea también  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Plan Guides](~/relational-databases/performance/plan-guides.md) (Guías de plan)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
