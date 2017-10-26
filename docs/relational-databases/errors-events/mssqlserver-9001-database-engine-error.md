---
title: MSSQLSERVER_9001 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 9001 (Database Engine error)
ms.assetid: a54de936-90c6-4845-aa96-29d32f154601
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1eaae857105a13a133c2fc9cd216d701df9f51d5
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver9001"></a>MSSQLSERVER_9001
  
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
  

