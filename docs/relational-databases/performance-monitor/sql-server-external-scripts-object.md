---
title: SQL Server, objeto External Scripts | Microsoft Docs
ms.custom: 
ms.date: 03/21/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- External Scripts object
- SQLServer:External Scripts
ms.assetid: 8a75ccce-b174-4937-bc92-8e413b55afe1
caps.latest.revision: 7
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2e5f146f5684567ec39e62d9c6d7786f3506d8d0
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-external-scripts-object"></a>SQL Server, objeto External Scripts
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  El objeto **SQLServer:External Scripts** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona contadores para supervisar las acciones asociadas a la ejecución de scripts externos. Para obtener información sobre cómo ejecutar scripts externos, vea [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).  
  
 Esta tabla se describen los contadores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **External Scripts** .  
  
|Contadores de SQL Server External Scripts|Descripción|  
|------------------------------------------|-----------------|  
|**Errores de ejecución**|Número de errores en la ejecución de scripts externos.|  
|**Inicios de sesión de autenticación implícita**|Número de inicios de sesión de procesos satélite autenticados mediante autenticación implícita.|  
|**Ejecuciones en paralelo**|Número de scripts externos ejecutados con @parallel = 1.|  
|**Ejecuciones CC de SQL**|Número de scripts externos ejecutados con contexto de cálculo de SQL|  
|**Ejecuciones de streaming**|Número de scripts externos ejecutados con el parámetro @r_rowsPerRead.|  
|**Tiempo total de ejecución (ms)**|Tiempo total empleado en la ejecución de scripts externos.|  
|**Ejecuciones totales**|Número de scripts externos ejecutados.|  
  
## <a name="see-also"></a>Vea también  
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)   
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  

