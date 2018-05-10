---
title: MSSQLSERVER_3413 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 3413 (Database Engine error)
ms.assetid: 3fa07637-ba93-4633-aaf2-ade7d18bc487
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9cfa7a7f5b40767776c0db4ac58918ccf45080f4
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
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
  
