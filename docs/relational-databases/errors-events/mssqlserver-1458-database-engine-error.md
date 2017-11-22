---
title: MSSQLSERVER_1458 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 1458 (Database Engine error)
ms.assetid: adc78c59-a6f2-432b-9a07-fdd1dc2b9026
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 64e6c7221c95e0e7ad5622a896d113d779ad4538
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver1458"></a>MSSQLSERVER_1458
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|1458|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBM_FAILREDO_ON_PRIMARY|  
|Texto del mensaje|La copia principal de la base de datos '%.*ls' encontró el error %d, el estado %d y la gravedad %d. Se suspendió la creación de reflejos de la base de datos. Intente resolver la condición de error y reanude la creación de reflejo.|  
  
## <a name="explanation"></a>Explicación  
Este mensaje indica que la base de datos principal encontró un error que ocasionó la suspensión de la creación de reflejo de la base de datos.  
  
## <a name="user-action"></a>Acción del usuario  
En la mayoría de los casos, este error se corrige automáticamente. Si el problema continúa, el reinicio de la instancia de la base de datos o del servidor normalmente corrige el problema. Para obtener más información, busque el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de cada asociado para el error asociado que precedía a este mensaje.  
  
## <a name="see-also"></a>Vea también  
[Supervisar la creación de reflejo de la base de datos &#40;SQL Server&#41;](~/database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)  
  
