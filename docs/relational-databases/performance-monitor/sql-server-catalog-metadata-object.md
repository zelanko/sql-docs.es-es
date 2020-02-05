---
title: Catalog Metadata (objeto de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Catalog Metadata
ms.assetid: 665e63e6-4bd2-4091-92a5-327364db2f8d
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 3b408951b0a1f32bda0920260aae18ab93350fdd
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "67986715"
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
|**Base de frecuencia de aciertos de caché**|Solo para uso interno.|

Hay una instancia del contador para cada base de datos.

## <a name="see-also"></a>Consulte también  
[Supervisar el uso de recursos (Monitor de sistema)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)
