---
title: "Propiedades de base de datos (página del Almacén de consultas) | Microsoft Docs"
ms.custom: 
ms.date: 11/09/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.databaseproperties.querystore.f1
ms.assetid: da47d75e-291a-4305-acef-4b0aaf5215da
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 903eb21e82dc2b5e3a04f0b48b4f17365a0eac99
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="database-properties-query-store-page"></a>Propiedades de base de datos (página del Almacén de consultas)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Obtenga acceso a esta página desde la base de datos principal y úsela para configurar y modificar las propiedades del almacén de consultas de la base de datos. Estas opciones también se pueden configurar mediante las [opciones ALTER DATABASE SET](../../t-sql/statements/alter-database-transact-sql-set-options.md). Para información sobre el almacén de consultas, vea [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md).  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (hasta la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)) [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].|  
  
## <a name="options"></a>.  
 Modo de operación  
 Los valores válidos son OFF, READ_ONLY y READ_WRITE. OFF deshabilita el almacén de consultas. En el modo READ_WRITE, el almacén de consultas recopila y continúa el plan de consultas y la información de estadística del tiempo de ejecución. En el modo READ_ONLY, la información se puede leer del almacén de consultas, pero no se agrega información nueva. Si se ha agotado el espacio máximo del almacén de consultas, el almacén de consultas cambiará su modo de operación a READ_ONLY.  
  
 Modo de operación (real)  
 Obtiene el modo de operación real del almacén de consultas.  
  
 Modo de operación (solicitado)  
 Obtiene y establece el modo de operación que desea del almacén de consultas.  
  
 Intervalo del vaciado de datos (minutos)  
 Determina la frecuencia con la que los datos escritos en el almacén de consultas se conservan en el disco. Para optimizar el rendimiento, los datos recopilados por el almacén de consultas se escriben de manera asincrónica en el disco. Se configura la frecuencia con la que se produce esta transferencia asincrónica.  
  
 Intervalo de la recopilación de estadísticas  
 Obtiene y establece el valor del intervalo de la recopilación de estadísticas.  
  
 Tamaño máximo (MB)  
 Obtiene y establece el espacio asignado total al almacén de consultas.  
  
 Modo de captura del almacén de consultas  
 -   Ninguno no captura las nuevas consultas.  
  
-   Todo captura todas las consultas.  
  
-   Auto captura las consultas basadas en el consumo de recursos.  
  
 Umbral de consultas obsoletas (días)  
 Obtiene y establece el umbral de consultas obsoletas. Configure el argumento STALE_QUERY_THRESHOLD_DAYS para especificar el número de días en que se conservarán los datos en el almacén de consultas.  
  
 Depurar datos de consulta  
 Quita el contenido del almacén de consultas.  
  
 Gráficos circulares  
 En el gráfico de la izquierda se muestra el consumo total del archivo de la base de datos en el disco y la parte del archivo que se rellena con los datos del almacén de consultas.  
  
 En el gráfico de la derecha se muestra la parte de la cuota del almacén de consultas que se ha consumido actualmente. Observe que no se muestra la cuota en el gráfico de la izquierda. La cuota puede superar el tamaño actual de la base de datos.  
  
## <a name="remarks"></a>Notas  
 La característica del almacén de consultas ofrece a los DBA conocimientos sobre el rendimiento y la elección del plan de consultas. Esta característica simplifica la solución de problemas de rendimiento al permitirle encontrar rápidamente diferencias de rendimiento provocadas por cambios en los planes de consulta. Captura automáticamente un historial de consultas, planes y estadísticas en tiempo de ejecución, y los conserva para su revisión. Separa los datos por ventanas de tiempo, lo que permite ver patrones de uso la base de datos y comprender cuándo se produjeron cambios del plan de consultas en el servidor. El almacén de consultas se puede configurar con esta página de propiedades de base de datos de almacén de consultas o mediante la opción [ALTER DATABASE SET](../../t-sql/statements/alter-database-transact-sql-set-options.md) . El almacén de consultas presenta información mediante un cuadro de diálogo [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] . Para más información sobre el almacén de consultas, vea [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md).  
  
## <a name="see-also"></a>Ver también  
 [Query Store Stored Procedures &#40;Transact-SQL&#41; (Procedimientos almacenados del almacén de consultas &#40;Transact-SQL&#41;)](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [Query Store Catalog Views &#40;Transact-SQL&#41; (Vistas de catálogo del almacén de consultas &#40;Transact-SQL&#41;)](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)  
  
  
