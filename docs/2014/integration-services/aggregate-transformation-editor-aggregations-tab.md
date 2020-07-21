---
title: Editor de transformación agregado (pestaña agregaciones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.aggregationtransformation.aggregations.f1
helpviewer_keywords:
- Aggregate Transformation Editor
ms.assetid: a01cb124-ec79-4673-b1a1-bf4d60ee1b45
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 59bf17aa0c13fcc771a75253d5ac9f46a160c57c
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439512"
---
# <a name="aggregate-transformation-editor-aggregations-tab"></a>Editor de transformación Agregado (pestaña Agregaciones)
  Use la pestaña **Agregaciones** del cuadro de diálogo **Editor de transformación Agregado** para especificar las columnas que desea agregar y las propiedades de agregación. Puede aplicar diversas agregaciones. Esta transformación no genera una salida de errores.  
  
> [!NOTE]  
>  Las opciones para el recuento de claves, la escala de claves, la clave Count Distinct y la escala de claves distintas estarán disponibles en el componente si se especifican en la pestaña **Avanzadas** , en la salida si se especifican en la pantalla avanzada de la pestaña **Agregaciones** y en la columna si se especifican en la lista de columnas en la parte inferior de la pestaña **Agregaciones** .  
>   
>  En la transformación Agregado, **Claves** y **Escala de claves** hacen referencia al número de grupos que se esperan como resultado de una operación **Agrupar por** . **Claves Count Distinct** y **Escala Count Distinct** hacen referencia al número de valores distintos que se esperan como resultado de una operación **Recuento distinto** .  
  
 Para obtener más información acerca de la transformación Agregado, vea [Aggregate Transformation](data-flow/transformations/aggregate-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Avanzadas/Básicas**  
 Muestra u oculta opciones para configurar diversas agregaciones para varias salidas. De forma predeterminada, las opciones Avanzadas aparecen ocultas.  
  
 **Nombre de agregación**  
 En la pantalla Avanzadas, escriba un nombre descriptivo para la agregación.  
  
 **Agrupar por columnas**  
 En la pantalla Avanzadas, seleccione las columnas que quiere agrupar en la lista **Columnas de entrada disponibles** como se explica a continuación.  
  
 **Escala de claves**  
 En la pantalla Avanzadas, especifique opcionalmente el número aproximado de claves que podrá escribir la agregación. De forma predeterminada, el valor de esta opción es **No especificado**. Si se seleccionan las propiedades **Escala de claves** y **Claves** , tendrá prioridad el valor de **Claves** .  
  
|Value|Descripción|  
|-----------|-----------------|  
|Sin especificar|No se utiliza la propiedad Escala de claves.|  
|Bajo|La agregación podrá escribir aproximadamente 500 000 claves.|  
|Media|La agregación podrá escribir aproximadamente 5.000.000 claves.|  
|Alto|La agregación podrá escribir más de 25.000.000 claves.|  
  
 **Claves**  
 En la pantalla Avanzadas, especifique opcionalmente el número exacto de claves que podrá escribir la agregación. Si se especifican **Escala de claves** y **Claves** , tendrá prioridad **Claves** .  
  
 **Columnas de entrada disponibles**  
 Seleccione una columna en la lista de columnas de entrada disponibles con las casillas de la tabla.  
  
 **Columna de entrada**  
 Seleccione las columnas de entrada disponibles de la lista.  
  
 **Alias de salida**  
 Escriba un alias para cada columna. El nombre predeterminado es el de la columna de entrada, pero puede elegir cualquier nombre descriptivo único.  
  
 **operación**  
 Elija una operación de la lista de operaciones disponibles con la siguiente tabla como guía.  
  
|Operación|Descripción|  
|---------------|-----------------|  
|**GROUP BY**|Divide los conjuntos de datos en grupos. Podrán agruparse columnas con cualquier tipo de datos. Para obtener más información, vea GROUP BY.|  
|**Sume**|Suma los valores de una columna. Solo podrán sumarse las columnas con tipos de datos numéricos. Para obtener más información, vea SUM.|  
|**Average**|Devuelve la media de los valores de columna de una columna. Solo podrá calcularse la media de las columnas con tipos de datos numéricos. Para obtener más información, vea AVG.|  
|**Recuento**|Devuelve el número de elementos de un grupo. Para obtener más información, vea COUNT.|  
|**CountDistinct**|Devuelve el número de valores únicos distintos de NULL de un grupo. Para obtener más información, vea COUNT y Distinct.|  
|**Mínimo**|Devuelve el valor mínimo en un grupo. Está restringido a los tipos de datos numéricos.|  
|**Máximo**|Devuelve el valor máximo en un grupo. Está restringido a los tipos de datos numéricos.|  
  
 **Marcas de comparación**  
 Si selecciona **Agrupar por**, use las casillas para controlar cómo realiza la transformación la comparación. Para obtener más información acerca de las opciones de comparación de cadenas, vea [Comparing String Data](data-flow/comparing-string-data.md).  
  
 **Escala Count DISTINCT**  
 Opcionalmente, puede especificar el número aproximado de valores DISTINCT que podrá escribir la agregación. De forma predeterminada, el valor de esta opción es **No especificado**. Si `CountDistinctScale` se especifican y **CountDistinctKeys** , **CountDistinctKeys** tiene prioridad.  
  
|Value|Descripción|  
|-----------|-----------------|  
|Sin especificar|No se utiliza la propiedad `CountDistinctScale`.|  
|Bajo|La agregación podrá escribir aproximadamente 500.000 valores DISTINCT.|  
|Media|La agregación podrá escribir aproximadamente 5 000 000 valores DISTINCT.|  
|Alto|La agregación podrá escribir más de 25.000.000 valores DISTINCT.|  
  
 **Claves Count DISTINCT**  
 Opcionalmente, puede especificar el número exacto de valores DISTINCT que podrá escribir la agregación. Si `CountDistinctScale` se especifican y **CountDistinctKeys** , **CountDistinctKeys** tiene prioridad.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformación agregado &#40;pestaña avanzadas&#41;](../../2014/integration-services/aggregate-transformation-editor-advanced-tab.md)   
 [Agregar valores en un conjunto de datos mediante la transformación Agregado](data-flow/transformations/aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
  
