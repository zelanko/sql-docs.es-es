---
title: MSSQLSERVER_10531 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10531 (Database Engine error)
ms.assetid: bb40e994-231c-44ce-933f-8d767fb2f450
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1706e67643b2f0c5360399b13a38b5dcec57d9ce
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85781463"
---
# <a name="mssqlserver_10531"></a>MSSQLSERVER_10531
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|10531|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_NO_ELIGIBLE_STMT|  
|Texto del mensaje|No se puede crear la guía de plan '%.*ls' a partir de la memoria caché porque el usuario no tiene los permisos adecuados. Conceda el permiso VIEW SERVER STATE al usuario que va a crear la guía de plan.|  
  
## <a name="explanation"></a>Explicación  
El usuario no tiene los permisos adecuados para crear la guía de plan especificada a partir de la memoria caché.  
  
## <a name="user-action"></a>Acción del usuario  
Conceda el permiso VIEW SERVER STATE al usuario que va a crear la guía de plan.  
  
## <a name="see-also"></a>Consulte también  
[Guías de plan](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
