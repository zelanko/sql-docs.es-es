---
title: MSSQLSERVER_10536 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 10536 (Database Engine error)
ms.assetid: 9f97b41f-0ef8-4ad2-aec0-906a5d7522ba
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 00ca6874fc2b46c1b01495c5c7a0808265b0dd77
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37428954"
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
  
  
