---
title: MSSQLSERVER_10539 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10539 (Database Engine error)
ms.assetid: 49c26ff7-18b8-4f07-a087-f45f63463b3b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 18fafa113002b4a2420ac8784c48451a1d69aa56
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62916070"
---
# <a name="mssqlserver_10539"></a>MSSQLSERVER_10539
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|10539|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_NO_PLAN_FOR_STMT|  
|Texto del mensaje|No se puede crear la guía de plan '%.*ls' a partir de la memoria caché porque no está disponible un plan de consulta para la instrucción con desplazamiento de inicio %d. Este problema puede producirse si la instrucción depende de objetos de base de datos que aún no se han creado. Asegúrese de que todos los objetos de base de datos necesarios existen y ejecute la instrucción antes de crear la guía de plan.|  
  
## <a name="explanation"></a>Explicación  
 No se dispone de un plan de consulta en la memoria caché de plan para la instrucción con el desplazamiento de inicio especificado.  
  
## <a name="user-action"></a>Acción del usuario  
 Asegúrese de que todos los objetos de base de datos necesarios existen y ejecute la instrucción antes de crear la guía de plan.  
  
## <a name="see-also"></a>Consulte también  
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
