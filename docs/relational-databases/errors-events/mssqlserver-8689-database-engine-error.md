---
title: MSSQLSERVER_8689 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 8689 (Database Engine error)
ms.assetid: 99467a32-6576-4272-a076-b16c06933f2a
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9bde8c78bcece74c17820bb11390c048355e4d5a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver8689"></a>MSSQLSERVER_8689
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|8689|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|USEPLAN_ERR_NO_DB|  
|Texto del mensaje|La base de datos '%.*ls' especificada en la sugerencia USE PLAN no existe. Especifique una base de datos existente.|  
  
## <a name="explanation"></a>Explicación  
Una de las bases de datos que se especifican en la sugerencia USE PLAN no existe.  
  
## <a name="user-action"></a>Acción del usuario  
Asegúrese de que todas las bases de datos que se especifican en la sugerencia USE PLAN existen.  
  
## <a name="see-also"></a>Vea también  
[Sugerencias de consulta &#40;Transact-SQL&#41;](~/t-sql/queries/hints-transact-sql-query.md)  
[Plan Guides](~/relational-databases/performance/plan-guides.md) (Guías de plan)  
  
