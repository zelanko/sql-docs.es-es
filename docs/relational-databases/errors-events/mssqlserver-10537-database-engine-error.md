---
title: MSSQLSERVER_10537 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10537 (Database Engine error)
ms.assetid: 728469a4-6523-4a37-925f-a950d75420fa
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4a3dfb73f5ca3b073cf0d5ded864669f977c6aee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63048587"
---
# <a name="mssqlserver10537"></a>MSSQLSERVER_10537
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
## <a name="see-also"></a>Consulte también  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Guías de plan](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
