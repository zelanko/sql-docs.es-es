---
title: Cursor Manager by Type (objeto de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Cursor Manager by Type object
- SQLServer:Cursor Manager by Type
ms.assetid: d67fbd8a-7554-4a16-96f1-d9ee857a95e3
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 35fa15dc6651d8bfd9b6d32cafd00cd47698560b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52804257"
---
# <a name="sql-server-cursor-manager-by-type-object"></a>Cursor Manager by Type (objeto de SQL Server)
  El objeto **SQLServer:Cursor Manager by Type** proporciona contadores para supervisar cursores agrupados por tipo.  
  
 En la siguiente tabla se describen los contadores de **Cursor Manager by Type** de SQL Server.  
  
|Contadores de Cursor Manager by Type|Descripción|  
|-------------------------------------|-----------------|  
|**Cursores activos**|Número de cursores activos.|  
|**Frecuencia de aciertos de caché**|Proporción entre los aciertos de caché y las búsquedas.|  
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
  
## <a name="see-also"></a>Vea también  
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
