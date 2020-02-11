---
title: Cubos en modelos multidimensionales | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- OLAP objects [Analysis Services], cubes
- cubes [Analysis Services], about cubes
- cubes [Analysis Services]
- OLAP [Analysis Services], cubes
ms.assetid: e0f7acf3-4b07-41fc-a5fc-ac30b4a56c54
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c7ce00bc87ca17c97996023d7cb9a4745b9882f3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66076104"
---
# <a name="cubes-in-multidimensional-models"></a>Cubos en modelos multidimensionales
  Un cubo es una estructura multidimensional que contiene información con fines analíticos; sus componentes principales son las dimensiones y las medidas. Las dimensiones definen la estructura del cubo que se utiliza para segmentar y dividir los datos, y las medidas proporcionan valores numéricos agregados importantes para el usuario final. Como estructura lógica, un cubo permite a una aplicación cliente recuperar valores, de medidas, como si estuvieran almacenados en las celdas del cubo; las celdas se definen para cada posible valor resumido. Las celdas del cubo se definen por la intersección de miembros de dimensión y contienen los valores agregados de las medidas en esa intersección concreta.  
  
## <a name="benefits-of-using-cubes"></a>Ventajas del uso de cubos  
 Un cubo proporciona un único lugar en el que se almacenan todos los datos relacionados con fines analíticos.  
  
## <a name="components-of-cubes"></a>Componentes de los cubos  
 Un cubo consta de:  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|Dimensions|[Dimensiones en modelos multidimensionales](dimensions-in-multidimensional-models.md)|  
|Medidas y grupos de medida|[Crear medidas y grupos de medida en modelos multidimensionales](create-measures-and-measure-groups-in-multidimensional-models.md)|  
|Particiones|[Particiones en modelos multidimensionales](partitions-in-multidimensional-models.md)|  
|perspectivas|[Perspectivas de modelos multidimensionales](perspectives-in-multidimensional-models.md)|  
|Jerarquías|[Crear jerarquías definidas por el usuario](user-defined-hierarchies-create.md)|  
|Acciones|[Acciones en modelos multidimensionales](actions-in-multidimensional-models.md)|  
|Indicadores clave de rendimiento (KPI)|[Indicadores clave de rendimiento &#40;KPI&#41; en modelos multidimensionales](key-performance-indicators-kpis-in-multidimensional-models.md)|  
|Cálculos|[Cálculos en modelos multidimensionales](calculations-in-multidimensional-models.md)|  
|Translations|[Traducciones en modelos multidimensionales](translations-in-multidimensional-models-analysis-services.md)|  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Crear un cubo con el Asistente para cubos](create-a-cube-using-the-cube-wizard.md)|Describe la utilización del Asistente para cubos para definir un cubo, dimensiones, atributos de dimensión y jerarquías definidas por el usuario.|  
|[Crear medidas y grupos de medida en modelos multidimensionales](create-measures-and-measure-groups-in-multidimensional-models.md)|Describe cómo definir los grupos de medida.|  
|[Cálculos en modelos multidimensionales](calculations-in-multidimensional-models.md)|Describe cómo definir y configurar un cálculo en un script MDX.|  
|[Acciones en modelos multidimensionales](actions-in-multidimensional-models.md)|Describe cómo definir y configurar una acción.|  
|[Perspectivas de modelos multidimensionales](perspectives-in-multidimensional-models.md)|Describe cómo definir y configurar una perspectiva.|  
|[Definir procedimientos almacenados](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)|Describe cómo trabajar con los procedimientos almacenados.|  
  
  
