---
title: Catalog Metadata (objeto de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Catalog Metadata
ms.assetid: 665e63e6-4bd2-4091-92a5-327364db2f8d
author: dagiro
ms.author: v-dagir
manager: craigg
ms.openlocfilehash: 1f92f446ebd8d3f8efdd2c3ff8e62ec46c55b60a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47826043"
---
# <a name="sql-server-catalog-metadata-object"></a>SQL Server, objeto de metadatos de catálogo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
El objeto de rendimiento **Metadatos de SQLServer:Catalog** proporciona contadores para los metadatos de catálogo de SQL Server.

En la tabla siguiente se describen los objetos de rendimiento de **metadatos de catálogo** de SQL Server.


|**Contadores de metadatos de catálogo de SQL Server**|Descripción|  
|-------------|-----------------|  
|**Catalog Metadata Object**|Número de entradas en la caché de metadatos de catálogo.|
|**Cache Entries Pinned Count**|Número de entradas de caché de metadatos de catálogo que están fijadas.|
|**Frecuencia de aciertos de caché**|Proporción entre aciertos de caché de metadatos de catálogo y búsquedas.|
|**Base de frecuencia de aciertos de caché**|Exclusivamente para uso interno.|

Hay una instancia del contador para cada base de datos.

## <a name="see-also"></a>Ver también  
[Supervisar el uso de recursos (Monitor de sistema)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)
