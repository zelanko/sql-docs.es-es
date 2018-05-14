---
title: MSSQLSERVER_9001 | Microsoft Docs
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
- 9001 (Database Engine error)
ms.assetid: a54de936-90c6-4845-aa96-29d32f154601
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 73d355fff56057297468319f4434714c09536e0e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver9001"></a>MSSQLSERVER_9001
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|9001|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|LOG_NOT_AVAIL|  
|Texto del mensaje|El registro de la base de datos '%.*ls' no está disponible. Vea los mensajes de error relacionados en el registro de eventos. Corrija los errores y reinicie la base de datos.|  
  
## <a name="explanation"></a>Explicación  
El registro de la base de datos se dejó sin conexión. Normalmente esto indica un error grave que requiere reiniciar la base de datos.  
  
## <a name="user-action"></a>Acción del usuario  
Diagnostique otros errores y reinicie la sesión de SQL Server si aún no se ha reiniciado.  
  
