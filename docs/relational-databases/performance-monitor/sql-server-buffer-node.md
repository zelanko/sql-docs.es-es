---
title: SQL Server:Buffer Node | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Buffer Node
- Buffer Node object
ms.assetid: fd3f9f0f-7c38-4cfd-a0c5-ee93dd52d9a5
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 9011394dccf472499c1c8a8bd1023b7c23009883
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "67987212"
---
# <a name="sql-serverbuffer-node"></a>SQL Server:Buffer Node
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El objeto **Buffer Node** proporciona contadores que complementan a los contadores proporcionados por el objeto **Buffer Manager** . Este objeto permite supervisar la distribución de páginas del grupo de búferes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para cada nodo de acceso no uniforme a memoria (NUMA). Existe una instancia del objeto **Buffer Node** para cada nodo NUMA que está en uso. En la arquitectura no NUMA, habrá una sola instancia del objeto **Buffer Node** .  
  
## <a name="buffer-node-performance-objects"></a>Objetos de rendimiento Buffer Node  
 En esta tabla se describen los objetos de rendimiento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Buffer Node**de**.  
  
|Contadores de SQLServer:Buffer Node|Descripción|  
|-------------------------------------|-----------------|  
|**Páginas de base de datos**|Indica el número de páginas del grupo de búferes de este nodo con contenido de la base de datos.|  
|**Duración prevista de la página**|Indica el número mínimo de segundos que una página permanecerá en el grupo de búferes de este nodo sin referencias.|  
|**Búsquedas de páginas de nodos locales por segundo**|Indica el número de solicitudes de búsqueda de este nodo que se satisfacen desde este mismo nodo.|  
|**Búsquedas de páginas de nodos remotos por segundo**|Indica el número de solicitudes de búsqueda de este nodo que se satisfacen desde otros nodos.|  
  
 Si SQL Server se ejecuta en un hardware que no es de NUMA, los contadores de los objetos **Buffer Node** y **Buffer Manager** deben coincidir.  
  
 En hardware de NUMA, las sumas de todos los contadores respectivos de **Buffer Node** deben coincidir con sus equivalentes de **Buffer Manager**.  
  
> [!NOTE]  
>  Es posible que las sumas y los valores de contador no coincidan debido precisamente a la naturaleza dinámica de los contadores y la precisión del muestreo.  
  
## <a name="see-also"></a>Consulte también  
 [Buffer Manager (objeto de SQL Server)](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)   
 [Opciones de configuración de memoria del servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)  
  
  
