---
title: Almacenamiento proactivo en caché (particiones) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4959473b120a3a8a0c289ff3cd8f91e89df44b86
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34020762"
---
# <a name="partitions---proactive-caching"></a>Particiones - almacenamiento en caché automático
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  El almacenamiento en caché automático proporciona la creación y administración automáticas de la memoria caché MOLAP para objetos OLAP. Los cubos incorporan inmediatamente los cambios que se realizan en los datos de la base de datos, basándose en las notificaciones recibidas de la base de datos. El objetivo del almacenamiento en caché automático consiste en proporcionar el rendimiento de MOLAP tradicional, a la vez que se conserva la inmediatez y la facilidad de administración que proporciona ROLAP.  
  
 Un objeto <xref:Microsoft.AnalysisServices.ProactiveCaching> simple se compone de una especificación de tiempo y una notificación de tabla. La especificación de tiempo define el horario para actualizar la caché una vez recibida una notificación de cambio. La notificación de tabla define el esquema de la notificación entre la tabla de datos y el objeto <xref:Microsoft.AnalysisServices.ProactiveCaching>.  
  
 El almacenamiento OLAP multidimensional (MOLAP) proporciona la mejor respuesta de consultas, a pesar de cierta latencia de datos. El almacenamiento OLAP relacional (ROLAP) en tiempo real permite a los usuarios examinar inmediatamente los cambios más recientes en un origen de datos, a pesar de un rendimiento considerablemente inferior que el almacenamiento OLAP multidimensional (MOLAP) debido a la ausencia de resúmenes de datos precalculados y a que el almacenamiento relacional no está optimizado para consultas de estilo OLAP. Si tiene aplicaciones en las que los usuarios necesitan ver los datos recientes y también desea obtener las ventajas de rendimiento del almacenamiento MOLAP, SQL Server Analysis Services ofrece la opción del almacenamiento en caché automático para solucionar este escenario, especialmente en combinación con el uso de particiones. El almacenamiento en caché automático se establece por partición y por dimensión. Las opciones de almacenamiento en caché automático proporcionan un equilibrio entre el rendimiento mejorado del almacenamiento MOLAP y la inmediatez del almacenamiento ROLAP, así como un procesamiento automático de las particiones cuando los datos subyacentes cambian o conforme a una programación establecida.  
  
## <a name="proactive-caching-configuration-options"></a>Opciones de configuración del almacenamiento en caché automático  
 SQL Server Analysis Services proporciona varias opciones de configuración del almacenamiento en caché automático que permiten maximizar el rendimiento, minimizar la latencia y programar el procesamiento. Las características de almacenamiento en caché automático simplifican el proceso de administrar la obsolescencia de datos. La configuración del almacenamiento en caché automático determina la frecuencia con la que se vuelve a generar la estructura OLAP multidimensional, también denominada caché MOLAP, si se consulta el almacenamiento MOLAP desusado mientras se vuelve a generar la caché o el origen de datos ROLAP subyacente y si se vuelve a generar la caché según una programación o según los cambios en la base de datos.  
  
### <a name="minimizing-latency"></a>Minimizar la latencia  
 Si se configura el almacenamiento en caché automático para minimizar la latencia, las consultas del usuario en un objeto OLAP se realizan en un almacenamiento ROLAP o en un almacenamiento MOLAP, dependiendo de si se han realizado cambios recientes en los datos y la forma en que el almacenamiento en caché automático está configurado. El motor de consultas dirige las consultas a los datos de origen del almacenamiento MOLAP hasta que se realicen los cambios en el origen de datos. A fin de minimizar la latencia, una vez realizados los cambios en un origen de datos, se pueden quitar los objetos MOLAP almacenados en la caché y la consulta cambia al almacenamiento ROLAP mientras que los objetos MOLAP se vuelven a generar en la caché. Después de que se vuelvan a generar y se procesen los objetos MOLAP, las consultas se cambian de forma automática al almacenamiento MOLAP. La actualización de la caché puede ser muy rápida en una partición pequeña, como la actual, que puede ser tan pequeña como el día actual.  
  
### <a name="maximizing-performance"></a>Maximizar el rendimiento  
 Para maximizar el rendimiento y al mismo tiempo reducir la latencia, el almacenamiento en caché también se puede utilizar sin quitar los objetos MOLAP actuales. Pueden continuar ejecutándose las consultas en los objetos MOLAP mientras se leen y se procesan los datos en una nueva caché. Este método proporciona un mejor rendimiento, pero podría devolver datos desusados en algunas consultas mientras se genera la nueva caché.  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento de dimensiones](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-storage.md)   
 [Almacenamiento de particiones del conjunto & #40; Analysis Services - Multidimensional & #41;](../../analysis-services/multidimensional-models/set-partition-storage-analysis-services-multidimensional.md)  
  
  
