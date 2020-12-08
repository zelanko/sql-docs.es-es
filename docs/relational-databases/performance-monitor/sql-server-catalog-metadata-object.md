---
title: Catalog Metadata (objeto de SQL Server) | Microsoft Docs
description: Obtenga información sobre el objeto de rendimiento SQLServer:Catalog Metadata, que proporciona contadores para los metadatos de catálogo de SQL Server.
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
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: a02c8d6253df487ebf5c01c8658f448ec680022c
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505819"
---
# <a name="sql-server-catalog-metadata-object"></a>SQL Server, objeto de metadatos de catálogo
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
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
