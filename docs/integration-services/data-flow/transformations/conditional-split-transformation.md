---
title: "Transformaci&#243;n Divisi&#243;n condicional | Microsoft Docs"
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
  - "sql13.dts.designer.conditionalsplittrans.f1"
helpviewer_keywords: 
  - "División condicional, transformación"
  - "enrutar filas a distintas salidas [Integration Services]"
ms.assetid: 3f8b5825-226f-413c-ba8f-0bb931ca3770
caps.latest.revision: 51
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 51
---
# Transformaci&#243;n Divisi&#243;n condicional
  La transformación División condicional puede dirigir filas de datos a salidas diferentes en función del contenido de los datos. La implementación de la transformación División condicional es similar a una estructura de decisión CASE de un lenguaje de programación. Evalúa expresiones y, en función de los resultados, dirige la fila de datos a la salida especificada. Esta transformación también proporciona una salida predeterminada, de modo que si una fila no coincide con ninguna expresión, se dirige a la salida predeterminada.  
  
## Configuración de la transformación División condicional  
 Puede configurar la transformación División condicional de las maneras siguientes:  
  
-   Proporcionar una expresión cuya evaluación devuelva un valor booleano para cada condición que desee probar con la transformación.  
  
-   Especificar el orden de evaluación de las condiciones. El orden es importante, ya que una fila se envía a la salida correspondiente a la primera condición que dé como resultado True.  
  
-   Especificar la salida predeterminada para la transformación. La transformación requiere que se especifique una salida predeterminada.  
  
 Cada fila de entrada solo se puede enviar a una salida, la correspondiente a la primera condición que resulte ser verdadera. Por ejemplo, las siguientes condiciones dirigen las filas de la columna **FirstName** que empiecen por la letra *A* a una salida, las filas que empiecen por la letra *B* a una salida diferente y todas las demás filas a la salida predeterminada.  
  
 Salida 1  
  
 `SUBSTRING(FirstName,1,1) == "A"`  
  
 Salida 2  
  
 `SUBSTRING(FirstName,1,1) == "B"`  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] incluye funciones y operadores que se pueden utilizar para crear expresiones que evalúen los datos de entrada y dirijan los datos de salida. Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
 La transformación División condicional incluye la propiedad personalizada **FriendlyExpression** . Esta propiedad se puede actualizar a través de una expresión de propiedad, al cargar el paquete. Para más información, vea [Usar expresiones de propiedad en paquetes](../../../integration-services/expressions/use-property-expressions-in-packages.md) y [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Esta transformación tiene una entrada, una o más salidas, y una salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el cuadro de diálogo **Editor de transformación División condicional** , vea [Conditional Split Transformation Editor](../../../integration-services/data-flow/transformations/conditional-split-transformation-editor.md).  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](../Topic/Common%20Properties.md)  
  
-   [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obtener más información sobre cómo establecer valores de propiedades, haga clic en uno de los temas siguientes:  
  
-   [Dividir un conjunto de datos usando la transformación División condicional](../../../integration-services/data-flow/transformations/split-a-dataset-by-using-the-conditional-split-transformation.md)  
  
-   [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## Tareas relacionadas  
 [Dividir un conjunto de datos usando la transformación División condicional](../../../integration-services/data-flow/transformations/split-a-dataset-by-using-the-conditional-split-transformation.md)  
  
## Vea también  
 [Flujo de datos](../../../integration-services/data-flow/data-flow.md)   
 [Transformaciones de Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  