---
title: "Editor de transformaci&#243;n Agregado (pesta&#241;a Avanzadas) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.aggregationtransformation.advanced.f1"
helpviewer_keywords: 
  - "Editor de transformación Agregado"
ms.assetid: 186a9736-2554-40a0-9cb2-877a8db5fde8
caps.latest.revision: 27
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# Editor de transformaci&#243;n Agregado (pesta&#241;a Avanzadas)
  Utilice la pestaña **Avanzadas** del cuadro de diálogo **Editor de transformación Agregado** para establecer las propiedades del componente, especificar agregaciones y establecer las propiedades de las columnas de entrada y salida.  
  
> [!NOTE]  
>  Las opciones para el recuento de claves, la escala de claves, la clave Count Distinct y la escala de claves distintas estarán disponibles en el componente si se especifican en la pestaña **Avanzadas**, en la salida si se especifican en la pantalla avanzada de la pestaña **Agregaciones** y en la columna si se especifican en la lista de columnas en la parte inferior de la pestaña **Agregaciones**.  
>   
>  En la transformación Agregado, **Claves** y **Escala de claves** hacen referencia al número de grupos que se esperan como resultado de una operación **Agrupar por** . **Claves Count Distinct** y **Escala Count Distinct** hacen referencia al número de valores distintos que se esperan como resultado de una operación **Recuento distinto** .  
  
 Para obtener más información acerca de la transformación Agregado, vea [Aggregate Transformation](../../../integration-services/data-flow/transformations/aggregate-transformation.md).  
  
## Opciones  
 **Escala de claves**  
 Si lo desea, especifique el número aproximado de claves que espera la agregación. La transformación utiliza esta información para optimizar el tamaño de caché inicial. De forma predeterminada, el valor de esta opción es **No especificado**. Si se especifica tanto **Escala de claves** como **Número de claves** , prevalece la opción **Número de claves** .  
  
|Value|Description|  
|-----------|-----------------|  
|No especificado|No se utiliza la propiedad **Escala de claves** .|  
|Baja|La agregación podrá escribir aproximadamente 500 000 claves.|  
|Media|La agregación podrá escribir aproximadamente 5.000.000 claves.|  
|Alta|La agregación podrá escribir más de 25.000.000 claves.|  
  
 **Número de claves**  
 Si lo desea, especifique el número exacto de claves que espera la agregación. La transformación utiliza esta información para optimizar el tamaño de caché inicial. Si se especifica tanto **Escala de claves** como **Número de claves** , prevalece la opción **Número de claves** .  
  
 **Escala Count Distinct**  
 Opcionalmente, puede especificar el número aproximado de valores DISTINCT que podrá escribir la agregación. De forma predeterminada, el valor de esta opción es **No especificado**. Si se especifica tanto **Escala Count Distinct** como **Claves Count Distinct** , prevalece la opción **Claves Count Distinct** .  
  
|Value|Description|  
|-----------|-----------------|  
|No especificado|No se utiliza la propiedad CountDistinctScale.|  
|Baja|La agregación podrá escribir aproximadamente 500.000 valores DISTINCT.|  
|Media|La agregación podrá escribir aproximadamente 5 000 000 valores DISTINCT.|  
|Alta|La agregación podrá escribir más de 25.000.000 valores DISTINCT.|  
  
 **Claves Count Distinct**  
 Opcionalmente, puede especificar el número exacto de valores DISTINCT que podrá escribir la agregación. Si se especifica tanto **Escala Count Distinct** como **Claves Count Distinct** , prevalece la opción **Claves Count Distinct** .  
  
 **Factor de ampliación automática**  
 Utilice un valor comprendido entre 1 y 100 para especificar el porcentaje en el que se puede ampliar la memoria durante la agregación. De forma predeterminada, el valor de esta opción es **25%**.  
  
## Vea también  
 [Referencia de errores y mensajes de Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformación Agregado &#40;pestaña Agregaciones&#41;](../../../integration-services/data-flow/transformations/aggregate-transformation-editor-aggregations-tab.md)   
 [Agregar valores en un conjunto de datos mediante la transformación Agregado](../../../integration-services/data-flow/transformations/aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
  