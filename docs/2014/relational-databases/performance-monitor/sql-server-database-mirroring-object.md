---
title: Database Mirroring (objeto de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Database Mirroring
- database mirroring [SQL Server], performance counters
- performance counters [SQL Server], database mirroring
- Database Mirroring object
ms.assetid: a27b51ee-7637-4525-9424-bcc16947dc13
caps.latest.revision: 25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ff85c29870300199b33680dfc3edbf6c275688fa
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37273061"
---
# <a name="sql-server-database-mirroring-object"></a>Database Mirroring (objeto de SQL Server)
  El objeto de rendimiento **SQLServer:Creación de reflejo de la base de datos** contiene contadores de rendimiento que proporcionan información acerca de la creación de reflejo de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . En la siguiente tabla se enumeran los contadores incluidos en este objeto.  
  
|Nombre|Descripción|  
|----------|-----------------|  
|**Bytes recibidos/seg.**|Número de bytes recibidos por segundo.|  
|**Bytes enviados/seg.**|Número de bytes enviados por segundo.|  
|**Bytes de registro recibidos/s**|Número de bytes de registro recibidos por segundo.|  
|**Bytes de registro rehechos desde la caché/s**|Número de bytes de registro rehechos que se obtuvieron de la caché del registro de reflejo en el último segundo.<br /><br /> Este contador se utiliza solo en el servidor reflejado. En el servidor principal el valor es siempre 0.|  
|**Bytes de registro enviados desde la caché/s**|Número de bytes de registro enviados que se obtuvieron desde la caché del registro de reflejo en el último segundo.<br /><br /> Este contador se utiliza solo en el servidor principal. En el servidor reflejado el valor es siempre 0.|  
|**Bytes de registro enviados/seg.**|Número de bytes de registro enviados por segundo.|  
|**Bytes de registro comprimidos recibidos/s**|Número de bytes de registro comprimidos recibidos en el último segundo.|  
|**Bytes de registro comprimidos enviados/s**|Número de bytes de registro comprimidos enviados en el último segundo.|  
|**Tiempo de protección de registro (ms)**|Número de milisegundos que los bloques de registro esperaron a ser protegidos en el disco en el último segundo.|  
|**Número de KB de registro por deshacer**|Número total de kilobytes de registro que debe analizar el nuevo servidor reflejado tras la conmutación por error.<br /><br /> Este contador se utiliza solo en el servidor reflejado durante la fase de deshacer. Cuando finaliza la fase de deshacer, el contador se restablece en 0. En el servidor principal el valor es siempre 0.|  
|**Número de KB de registro examinados para deshacer**|Número total de kilobytes de registro que ha analizado el nuevo servidor reflejado desde la conmutación por error.<br /><br /> Este contador se utiliza solo en el servidor reflejado durante la fase de deshacer. Cuando finaliza la fase de deshacer, el contador se restablece en 0. En el servidor principal el valor es siempre 0.|  
|**Tiempo de control de flujo de envío de registro (ms)**|Número de milisegundos que los mensajes de secuencia de registro esperaron el control de flujo de envío en el último segundo.<br /><br /> El envío de datos y metadatos de registro al asociado de reflejo es la operación que más datos utiliza en el reflejo de base de datos y podría monopolizar los búferes de envío de reflejo de la base de datos y de Service Broker. Utilice este contador para supervisar el uso que hace la sesión de creación de reflejo de la base de datos de este búfer.|  
|**KB de envío de registro en cola**|Número total de kilobytes de registro que todavía no se han enviado al servidor reflejado.|  
|**Transacciones de escritura reflejadas/s**|Número de transacciones que se escribieron en la base de datos reflejada y esperaron a que el registro se enviara al servidor reflejado para confirmarse, en el último segundo.<br /><br /> Este contador solo se incrementa cuando el servidor principal está enviando activamente entradas de registro al servidor reflejado.|  
|**Páginas enviadas/seg.**|Número de páginas enviadas por segundo.|  
|**Recepciones/seg.**|Número de recepciones de mensajes reflejados por segundo.|  
|**Bytes rehechos/seg.**|Número de bytes de registro puestos al día en la base de datos reflejada por segundo.|  
|**KB de cola rehecha**|Número total de kilobytes de registro reforzado que aún están pendientes de aplicarse en la base de datos reflejada para ponerla al día. Se envía desde el servidor reflejado al servidor principal.|  
|**Tiempo de confirmación de Enviar/Recibir**|Milisegundos que esperaron los mensajes la confirmación del asociado en el último segundo.<br /><br /> Este contador es útil para solucionar un problema que podría producirse por un cuello de botella de la red, por ejemplo conmutaciones por error inexplicadas, una cola de envío grande o una elevada latencia de las transacciones. En casos como éste, puede analizar el valor de este contador para determinar si la red es la causa del problema.|  
|**Envíos/seg.**|Número de mensajes reflejados enviados por segundo.|  
|**Retraso de transacción**|Retraso en la espera de reconocimiento de confirmación no terminada.|  
  
> [!NOTE]  
>  En cada asociado, algunos contadores muestran el valor cero según el rol que realice el asociado en ese momento.  
  
## <a name="remarks"></a>Notas  
 Los contadores de rendimiento le permiten supervisar el rendimiento de la creación de reflejo de la base de datos. Por ejemplo, puede examinar el contador **Retraso de transacción** para ver si la creación de reflejo de la base de datos está afectando al rendimiento del servidor principal; puede examinar los contadores **Cola rehecha** y **Envío de registro en cola** para ver el comportamiento de la base de datos reflejada con respecto a la base de datos principal. Puede examinar el contador **Bytes de registro enviados/s** para supervisar la parte del registro enviada por segundo.  
  
## <a name="see-also"></a>Vea también  
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
