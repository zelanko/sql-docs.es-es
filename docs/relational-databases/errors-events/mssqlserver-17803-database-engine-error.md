---
title: MSSQLSERVER_17803 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 17803 (Database Engine error)
ms.assetid: 28591a19-258d-4891-b78a-4686789bb2d7
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 84dad82e56f418813c5a6ddfaf5425b3b9aec9f8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver17803"></a>MSSQLSERVER_17803
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|17803|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SRV_NOMEMORY|  
|Texto del mensaje|Error de asignación de memoria durante el establecimiento de la conexión. Reduzca la carga de memoria no esencial o aumente la memoria del sistema. Se cerró la conexión.%.*ls|  
  
## <a name="explanation"></a>Explicación  
El servidor se está quedando sin memoria.  
  
## <a name="user-action"></a>Acción del usuario  
Determine la causa por la que el servidor se está quedando sin memoria. Puede ser útil seguir un procedimiento para solucionar problemas genéricos de memoria  
  
