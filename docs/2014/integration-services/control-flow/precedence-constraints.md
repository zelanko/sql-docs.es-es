---
title: Restricciones de precedencia | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- tasks [Integration Services], precedence constraints
- control flow [Integration Services], precedence constraints
- precedence constraints [Integration Services]
- constraints [Integration Services]
- sequence execution options [Integration Services]
- containers [Integration Services], precedence constraints
ms.assetid: c5ce5435-fd89-4156-a11f-68470a69aa9f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bc23747a13ee2e5b126b7e57ba7121878d05643d
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176475"
---
# <a name="precedence-constraints"></a>Restricciones de precedencia
  Las restricciones de precedencia vinculan ejecutables, contenedores y tareas de paquetes en un flujo de control, y especifican condiciones que determinan si se ejecutan los ejecutables. Un ejecutable puede ser un contenedor de bucles For, de bucles Foreach o de secuencia, o bien una tarea o un controlador de eventos. Los controladores de eventos usan las restricciones de precedencia para vincular sus ejecutables en un flujo de control.

 Una restricción de precedencia vincula dos ejecutables: el ejecutable de precedencia y el ejecutable restringido. El ejecutable de precedencia se ejecuta antes del ejecutable restringido y el resultado de la ejecución del ejecutable de precedencia puede determinar si se ejecuta el ejecutable restringido. El siguiente diagrama muestra dos ejecutables vinculados por una restricción de precedencia.

 ![Ejecutables conectados mediante una restricción de precedencia](../media/ssis-pcsimple.gif "Ejecutables conectados mediante una restricción de precedencia")

 En un flujo de control lineal, es decir, un flujo sin bifurcaciones, las restricciones de precedencia controlan ellas mismas la secuencia en que se ejecutan las tareas. Si un flujo de control se bifurca, el motor de tiempo de ejecución de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] determina el orden de ejecución entre las tareas y contenedores que siguen inmediatamente la bifurcación. El motor de tiempo de ejecución también determina el orden de ejecución entre los flujos de trabajo no conectados en un flujo de control.

 La arquitectura de contenedor anidado de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] habilita todos los contenedores, salvo el contenedor del host de la tarea que encapsula una sola tarea, para incluir otros contenedores, cada uno de los cuales tiene su propio flujo de control. Los contenedores de bucles For, de bucles Foreach y de secuencia pueden incluir varias tareas y otros contenedores, que a su vez pueden incluir varias tareas y contenedores. Por ejemplo, un paquete con una tarea Script y un contenedor de secuencias tiene una restricción de precedencia que vincula la tarea Script y el contenedor de secuencias. El contenedor de secuencias incluye tres tareas Script y las restricciones de precedencia vinculan las tres tareas Script en un flujo de control. El siguiente diagrama muestra las restricciones de precedencia en un paquete con dos niveles de anidamiento.

 ![Restricciones de precedencia en un paquete](../media/mw-dts-12.gif "Restricciones de precedencia en un paquete")

 Dado que el paquete se encuentra en la parte superior de la jerarquía de contenedores de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , no se pueden vincular varios paquetes mediante restricciones de precedencia. Sin embargo, puede agregar una tarea Ejecutar paquete a un paquete y vincular indirectamente otro paquete en el flujo de control.

 Puede configurar las restricciones de precedencia de las siguientes maneras:

-   Especificar una operación de evaluación. La restricción de precedencia usa un valor de restricción, una expresión, ambas cosas o una de ellas para determinar si se ejecuta el ejecutable restringido.

-   Si la restricción de precedencia usa un resultado de ejecución, puede especificar el resultado de ejecución para que sea correcto, error o conclusión.

-   Si la restricción de precedencia usa un resultado de evaluación, puede proporcionar una expresión que se evalúa como un valor booleano.

-   Especificar si la restricción de precedencia se evalúa individualmente o junto con otras restricciones que se aplican al ejecutable restringido.

## <a name="evaluation-operations"></a>Operaciones de evaluación
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] proporciona las siguientes operaciones de evaluación:

-   Una restricción que usa solamente el resultado de la ejecución del ejecutable de precedencia para determinar si el ejecutable restringido se ejecuta. El resultado de la ejecución del ejecutable de precedencia puede ser conclusión, correcto o error. Esta es la operación predeterminada.

-   Una expresión que se evalúa para determinar si se ejecuta el ejecutable restringido. Si la expresión se evalúa como TRUE, el ejecutable restringido se ejecuta.

-   Una expresión y una restricción que combina los requisitos de los resultados de la ejecución del ejecutable de precedencia y los resultados de devolución de la evaluación de la expresión.

-   Una expresión o una restricción que usa los resultados de la ejecución del ejecutable de precedencia o los resultados de devolución de la evaluación de la expresión.

 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] usa colores para identificar el tipo de restricción de precedencia. La restricción de operación realizada correctamente es verde, la de error es roja y la de conclusión es azul. Para mostrar etiquetas de texto en el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] que muestran el tipo de la restricción, debe configurar las características de accesibilidad del Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] .

 La expresión debe ser una expresión de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] válida y puede incluir funciones, operadores y variables del sistema y personalizadas. Para obtener más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../expressions/integration-services-ssis-expressions.md) y [Variables de Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md).

## <a name="execution-results"></a>Resultados de la ejecución
 La restricción de precedencia puede usar los siguientes resultados de ejecución individualmente o combinados con una expresión.

-   La conclusión requiere solamente que el ejecutable de precedencia se haya completado, sin importar su resultado, para que el ejecutable restringido se pueda ejecutar.

-   El resultado correcto requiere que el ejecutable de precedencia se complete correctamente para que pueda ejecutarse el ejecutable restringido.

-   El resultado de error requiere que el ejecutable de precedencia genere un error para que pueda ejecutarse el ejecutable restringido.

> [!NOTE]
>  Solo las restricciones de precedencia que son miembros de la misma colección `Precedence Constraint` se pueden agrupar en una condición lógica AND. Por ejemplo, no se pueden combinar restricciones de precedencia de dos contenedores de bucles Foreach.

## <a name="configuration-of-the-precedence-constraint"></a>Configuración de la restricción de precedencia
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.

 Para obtener información sobre las propiedades que se pueden configurar en el Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , vea [Editor de restricciones de precedencia](../precedence-constraint-editor.md).

 Para obtener información sobre cómo establecer mediante programación estas propiedades, vea <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint>.

## <a name="related-tasks"></a>Related Tasks
 Para obtener información detallada sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:

-   [Establecer las propiedades de una restricción de precedencia](../set-the-properties-of-a-precedence-constraint.md)

-   [Establecer el valor de una restricción de precedencia mediante el menú contextual](../set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)

-   [Conectar tareas y contenedores mediante una restricción de precedencia predeterminada](../connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)

     En este tema se ofrece información sobre cómo se configura el comportamiento predeterminado para las restricciones de precedencia y cómo se conectan los ejecutables mediante las restricciones de precedencia predeterminadas.

## <a name="related-content"></a>Contenido relacionado
 Artículo técnico, sobre [ejemplos de expresiones SSIS](https://go.microsoft.com/fwlink/?LinkId=220761), en social.technet.microsoft.com

## <a name="see-also"></a>Consulte también
 [Agregar expresiones a las restricciones de precedencia](../add-expressions-to-precedence-constraints.md) [varias restricciones de precedencia](../multiple-precedence-constraints.md)


