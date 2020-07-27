---
title: SQL Server, objeto External Scripts | Microsoft Docs
description: Obtenga información sobre el objeto SQLServer:External Scripts, que proporciona contadores para supervisar las acciones asociadas a la ejecución de scripts externos.
ms.custom: ''
ms.date: 03/21/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- External Scripts object
- SQLServer:External Scripts
ms.assetid: 8a75ccce-b174-4937-bc92-8e413b55afe1
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: fb8ded658e80c3530b916ea81595ac5fa5c99f52
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2020
ms.locfileid: "86457432"
---
# <a name="sql-server-external-scripts-object"></a>SQL Server, objeto External Scripts
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  El objeto **SQLServer:External Scripts** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona contadores para supervisar las acciones asociadas a la ejecución de scripts externos. Para obtener información sobre cómo ejecutar scripts externos, vea [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).  
  
 En esta tabla se describen los contadores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **External Scripts**.  
  
|Contadores de SQL Server External Scripts|Descripción|  
|------------------------------------------|-----------------|  
|**Errores de ejecución**|Número de errores en la ejecución de scripts externos.|  
|**Inicios de sesión de autenticación implícita**|Número de inicios de sesión de procesos satélite autenticados mediante autenticación implícita.|  
|**Ejecuciones en paralelo**|Número de scripts externos ejecutados con @parallel = 1.|  
|**Ejecuciones CC de SQL**|Número de scripts externos ejecutados con contexto de cálculo de SQL|  
|**Ejecuciones de streaming**|Número de scripts externos ejecutados con el parámetro @r_rowsPerRead.|  
|**Tiempo total de ejecución (ms)**|Tiempo total empleado en la ejecución de scripts externos.|  
|**Ejecuciones totales**|Número de scripts externos ejecutados.|  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)   
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
