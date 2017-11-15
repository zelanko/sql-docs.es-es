---
title: MSSQLSERVER_10521 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 10521 (Database Engine error)
ms.assetid: ba2d7e44-207c-4428-b5f0-c975ac122c0d
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: fd1bca867b0b6e5f6dbf26d892f48aa53b619c87
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver10521"></a>MSSQLSERVER_10521
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|10521|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_PARAM_NEEDED|  
|Texto del mensaje|No se puede crear la guía de plan '%.\*ls' porque se especificó **@type** como '%ls' y el valor del parámetro '%ls' es NULL. Este tipo requiere un valor no NULL para el parámetro. Especifique un valor no NULL para el parámetro o cambie el tipo por otro que admita un valor NULL para el parámetro.|  
  
## <a name="explanation"></a>Explicación  
El tipo especificado en **@type** requiere un valor distinto de NULL para el parámetro especificado; sin embargo, se proporcionó un valor NULL.  
  
## <a name="user-action"></a>Acción del usuario  
Especifique un valor no NULL para el parámetro o cambie el tipo por otro que admita un valor NULL para el parámetro.  
  
## <a name="see-also"></a>Vea también  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Plan Guides](~/relational-databases/performance/plan-guides.md) (Guías de plan)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
