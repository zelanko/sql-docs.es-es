---
title: Contenedor de bucles Para | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.forloopcontainerdetails.f1
helpviewer_keywords:
- repeating control flow
- containers [Integration Services], For Loop
- For Loop containers
ms.assetid: 44cf7355-992b-4bbf-a28c-bfb012de06f6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 991223c373113b465c3182f552e5f5d157efef9f
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58384723"
---
# <a name="for-loop-container"></a>Contenedor de bucles For
  El contenedor de bucles For define un flujo de control que se repite en un paquete. La implementación del bucle es similar a la estructura de bucle **For** de los lenguajes de programación. En cada repetición del bucle, el contenedor de bucles For evalúa una expresión y repite el flujo de trabajo hasta que la expresión se evalúe como `False`.  
  
 El contenedor de bucles For usa los elementos siguientes para definir el bucle:  
  
-   Una expresión de inicialización opcional que asigna valores a los contadores de bucle.  
  
-   Una expresión de evaluación que contiene la expresión usada para comprobar si el bucle debe detenerse o continuar.  
  
-   Una expresión de iteración opcional que incrementa o disminuye el contador del bucle.  
  
 El siguiente diagrama muestra un contenedor de bucles For con una tarea Enviar correo. Si la expresión de inicialización es `@Counter = 0`, la expresión de evaluación es `@Counter < 4`y la expresión de iteración es `@Counter = @Counter + 1`, el bucle se repetirá cuatro veces y enviará cuatro mensajes de correo electrónico.  
  
 ![Un contenedor de bucles Para repite una tarea cuatro veces](../media/ssis-forloop.gif "A For Loop container repeats a task four times")  
  
 Las expresiones deben ser expresiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] válidas.  
  
 Para crear las expresiones de inicialización y asignación, puede utilizar el operador de asignación (=). La gramática de expresiones de Integration Services no admite este operador; solo se puede utilizar en las expresiones de inicialización y asignación del contenedor de bucles For. Cualquier expresión que use el operador de asignación necesita tener la sintaxis `@Var = <expression>`, donde **Var** es una variable de tiempo de ejecución y \<expression> es una expresión que sigue las reglas de sintaxis de la expresión [!INCLUDE[ssIS](../../../includes/ssis-md.md)]. La expresión puede incluir variables, literales y cualquier operador o función compatible con la gramática de expresiones de SSIS. La evaluación de la expresión debe devolver un tipo de datos que se pueda convertir al tipo de datos de la variable.  
  
 Un contenedor de bucles For solo puede tener una expresión de evaluación. Esto significa que el contenedor de bucles For ejecutará todos los elementos de flujo de control el mismo número de veces. Como el contenedor de bucles For puede incluir otros contenedores de bucles For, es posible generar bucles anidados e implementar bucles complejos en paquetes.  
  
 Puede establecer una propiedad de transacción en el contenedor de bucles For para definir una transacción para un subconjunto del flujo de control del paquete. De esta manera, puede administrar las transacciones en mayor detalle. Por ejemplo, si un contenedor de bucles For repite un flujo de control que actualiza los datos de una tabla varias veces, puede configurar el bucle For y su flujo de control para que utilicen una transacción, a fin de asegurarse de que si no se actualizan todos los datos correctamente, no se actualice ningún dato. Para más información, vea [Transacciones de Integration Services](../integration-services-transactions.md).  
  
## <a name="configuration-of-the-for-loop-container"></a>Configuración del contenedor de bucles For  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor de bucles For](../for-loop-editor.md)  
  
-   [Página Expresiones](../expressions/expressions-page.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, vea la documentación de la clase **T:Microsoft.SqlServer.Dts.Runtime.ForLoop** en la Guía del desarrollador.  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obtener información acerca de cómo configurar el contenedor de bucles For, vea los temas siguientes.  
  
-   [Configurar un contenedor de bucles For](for-loop-container.md)  
  
-   [Establecer las propiedades de tareas o contenedores](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>Vea también  
 [Flujo de control](control-flow.md)   
 [Expresiones de Integration Services &#40;SSIS&#41;](../expressions/integration-services-ssis-expressions.md)  
  
  
