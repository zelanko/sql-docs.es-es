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
ms.openlocfilehash: b8c4e7237aa7ea39673b62543d77f9796c5bc46a
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554110"
---
# <a name="mssqlserver_10536"></a>MSSQLSERVER_10536
    
## <a name="details"></a>Detalles  
  
|Atributo|Value|  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|10536|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_TOO_MANY_STMTS|  
|Texto del mensaje|No se puede crear la Guía de plan '%.\*ls' porque el lote o módulo correspondiente al especificado `@plan_handle` contiene más de 1000 instrucciones válidas. Cree una guía de plan para cada instrucción en el lote o módulo especificando un valor `statement_start_offset` para cada instrucción.|  
  
## <a name="explanation"></a>Explicación  
 El lote o módulo correspondiente al identificador `@plan_handle` especificado contiene más de 1000 instrucciones válidas.  
  
## <a name="user-action"></a>Acción del usuario  
 Cree una guía de plan para cada instrucción en el lote o módulo especificando un valor `statement_start_offset` para cada instrucción.  
  
## <a name="see-also"></a>Consulte también  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [Guías de plan](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
