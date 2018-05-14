---
title: Clase de eventos Umbral de la CPU superado | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: event-classes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- CPU Threshold Exceeded Event Class
ms.assetid: eb106f7d-baa3-4a2b-96b2-f9fe0844057d
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9a5522e2283e4e7856050cacc4db8cb8dd359967
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="cpu-threshold-exceeded-event-class"></a>Clase de eventos Umbral de la CPU superado
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Esta clase de eventos indica que el regulador de recursos ha detectado una consulta que supera el umbral de la CPU especificado para REQUEST_MAX_CPU_TIME_SEC.  
  
> [!NOTE]  
>  El intervalo para la detección de este evento es de cinco segundos. Está garantizado que se generará un evento si una consulta supera el límite especificado por lo menos en cinco segundos. Sin embargo, si una consulta supera el umbral especificado en menos de cinco segundos, es posible que se omita su detección dependiendo del tiempo de ejecución de la consulta y del momento en el que se llevó a cabo el último barrido para la detección.  
  
## <a name="cpu-threshold-exceeded-data-columns"></a>Columnas de datos del Umbral de la CPU superado  
  
|Nombre de columna de datos|Tipo de datos|Description|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|CPU|**int**|Uso de la CPU en milisegundos.|18|Sí|  
|EventClass|**int**|214|27|no|  
|EventSubClass|**int**|Infracción del límite de la CPU.|21|Sí|  
|GroupID|**int**|Id. del grupo donde se produjo la infracción.|66|Sí|  
|OwnerID|**int**|SPID del proceso que produjo la infracción.|58|Sí|  
|SPID|**int**|Id. del proceso de servidor que dispara este evento.<br /><br /> Nota: Este puede ser diferente al SPID del usuario actual si un subproceso del sistema valida el uso de la CPU como una tarea en segundo plano.|12|Sí|  
|StartTime|**datetime**|El momento en el que se desencadenó este evento.|14|Sí|  
  
## <a name="see-also"></a>Ver también  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
