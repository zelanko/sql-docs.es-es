---
title: Configurar propiedades de medidas | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
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
- additivity [Analysis Services]
- ID property
- ErrorConfiguration property
- AggregateFunction property
- DisplayFolder property
- IgnoreUnrelatedDimensions property
- FormatString property
- Description property
- semiadditive
- properties [Analysis Services], measure groups
- aggregate functions [Analysis Services]
- DataType property
- ProcessingMode property
- MeasureExpression property
- AggregationPrefix property
- Visible property
- properties [Analysis Services], measures
- StorageLocation property
- StorageMode property
- formats [Analysis Services], measures
- Source property
- aggregations [Analysis Services], measures
- measures [Analysis Services], properties
- nonadditive [Analysis Services]
- Name property
- measures [Analysis Services], display formats
- ProcessingPriority property
- measure groups [Analysis Services], properties
- Type property
- ProactiveCaching property
ms.assetid: e9031078-c4f5-4986-b0c9-4d064b622ab7
caps.latest.revision: 50
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 576efdd0bac4b8298e3d204b065bbbd55ba6fff3
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="configure-measure-properties"></a>Configurar propiedades de medidas
  Las medidas tienen propiedades que permiten definir su funcionamiento, así como controlar cómo aparecen ante los usuarios.  
  
 Puede establecer propiedades en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] al crear o editar un cubo o una medida. También puede establecerlas mediante programación, usando MDX o AMO. Vea [Crear medidas y grupos de medida en modelos multidimensionales](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md), [CREATE MEMBER &#40;instrucción MDX&#41;](../../mdx/mdx-data-definition-create-member.md) y [Programar objetos básicos OLAP en AMO](../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-olap-basic-objects.md) para obtener más información.  
  
## <a name="measure-properties"></a>Propiedades de medidas  
 Las medidas heredan determinadas propiedades del grupo de medida del que son miembro, aunque estas propiedades se reemplazan en el nivel de medida. Las propiedades de medidas determinan cómo se agrega una medida, su tipo de datos, el nombre que se muestra al usuario, la carpeta para mostrar en la que aparecerá la medida, su cadena de formato, cualquier expresión de medida, la columna de origen subyacente y la visibilidad para los usuarios.  
  
|Propiedad|Definición|  
|--------------|----------------|  
|**AggregateFunction**|Requerido. Determina cómo se agregan las medidas. **Sum** es la agregación predeterminada. Para más información, vea [Use Aggregate Functions](../../analysis-services/multidimensional-models/use-aggregate-functions.md) para obtener una descripción de cada función.|  
|**DataType**|Requerido. Especifica el tipo de datos de la columna de la tabla de hechos subyacente a la que se enlaza la medida. Este valor se hereda de la columna de origen de forma predeterminada.|  
|**Description**|Ofrece una descripción de la medida, que se puede mostrar en aplicaciones cliente.|  
|**DisplayFolder**|Especifica la carpeta en la que se mostrará la medida a los usuarios cuando se conecten al cubo. Cuando un cubo tiene muchas medidas, se pueden utilizar carpetas para mostrar para categorizar las medidas y mejorar la exploración para el usuario.|  
|**FormatString**|Puede seleccionar el formato que se utiliza para mostrar los valores de las medidas a los usuarios mediante la propiedad **FormatString** de la medida.<br /><br /> Aunque se proporciona una lista de los formatos de visualización en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], se pueden especificar muchos otros formatos que no están en la lista. Puede especificar cualquier formato con nombre o definido por el usuario que sea válido en Microsoft Visual Basic.|  
|**ID**|Requerido. Muestra el identificador único (Id.) de la medida. Esta propiedad es de solo lectura.|  
|**MeasureExpression**|Especifica una expresión MDX restringida que define el valor de la medida. La expresión se evalúa en el nivel de hoja antes de agregarse, y permite la ponderación de un valor. Por ejemplo, en la conversión de moneda en que la tasa de cambio pondera un importe de ventas.|  
|**Nombre**|Requerido. Especifica el nombre de la medida.|  
|**Source**|Requerido. Especifica la columna de la vista del origen de datos a la que se enlaza la medida. Vea [Orígenes de datos y enlaces &#40;SSAS multidimensional&#41;](../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).|  
|**Visible**|Determina la visibilidad de la medida en las aplicaciones cliente.|  
  
## <a name="see-also"></a>Vea también  
 [Configurar las propiedades de los grupos de medida](../../analysis-services/multidimensional-models/configure-measure-group-properties.md)   
 [Modificar medidas](../../analysis-services/lesson-3-1-modifying-measures.md)  
  
  
