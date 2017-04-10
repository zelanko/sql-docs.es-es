---
title: "Configurar propiedades de medidas | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "aditividad [Analysis Services]"
  - "ID, propiedad"
  - "ErrorConfiguration, propiedad"
  - "AggregateFunction, propiedad"
  - "DisplayFolder, propiedad"
  - "IgnoreUnrelatedDimensions, propiedad"
  - "FormatString, propiedad"
  - "Description, propiedad"
  - "suma parcial"
  - "propiedades [Analysis Services], grupos de medida"
  - "agregado, funciones [Analysis Services]"
  - "DataType, propiedad"
  - "ProcessingMode, propiedad"
  - "MeasureExpression, propiedad"
  - "AggregationPrefix, propiedad"
  - "Visible, propiedad"
  - "propiedades [Analysis Services], medidas"
  - "StorageLocation, propiedad"
  - "StorageMode, propiedad"
  - "formatos [Analysis Services], medidas"
  - "Source, propiedad"
  - "agregaciones [Analysis Services], medidas"
  - "medidas [Analysis Services], propiedades"
  - "no aditiva [Analysis Services]"
  - "Name, propiedad"
  - "medidas [Analysis Services], formatos de visualización"
  - "ProcessingPriority, propiedad"
  - "grupos de medida [Analysis Services], propiedades"
  - "Type, propiedad"
  - "ProactiveCaching, propiedad"
ms.assetid: e9031078-c4f5-4986-b0c9-4d064b622ab7
caps.latest.revision: 50
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 50
---
# Configurar propiedades de medidas
  Las medidas tienen propiedades que permiten definir su funcionamiento, así como controlar cómo aparecen ante los usuarios.  
  
 Puede establecer propiedades en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] al crear o editar un cubo o una medida. También puede establecerlas mediante programación, usando MDX o AMO. Vea [Crear medidas y grupos de medida en modelos multidimensionales](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md), [CREATE MEMBER &#40;instrucción MDX&#41;](../Topic/CREATE%20MEMBER%20Statement%20\(MDX\).md) y [Programar objetos básicos OLAP en AMO](../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-olap-basic-objects.md) para obtener más información.  
  
## Propiedades de medidas  
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
  
## Vea también  
 [Configurar las propiedades de los grupos de medida](../../analysis-services/multidimensional-models/configure-measure-group-properties.md)   
 [Modificar medidas](../../analysis-services/modifying-measures.md)  
  
  