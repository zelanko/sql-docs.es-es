---
title: MSSQLSERVER_10532 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10532 (Database Engine error)
ms.assetid: 01da29ee-bf67-433f-8148-587a7e8d1d76
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6d08c70c063142ff93e15464a04ddf156f290ea5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62985960"
---
# <a name="mssqlserver10532"></a>MSSQLSERVER_10532
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|10532|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_NO_ELIGIBLE_STMT|  
|Texto del mensaje|No se puede crear la guía de plan '%.\*ls' porque el lote o módulo especificado por **@plan_handle** no contiene una instrucción válida para una guía de plan. Especifique un valor distinto para **@plan_handle** .|  
  
## <a name="explanation"></a>Explicación  
El lote o módulo especificado por **@plan_handle** no contiene una instrucción válida para una guía de plan.  
  
## <a name="user-action"></a>Acción del usuario  
Especifique un valor distinto para **@plan_handle** .  
  
## <a name="see-also"></a>Consulte también  
[Guías de plan](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
