---
title: Query Store (objeto de SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Query Store object
- SQL Server:Query Store
ms.assetid: b4a04acd-0b66-44a5-b72d-1a45b49e13e6
caps.latest.revision: "8"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b3bfa37e7f645148daa38f8e79b8c51aaf1613c0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-query-store-object"></a>SQL Server, objeto Query Store
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  El objeto Query Store proporciona contadores para supervisar la utilización de recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para almacenar textos de las consultas, planes de ejecución y estadísticas de tiempo de ejecución para los objetos como procedimientos almacenados, instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc y preparadas y desencadenadores.  
  
 En esta tabla se describen los contadores de **SQLServer:Query Store**.  
  
|Contadores del Almacén de consultas de SQL Server|Descripción|  
|-------------------------------------|-----------------|  
|**Uso de CPU del Almacén de consultas**|Indica el uso de almacenes de consultas de la CPU.|  
|**Lecturas lógicas del Almacén de consultas**|Indica el número de lecturas lógicas realizadas por el Almacén de consultas.|  
|**Escrituras lógicas del Almacén de consultas**|Indica la cantidad de datos que se ponen en cola para vaciarlos desde el Almacén de consultas. La frecuencia y el retraso para agregar elementos (que representan las estadísticas de tiempo de ejecución) a la cola se controla mediante la opción Intervalo de vaciado de datos.|  
|**Lecturas físicas del Almacén de consultas**|Indica el número de lecturas físicas realizadas por el Almacén de consultas.|  
  
 Cada contador del objeto contiene las instancias siguientes:  
  
|Instancia del Almacén de consultas|Descripción|  
|--------------------------|-----------------|  
|**_Total**|Información para el Almacén de consultas para esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|\<nombre de la base de datos>|Información del Almacén de consultas para esta base de datos.|  
  
## <a name="see-also"></a>Vea también  
 [Supervisar el rendimiento mediante el almacén de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Query Store Stored Procedures &#40;Transact-SQL&#41; (Procedimientos almacenados del almacén de consultas &#40;Transact-SQL&#41;)](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [Query Store Catalog Views &#40;Transact-SQL&#41; (Vistas de catálogo del almacén de consultas &#40;Transact-SQL&#41;)](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
