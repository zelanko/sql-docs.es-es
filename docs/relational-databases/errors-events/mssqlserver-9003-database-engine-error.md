---
title: MSSQLSERVER_9003 | Microsoft Docs
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
- 9003 (Database Engine error)
ms.assetid: 7fdfb391-5c6f-428b-b434-6c3d0b30fd7b
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 27d2fbf1bed8445eb8d3fd42000128741d2ee377
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver9003"></a>MSSQLSERVER_9003
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|9003|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|LOG_INVALID_LSN|  
|Texto del mensaje|El número de examen del registro %S_LSN pasado al examen del registro de la base de datos '%.*ls' no es válido. Este error puede indicar daños en los datos o que el archivo de registro (.ldf) no coincide con el archivo de datos (.mdf). Si esto error se produjo durante la replicación, vuelva a crear la publicación. De lo contrario, restaure la base de datos a partir de una copia de seguridad si el problema da lugar a un error durante el inicio.|  
  
## <a name="explanation"></a>Explicación  
Un componente pasó un número de flujo de registro no válido al administrador de registros para la base de datos. Podría corresponder a la replicación, a daños o a una incoherencia entre el archivo de datos principal y el registro.  
  
## <a name="user-action"></a>Acción del usuario  
Si esto ocurrió durante la replicación, vuelva a crear la publicación. De lo contrario, restaure una copia de seguridad.  
  

