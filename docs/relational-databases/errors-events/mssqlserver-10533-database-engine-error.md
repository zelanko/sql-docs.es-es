---
title: MSSQLSERVER_10533 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10533 (Database Engine error)
ms.assetid: cc2fbdab-7b90-415f-a1f9-066824344283
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 061afedceeafdaf2660bf46180a80105d85e2a39
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060739"
---
# <a name="mssqlserver10533"></a>MSSQLSERVER_10533
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
## <a name="see-also"></a>Consulte también  
[Guías de plan](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
