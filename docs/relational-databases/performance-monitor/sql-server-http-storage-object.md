---
title: SQL Server, HTTP_STORAGE_OBJECT | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: ae849f79-c581-42a5-a5cc-0a9ebea171b9
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: f863259a12be7ef2346ddfa333b79c95a920d2fe
ms.sourcegitcommit: 0c1d552b3256e1bd995e3c49e0561589c52c21bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2018
ms.locfileid: "53380466"
---
# <a name="sql-server-http-storage"></a>SQL Server, Almacenamiento HTTP
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El objeto de rendimiento **SQLServer:Almacenamiento HTTP** está compuesto por contadores de rendimiento que supervisan la cuenta de Microsoft Azure Storage. Si usa la característica [Archivos de datos de SQL Server de Microsoft Azure](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md) , puede almacenar archivos de base de datos en los blobs de almacenamiento de Microsoft Azure. Este objeto de rendimiento trata cada cuenta de Almacenamiento de Windows Azure como una unidad diferente.  
  
|Nombre de contador|Descripción|  
|------------------|-----------------|  
|**Avg. bytes/lectura**|Promedio de bytes transferidos desde el almacenamiento HTTP por lectura.|  
|**Avg. bytes/transferidos**|Promedio de bytes transferidos desde el almacenamiento HTTP durante las operaciones de lectura o escritura.|  
|**Avg. bytes/escritura**|Promedio de bytes transferidos desde el almacenamiento HTTP por escritura.|  
|**Promedio de microsegundos/lectura**|Promedio de microsegundos que invierten en realizar cada lectura desde el almacenamiento HTTP.|  
|**Promedio de microsegundos/lectura comp**|El promedio de microsegundos que HTTP tarda en completar la lectura para el almacenamiento.| 
|**Promedio de microsegundos/transferencia**|Promedio de microsegundos que se invierten en realizar cada transferencia en el almacenamiento HTTP.|  
|**Promedio de microsegundos/escritura**|Promedio de microsegundos que se invierten en realizar cada escritura en el almacenamiento HTTP.|  
|**Promedio de microsegundos/escritura comp**|El promedio de microsegundos que HTTP tarda en completar la escritura para el almacenamiento.|  
|**E/S de almacenamiento HTTP erróneas/s**|Número de solicitudes de escritura erróneas enviadas al almacenamiento HTTP por segundo.| 
|**Error/seg de E/S de Almacenamiento HTTP**|Número de solicitudes de reintento enviadas al almacenamiento HTTP por segundo.|  
|**E/S pendiente de almacenamiento HTTP**|Número total de E/S pendientes para su almacenamiento HTTP.|  
|**Lectura de bytes/seg**|Cantidad de datos que se transfieren desde almacenamiento HTTP por segundo durante las operaciones de lectura.|  
|**Lecturas/seg**|Número de lecturas por segundo en el almacenamiento HTTP.|  
|**Total de bytes/seg**|Cantidad de datos que se transfieren desde almacenamiento HTTP por segundo durante las operaciones de lectura o escritura.|  
|**Transferencias/seg**|Número de operaciones de lectura y escritura por segundo en el almacenamiento HTTP.|  
|**Escritura de bytes/seg**|Cantidad de datos que se transfieren desde almacenamiento HTTP por segundo durante las operaciones de escritura.|  
|**lógicas/s**|Número de escrituras por segundo en el almacenamiento HTTP.|  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
