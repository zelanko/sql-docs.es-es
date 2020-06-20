---
title: MSSQLSERVER_10532 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10532 (Database Engine error)
ms.assetid: 01da29ee-bf67-433f-8148-587a7e8d1d76
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 26ab34c319eff62737eae337828247fdfd7e901b
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968145"
---
# <a name="mssqlserver_10532"></a>MSSQLSERVER_10532
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|10532|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_NO_ELIGIBLE_STMT|  
|Texto del mensaje|No se puede crear la guía de plan '%.\*ls' porque el lote o módulo especificado por `@plan_handle` no contiene una instrucción válida para una guía de plan. Especifique un valor distinto para `@plan_handle`.|  
  
## <a name="explanation"></a>Explicación  
 El lote o módulo especificado por `@plan_handle` no contiene una instrucción válida para una guía de plan.  
  
## <a name="user-action"></a>Acción del usuario  
 Especifique un valor distinto para `@plan_handle`.  
  
## <a name="see-also"></a>Consulte también  
 [Guías de plan](../performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
