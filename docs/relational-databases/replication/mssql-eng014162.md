---
title: MSSQL_ENG014162 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014162 error
ms.assetid: a15eef3f-219f-45d3-8286-6a864c85a723
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 55e776eb45f31da4dfe60ac5bdeb148e458052ce
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37348677"
---
# <a name="mssqleng014162"></a>MSSQL_ENG014162
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|14162|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|Se ha establecido el umbral [%s:%s] para la publicación [%s]. Asegúrese de que el agente de mezcla se está ejecutando y cumple con el requisito esperado.|  
  
## <a name="explanation"></a>Explicación  
 La replicación le permite habilitar advertencias para varias condiciones. Incluye la superación de un período de tiempo específico para sincronizar cambios entre un publicador y suscriptor de mezcla. Se pueden especificar diferentes horas para las conexiones LAN y las de acceso telefónico.  
  
 Al habilitar una advertencia mediante el Monitor de replicación o [sp_replmonitorchangepublicationthreshold](../../relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql.md), especifica un umbral que determina cuándo se desencadena una advertencia. Cuando se alcanza o se supera un umbral, aparece una advertencia en el Monitor de replicación y se escribe un evento en el registro de eventos de Windows. Alcanzar un umbral también puede desencadenar una alerta del Agente SQL Server. Para obtener más información, vea [Establecer umbrales y advertencias en el Monitor de replicación](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md) y [Cómo supervisar la replicación mediante programación (programación con RMO)](../../relational-databases/replication/monitor/programmatically-monitor-replication.md).  
  
## <a name="user-action"></a>Acción del usuario  
 Si una suscripción supera un umbral de duración, debe determinar si hay algún problema de rendimiento en el sistema o si debe ajustarse el umbral. Una vez configurada la replicación, desarrolle una línea base de rendimiento que le permitirá determinar el comportamiento de la replicación con la carga de trabajo habitual de las aplicaciones y la topología. Incluya la duración de sincronización en esta línea base para poder establecer un valor adecuado para el umbral.  
  
 Si el valor del umbral es adecuado, pero está siendo superado, debe determinar dónde se encuentra el cuello de botella en el sistema. Para obtener más información acerca de cómo supervisar y solucionar problemas relacionados con el rendimiento de replicación, vea los temas siguientes:  
  
-   [Supervisar el rendimiento con el Monitor de replicación](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md), especialmente la sección "Ver detalles del rendimiento de la sincronización en la replicación de mezcla"  
  
## <a name="see-also"></a>Ver también  
 [Referencia de errores y eventos &#40;replicación&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
