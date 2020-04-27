---
title: Usar una expresión en un componente de flujo de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], data flow
- expressions [Integration Services], data flow components
ms.assetid: 9181b998-d24a-41fb-bb3c-14eee34f910d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bc9f6c28e775cdbd21806172d7074e655fdd1545
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66054819"
---
# <a name="use-an-expression-in-a-data-flow-component"></a>utilizar una expresión en un componente de flujo de datos
  Este procedimiento describe cómo agregar una expresión a la transformación División condicional o a la transformación Columna derivada. La transformación División condicional utiliza expresiones para definir las condiciones que dirigen las filas de datos a una salida de transformación y la transformación Columna derivada utiliza expresiones para definir los valores asignados a las columnas.  
  
 Para implementar una expresión en una transformación, el paquete ya debe incluir por lo menos una tarea Flujo de datos y un origen. Para obtener información sobre cómo agregar elementos a paquetes, vea los temas siguientes:  
  
-   [Agregar o eliminar tareas o contenedores en un flujo de control](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
    
  
-   [Agregar o eliminar un componente en un flujo de datos](data-flow/add-or-delete-a-component-in-a-data-flow.md)  
  
-   [Conectar componentes de un flujo de datos](data-flow/connect-components-in-a-data-flow.md)  
  
### <a name="to-create-an-expression"></a>Para crear una expresión  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  En el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] , haga clic en la pestaña **Flujo de control** y, a continuación, en la tarea Flujo de datos que contiene el flujo de datos en el que desea implementar la expresión.  
  
4.  Haga clic en la pestaña **Flujo de datos** y arrastre una transformación División condicional o Columna derivada del **Cuadro de herramientas** a la superficie de diseño.  
  
5.  Arrastre el conector verde desde el origen o desde una transformación a la transformación División condicional o Columna derivada.  
  
6.  Haga doble clic en la transformación para abrir el cuadro de diálogo correspondiente.  
  
7.  En el panel de la izquierda, expanda **Variables** para ver las variables del sistema y las definidas por el usuario, y expanda **Columnas** para ver las columnas de entrada de la transformación.  
  
8.  En el panel de la derecha, expanda **Funciones matemáticas**, **Funciones de cadena**, **Funciones de fecha y hora**, **Funciones NULL**, **Conversiones de tipo**y **Operadores** para tener acceso a las funciones, las conversiones y los operadores que proporciona la gramática de expresiones.  
  
9. Dependiendo de la transformación, siga uno de estos procedimientos para crear una expresión:  
  
    -   En el cuadro de diálogo **Editor de transformación División condicional** , arrastre las variables, columnas, funciones, operadores y conversiones a la columna **Condición** . O bien, puede escribir una expresión directamente en la columna **Condición** .  
  
    -   En el cuadro de diálogo **Editor de transformación Columna derivada** , arrastre las variables, columnas, funciones, operadores y conversiones a la columna **Expresión** . O bien, puede escribir una expresión directamente en la columna **Expresión** .  
  
        > [!NOTE]  
        >   Al quitar el foco de la columna **Condición** o **Expresión** , el texto de la expresión podría resaltarse para indicar que la sintaxis de la expresión es incorrecta.  
  
10. Haga clic en **Aceptar** para salir del cuadro de diálogo.  
  
    > [!NOTE]  
    >  Si la expresión no es válida, aparece una alerta que describe los errores de sintaxis de la expresión.  
  
## <a name="see-also"></a>Consulte también  
 [Integration Services &#40;expresiones de&#41; SSIS](expressions/integration-services-ssis-expressions.md)   
 [División condicional, transformación](data-flow/transformations/conditional-split-transformation.md)   
 [Transformación columna derivada](data-flow/transformations/derived-column-transformation.md)   
 [Tarea flujo de datos](control-flow/data-flow-task.md)   
 [Flujo de datos](data-flow/data-flow.md)  
  
  
