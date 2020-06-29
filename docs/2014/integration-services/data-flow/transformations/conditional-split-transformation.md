---
title: Transformación División condicional | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.conditionalsplittrans.f1
helpviewer_keywords:
- Conditional Split transformation
- route rows to different outputs [Integration Services]
ms.assetid: 3f8b5825-226f-413c-ba8f-0bb931ca3770
author: chugugrace
ms.author: chugu
ms.openlocfilehash: eba0f7b305d3b08692c69cc44202f9d565ca9d38
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85430942"
---
# <a name="conditional-split-transformation"></a>División condicional, transformación
  La transformación División condicional puede dirigir filas de datos a salidas diferentes en función del contenido de los datos. La implementación de la transformación División condicional es similar a una estructura de decisión CASE en un lenguaje de programación. Evalúa expresiones y, en función de los resultados, dirige la fila de datos a la salida especificada. Esta transformación también proporciona una salida predeterminada, por lo que si una fila no coincide con ninguna expresión, se dirige a la salida predeterminada.  
  
## <a name="configuration-of-the-conditional-split-transformation"></a>Configuración de la transformación División condicional  
 Puede configurar la transformación División condicional de las maneras siguientes:  
  
-   Proporcionar una expresión cuya evaluación devuelva un valor booleano para cada condición que desee probar con la transformación.  
  
-   Especificar el orden de evaluación de las condiciones. El orden es importante, ya que una fila se envía a la salida correspondiente a la primera condición que dé como resultado True.  
  
-   Especificar la salida predeterminada para la transformación. La transformación requiere que se especifique una salida predeterminada.  
  
 Cada fila de entrada solo se puede enviar a una salida, la correspondiente a la primera condición que resulte ser verdadera. Por ejemplo, las siguientes condiciones dirigen las filas de la columna **FirstName** que empiecen por la letra *A* a una salida, las filas que empiecen por la letra *B* a una salida diferente y todas las demás filas a la salida predeterminada.  
  
 Salida 1  
  
 `SUBSTRING(FirstName,1,1) == "A"`  
  
 Salida 2  
  
 `SUBSTRING(FirstName,1,1) == "B"`  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] incluye funciones y operadores que se pueden utilizar para crear expresiones que evalúen los datos de entrada y dirijan los datos de salida. Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../expressions/integration-services-ssis-expressions.md).  
  
 La transformación División condicional incluye la propiedad personalizada `FriendlyExpression`. Esta propiedad se puede actualizar a través de una expresión de propiedad, al cargar el paquete. Para más información, vea [Usar expresiones de propiedad en paquetes](../../expressions/use-property-expressions-in-packages.md) y [Propiedades personalizadas de transformación](transformation-custom-properties.md).  
  
 Esta transformación tiene una entrada, una o más salidas, y una salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el cuadro de diálogo **Editor de transformación División condicional** , vea [Conditional Split Transformation Editor](../../conditional-split-transformation-editor.md).  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](../../common-properties.md)  
  
-   [Propiedades personalizadas de transformación](transformation-custom-properties.md)  
  
 Para obtener más información sobre cómo establecer valores de propiedades, haga clic en uno de los temas siguientes:  
  
-   [Dividir un conjunto de datos usando la transformación División condicional](conditional-split-transformation.md)  
  
-   [Establecer las propiedades de un componente de flujo de datos](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [Dividir un conjunto de datos usando la transformación División condicional](conditional-split-transformation.md)  
  
## <a name="see-also"></a>Consulte también  
 [Flujo de datos](../data-flow.md)   
 [Transformaciones de Integration Services](integration-services-transformations.md)  
  
  
