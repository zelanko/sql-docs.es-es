---
title: Elegir un solucionador | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- default conflict resolver
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: b7dec3fa-d9d9-409d-b946-f9b9a3202829
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 17c751898aee25fa98bfeb6c2a7e1f1143bc61ae
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/25/2020
ms.locfileid: "62931626"
---
# <a name="choose-a-resolver"></a>Elegir un solucionador
  Al elegir un solucionador, tenga en cuenta la importancia que tiene la resolución de conflictos en la aplicación y considere si debe utilizar el solucionador de conflictos predeterminado basado en prioridad o un solucionador de artículos.  
  
 Si los datos están divididos sin que varios usuarios escriban en las mismas particiones, y la topología de replicación es relativamente básica (un publicador y unos pocos suscriptores), los conflictos serán escasos o inexistentes. En estos entornos, es probable que no necesite una estrategia de resolución de conflictos compleja. Se recomienda una estrategia que utilice la configuración predeterminada para la resolución de conflictos, por medio de suscripciones en el cliente y una directiva de prioridad. Si la topología es más compleja (por ejemplo, si utiliza suscriptores de republicación), es posible que sea más apropiado utilizar suscripciones en el servidor con prioridades específicas.  
  
 Se recomienda utilizar un solucionador de artículos cuando las necesidades de la organización requieren una solución más específica que la que ofrece el solucionador predeterminado. Si elige utilizar un solucionador de artículos, se recomienda utilizar un controlador de lógica de negocios. Para obtener más información, consulte [Ejecutar lógica de negocios durante la sincronización de mezcla](execute-business-logic-during-merge-synchronization.md).  
  
 En última instancia, la decisión de utilizar un solucionador predeterminado o de artículos debe basarse en los datos y en las necesidades de lógica de negocios de la aplicación. Por ejemplo, considere el caso de empleados que escriben los datos de clasificación de los clientes en un conjunto de tablas sin particiones en diferentes suscriptores; los empleados pertenecen a distintas categorías de trabajo (jefes de sucursal, jefes de línea, personal de ventas) y la categoría del trabajo determina qué datos tienen prioridad. En este caso, se puede crear un solucionador de artículos que utilice los datos de categoría del trabajo procedentes del artículo para determinar el ganador en caso de conflicto.  
  
 Si es probable que se produzcan conflictos con cierta frecuencia, éstas son las decisiones más importantes que debe considerar al implementar una estrategia de resolución de conflictos.  
  
|Problema de resolución de conflictos|Recomendación|  
|-------------------------------|--------------------|  
|Diferentes categorías de usuarios necesitan diferentes valores de prioridad.|Utilice el solucionador predeterminado y cree suscripciones en el servidor con diferentes valores de prioridad.<br /><br /> -O bien-<br /><br /> Utilice un solucionador de artículos que reconozca una columna de valor de autoridad en el artículo para ayudar a solucionar el conflicto.|  
|Se desea una solución del conflicto basada en la prioridad.|Utilice el solucionador predeterminado y cree suscripciones de cliente.|  
|Es aceptable que varios usuarios cambien la misma fila de datos, siempre que no se hagan cambios conflictivos en la misma columna.|Utilice el solucionador predeterminado o un solucionador de artículos con el seguimiento por columnas habilitado.|  
|Marcar como conflicto cualquier cambio múltiple en los valores de una fila.|Utilice el solucionador predeterminado o un solucionador de artículos con el seguimiento por filas habilitado.|  
|Marcar como conflicto cualquier cambio múltiple en los valores de un registro lógico.|Utilice el solucionador predeterminado con seguimiento por registro lógico (la característica de registros lógicos no admite el uso de solucionadores personalizados ni controladores de lógica de negocios).|  
|Los datos resultantes del conflicto deben ser diferentes de los datos originales en conflicto.|Utilice un solucionador de artículos que calcule nuevos valores.|  
  
## <a name="see-also"></a>Consulte también  
 [Detecting and Resolving Conflicts in Logical Records](advanced-merge-replication-conflict-resolving-in-logical-record.md)   
 [Detección y resolución de conflictos de replicación de mezcla avanzada](advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Volver a publicar datos](../republish-data.md)  
  
  
