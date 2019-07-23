---
title: blocked process threshold (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- thresholds [SQL Server]
- blocked process threshold option
ms.assetid: 3d46d143-bc6a-4220-8b55-6baa37547c25
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 84a94dc6b1d4f2f6f0c921f81746eb64f41d2f07
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68013114"
---
# <a name="blocked-process-threshold-server-configuration-option"></a>blocked process threshold (opción de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Utilice la opción **blocked process threshold** (umbral de proceso bloqueado) para especificar el umbral, en segundos, con el que se generan los informes de procesos bloqueados. El umbral puede establecerse en un valor comprendido entre 0 y 86.400. De manera predeterminada, se producen informes de procesos no bloqueados. Este evento no se genera para las tareas del sistema o las tareas que están esperando en recursos que no generan interbloqueos detectables.  
  
 Puede definir una [alerta](../../ssms/agent/alerts.md) para que se ejecute cuando se genera este evento. Por ejemplo, puede elegir que se envíe un aviso al localizador del administrador para que tome la acción adecuada en una situación de bloqueo.  
  
 El umbral de proceso bloqueado utiliza el subproceso en segundo plano de supervisión de interbloqueos para desplazarse por la lista de tareas a la espera de un tiempo superior al del umbral configurado o múltiplo de ese tiempo. El evento se genera una vez por intervalo de informe para cada tarea bloqueada.  
  
 El informe de procesos bloqueados se realiza de la mejor forma posible. No existe ninguna garantía de que los informes generados muestren resultados en tiempo real.  
  
 La configuración surte efecto inmediatamente, sin necesidad de detener y reiniciar el servidor.  
  
## <a name="examples"></a>Ejemplos  
 El siguiente ejemplo establece `blocked process threshold` en `20` segundos y genera un informe de proceso bloqueado para cada tarea bloqueada.  
  
```  
sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE ;  
GO  
sp_configure 'blocked process threshold', 20 ;  
GO  
RECONFIGURE ;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Blocked Process Report (clase de eventos)](../../relational-databases/event-classes/blocked-process-report-event-class.md)  
  
  
