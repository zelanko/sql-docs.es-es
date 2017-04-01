---
title: "Restricciones de precedencia | Microsoft Docs"
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
  - "sql13.dts.designer.precedenceconstraint.f1"
helpviewer_keywords: 
  - "tareas [Integration Services], restricciones de precedencia"
  - "flujo de control [Integration Services], restricciones de precedencia"
  - "restricciones de precedencia [Integration Services]"
  - "restricciones [Integration Services]"
  - "ejecución de secuencias, opciones [Integration Services]"
  - "contenedores [Integration Services], restricciones de precedencia"
ms.assetid: c5ce5435-fd89-4156-a11f-68470a69aa9f
caps.latest.revision: 51
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 50
---
# Restricciones de precedencia
  Las restricciones de precedencia vinculan ejecutables, contenedores y tareas de paquetes en un flujo de control, y especifican condiciones que determinan si se ejecutan los ejecutables. Un ejecutable puede ser un contenedor de bucles For, de bucles Foreach o de secuencia, o bien una tarea o un controlador de eventos. Los controladores de eventos usan las restricciones de precedencia para vincular sus ejecutables en un flujo de control.  
  
 Una restricción de precedencia vincula dos ejecutables: el ejecutable de precedencia y el ejecutable restringido. El ejecutable de precedencia se ejecuta antes del ejecutable restringido y el resultado de la ejecución del ejecutable de precedencia puede determinar si se ejecuta el ejecutable restringido. El siguiente diagrama muestra dos ejecutables vinculados por una restricción de precedencia.  
  
 ![Ejecutables conectados mediante una restricción de precedencia](../../integration-services/control-flow/media/ssis-pcsimple.gif "Ejecutables conectados mediante una restricción de precedencia")  
  
 En un flujo de control lineal, es decir, un flujo sin bifurcaciones, las restricciones de precedencia controlan ellas mismas la secuencia en que se ejecutan las tareas. Si un flujo de control se bifurca, el motor de tiempo de ejecución de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] determina el orden de ejecución entre las tareas y contenedores que siguen inmediatamente la bifurcación. El motor de tiempo de ejecución también determina el orden de ejecución entre los flujos de trabajo no conectados en un flujo de control.  
  
 La arquitectura de contenedor anidado de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] habilita todos los contenedores, salvo el contenedor del host de la tarea que encapsula una sola tarea, para incluir otros contenedores, cada uno de los cuales tiene su propio flujo de control. Los contenedores de bucles For, de bucles Foreach y de secuencia pueden incluir varias tareas y otros contenedores, que a su vez pueden incluir varias tareas y contenedores. Por ejemplo, un paquete con una tarea Script y un contenedor de secuencias tiene una restricción de precedencia que vincula la tarea Script y el contenedor de secuencias. El contenedor de secuencias incluye tres tareas Script y las restricciones de precedencia vinculan las tres tareas Script en un flujo de control. El siguiente diagrama muestra las restricciones de precedencia en un paquete con dos niveles de anidamiento.  
  
 ![Restricciones de precedencia en un paquete](../../integration-services/control-flow/media/mw-dts-12.gif "Restricciones de precedencia en un paquete")  
  
 Dado que el paquete se encuentra en la parte superior de la jerarquía de contenedores de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , no se pueden vincular varios paquetes mediante restricciones de precedencia. Sin embargo, puede agregar una tarea Ejecutar paquete a un paquete y vincular indirectamente otro paquete en el flujo de control.  
  
 Puede configurar las restricciones de precedencia de las siguientes maneras:  
  
-   Especificar una operación de evaluación. La restricción de precedencia usa un valor de restricción, una expresión, ambas cosas o una de ellas para determinar si se ejecuta el ejecutable restringido.  
  
-   Si la restricción de precedencia usa un resultado de ejecución, puede especificar el resultado de ejecución para que sea correcto, error o conclusión.  
  
-   Si la restricción de precedencia usa un resultado de evaluación, puede proporcionar una expresión que se evalúa como un valor booleano.  
  
