---
title: blocked process threshold (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- thresholds [SQL Server]
- blocked process threshold option
ms.assetid: 3d46d143-bc6a-4220-8b55-6baa37547c25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3901c87ebc217427e8d48f1cd299ba6831fa93b3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48148695"
---
# <a name="blocked-process-threshold-server-configuration-option"></a>blocked process threshold (opción de configuración del servidor)
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
  
## <a name="see-also"></a>Vea también  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Blocked Process Report (clase de eventos)](../../relational-databases/event-classes/blocked-process-report-event-class.md)  
  
  
