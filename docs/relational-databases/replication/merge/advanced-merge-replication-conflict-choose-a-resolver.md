---
title: Elegir un solucionador | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- default conflict resolver
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: b7dec3fa-d9d9-409d-b946-f9b9a3202829
caps.latest.revision: 33
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4d56dbad56be7bf0762bb4d43fcc3138f547fe30
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37355387"
---
# <a name="advanced-merge-replication-conflict---choose-a-resolver"></a>Conflictos de replicación de mezcla avanzada: elegir un solucionador
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Al elegir un solucionador, tenga en cuenta la importancia que tiene la resolución de conflictos en la aplicación y considere si debe utilizar el solucionador de conflictos predeterminado basado en prioridad o un solucionador de artículos.  
  
 Si los datos están divididos sin que varios usuarios escriban en las mismas particiones, y la topología de replicación es relativamente básica (un publicador y unos pocos suscriptores), los conflictos serán escasos o inexistentes. En estos entornos, es probable que no necesite una estrategia de resolución de conflictos compleja. Se recomienda una estrategia que utilice la configuración predeterminada para la resolución de conflictos, por medio de suscripciones en el cliente y una directiva de prioridad. Si la topología es más compleja (por ejemplo, si utiliza suscriptores de republicación), es posible que sea más apropiado utilizar suscripciones en el servidor con prioridades específicas.  
  
 Se recomienda utilizar un solucionador de artículos cuando las necesidades de la organización requieren una solución más específica que la que ofrece el solucionador predeterminado. Si elige utilizar un solucionador de artículos, se recomienda utilizar un controlador de lógica de negocios. Para obtener más información, consulte [Ejecutar lógica de negocios durante la sincronización de mezcla](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
 En última instancia, la decisión de utilizar un solucionador predeterminado o de artículos debe basarse en los datos y en las necesidades de lógica de negocios de la aplicación. Por ejemplo, considere el caso de empleados que escriben los datos de clasificación de los clientes en un conjunto de tablas sin particiones en diferentes suscriptores; los empleados pertenecen a distintas categorías de trabajo (jefes de sucursal, jefes de línea, personal de ventas) y la categoría del trabajo determina qué datos tienen prioridad. En este caso, se puede crear un solucionador de artículos que utilice los datos de categoría del trabajo procedentes del artículo para determinar el ganador en caso de conflicto.  
  
 Si es probable que se produzcan conflictos con cierta frecuencia, éstas son las decisiones más importantes que debe considerar al implementar una estrategia de resolución de conflictos.  
  
|Problema de resolución de conflictos|Recomendación|  
|-------------------------------|--------------------|  
|Diferentes categorías de usuarios necesitan diferentes valores de prioridad.|Utilice el solucionador predeterminado y cree suscripciones en el servidor con diferentes valores de prioridad.<br /><br /> o bien<br /><br /> Utilice un solucionador de artículos que reconozca una columna de valor de autoridad en el artículo para ayudar a solucionar el conflicto.|  
|Se desea una solución del conflicto basada en la prioridad.|Utilice el solucionador predeterminado y cree suscripciones de cliente.|  
|Es aceptable que varios usuarios cambien la misma fila de datos, siempre que no se hagan cambios conflictivos en la misma columna.|Utilice el solucionador predeterminado o un solucionador de artículos con el seguimiento por columnas habilitado.|  
|Marcar como conflicto cualquier cambio múltiple en los valores de una fila.|Utilice el solucionador predeterminado o un solucionador de artículos con el seguimiento por filas habilitado.|  
|Marcar como conflicto cualquier cambio múltiple en los valores de un registro lógico.|Utilice el solucionador predeterminado con seguimiento por registro lógico (la característica de registros lógicos no admite el uso de solucionadores personalizados ni controladores de lógica de negocios).|  
|Los datos resultantes del conflicto deben ser diferentes de los datos originales en conflicto.|Utilice un solucionador de artículos que calcule nuevos valores.|  
  
## <a name="see-also"></a>Ver también  
 [Detectar y solucionar conflictos en registros lógicos](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)   
 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Volver a publicar datos](../../../relational-databases/replication/republish-data.md)  
  
  