-   Especificar si la restricción de precedencia se evalúa individualmente o junto con otras restricciones que se aplican al ejecutable restringido.  
  
## Operaciones de evaluación  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona las siguientes operaciones de evaluación:  
  
-   Una restricción que usa solamente el resultado de la ejecución del ejecutable de precedencia para determinar si el ejecutable restringido se ejecuta. El resultado de la ejecución del ejecutable de precedencia puede ser conclusión, correcto o error. Esta es la operación predeterminada.  
  
-   Una expresión que se evalúa para determinar si se ejecuta el ejecutable restringido. Si la expresión se evalúa como TRUE, el ejecutable restringido se ejecuta.  
  
-   Una expresión y una restricción que combina los requisitos de los resultados de la ejecución del ejecutable de precedencia y los resultados de devolución de la evaluación de la expresión.  
  
-   Una expresión o una restricción que usa los resultados de la ejecución del ejecutable de precedencia o los resultados de devolución de la evaluación de la expresión.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] usa colores para identificar el tipo de restricción de precedencia. La restricción de operación realizada correctamente es verde, la de error es roja y la de conclusión es azul. Para mostrar etiquetas de texto en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] que muestran el tipo de la restricción, debe configurar las características de accesibilidad del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 La expresión debe ser una expresión de [!INCLUDE[ssIS](../../includes/ssis-md.md)] válida y puede incluir funciones, operadores y variables del sistema y personalizadas. Para obtener más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md) y [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## Resultados de la ejecución  
 La restricción de precedencia puede usar los siguientes resultados de ejecución individualmente o combinados con una expresión.  
  
-   La conclusión requiere solamente que el ejecutable de precedencia se haya completado, sin importar su resultado, para que el ejecutable restringido se pueda ejecutar.  
  
-   El resultado correcto requiere que el ejecutable de precedencia se complete correctamente para que pueda ejecutarse el ejecutable restringido.  
  
-   El resultado de error requiere que el ejecutable de precedencia genere un error para que pueda ejecutarse el ejecutable restringido.  
  
> [!NOTE]  
>  Solo las restricciones de precedencia que son miembros de la misma colección **Precedence Constraint** se pueden agrupar en una condición lógica AND. Por ejemplo, no se pueden combinar restricciones de precedencia de dos contenedores de bucles Foreach.  
  
## Configuración de la restricción de precedencia  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener información sobre las propiedades que se pueden configurar en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)], vea [Editor de restricciones de precedencia](../Topic/Precedence%20Constraint%20Editor.md).  
  
 Para obtener información sobre cómo establecer mediante programación estas propiedades, vea <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint>.  
  
## Tareas relacionadas  
 Para obtener información detallada sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Establecer las propiedades de una restricción de precedencia](../Topic/Set%20the%20Properties%20of%20a%20Precedence%20Constraint.md)  
  
-   [Establecer el valor de una restricción de precedencia mediante el menú contextual](../Topic/Set%20the%20Value%20of%20a%20Precedence%20Constraint%20by%20Using%20the%20Shortcut%20Menu.md)  
  
-   [Conectar tareas y contenedores mediante una restricción de precedencia predeterminada](../Topic/Connect%20Tasks%20and%20Containers%20by%20Using%20a%20Default%20Precedence%20Constraint.md)  
  
     En este tema se ofrece información sobre cómo se configura el comportamiento predeterminado para las restricciones de precedencia y cómo se conectan los ejecutables mediante las restricciones de precedencia predeterminadas.  
  
## Contenido relacionado  
 Artículo técnico, sobre [ejemplos de expresiones SSIS](http://go.microsoft.com/fwlink/?LinkId=220761), en social.technet.microsoft.com  
  
## Vea también  
 [Agregar expresiones a las restricciones de precedencia](../Topic/Add%20Expressions%20to%20Precedence%20Constraints.md)   
 [Varias restricciones de precedencia](../Topic/Multiple%20Precedence%20Constraints.md)  
  
  