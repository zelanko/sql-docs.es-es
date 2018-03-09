---
title: MSSQLSERVER_3413 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 3413 (Database Engine error)
ms.assetid: 3fa07637-ba93-4633-aaf2-ade7d18bc487
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a80a7910d387e31efd48e487761a133c9598dfbd
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver3413"></a>MSSQLSERVER_3413
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|3413|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|MARKDB|  
|Texto del mensaje|Id. de base de datos %d. No se pudo marcar la base de datos como sospechosa. Error del recorrido con Getnext NC en sys.databases.database_id. Consulte los errores anteriores del registro de errores para identificar la causa y corregir cualquier problema relacionado.|  
  
## <a name="explanation"></a>Explicación  
Se produjo un error inesperado al intentar marcar una base de datos de usuario como SUSPECT en el catálogo. El estado SUSPECT no será persistente.  
  
## <a name="user-action"></a>Acción del usuario  
Vea los errores anteriores y solucione el problema.  
  
