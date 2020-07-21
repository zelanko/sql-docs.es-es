---
title: MSSQLSERVER_10531 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10531 (Database Engine error)
ms.assetid: bb40e994-231c-44ce-933f-8d767fb2f450
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8de08a9760b1df4d3c8be4d57009e0bcb2d71b6e
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554160"
---
# <a name="mssqlserver_10531"></a>MSSQLSERVER_10531
    
## <a name="details"></a>Detalles  
  
|Atributo|Value|  
|-|-|  
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
 [Guías de plan](../performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
