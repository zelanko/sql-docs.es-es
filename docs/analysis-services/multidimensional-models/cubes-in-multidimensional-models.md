---
title: Cubos en modelos multidimensionales | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OLAP objects [Analysis Services], cubes
- cubes [Analysis Services], about cubes
- cubes [Analysis Services]
- OLAP [Analysis Services], cubes
ms.assetid: e0f7acf3-4b07-41fc-a5fc-ac30b4a56c54
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1a555a25c41b4860aa16d5a2cfd43749a0ccd65d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="cubes-in-multidimensional-models"></a>Cubos en modelos multidimensionales
  Un cubo es una estructura multidimensional que contiene información con fines analíticos; sus componentes principales son las dimensiones y las medidas. Las dimensiones definen la estructura del cubo que se utiliza para segmentar y dividir los datos, y las medidas proporcionan valores numéricos agregados importantes para el usuario final. Como estructura lógica, un cubo permite a una aplicación cliente recuperar valores, de medidas, como si estuvieran almacenados en las celdas del cubo; las celdas se definen para cada posible valor resumido. Las celdas del cubo se definen por la intersección de miembros de dimensión y contienen los valores agregados de las medidas en esa intersección concreta.  
  
## <a name="benefits-of-using-cubes"></a>Ventajas del uso de cubos  
 Un cubo proporciona un único lugar en el que se almacenan todos los datos relacionados con fines analíticos.  
  
## <a name="components-of-cubes"></a>Componentes de los cubos  
 Un cubo consta de:  
  
|Elemento|Description|  
|-------------|-----------------|  
|Dimensions|[Dimensiones en modelos multidimensionales](../../analysis-services/multidimensional-models/dimensions-in-multidimensional-models.md)|  
|Medidas y grupos de medida|[Crear medidas y grupos de medida en modelos multidimensionales](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)|  
|Particiones|[Particiones en modelos multidimensionales](../../analysis-services/multidimensional-models/partitions-in-multidimensional-models.md)|  
|Perspectivas|[Perspectivas de modelos multidimensionales](../../analysis-services/multidimensional-models/perspectives-in-multidimensional-models.md)|  
|Jerarquías|[Crear jerarquías definidas por el usuario](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)|  
|Acciones|[Acciones en modelos multidimensionales](../../analysis-services/multidimensional-models/actions-in-multidimensional-models.md)|  
|Indicadores clave de rendimiento (KPI)|[Indicadores clave de rendimiento &#40;KPI&#41; en modelos multidimensionales](../../analysis-services/multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)|  
|Cálculos|[Cálculos en modelos multidimensionales](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)|  
|Traducciones|[Traducciones en modelos multidimensionales &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)|  
  
## <a name="related-tasks"></a>Tareas relacionadas  
  
|Tema|Description|  
|-----------|-----------------|  
|[Crear un cubo con el Asistente para cubos](../../analysis-services/multidimensional-models/create-a-cube-using-the-cube-wizard.md)|Describe la utilización del Asistente para cubos para definir un cubo, dimensiones, atributos de dimensión y jerarquías definidas por el usuario.|  
|[Crear medidas y grupos de medida en modelos multidimensionales](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)|Describe cómo definir los grupos de medida.|  
|[Cálculos en modelos multidimensionales](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)|Describe cómo definir y configurar un cálculo en un script MDX.|  
|[Acciones en modelos multidimensionales](../../analysis-services/multidimensional-models/actions-in-multidimensional-models.md)|Describe cómo definir y configurar una acción.|  
|[Perspectivas de modelos multidimensionales](../../analysis-services/multidimensional-models/perspectives-in-multidimensional-models.md)|Describe cómo definir y configurar una perspectiva.|  
|[Definir procedimientos almacenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)|Describe cómo trabajar con los procedimientos almacenados.|  
  
  

