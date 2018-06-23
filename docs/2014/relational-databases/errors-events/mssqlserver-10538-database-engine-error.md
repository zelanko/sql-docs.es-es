---
title: MSSQLSERVER_10538 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 10538 (Database Engine error)
ms.assetid: 284d19b4-4979-4cbe-a9be-ac1104433c69
caps.latest.revision: 9
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 2288e66d08120440e96864ecadf3cd775a01cf8c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111363"
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
  
  
