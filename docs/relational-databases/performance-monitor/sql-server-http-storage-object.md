---
title: SQL Server, HTTP_STORAGE_OBJECT | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ae849f79-c581-42a5-a5cc-0a9ebea171b9
caps.latest.revision: 7
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ea717edbbed863b262617e457ac29fc3d45a4be4
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-httpstorageobject"></a>SQL Server, HTTP_STORAGE_OBJECT
  El objeto de rendimiento de **SQLServer:HTTP_STORAGE_OBJECT** está compuesto de contadores de rendimiento que supervisan la cuenta de almacenamiento de Microsoft Azure. Si usa la característica [Archivos de datos de SQL Server de Microsoft Azure](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md) , puede almacenar archivos de base de datos en los blobs de almacenamiento de Microsoft Azure. Este objeto de rendimiento trata cada cuenta de Almacenamiento de Windows Azure como una unidad diferente.  
  
|Nombre de contador|Descripción|  
|------------------|-----------------|  
|**Lectura de bytes/seg**|Cantidad de datos que se transfieren desde almacenamiento HTTP por segundo durante las operaciones de lectura.|  
|**Escritura de bytes/seg**|Cantidad de datos que se transfieren desde almacenamiento HTTP por segundo durante las operaciones de escritura.|  
|**Total de bytes/seg**|Cantidad de datos que se transfieren desde almacenamiento HTTP por segundo durante las operaciones de lectura o escritura.|  
|**Lecturas/seg**|Número de lecturas por segundo en el almacenamiento HTTP.|  
|**lógicas/s**|Número de escrituras por segundo en el almacenamiento HTTP.|  
|**Transferencias/seg**|Número de operaciones de lectura y escritura por segundo en el almacenamiento HTTP.|  
|**Avg. bytes/lectura**|Promedio de bytes transferidos desde el almacenamiento HTTP por lectura.|  
|**Avg. bytes/lectura BASE**|Exclusivamente para uso interno.|
|**Avg. bytes/transferidos**|Promedio de bytes transferidos desde el almacenamiento HTTP durante las operaciones de lectura o escritura.|  
|**Avg. bytes/transferidos BASE**|Exclusivamente para uso interno.|
|**Avg. bytes/escritura**|Promedio de bytes transferidos desde el almacenamiento HTTP por escritura.|  
|**Avg. bytes/escritura BASE**|Exclusivamente para uso interno.|
|**Promedio de microsegundos/lectura**|Promedio de microsegundos que invierten en realizar cada lectura desde el almacenamiento HTTP.|  
|**Promedio de microsegundos/lectura BASE**|Exclusivamente para uso interno.|
|**Promedio de microsegundos/lectura comp**|El promedio de microsegundos que HTTP tarda en completar la lectura para el almacenamiento.| 
|**Promedio de microsegundos/lectura comp BASE**|Exclusivamente para uso interno.|
|**Promedio de microsegundos/escritura**|Promedio de microsegundos que se invierten en realizar cada escritura en el almacenamiento HTTP.|  
|**Promedio de microsegundos/transferencia**|Promedio de microsegundos que se invierten en realizar cada transferencia en el almacenamiento HTTP.|  
|**Promedio de microsegundos/transferencia BASE**|Exclusivamente para uso interno.|
|**Promedio de microsegundos/escritura BASE**|Exclusivamente para uso interno.|
|**Promedio de microsegundos/escritura comp**|El promedio de microsegundos que HTTP tarda en completar la escritura para el almacenamiento.|  
|**Promedio de microsegundos/escritura comp BASE**|Exclusivamente para uso interno.|
|**E/S pendiente de almacenamiento HTTP**|Número total de E/S pendientes para su almacenamiento HTTP.|  
|**E/S de almacenamiento HTTP erróneas/s**|Número de solicitudes de escritura erróneas enviadas al almacenamiento HTTP por segundo.| 
|**Error/seg de E/S de almacenamiento HTTP**|Número de solicitudes de reintento enviadas al almacenamiento HTTP por segundo.|  
  
## <a name="see-also"></a>Vea también  
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
