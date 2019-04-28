---
title: MSSQLSERVER_10521 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10521 (Database Engine error)
ms.assetid: ba2d7e44-207c-4428-b5f0-c975ac122c0d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ecaffb9e40024eca7cbeac77f4b50058e5440cee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62870614"
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
|Texto del mensaje|No se puede crear la Guía de plan ' %. \*ls' porque `@type` se especificó como '%ls' y el parámetro '%ls' es NULL. Este tipo requiere un valor no NULL para el parámetro. Especifique un valor no NULL para el parámetro o cambie el tipo por otro que admita un valor NULL para el parámetro.|  
  
## <a name="explanation"></a>Explicación  
 El tipo especificado en `@type` requiere un valor no NULL para el parámetro especificado; sin embargo, se proporcionó un valor NULL.  
  
## <a name="user-action"></a>Acción del usuario  
 Especifique un valor no NULL para el parámetro o cambie el tipo por otro que admita un valor NULL para el parámetro.  
  
## <a name="see-also"></a>Vea también  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [Guías de plan](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
