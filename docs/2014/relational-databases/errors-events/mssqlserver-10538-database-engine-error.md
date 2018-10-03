---
title: MSSQLSERVER_10538 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10538 (Database Engine error)
ms.assetid: 284d19b4-4979-4cbe-a9be-ac1104433c69
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: aa6bce659e20fb80f013539049cc1b99e3e0b4c1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48055245"
---
# <a name="mssqlserver10538"></a>MSSQLSERVER_10538
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|10538|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_INVALID_PLANGUIDE_HANDLE|  
|Texto del mensaje|No se encuentra la guía de plan porque el Id. de guía de plan especificado es NULL o no es válido, o porque no tiene permiso para el objeto al que hace referencia la guía de plan. Compruebe que el id. de guía de plan es válido, la sesión actual está establecida en el contexto de base de datos correcto y que tiene permiso ALTER para el objeto al que hace referencia la guía de plan o el permiso ALTER DATABASE.|  
  
## <a name="explanation"></a>Explicación  
 El identificador de la guía de plan especificada es NULL o no es válido, o no se tiene permiso para el objeto al que hace referencia la guía de plan.  
  
## <a name="user-action"></a>Acción del usuario  
 Compruebe que el identificador de guía de plan es válido, la sesión actual está establecida en el contexto de base de datos correcto y se tiene el permiso ALTER DATABASE o ALTER para el objeto al que hace referencia la guía de plan.  
  
## <a name="see-also"></a>Vea también  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [Guías de plan](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
