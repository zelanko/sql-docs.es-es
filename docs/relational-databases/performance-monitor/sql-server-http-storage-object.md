---
title: SQL Server, HTTP_STORAGE_OBJECT | Microsoft Docs
description: Obtenga información sobre el objeto de rendimiento SQLServer:HTTP Storage, que está compuesto por contadores de rendimiento que supervisan una cuenta de Azure Storage.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: ae849f79-c581-42a5-a5cc-0a9ebea171b9
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 6ca729c6097b02142e4459a0c11e5ad77741ea37
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505720"
---
# <a name="sql-server-http-storage"></a>SQL Server, Almacenamiento HTTP
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  El objeto de rendimiento **SQLServer:Almacenamiento HTTP** está compuesto por contadores de rendimiento que supervisan la cuenta de Microsoft Azure Storage. Si usa la característica [Archivos de datos de SQL Server de Microsoft Azure](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md), puede almacenar archivos de base de datos en blobs de Azure Storage Blob. Este objeto de rendimiento trata cada cuenta de Azure Storage como una unidad diferente.  
  
|Nombre del contador|Descripción|  
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
  
  
