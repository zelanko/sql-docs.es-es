---
title: MSSQLSERVER_3413 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 3413 (Database Engine error)
ms.assetid: 3fa07637-ba93-4633-aaf2-ade7d18bc487
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 0c98db87f49ef52d68e49b8553a09b77fb18b3f0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver3413"></a>MSSQLSERVER_3413
  
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
  
