---
title: Cursor Manager by Type (objeto de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Cursor Manager by Type object
- SQLServer:Cursor Manager by Type
ms.assetid: d67fbd8a-7554-4a16-96f1-d9ee857a95e3
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 712cc824e6faa834bd8d6023e4948e9e80dfabce
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "67986695"
---
# <a name="sql-server-cursor-manager-by-type-object"></a>Cursor Manager by Type (objeto de SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El objeto **SQLServer:Cursor Manager by Type** proporciona contadores para supervisar cursores agrupados por tipo.  
  
 En la siguiente tabla se describen los contadores de **Cursor Manager by Type** de SQL Server.  
  
|Contadores de Cursor Manager by Type|Descripción|  
|-------------------------------------|-----------------|  
|**Cursores activos**|Número de cursores activos.|  
|**Frecuencia de aciertos de caché**|Proporción entre los aciertos de caché y las búsquedas.|  
|**Base de frecuencia de aciertos de caché**|Solo para uso interno.| 
|**Recuentos de cursores en caché**|Número de cursores de un tipo determinado en la caché.|  
|**Recuentos de uso de caché de cursor/seg.**|Número de veces que se ha utilizado cada tipo de cursor en caché.|  
|**Uso de memoria de cursores**|Cantidad de memoria consumida por los cursores en kilobytes (KB).|  
|**Solicitudes de cursor/seg.**|Número de solicitudes de cursor de SQL recibidas por el servidor.|  
|**Uso de tablas de trabajo de cursores**|Número de tablas de trabajo utilizadas por los cursores.|  
|**Número de planes de cursor activos**|Número de planes de cursor.|  
  
 Cada contador del objeto contiene las instancias siguientes:  
  
|Instancia del administrador de cursor|Descripción|  
|-----------------------------|-----------------|  
|**_Total**|Información sobre todos los cursores.|  
|**API Cursor**|Solo información del cursor de API.|  
|**TSQL Global Cursor**|Solo información del cursor global de [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|**TSQL Local Cursor**|Solo información del cursor local de [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
