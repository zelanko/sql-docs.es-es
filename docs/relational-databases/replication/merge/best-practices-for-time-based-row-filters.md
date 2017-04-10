---
title: "Pr&#225;cticas recomendadas para filtros de fila basados en el tiempo | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "prácticas recomendadas"
ms.assetid: 773c5c62-fd44-44ab-9c6b-4257dbf8ffdb
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# Pr&#225;cticas recomendadas para filtros de fila basados en el tiempo
  Los usuarios de aplicaciones requieren con frecuencia un subconjunto de datos de una tabla basado en el tiempo. Por ejemplo, un vendedor puede requerir datos para pedidos de la semana pasada o un programador de eventos puede requerir datos para eventos de la semana próxima. En muchos casos, las aplicaciones utilizan las consultas que contienen los **GETDATE()** función para lograr esto. Considere la siguiente instrucción de filtro de fila:  
  
```  
WHERE SalesPersonID = CONVERT(INT,HOST_NAME()) AND OrderDate >= (GETDATE()-6)  
```  
  
 Con un filtro de este tipo, se suele asumir que siempre ocurren dos cosas cuando se ejecuta el agente de mezcla: las filas que cumplen este filtro se replican en los suscriptores y las filas que no lo cumplen se borran en los suscriptores. (Para obtener más información acerca del filtrado con **HOST_NAME ()**, consulte [filtros de fila parametrizados](../../../relational-databases/replication/merge/parameterized-row-filters.md).) Sin embargo, la replicación de mezcla solo replica y borra los datos que han cambiado desde la última sincronización, independientemente de cómo defina un filtro de fila para esos datos.  
  
 Para que la replicación de mezcla procese una fila, los datos de la fila deben cumplir el filtro de fila y haber cambiado desde la última sincronización. En el caso de la tabla **SalesOrderHeader** , se incluye **OrderDate** cuando se inserta una fila. Las filas se replican en el suscriptor como se espera porque la inserción es un cambio en los datos. Sin embargo, si hay filas en el suscriptor que ya no cumplen el filtro (son para pedidos con más de siete días de antigüedad), no se quitan del suscriptor a menos que se actualicen por alguna otra razón.  
  
 El caso del programador de eventos muestra mejor aún el problema con este tipo de filtro. Considere el siguiente filtro para una tabla **Events** :  
  
```  
WHERE EventCoordID = CONVERT(INT,HOST_NAME()) AND EventDate <= (GETDATE()+6)  
```  
  
 Para una tabla que contiene eventos, se pueden realizar inserciones mucho antes de la fecha del evento. Si la inserción de un evento de la semana próxima se realizó hace un mes y la fila no se actualizó por alguna razón, no se replica la fila en el suscriptor aunque cumpla el filtro de fila.  
  
 Además, según cómo esté configurada la publicación, la replicación de mezcla evalúa los filtros en momentos diferentes:  
  
-   Si una publicación utiliza particiones precalculadas (opción predeterminada), los filtros se evalúan cuando se inserta o actualiza una fila.  
  
-   Si la publicación no utiliza particiones precalculadas, los filtros se evalúan cuando se ejecuta el agente de mezcla.  
  
 Para obtener más información acerca de las particiones precalculadas, vea [optimizar el rendimiento de filtro con parámetros con particiones precalculadas](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md). El momento en que se evalúa el filtro afecta a los datos que cumplen el filtro. Por ejemplo, si una publicación utiliza particiones precalculadas y sincroniza datos cada dos días, el subconjunto de datos del vendedor podría incluir filas hasta dos días más antiguas de lo esperado.  
  
## Recomendaciones para usar filtros de fila basados en el tiempo  
 El método siguiente proporciona una buena solución para filtrar en función del tiempo:  
  
-   Agregue una columna a la tabla con el tipo de datos **bit**. Esta columna se usa para indicar si se debe replicar una fila.  
  
-   Utilice un filtro de fila que haga referencia a la nueva columna en lugar de una columna basada en el tiempo.  
  
-   Cree un trabajo del Agente SQL Server (o un trabajo programado con otro mecanismo) que actualice la columna antes de que se ejecute el agente de mezcla según esté programado.  
  
 Este enfoque soluciona los inconvenientes de utilizar **GETDATE()** u otro método basado en tiempo y evita el problema de tener que determinar cuando se evalúan los filtros para las particiones. Considere el siguiente ejemplo de una tabla **Events** :  
  
|**EventID**|**EventName**|**EventCoordID**|**EventDate**|**Replicar**|  
|-----------------|-------------------|----------------------|-------------------|-------------------|  
|1|Reception|112|2006-10-04|1|  
|2|Dinner|112|2006-10-10|0|  
|3|Party|112|2006-10-11|0|  
|4|Wedding|112|2006-10-12|0|  
  
 El filtro de fila para esta tabla tendría este aspecto:  
  
```  
WHERE EventCoordID = CONVERT(INT,HOST_NAME()) AND Replicate = 1  
```  
  
 El trabajo del Agente SQL Server podría ejecutar instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)] similares a las siguientes antes de que se ejecute cada agente de mezcla:  
  
```  
UPDATE Events SET Replicate = 0 WHERE Replicate = 1  
GO  
UPDATE Events SET Replicate = 1 WHERE EventDate <= GETDATE()+6  
GO  
```  
  
 La primera línea restablece la columna **Replicate** en **0**y la segunda línea establece la columna en **1** para los eventos que tienen lugar en los siete días siguientes. Si esta instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] se ejecuta el 7 de octubre de 2006, la tabla se actualiza a:  
  
|**EventID**|**EventName**|**EventCoordID**|**EventDate**|**Replicar**|  
|-----------------|-------------------|----------------------|-------------------|-------------------|  
|1|Reception|112|2006-10-04|0|  
|2|Dinner|112|2006-10-10|1|  
|3|Party|112|2006-10-11|1|  
|4|Wedding|112|2006-10-12|1|  
  
 Los eventos para la semana siguiente se marcan ahora como listos para replicación. La próxima vez que se ejecute el agente de mezcla para la suscripción que utiliza el coordinador de eventos 112, se descargarán las filas 2, 3 y 4 en el suscriptor y se quitará la fila 1 del suscriptor.  
  
## Vea también  
 [GETDATE & #40; Transact-SQL & #41;](../../../t-sql/functions/getdate-transact-sql.md)   
 [Implementar trabajos](../../../ssms/agent/implement-jobs.md)   
 [Filtros de fila con parámetros](../../../relational-databases/replication/merge/parameterized-row-filters.md)  
  
  