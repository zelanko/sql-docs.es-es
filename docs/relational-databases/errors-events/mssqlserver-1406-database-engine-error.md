---
title: MSSQLSERVER_1406 | Microsoft Docs
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
helpviewer_keywords: 1406 (Database Engine error)
ms.assetid: 915f97de-9b74-41f8-8bd5-b2d061416718
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 19edf0ace27b35934e3a4d63c586893bd8cfc18f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver1406"></a>MSSQLSERVER_1406
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|1406|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBM_BADSTATEFORFORCESERVICE|  
|Texto del mensaje|No se puede forzar el servicio de forma segura. Quite el reflejo de la base de datos y recupere la base de datos "%.*ls" para obtener acceso.|  
  
## <a name="explanation"></a>Explicación  
El [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] no puede forzar el servicio porque el estado de creación de reflejo no puede garantizar que el proceso de forzar el servicio funcione correctamente.  
  
## <a name="user-action"></a>Acción del usuario  
Quite el reflejo de la base de datos. Después, puede recuperar la base de datos reflejada para obtener acceso a ella.  
  
## <a name="see-also"></a>Vea también  
[Forzar el servicio en una sesión de creación de reflejo de la base de datos &#40;Transact-SQL&#41;](~/database-engine/database-mirroring/force-service-in-a-database-mirroring-session-transact-sql.md)  
[Quitar la creación de reflejo de la base de datos &#40;SQL Server&#41;](~/database-engine/database-mirroring/removing-database-mirroring-sql-server.md)  
  
