---
title: FileTable (objeto de SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLServer:FileTable
ms.assetid: 325f5e58-1095-450f-9321-dfacfe6fd55f
caps.latest.revision: 3
author: dagiro
ms.author: v-dagir
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 321ed2db9195a957f10982fe07f1da7b8cb01c25
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-filetable-object"></a>SQL Server, objeto FileTable
El objeto de rendimiento **SQLServer:FileTable** proporciona contadores para las estadísticas asociadas a FileTable y acceso sin transacciones.

En la siguiente tabla se describen los objetos de rendimiento **FileTable** de SQL Server.

|**Contadores de FileTable de SQL Server**|Description|  
|-------------|-----------------|  
|**Tiempo promedio de eliminación de elemento de FileTable**|Promedio de tiempo (en milisegundos) necesario para eliminar un elemento de FileTable.|
|**Tiempo promedio de enumeración de FileTable**|Promedio de tiempo (en milisegundos) necesario para una solicitud de enumeración de FileTable.|
|**Tiempo promedio de operaciones de eliminación de identificación de FileTable**|Promedio de tiempo (en milisegundos) necesario para eliminar un identificador de FileTable.|
|**Tiempo promedio para mover elemento de FileTable**|Promedio de tiempo (en milisegundos) necesario para mover un elemento de FileTable.|
|**Tiempo medio por solicitud de archivo E/S**|Promedio de tiempo (en milisegundos) empleado en el tratamiento de una solicitud de E/S de archivo entrante.|
|**Tiempo medio por respuesta de archivo E/S**|Promedio de tiempo (en milisegundos) empleado en el tratamiento de una respuesta de E/S de archivo saliente.|
|**Tiempo promedio para cambiar nombre de elemento de FileTable**|Promedio de tiempo (en milisegundos) necesario para cambiar el nombre de un elemento de FileTable.|
|**Tiempo promedio para obtener elemento de FileTable**|Promedio de tiempo (en milisegundos) necesario para recuperar un elemento de FileTable.|
|**Tiempo promedio de actualización de elemento de FileTable**|Promedio de tiempo (en milisegundos) necesario para actualizar un elemento de FileTable.|
|**Operaciones de base de datos de FileTable/s**|Número total de eventos operativos de base de datos procesados por el componente de almacén de FileTable por segundo.|
|**Solicitudes de enumeración de FileTable/s**|Número total de solicitudes de enumeración de FileTable por segundo.|
|**Solicitudes de archivo E/S de FileTable/s**|Número total de solicitudes de E/S de archivo de FileTable entrantes por segundo.|
|**Respuesta de archivo E/S de FileTable/s**|Número total de respuestas de E/S de archivos salientes por segundo.|
|**Solicitudes de eliminación de elemento de FileTable/s**|Número total de solicitudes de eliminación de elemento de FileTable por segundo.|
|**Solicitudes de obtención de elemento de FileTable/s**|Número total de solicitudes de recuperación de elemento de FileTable por segundo.|
|**Solicitudes para mover elemento de FileTable/s**|Número total de solicitudes de desplazamiento de elemento de FileTable por segundo.|
|**Solicitudes para cambiar nombre de elemento de FileTable/s**|Número total de solicitudes de cambio de nombre de elemento de FileTable por segundo.|
|**Solicitudes de actualización de elemento de FileTable/s**|Número total de solicitudes de actualización de elemento de FileTable por segundo.|
|**Operaciones de eliminación de identificación de FileTable/s**|Número total de operaciones de eliminación de identificación de FileTable por segundo.|
|**Operaciones de tabla de FileTable/s**|Número total de eventos operativos de tabla procesados por el componente de almacén de FileTable por segundo.|
|**BASE de tiempo de eliminación de elemento de FileTable**|Exclusivamente para uso interno.|
|**BASE de tiempo de enumeración de FileTable**|Exclusivamente para uso interno.|
|**BASE de tiempo de eliminación de identificación de FileTable**|Exclusivamente para uso interno.|
|**BASE de tiempo para mover elemento de FileTable**|Exclusivamente para uso interno.|
|**Tiempo por BASE de solicitud de archivo E/S**|Exclusivamente para uso interno.|
|**Tiempo por BASE respuesta de archivo E/S**|Exclusivamente para uso interno.|
|**BASE de tiempo para cambiar nombre de elemento de FileTable**|Exclusivamente para uso interno.|
|**BASE de tiempo para obtener elemento de FileTable**|Exclusivamente para uso interno.|
|**BASE de tiempo de actualización de elemento de FileTable**|Exclusivamente para uso interno.| 
 
## <a name="see-also"></a>Vea también  
[Supervisar el uso de recursos (Monitor de sistema)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)

