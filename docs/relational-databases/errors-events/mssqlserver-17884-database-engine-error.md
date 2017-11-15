---
title: MSSQLSERVER_17884 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 17884 (Database Engine error)
ms.assetid: 8d05ba05-3f71-4dc3-bd81-2ea5ac9fe843
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 0809cba2c3c48822d21c181e0e0cb482fc7aa169
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver17884"></a>MSSQLSERVER_17884
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|17884|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SRV_SCHEDULER_DEADLOCK|  
|Texto del mensaje|Un subproceso de trabajo no ha recogido las nuevas consultas asignadas al proceso en el nodo %d durante los últimos %d segundos. Puede que contribuya a ello la existencia de consultas de bloqueo o consultas que se ejecutan durante mucho tiempo, lo cual puede degradar el tiempo de respuesta del cliente. Utilice la opción de configuración "max worker threads" para aumentar el número de subprocesos permitidos u optimice las consultas que se estén ejecutando.  Uso del proceso de SQL: %d%%. Sistema inactivo: %d%%.|  
  
## <a name="explanation"></a>Explicación  
No hay ningún signo de progreso en ninguno de los programadores y esto podría deberse a interbloqueos donde ninguno de los subprocesos puede avanzar, o a que no se ha elegido ni procesado ningún trabajo nuevo. Si la utilización del proceso es baja, otros procesos del equipo pueden estar ocasionando el colapso de la CPU del proceso de servidor.  
  
## <a name="user-action"></a>Acción del usuario  
Determine por qué se está produciendo el bloqueo y no se observa ningún progreso, y resuelva la situación como corresponda. Si la utilización del proceso es baja, compruebe la carga del sistema ocasionada por otros procesos.  
  
