---
title: MSSQLSERVER_10536 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10536 (Database Engine error)
ms.assetid: 9f97b41f-0ef8-4ad2-aec0-906a5d7522ba
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e5ddb4df0089b488d3a15c76a76abef8be154848
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62870528"
---
# <a name="mssqlserver10536"></a>MSSQLSERVER_10536
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|10536|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_TOO_MANY_STMTS|  
|Texto del mensaje|No se puede crear la Guía de plan ' %. \*ls' porque el lote o módulo correspondiente al especificado `@plan_handle` contiene más de 1000 instrucciones válidas. Cree una guía de plan para cada instrucción en el lote o módulo especificando un valor `statement_start_offset` para cada instrucción.|  
  
## <a name="explanation"></a>Explicación  
 El lote o módulo correspondiente al identificador `@plan_handle` especificado contiene más de 1000 instrucciones válidas.  
  
## <a name="user-action"></a>Acción del usuario  
 Cree una guía de plan para cada instrucción en el lote o módulo especificando un valor `statement_start_offset` para cada instrucción.  
  
## <a name="see-also"></a>Vea también  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [Guías de plan](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
