---
title: MSSQL_ENG014164 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014164 error
ms.assetid: cd81b601-2ec3-4358-ad58-c2655496e6a1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ddf88cbdfd25d77ca3f2eadf4176309d02a084e6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049105"
---
# <a name="mssql_eng014164"></a>MSSQL_ENG014164
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|14164|  
|Origen de eventos|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|Se ha establecido el umbral [%s:%s] para la publicación [%s]. Asegúrese de que el agente de mezcla se está ejecutando y cumple con el requisito esperado.|  
  
## <a name="explanation"></a>Explicación  
 La replicación le permite habilitar advertencias para varias condiciones. Incluye el error al procesar un número suficiente de filas al sincronizar cambios entre un suscriptor y un publicador de mezcla. Se pueden especificar diferentes horas para las conexiones LAN y las de acceso telefónico.  
  
 Al habilitar una advertencia mediante el Monitor de replicación o [sp_replmonitorchangepublicationthreshold](/sql/relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql), especifica un umbral que determina cuándo se desencadena una advertencia. Cuando se alcanza o se supera un umbral, aparece una advertencia en el Monitor de replicación y se escribe un evento en el registro de eventos de Windows. Alcanzar un umbral también puede desencadenar una alerta del Agente SQL Server. Para obtener más información, vea [Establecer umbrales y advertencias en el Monitor de replicación](monitor/set-thresholds-and-warnings-in-replication-monitor.md) y [Cómo supervisar la replicación mediante programación (programación con RMO)](monitoring-replication.md).  
  
## <a name="user-action"></a>Acción del usuario  
 Si una suscripción no cumple un umbral de procesamiento de filas, debe determinar si hay algún problema de rendimiento en el sistema o si debe ajustarse el umbral. Una vez configurada la replicación, desarrolle una línea base de rendimiento que le permitirá determinar el comportamiento de la replicación con la carga de trabajo habitual de las aplicaciones y la topología. Incluya el número de filas procesadas en esta línea base para poder establecer un valor adecuado para el umbral.  
  
 Si el valor del umbral es adecuado, pero está siendo superado, debe determinar dónde se encuentra el cuello de botella en el sistema. Para obtener más información acerca de cómo supervisar y solucionar problemas relacionados con el rendimiento de replicación, vea los temas siguientes:  
  
-   [Supervisar el rendimiento con el Monitor de replicación](monitor/monitor-performance-with-replication-monitor.md), especialmente la sección "Ver detalles del rendimiento de la sincronización en la replicación de mezcla"  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y eventos &#40;replicación&#41;](errors-and-events-reference-replication.md)  
  
  
