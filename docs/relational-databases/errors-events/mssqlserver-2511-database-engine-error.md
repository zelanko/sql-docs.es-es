---
title: MSSQLSERVER_2511 | Microsoft Docs
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
- 2511 (Database Engine error)
ms.assetid: 9a00c0ed-eb4b-4fae-8016-192396006c37
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 78294d9d2343d5b17cf7be0473e778fbd060ed20
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver2511"></a>MSSQLSERVER_2511
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|2511|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC_KEYS_OUT_OF_ORDER|  
|Texto del mensaje|Error de tabla: id. de objeto %d, id. de índice %d, id. de partición %I64d, id. de unidad de asignación %I64d (tipo %.*ls). Las claves no están ordenadas en la página %S_PGID, zonas %d y %d.|  
  
## <a name="explanation"></a>Explicación  
Se detectaron claves desordenadas en el índice especificado. La página en la que están las claves puede estar dañada.  
  
## <a name="user-action"></a>Acción del usuario  
Vuelva a generar el índice especificado usando la instrucción ALTER INDEX REBUILD.  
  
