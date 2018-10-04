---
title: Agregar expresiones a las restricciones de precedencia | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- precedence executables [Integration Services]
- precedence constraints [Integration Services], adding expressions
- adding expressions
- constrained executables [Integration Services]
- combining constraints
- expressions [Integration Services], constraints
ms.assetid: 5574d89a-a68e-4b84-80ea-da93305e5ca1
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8cee9f40b308c545a9ebc74f2e4f1a88618d5008
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48208285"
---
# <a name="add-expressions-to-precedence-constraints"></a>Agregar expresiones a las restricciones de precedencia
  Una restricción de precedencia puede utilizar una expresión para definir la restricción entre dos aplicaciones ejecutables: el ejecutable de precedencia y el ejecutable restringido. Los ejecutables pueden ser tareas o contenedores. La expresión se puede usar por sí sola o combinada con el resultado de la ejecución del ejecutable de precedencia. El resultado de la ejecución de un ejecutable es su ejecución correcta o un error. Cuando configura el resultado de ejecución de una restricción de precedencia, puede establecer el resultado de ejecución en `Success`, `Failure` o `Completion`. `Success` exige la ejecución correcta del ejecutable de precedencia, `Failure` requiere que el ejecutable de precedencia genere un error y `Completion` indica que el ejecutable restringido se debe ejecutar independientemente de si la tarea de precedencia se ejecuta correctamente o genera un error. Para más información, consulte [Precedence Constraints](control-flow/precedence-constraints.md).  
  
 La expresión debe evaluarse como `True` o `False` y debe ser una expresión válida de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. La expresión puede usar literales, variables del sistema y personalizadas, y las funciones y operadores que proporciona la gramática de expresiones de [!INCLUDE[ssIS](../includes/ssis-md.md)] . Por ejemplo, la expresión `@Count == SQRT(144) + 10` usa la variable `Count`, la función SQRT y los operadores igual (==) y sumar (+). Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md).  
  
 En la ilustración siguiente, la tarea A y la tarea B están vinculadas por una restricción de precedencia que usa un resultado de ejecución y una expresión. El valor de restricción se establece en `Success` y la expresión es `@X >== @Z`. La tarea B, la tarea restringida, se ejecuta solamente si la tarea A se completa correctamente y el valor de la variable `X` es mayor o igual al valor de la variable `Z`.  
  
 ![Restricciones de precedencia entre dos tareas](media/mw-dts-03.gif "Precedence constraint between two tasks")  
  
 Los ejecutables también se pueden vincular mediante varias restricciones de precedencia que contienen diferentes expresiones. Por ejemplo, en la siguiente ilustración, las tareas B y C están vinculadas a la tarea A por restricciones de precedencia que usan resultados de ejecución y expresiones. Ambos valores de restricción se establecen en `Success.` una restricción de precedencia incluye la expresión `@X >== @Z`, y la otra restricción de precedencia incluye la expresión `@X < @Z`. Según los valores de la variable `X` y la variable `Z`, se ejecuta la tarea C o la tarea B.  
  
 ![Expresiones en restricciones de precedencia](media/mw-dts-04.gif "Expressions on precedence constraints")  
  
 Puede agregar o modificar una expresión mediante el **Editor de restricciones de precedencia** en el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] , o en la ventana Propiedades que proporciona [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] . Sin embargo, la ventana Propiedades no proporciona ninguna comprobación de la sintaxis de la expresión.  
  
 Si una restricción de precedencia incluye una expresión, aparece un icono en la superficie de diseño de la pestaña **Flujo de control** , junto a la restricción de precedencia, y la información sobre herramientas del icono muestra la expresión.  
  
## <a name="combining-execution-values-and-expressions"></a>Combinar valores de ejecución y expresiones  
 La siguiente tabla describe los efectos de combinar una restricción de valor de ejecución y una expresión en una restricción de precedencia.  
  
|Operación de evaluación|La restricción se evalúa como|La expresión se evalúa como|El ejecutable restringido se ejecuta|  
|--------------------------|-----------------------------|-----------------------------|---------------------------------|  
|Restricción|True|N/D|True|  
|Restricción|False|N/D|False|  
|Expresión|N/D|True|True|  
|Expresión|N/D|False|False|  
|Restricción y expresión|True|True|True|  
|Restricción y expresión|True|False|False|  
|Restricción y expresión|False|True|False|  
|Restricción y expresión|False|False|False|  
|Restricción o expresión|True|True|True|  
|Restricción o expresión|True|False|True|  
|Restricción o expresión|False|True|True|  
|Restricción o expresión|False|False|False|  
  
### <a name="to-add-an-expression-to-a-precedence-constraint"></a>Para agregar una expresión a una restricción de precedencia  
  
-   [Usar una expresión en una restricción de precedencia](../../2014/integration-services/use-an-expression-in-a-precedence-constraint.md)  
  
-   [Establecer las propiedades de una restricción de precedencia](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)  
  
## <a name="external-resources"></a>Recursos externos  
 Artículo técnico, sobre [ejemplos de expresiones SSIS](http://go.microsoft.com/fwlink/?LinkId=220761), en social.technet.microsoft.com  
  
## <a name="see-also"></a>Vea también  
 [Varias restricciones de precedencia](../../2014/integration-services/multiple-precedence-constraints.md)   
 [Restricciones de precedencia](control-flow/precedence-constraints.md)  
  
  
