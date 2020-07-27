---
title: Query Store (objeto de SQL Server) | Microsoft Docs
description: Obtenga información sobre el objeto Almacén de consultas (Query Store), que proporciona contadores para supervisar el uso de recursos de SQL Server para almacenar textos de consulta, planes de ejecución y estadísticas del entorno de ejecución.
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store object
- SQL Server:Query Store
ms.assetid: b4a04acd-0b66-44a5-b72d-1a45b49e13e6
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 28a4a3a1711a72f7944dc48b12add759160d1dc9
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458759"
---
# <a name="sql-server-query-store-object"></a>SQL Server, objeto Query Store

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

El objeto Query Store proporciona contadores para supervisar la utilización de recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para almacenar textos de las consultas, planes de ejecución y estadísticas de tiempo de ejecución para los objetos como procedimientos almacenados, instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc y preparadas y desencadenadores.  
  
En esta tabla se describen los contadores del **Almacén de consultas de SQL Server**.  
  
|Contadores del Almacén de consultas de SQL Server|Descripción|  
|-------------------------------------|-----------------|  
|**Uso de CPU del Almacén de consultas**|Indica el uso de la CPU en Almacén de consultas como un percentil del uso de la CPU por parte de otros procesos.|  
|**Lecturas lógicas del Almacén de consultas**|Indica el número de lecturas lógicas realizadas por el Almacén de consultas.|  
|**Escrituras lógicas del Almacén de consultas**|Indica la cantidad de datos que se ponen en cola para vaciarlos desde el Almacén de consultas. La frecuencia y el retraso para agregar elementos (que representan las estadísticas de tiempo de ejecución) a la cola se controla mediante la opción Intervalo de vaciado de datos.|  
|**Lecturas físicas del Almacén de consultas**|Indica el número de lecturas físicas realizadas por el Almacén de consultas.|  
  
 Cada contador del objeto contiene las instancias siguientes:  
  
|Instancia del Almacén de consultas|Descripción|  
|--------------------------|-----------------|  
|**_Total**|Información para el Almacén de consultas para esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|\<database name>|Información del Almacén de consultas para esta base de datos.|  
  
## <a name="see-also"></a>Consulte también  

- [Supervisar el rendimiento mediante el Almacén de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)
- [Procedimientos almacenados del almacén de consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)
- [Query Store Catalog Views (Vistas de catálogo del almacén de consultas) &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)
- [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
