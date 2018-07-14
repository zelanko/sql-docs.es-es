---
title: Establecer las propiedades de una restricción de precedencia | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Precedence Constraint Editor dialog box
- precedence constraints [Integration Services], properties
ms.assetid: d990f600-5c09-4cd5-8528-0a58d79dc9f2
caps.latest.revision: 47
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 38e20290eb9499191307c7afb146e9242603c3ed
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37271351"
---
# <a name="set-the-properties-of-a-precedence-constraint"></a>Establecer las propiedades de una restricción de precedencia
  Para establecer las propiedades en restricciones de precedencia, puede utilizar una de estas herramientas:  
  
-   Puede utilizar el cuadro de diálogo **Editor de restricciones de precedencia** .  
  
-   Puede utilizar la ventana Propiedades. En la ventana Propiedades se enumeran las propiedades para configurar restricciones de precedencia que no están disponibles en el cuadro de diálogo **Editor de restricciones de precedencia** . En dicha ventana se puede proporcionar una descripción y un nombre de la restricción de precedencia y configurar la anotación que se debe mostrar para ella en la superficie de diseño.  
  
 Los procedimientos siguientes describen cómo establecer propiedades en restricciones de precedencia utilizando cada una de estas herramientas.  
  
### <a name="to-set-the-properties-of-a-precedence-constraint-by-using-the-precedence-constraint-editor"></a>Para establecer las propiedades de una restricción de precedencia mediante el Editor de restricciones de precedencia  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** .  
  
4.  Haga doble clic en la restricción de precedencia.  
  
     Se abre el **Editor de restricciones de precedencia** .  
  
5.  En la lista desplegable **Operación de evaluación** , seleccione una operación de evaluación.  
  
6.  En el `Value` lista desplegable, seleccione el resultado de la ejecución del ejecutable de precedencia.  
  
7.  Si la operación de evaluación usa una expresión, en el `Expression` cuadro, escriba una expresión y haga clic en **prueba** para evaluar la expresión.  
  
    > [!NOTE]  
    >  Los nombres de variables distinguen entre mayúsculas y minúsculas.  
  
8.  Si hay varias tareas o contenedores conectados al ejecutable restringido, seleccione **lógico y** para especificar que los resultados de la ejecución de todos los ejecutables anteriores deben evaluarse como `true`. Seleccione **o lógico** para especificar que el resultado de la ejecución de un único debe evaluarse como `true`.  
  
9. Haga clic en **Aceptar** para cerrar el **Editor de restricciones de precedencia**.  
  
10. Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
### <a name="to-set-the-properties-of-a-precedence-constraint-by-using-the-properties-window"></a>Para establecer las propiedades de una restricción de precedencia mediante la ventana Propiedades  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea modificar.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** . En la superficie de diseño de la pestaña **Flujo de control** , haga clic con el botón derecho en la restricción de precedencia y, luego, haga clic en **Propiedades**. En la ventana Propiedades, modifique los valores de las propiedades.  
  
4.  En la ventana **Propiedades** , establezca las siguientes propiedades de lectura y escritura para las restricciones de precedencia:  
  
    |Propiedad de lectura/escritura|Acción de configuración|  
    |--------------------------|--------------------------|  
    |Descripción|Escribir una descripción.|  
    |EvalOp|Seleccionar una operación de evaluación. Si el `Expression`, **ExpressionAndConstant**, o **ExpressionOrConstant** está seleccionada la operación, puede especificar una expresión.|  
    |Expresión|Si la operación de evaluación contiene una expresión, se debe proporcionar una expresión. La expresión debe evaluarse como un valor booleano. Para más información sobre el lenguaje de expresiones, vea [Expresiones de Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md).|  
    |AND lógico|Establecer `LogicalAnd` para especificar si la restricción de precedencia se evalúa en conjunto con otras restricciones de precedencia, cuando preceden varios ejecutables y están vinculados al ejecutable restringido|  
    |Nombre|Actualizar el nombre de la restricción de precedencia.|  
    |ShowAnnotation|Especificar el tipo de anotación que se va a usar. Elija **Never** para deshabilitar anotaciones, **AsNeeded** para habilitar anotaciones a petición, **ConstraintName** para realizar anotaciones automáticamente usando el valor de la propiedad Name, **ConstraintDescription** para realizar anotaciones automáticamente usando el valor de la propiedad Description y **ConstraintOptions** para realizar anotaciones automáticamente al usar el valor de las propiedades Value y Expression.|  
    |Valor|Si la operación de evaluación especificada en la propiedad EvalOP contiene una restricción, seleccione el resultado de la ejecución del ejecutable de restricción.|  
  
5.  Cierre la ventana Propiedades.  
  
6.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
## <a name="see-also"></a>Vea también  
 [Restricciones de precedencia](control-flow/precedence-constraints.md)   
 [Conectar tareas y contenedores mediante una restricción de precedencia predeterminada](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)   
 [Establecer el valor de una restricción de precedencia mediante el menú contextual](../../2014/integration-services/set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)   
 [Usar una expresión en una restricción de precedencia](../../2014/integration-services/use-an-expression-in-a-precedence-constraint.md)  
  
  
