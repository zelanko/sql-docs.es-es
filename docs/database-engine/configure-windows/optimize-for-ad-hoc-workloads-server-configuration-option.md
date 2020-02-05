---
title: optimize for ad hoc workloads (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 11/17/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- optimize for ad hoc workloads option
ms.assetid: 0972e028-3a8e-454b-a186-e814a1d431f2
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c66a4d3826493d10974ab4ce8363e3adde1bd0fa
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "67998416"
---
# <a name="optimize-for-ad-hoc-workloads-server-configuration-option"></a>optimize for ad hoc workloads (opción de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  La opción **Optimizar para cargas de trabajo ad hoc** se utiliza para mejorar la eficiencia de la memoria caché del plan para cargas de trabajo que contienen muchos lotes ad hoc de uso único. Cuando esta opción está establecida en 1, [!INCLUDE[ssDE](../../includes/ssde-md.md)] almacena un pequeño código auxiliar del plan compilado en la memoria caché del plan al compilar un lote por primera vez, en lugar del plan compilado completo. Esto ayuda a disminuir la demanda de memoria al impedir que la memoria caché del plan se llene de planes compilados que no se reutilizan. 
  
  El código auxiliar del plan compilado permite que [!INCLUDE[ssDE](../../includes/ssde-md.md)] reconozca que este lote ad hoc se ha compilado antes, pero que solo se ha almacenado un código auxiliar del plan compilado, de modo que cuando se invoca de nuevo este lote (compilado o ejecutado), [!INCLUDE[ssDE](../../includes/ssde-md.md)] compila el lote, quita de la memoria caché del plan el código auxiliar del plan compilado y agrega el plan compilado completo a la memoria caché del plan. 
  
 El código auxiliar del plan compilado es uno de los elementos cacheobjtypes mostrados por la vista de catálogo sys.dm_exec_cached_plans. Tiene un identificador de sql e identificador del plan único. El código auxiliar del plan compilado no tiene un plan de ejecución asociado a él por lo que, al consultar el identificador del plan, no se devolverá un plan de presentación XML.  
  
 [La marca de seguimiento 8032](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) revierte los parámetros de límite de la memoria caché al valor [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] de RTM que, en general, permite que las memorias caché sean mayores. Use este valor cuando las entradas de caché que se reutilizan con frecuencia no quepan en la caché y cuando la opción de configuración del servidor Optimizar para cargas de trabajo ad hoc no haya podido resolver el problema con la caché de planes.  
  
> [!WARNING]  
>  La marca de seguimiento 8032 puede ocasionar la degradación del rendimiento si las memorias caché grandes suponen que haya menos memoria disponible para otros consumidores de memoria, como el grupo de búferes.  

## <a name="recommendations"></a>Recomendaciones
Evite tener un gran número de planes de uso único en la caché de planes. Una de las causas más comunes por las que ocurre este problema es porque los tipos de datos de los parámetros de consulta no están definidos de forma coherente. Esto se aplica especialmente a la longitud de las cadenas, pero puede aplicarse a cualquier tipo de datos que tenga una longitud máxima, una precisión o una escala. Por ejemplo, si un parámetro denominado @Greeting se pasa como un nvarchar (10) en una llamada y un nvarchar (20) en la siguiente llamada, se crean planes independientes para cada tamaño de parámetro. Si una consulta tiene varios parámetros y no están definidos de forma coherente cuando se realiza su llamada, podría existir un gran número de planes de consulta para cada consulta. Podrían existir planes para cada combinación de longitudes y tipos de datos de parámetros de consulta que se haya usado.

Si el número de planes de uso único usa una parte significativa de memoria de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] en un servidor OLTP y estos planes son planes ad hoc, use esta opción de servidor para reducir el uso de memoria con estos objetos.
Para determinar el número de planes almacenados en caché de uso único, ejecute la consulta siguiente:

```sql
SELECT objtype, cacheobjtype, 
  AVG(usecounts) AS Avg_UseCount, 
  SUM(refcounts) AS AllRefObjects, 
  SUM(CAST(size_in_bytes AS bigint))/1024/1024 AS Size_MB
FROM sys.dm_exec_cached_plans
WHERE objtype = 'Adhoc' AND usecounts = 1
GROUP BY objtype, cacheobjtype;
```

> [!IMPORTANT]
> Establecer la opción **Optimizar para cargas de trabajo ad hoc** en 1 afecta solo a los planes nuevos; los planes que ya están en la memoria caché del plan no resultan afectados.
> Para afectar a los planes de consulta que ya están almacenados en caché inmediatamente, es necesario borrar la cache mediante [ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) o reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="see-also"></a>Consulte también  
 [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
