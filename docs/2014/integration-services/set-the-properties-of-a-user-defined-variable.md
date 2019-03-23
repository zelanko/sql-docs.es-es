---
title: Establecer las propiedades de una Variable definida por el usuario | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- modifying variables
- variables [Integration Services], properties
ms.assetid: f98ddbec-f668-4dba-a768-44ac3ae0536f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4aaac5f66e8c01364419d8d2d9d5e853bf929ef7
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58385533"
---
# <a name="set-the-properties-of-a-user-defined-variable"></a>Establecer las propiedades de una variable definida por el usuario
  Para establecer las propiedades de una variable definida por el usuario en [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], puede utilizar una de las características siguientes:  
  
-   Ventana Variables.  
  
-   Ventana Propiedades. El **propiedades** ventana enumeran las propiedades para configurar variables que no están disponibles en el **Variables** ventana: Descripción, EvaluateAsExpression, Expression, ReadOnly, ValueType y IncludeInDebugDump.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] también proporciona un conjunto de variables del sistema cuyas propiedades no se pueden actualizar, excepto la propiedad de RaiseChangedEvent.  
  
 **Expresiones de valor en Variables**  
  
 Cuando se usa la ventana **Propiedades** para establecer expresiones en una variable definida por el usuario:  
  
-   El valor de una variable se puede establecer por las propiedades Value o Expression. De forma predeterminada, la propiedad EvaluateAsExpression se establece en `False` y el valor de la variable se establece la propiedad Value. Para usar una expresión para establecer el valor, primero debe establecer EvaluateAsExpression en `True`y, a continuación, escriba una expresión en la propiedad de expresión. La propiedad Value se establece automáticamente en el resultado de la evaluación de la expresión.  
  
-   La propiedad ValueType contiene el tipo de datos del valor de la propiedad Value. Si Value se establece con una expresión, ValueType se actualiza automáticamente a un tipo de datos compatible con el resultado de la evaluación de la expresión. Por ejemplo, si Value contiene 0 y la propiedad ValueType contiene **Int32** y, a continuación, Establece Expression en GETDATE(), Value contiene la fecha y hora actuales y ValueType se establecerá en `DateTime`.  
  
-   La ventana **Propiedades** de la variable proporciona acceso al cuadro de diálogo **Generador de expresiones** . Esta herramienta se puede usar para generar, validar y evaluar expresiones. Para más información, vea [Generador de expresiones](expressions/expression-builder.md) y [Expresiones de Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md).  
  
 Cuando se usa la ventana **Variables** para establecer expresiones en una variable definida por el usuario:  
  
-   Para usar una expresión para establecer el valor de la variable, primero confirme que el tipo de datos es compatible con el resultado de evaluación de la expresión y, a continuación, escriba una expresión en el `Expression` columna de la **Variables** ventana. La propiedad EvaluateAsExpression en el **propiedades** ventana se establece automáticamente en `True`.  
  
-   Cuando asigne una expresión a una variable, un marcador especial de icono se muestra junto a la variable. Este marcador de icono especial también aparece junto a los administradores de conexiones y las tareas con expresiones establecidas.  
  
-   La ventana **Variables** de la variable proporciona acceso al cuadro de diálogo **Generador de expresiones** . Esta herramienta se puede usar para generar, validar y evaluar expresiones. Para más información, vea [Generador de expresiones](expressions/expression-builder.md) y [Expresiones de Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md).  
  
 Tanto en el **Variables** y **propiedades** ventana, si asigna una expresión a la variable, y `EvaluateAsExpression` está establecido en `True`, no se puede cambiar el tipo de datos.  
  
 **Establezca las propiedades de nombre y Namespace**  
  
 Los valores de las propiedades `Name` y `Namespace` deben empezar con una letra, como se define en el Estándar Unicode 2.0, o un carácter de subrayado (_). Los caracteres siguientes pueden ser letras o números, tal como se define en el Estándar Unicode 2.0, o el carácter de subrayado (\_).  
  
## <a name="using-the-variables-window-to-set-properties"></a>Usar la ventana Variables para establecer propiedades  
  
#### <a name="to-set-the-properties-of-a-variable-by-using-the-variables-window"></a>Para establecer las propiedades de una variable mediante la ventana Variables  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga clic con el botón secundario en el paquete para abrirlo.  
  
3.  En el menú **SSIS** , haga clic en **Variables**.  
  
     También puede ver la ventana **Variables** si asigna el comando View.Variables a una combinación de teclas que desee en la página **Teclado** del cuadro de diálogo **Opciones** .  
  
4.  Opcionalmente, haga clic en **Opciones de cuadrícula** de la ventana **Variables**, seleccione las columnas que aparecen en la ventana **Variables** y seleccione filtros para aplicarlos a la lista de variables.  
  
5.  Seleccione la variable en la lista y, a continuación, actualice los valores de la `Name`, **tipo de datos**, `Value`, `Namespace`, **Generar evento de cambio**, **descripción,** y `Expression` columnas.  
  
6.  Seleccione la variable en la lista y haga clic en **Mover variable** para cambiar el ámbito.  
  
7.  Para guardar el paquete actualizado, en el menú **Archivo** , haga clic en **Guardar los elementos seleccionados**.  
  
## <a name="using-the-properties-window-to-set-properties"></a>Usar la ventana Propiedades para establecer propiedades  
  
#### <a name="to-set-the-properties-of-a-variable-by-using-the-properties-window"></a>Para establecer las propiedades de una variable mediante la ventana Propiedades  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga clic con el botón secundario en el paquete para abrirlo.  
  
3.  En el menú **Ver** , haga clic en **Ventana de propiedades**.  
  
4.  En el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] , haga clic en la pestaña **Explorador de paquetes** y expanda el nodo Paquete.  
  
5.  Para modificar variables en el ámbito de paquete, expanda el nodo Variables; también puede expandir los nodos Controladores de eventos o Ejecutables hasta localizar el nodo Variables que contiene la variable que desea modificar.  
  
6.  Haga clic en la variable cuyas propiedades desee modificar.  
  
7.  En la ventana **Propiedades** , actualice las propiedades de la variable de lectura y escritura. Algunas propiedades son solo de lectura/escritura para las variables definidas por el usuario.  
  
     Para más información sobre las propiedades, vea [Integration Services &#40;SSIS&#41; Variables](integration-services-ssis-variables.md).  
  
8.  Para guardar el paquete actualizado, en el menú **Archivo** , haga clic en **Guardar los elementos seleccionados**.  
  
## <a name="see-also"></a>Vea también  
 [Variables de Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md)   
 [Usar variables en paquetes](../../2014/integration-services/use-variables-in-packages.md)   
 [Agregar, eliminar, cambiar el ámbito de la variable definida por el usuario en un paquete](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
  
