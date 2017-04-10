---
title: "Editor de transformaci&#243;n Anulaci&#243;n de dinamizaci&#243;n | Microsoft Docs"
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
  - "sql13.dts.designer.unpivottransformation.f1"
helpviewer_keywords: 
  - "Editor de transformación Anulación de dinamización"
ms.assetid: 72a36ef0-4070-4f6c-9c74-0720109617dd
caps.latest.revision: 35
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 35
---
# Editor de transformaci&#243;n Anulaci&#243;n de dinamizaci&#243;n
  Use el cuadro de diálogo **Editor de transformación Anulación de dinamización** para seleccionar las columnas que se van a dinamizar en filas y especificar la columna de datos y la nueva columna de salida del valor dinámico.  
  
> [!NOTE]  
>  Este tema usa el escenario Anulación de dinamización descrito en [Transformación Anulación de dinamización](../../../integration-services/data-flow/transformations/unpivot-transformation.md) para mostrar el uso de las opciones.  
  
 Para obtener más información acerca de la transformación Anulación de dinamización, vea [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md).  
  
## Opciones  
 **Columnas de entrada disponibles**  
 Especifique las columnas que deben pasar a ser filas mediante las casillas.  
  
 **Nombre**  
 Muestra el nombre de la columna de entrada disponible.  
  
 **Paso a través**  
 Indique si desea incluir la columna en la salida de anulación de dinamización.  
  
 **Columna de entrada**  
 Seleccione de la lista de entradas disponibles las columnas para cada fila. Las selecciones se reflejan en las casillas activadas en la tabla **Columnas de entrada disponibles** .  
  
 En el escenario Anulación de dinamización descrito en [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md), las columnas de entrada son las columnas **Ham**, **Soda**, **Milk**, **Beer**y **Chips** .  
  
 **Columna de destino**  
 Escriba un nombre para la columna de datos.  
  
 En el escenario Anulación de dinamización descrito en [Transformación Anulación de dinamización](../../../integration-services/data-flow/transformations/unpivot-transformation.md), la columna de destino es la columna de cantidad (**Qty**).  
  
 **Valor de clave dinámica**  
 Escriba el nombre del valor de dinamización. El nombre predeterminado es el de la columna de entrada, pero puede elegir cualquier nombre descriptivo único.  
  
 Puede especificar el valor de esta propiedad con una expresión de propiedad.  
  
 En el escenario Anulación de dinamización descrito en [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md), los valores de dinamización se mostrarán como valores de texto en la nueva columna Product, designada en la opción **Nombre de la columna del valor de clave dinámica** , como los valores de texto **Ham**, **Soda**, **Milk**, **Beer**y **Chips**.  
  
 **Nombre de la columna del valor de clave dinámica**  
 Escriba un nombre para la columna del valor de dinamización. El valor predeterminado es "Valor de clave dinámica", pero podrá elegir cualquier nombre descriptivo único.  
  
 En el escenario Anulación de dinamización descrito en [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md), el Nombre de la columna del valor de clave dinámica es **Product** y designa la nueva columna **Product** en la que se anula la dinamización de las columnas **Ham**, **Soda**, **Milk**, **Beer**y **Chips** .  
  
## Vea también  
 [Referencia de errores y mensajes de Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Transformación dinámica](../../../integration-services/data-flow/transformations/pivot-transformation.md)  
  
  