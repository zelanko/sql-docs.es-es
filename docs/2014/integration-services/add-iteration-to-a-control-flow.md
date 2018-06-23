---
title: Agregar iteración a un flujo de Control | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- repeating workflows
- adding iterations
- control flow [Integration Services], iterations
- expressions [Integration Services], control flow
- iterations [Integration Services]
- For Loop containers
ms.assetid: eb3a7494-88ae-4165-9d0f-58715eb1734a
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 7727dafeee728347511e91723ae9674fe9fd089e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108647"
---
# <a name="add-iteration-to-a-control-flow"></a>Agregar iteración a un flujo de control
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] incluye el contenedor de bucles Para, un elemento de flujo de control que simplifica la inclusión de bucles que repiten condicionalmente un flujo de control en un paquete. Para más información, consulte [For Loop Container](control-flow/for-loop-container.md).  
  
 El contenedor de bucles For evalúa una condición en cada iteración del bucle y se detiene cuando la condición es false. El contenedor de bucles For incluye expresiones para inicializar el bucle, especificando la condición de evaluación que detiene la ejecución del flujo de control repetido y asignando un valor a una expresión que actualiza el valor con el que se compara la condición de evaluación. Debe proporcionar una condición de evaluación, pero las expresiones de inicialización y asignación son opcionales.  
  
 El contenedor de bucles For no proporciona ninguna funcionalidad, sino que proporciona solo la estructura sobre la que se genera un flujo de control repetible. Para proporcionar la funcionalidad del contenedor, debe incluir por lo menos una tarea en el contenedor de bucles For. Para más información, consulte [Integration Services Tasks](control-flow/integration-services-tasks.md).  
  
 El contenedor de bucles For puede incluir un flujo de control con varias tareas y otros contenedores. Agregar tareas y contenedores a un contenedor de bucles For es similar a agregarlas a un paquete, salvo que las tareas y contenedores se arrastran al contenedor de bucles For en lugar de al paquete. Si el contenedor de bucles For incluye más de una tarea o contenedor, puede conectarlos mediante restricciones de precedencia, tal y como se hace en un paquete. Para más información, consulte [Precedence Constraints](control-flow/precedence-constraints.md).  
  
## <a name="using-expressions-in-for-loop-configuration"></a>Uso de expresiones en la configuración de bucles For  
 Al configurar el contenedor de bucles For especificando una condición de evaluación, valor de inicialización o valor de asignación, puede usar literales o expresiones.  
  
 Las expresiones pueden incluir variables. La ventaja de usar variables es que se pueden actualizar en tiempo de ejecución, lo que hace que los paquetes sean más flexibles y fáciles de administrar. La longitud máxima de una expresión es 4000 caracteres.  
  
 Al especificar una variable en una expresión, el nombre de la variable debe venir precedido por el signo (@). Por ejemplo, para una variable denominada `Counter`, escriba @Counter en la expresión que usa el contenedor de bucles for. Si se incluye la propiedad de espacio de nombres en la variable, debe escribir la variable y el espacio de nombres entre paréntesis. Por ejemplo, para un `Counter` variable en el `MyNamespace` espacio de nombres, tipo [@MyNamespace::Counter].  
  
 Las variables que usa el contenedor de bucles For se deben definir en el ámbito del contenedor de bucles For o en el ámbito de cualquier contenedor que se encuentre más arriba en la jerarquía de contenedores de paquetes. Por ejemplo, un contenedor de bucles For puede usar variables definidas en su ámbito y también variables definidas en el ámbito de paquetes. Para más información, vea [Variables de Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md) y [Usar variables en paquetes](../../2014/integration-services/use-variables-in-packages.md).  
  
 La gramática de expresiones de [!INCLUDE[ssIS](../includes/ssis-md.md)] proporciona un conjunto completo de operadores y funciones para implementar expresiones complejas usadas para la evaluación, inicialización o asignación. Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md).  
  
### <a name="to-implement-a-for-loop-container-in-a-control-flow"></a>Para implementar un contenedor de bucles For en un flujo de control  
  
1.  Agregue el contenedor de bucles For al paquete. Para obtener más información, vea [agregar o eliminar una tarea o un contenedor en un flujo de Control](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
2.  Agregue tareas y contenedores al contenedor de bucles For. Para obtener más información, vea [agregar o eliminar una tarea o un contenedor en un flujo de Control](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
3.  Conecte tareas y contenedores en el contenedor de bucles For mediante restricciones de precedencia. Para más información, vea [Conectar tareas y contenedores mediante una restricción de precedencia predeterminada](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md).  
  
4.  Configure el contenedor de bucles For. Para más información, vea [Configurar un contenedor de bucles For](../../2014/integration-services/configure-a-for-loop-container.md).  
  
## <a name="see-also"></a>Vea también  
 [Agregar o eliminar una tarea o un contenedor en un flujo de Control](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [Agrupar o desagrupar componentes](group-or-ungroup-components.md)   
 [Conectar tareas y contenedores mediante una restricción de precedencia predeterminada](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)   
 [Agregar enumeración a un flujo de Control](../../2014/integration-services/add-enumeration-to-a-control-flow.md)   
 [Flujo de control](control-flow/control-flow.md)  
  
  