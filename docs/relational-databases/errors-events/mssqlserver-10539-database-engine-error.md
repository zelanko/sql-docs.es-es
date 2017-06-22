---
title: MSSQLSERVER_10539 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 10539 (Database Engine error)
ms.assetid: 49c26ff7-18b8-4f07-a087-f45f63463b3b
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5d54a85fe2f839e2339234b790acda4e1df0c549
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver10539"></a>MSSQLSERVER_10539
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|10539|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_NO_PLAN_FOR_STMT|  
|Texto del mensaje|No se puede crear la guía de plan '%.*ls' a partir de la memoria caché porque no está disponible un plan de consulta para la instrucción con desplazamiento de inicio %d. Este problema puede producirse si la instrucción depende de objetos de base de datos que aún no se han creado. Asegúrese de que todos los objetos de base de datos necesarios existen y ejecute la instrucción antes de crear la guía de plan.|  
  
## <a name="explanation"></a>Explicación  
No se dispone de un plan de consulta en la memoria caché de plan para la instrucción con el desplazamiento de inicio especificado.  
  
## <a name="user-action"></a>Acción del usuario  
Asegúrese de que todos los objetos de base de datos necesarios existen y ejecute la instrucción antes de crear la guía de plan.  
  
## <a name="see-also"></a>Vea también  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  

