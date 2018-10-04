---
title: MSSQLSERVER_10533 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10533 (Database Engine error)
ms.assetid: cc2fbdab-7b90-415f-a1f9-066824344283
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 86bd82dfd095baeacb35f8454859adb938123f52
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48066345"
---
# <a name="mssqlserver10533"></a>MSSQLSERVER_10533
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|10533|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_NAME_TOO_BIG|  
|Texto del mensaje|No se puede crear la guía de plan '%.*ls' porque su nombre supera el número máximo de caracteres permitido, 124. Especifique un nombre que contenga menos de 125 caracteres.|  
  
## <a name="explanation"></a>Explicación  
 El nombre de la guía de plan supera 124 caracteres, el número máximo permitido.  
  
## <a name="user-action"></a>Acción del usuario  
 Especifique un nombre que contenga menos de 125 caracteres.  
  
## <a name="see-also"></a>Vea también  
 [Guías de plan](../performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
