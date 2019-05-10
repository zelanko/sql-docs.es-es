---
title: Configurar propiedades de medidas | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e93b254e42b117f97ea6bc2d71afe5487f6a5197
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2019
ms.locfileid: "65357416"
---
# <a name="configure-measure-properties"></a>Configurar propiedades de medidas
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Las medidas tienen propiedades que permiten definir su funcionamiento, así como controlar cómo aparecen ante los usuarios.  
  
 Puede establecer propiedades en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] al crear o editar un cubo o una medida. También puede establecerlas mediante programación, usando MDX o AMO. Vea [Crear medidas y grupos de medida en modelos multidimensionales](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md), [CREATE MEMBER &#40;instrucción MDX&#41;](../../mdx/mdx-data-definition-create-member.md) y [Programar objetos básicos OLAP en AMO](https://docs.microsoft.com/bi-reference/amo/programming-amo-olap-basic-objects) para obtener más información.  
  
## <a name="measure-properties"></a>Propiedades de medidas  
 Las medidas heredan determinadas propiedades del grupo de medida del que son miembro, aunque estas propiedades se reemplazan en el nivel de medida. Las propiedades de medidas determinan cómo se agrega una medida, su tipo de datos, el nombre que se muestra al usuario, la carpeta para mostrar en la que aparecerá la medida, su cadena de formato, cualquier expresión de medida, la columna de origen subyacente y la visibilidad para los usuarios.  
  
|Property|Definición|  
|--------------|----------------|  
|**AggregateFunction**|Requerido. Determina cómo se agregan las medidas. **Sum** es la agregación predeterminada. Para más información, vea [Use Aggregate Functions](../../analysis-services/multidimensional-models/use-aggregate-functions.md) para obtener una descripción de cada función.|  
|**DataType**|Requerido. Especifica el tipo de datos de la columna de la tabla de hechos subyacente a la que se enlaza la medida. Este valor se hereda de la columna de origen de forma predeterminada.|  
|**Descripción**|Ofrece una descripción de la medida, que se puede mostrar en aplicaciones cliente.|  
|**DisplayFolder**|Especifica la carpeta en la que se mostrará la medida a los usuarios cuando se conecten al cubo. Cuando un cubo tiene muchas medidas, se pueden utilizar carpetas para mostrar para categorizar las medidas y mejorar la exploración para el usuario.|  
|**FormatString**|Puede seleccionar el formato que se utiliza para mostrar los valores de las medidas a los usuarios mediante la propiedad **FormatString** de la medida.<br /><br /> Aunque se proporciona una lista de los formatos de visualización en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], se pueden especificar muchos otros formatos que no están en la lista. Puede especificar cualquier formato con nombre o definido por el usuario que sea válido en Microsoft Visual Basic.|  
|**ID**|Requerido. Muestra el identificador único (Id.) de la medida. Esta propiedad es de solo lectura.|  
|**MeasureExpression**|Especifica una expresión MDX restringida que define el valor de la medida. La expresión se evalúa en el nivel de hoja antes de agregarse, y permite la ponderación de un valor. Por ejemplo, en la conversión de moneda en que la tasa de cambio pondera un importe de ventas.|  
|**Name**|Requerido. Especifica el nombre de la medida.|  
|**Source**|Requerido. Especifica la columna de la vista del origen de datos a la que se enlaza la medida. Vea [Orígenes de datos y enlaces &#40;SSAS multidimensional&#41;](../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).|  
|**Visible**|Determina la visibilidad de la medida en las aplicaciones cliente.|  
  
## <a name="see-also"></a>Vea también  
 [Configurar las propiedades de los grupos de medida](../../analysis-services/multidimensional-models/configure-measure-group-properties.md)   
 [Modificar medidas](../multidimensional-tutorial/lesson-3-1-modifying-measures.md)  
  
  
