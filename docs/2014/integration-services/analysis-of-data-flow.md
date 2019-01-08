---
title: Análisis del flujo de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 5654cb30-cad2-470c-97b3-59cb331033e5
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fa33b840a985cb3053ad8868c3b6153dc53822ad
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52515817"
---
# <a name="analysis-of-data-flow"></a>Análisis de flujo de datos
  Puede usar el [catalog.execution_data_statistics](../relational-databases/statistics/statistics.md) `SSISDB` vista para analizar el flujo de datos de los paquetes de la base de datos. Esta vista muestra una fila cada vez que un componente de flujo de datos envía datos a un componente de nivel inferior. La información se puede utilizar para obtener una descripción más profunda de las filas que se envían a cada componente.  
  
> [!NOTE]  
>  El nivel de registro se debe establecer en **Verbose** para capturar información en la vista catalog.execution_data_statistics.  
  
 El ejemplo siguiente muestra el número de filas enviadas entre los componentes de un paquete.  
  
```  
use SSISDB  
select package_name, task_name, source_component_name, destination_component_name, rows_sent  
from catalog.execution_data_statistics  
where execution_id = 132  
order by source_component_name, destination_component_name  
  
```  
  
 El ejemplo siguiente se calcula el número de filas por milisegundo enviadas por cada componente de una ejecución concreta. Los valores calculados son:  
  
-   **total_rows** : suma de todas las filas enviadas por el componente.  
  
-   **wall_clock_time_ms**: tiempo de ejecución total transcurrido, en milisegundos, para cada componente.  
  
-   **num_rows_per_millisecond**: número de filas por milisegundo enviadas por cada componente.  
  
 El `HAVING` cláusula se utiliza para evitar un error de división por cero en los cálculos.  
  
```  
use SSISDB  
select source_component_name, destination_component_name,  
    sum(rows_sent) as total_rows,  
    DATEDIFF(ms,min(created_time),max(created_time)) as wall_clock_time_ms,  
    ((0.0+sum(rows_sent)) / (datediff(ms,min(created_time),max(created_time)))) as [num_rows_per_millisecond]  
from [catalog].[execution_data_statistics]  
where execution_id = 132  
group by source_component_name, destination_component_name  
having (datediff(ms,min(created_time),max(created_time))) > 0  
order by source_component_name desc  
  
```  
  
## <a name="related-tasks"></a>Related Tasks  
 [Depurar el flujo de datos](troubleshooting/debugging-data-flow.md)  
  
 [Herramientas para solucionar problemas de la ejecución de paquetes](troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
## <a name="see-also"></a>Vea también  
 [Datos de flujos de datos](data-flow/data-in-data-flows.md)  
  
  
