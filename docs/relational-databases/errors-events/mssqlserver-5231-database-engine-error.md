---
title: MSSQLSERVER_5231 | Microsoft Docs
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
- 5231 (Database Engine error)
ms.assetid: 6954ae84-ed0b-4f4c-9d0a-e73f3d71476c
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0d5aab03a10bd82bcf02b695ce84fa0e8381c2e7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver5231"></a>MSSQLSERVER_5231
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|5231|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC4_DEADLOCK_SKIPPED_OBJECT|  
|Texto del mensaje|Id. de objeto O_ID (objeto 'NAME'): Se ha producido un interbloqueo al intentar bloquear este objeto para la comprobación. Este objeto ha sido omitido y no se va a procesar.|  
  
## <a name="explanation"></a>Explicación  
Se ha producido un interbloqueo cuando DBCC intentaba bloquear el objeto; DBCC ha sido elegido como víctima del interbloqueo. El objeto no se procesará.  
  
## <a name="user-action"></a>Acción del usuario  
None  
  
