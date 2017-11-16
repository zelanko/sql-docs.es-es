---
title: MSSQLSERVER_10520 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 10520 (Database Engine error)
ms.assetid: cc8799f1-5b90-4248-b209-e1d5087f9529
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 05acd414289507544caa7ae5806471982768949e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver10520"></a>MSSQLSERVER_10520
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|10520|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_PARAM_NOT_ALLOWED|  
|Texto del mensaje|No se puede crear la guía de plan '%.*ls' porque @type se especificó como '%ls' y se especificó un valor no NULL para el parámetro '%ls'. Este tipo requiere un valor NULL para el parámetro. Especifique NULL para el parámetro o cambie el tipo por otro que admita un valor no NULL para el parámetro.|  
  
## <a name="explanation"></a>Explicación  
El tipo especificado en @type requiere un valor NULL para el parámetro especificado; sin embargo, se proporcionó un valor distinto de NULL.  
  
## <a name="user-action"></a>Acción del usuario  
Especifique NULL para el parámetro o cambie el tipo por otro que admita un valor no NULL para el parámetro.  
  
## <a name="see-also"></a>Vea también  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Plan Guides](~/relational-databases/performance/plan-guides.md) (Guías de plan)  
  
