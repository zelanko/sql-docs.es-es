---
title: Propiedades de base de datos (página del Almacén de consultas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.querystore.f1
ms.assetid: da47d75e-291a-4305-acef-4b0aaf5215da
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 51116c993cf795e6390ac463f67f75e2ddff3e0e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62917216"
---
# <a name="database-properties-query-store-page"></a>Propiedades de base de datos (página del Almacén de consultas)
  Obtenga acceso a esta página desde la base de datos principal y úsela para configurar y modificar las propiedades del almacén de consultas de la base de datos. Estas opciones también se pueden configurar mediante las [opciones ALTER DATABASE SET](/sql/t-sql/statements/alter-database-transact-sql-set-options). Para información sobre el almacén de consultas, vea [Monitoring Performance By Using the Query Store](../performance/monitoring-performance-by-using-the-query-store.md).  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].|  
  
## <a name="options"></a>Opciones  
 Habilitar  
 Habilita y deshabilita el almacén de consultas.  
  
 Modo de operación  
 Los valores válidos son READ_ONLY y READ_WRITE. En el modo READ_WRITE, el almacén de consultas recopila y continúa el plan de consultas y la información de estadística del tiempo de ejecución. En el modo READ_ONLY, la información se puede leer del almacén de consultas, pero no se agrega información nueva. Si se ha agotado el espacio máximo del almacén de consultas, el almacén de consultas cambiará su modo de operación a READ_ONLY.  
  
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
  
 Umbral de consultas obsoletas (días)  
 Obtiene y establece el umbral de consultas obsoletas. Configure el argumento STALE_QUERY_THRESHOLD_DAYS para especificar el número de días en que se conservarán los datos en el almacén de consultas.  
  
 Depurar datos de consulta  
 Quita el contenido del almacén de consultas.  
  
 Gráficos circulares  
 En el gráfico de la izquierda se muestra el consumo total del archivo de la base de datos en el disco y la parte del archivo que se rellena con los datos del almacén de consultas.  
  
 En el gráfico de la derecha se muestra la parte de la cuota del almacén de consultas que se ha consumido actualmente. Observe que no se muestra la cuota en el gráfico de la izquierda. La cuota puede superar el tamaño actual de la base de datos.  
  
## <a name="remarks"></a>Comentarios  
 La característica del almacén de consultas ofrece a los DBA conocimientos sobre el rendimiento y la elección del plan de consultas. Esta característica simplifica la solución de problemas de rendimiento al permitirle encontrar rápidamente diferencias de rendimiento provocadas por cambios en los planes de consulta. Captura automáticamente un historial de consultas, planes y estadísticas en tiempo de ejecución, y los conserva para su revisión. Separa los datos por ventanas de tiempo, lo que permite ver patrones de uso la base de datos y comprender cuándo se produjeron cambios del plan de consultas en el servidor. El almacén de consultas se puede configurar con esta página de propiedades de base de datos de almacén de consultas o mediante la opción [ALTER DATABASE SET](/sql/t-sql/statements/alter-database-transact-sql-set-options) . El almacén de consultas presenta información mediante un cuadro de diálogo [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] . Para más información sobre el almacén de consultas, vea [Monitoring Performance By Using the Query Store](../performance/monitoring-performance-by-using-the-query-store.md).  
  
## <a name="see-also"></a>Vea también  
 [Query Store Stored Procedures &#40;Transact-SQL&#41; (Procedimientos almacenados del almacén de consultas &#40;Transact-SQL&#41;)](/sql/relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql)   
 [Query Store Catalog Views &#40;Transact-SQL&#41; (Vistas de catálogo del almacén de consultas &#40;Transact-SQL&#41;)](/sql/relational-databases/system-catalog-views/query-store-catalog-views-transact-sql)  
  
  
