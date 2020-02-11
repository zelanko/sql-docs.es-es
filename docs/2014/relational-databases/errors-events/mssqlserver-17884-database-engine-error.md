---
title: MSSQLSERVER_17884 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17884 (Database Engine error)
ms.assetid: 8d05ba05-3f71-4dc3-bd81-2ea5ac9fe843
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e31c7a78b74a307bc4c57216ef6c87e989493519
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62915137"
---
# <a name="mssqlserver_17884"></a>MSSQLSERVER_17884
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|17884|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SRV_SCHEDULER_DEADLOCK|  
|Texto del mensaje|Un subproceso de trabajo no ha recogido las nuevas consultas asignadas al proceso en el nodo %d durante los últimos %d segundos. Puede que contribuya a ello la existencia de consultas de bloqueo o consultas que se ejecutan durante mucho tiempo, lo cual puede degradar el tiempo de respuesta del cliente. Utilice la opción de configuración "max worker threads" para aumentar el número de subprocesos permitidos u optimice las consultas que se estén ejecutando.  Uso del proceso de SQL: %d%%. Sistema inactivo: %d%%.|  
  
## <a name="explanation"></a>Explicación  
 No hay ningún signo de progreso en ninguno de los programadores y esto podría deberse a interbloqueos donde ninguno de los subprocesos puede avanzar, o a que no se ha elegido ni procesado ningún trabajo nuevo. Si la utilización del proceso es baja, otros procesos del equipo pueden estar ocasionando el colapso de la CPU del proceso de servidor.  
  
## <a name="user-action"></a>Acción del usuario  
 Determine por qué se está produciendo el bloqueo y no se observa ningún progreso, y resuelva la situación como corresponda. Si la utilización del proceso es baja, compruebe la carga del sistema ocasionada por otros procesos.  
  
  
