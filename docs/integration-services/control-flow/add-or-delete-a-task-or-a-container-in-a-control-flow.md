---
title: Agregar o eliminar tareas o contenedores en un flujo de control | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- containers [Integration Services], adding
- adding tasks
- adding containers
- tasks [Integration Services], adding
ms.assetid: 653084c6-87a3-45d5-b458-914ecf24d56a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 648e58e6b8f86648d1e3bf1d80ff02916c4276be
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="add-or-delete-a-task-or-a-container-in-a-control-flow"></a>Agregar o eliminar tareas o contenedores en un flujo de control
  Cuando se trabaja en el diseñador de flujo de control, el cuadro de herramientas del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] enumera las tareas que proporciona [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para generar flujo de control en un paquete. Para obtener más información sobre el cuadro de herramientas, vea [SSIS Toolbox](../../integration-services/ssis-toolbox.md).  
  
 Un paquete puede incluir varias instancias de la misma tarea. Cada instancia de una tarea se identifica de forma exclusiva en el paquete y cada instancia se puede configurar de forma diferente.  
  
 Si se elimina una tarea, las restricciones de precedencia que conectan la tarea a otras tareas y contenedores en el flujo de control también se eliminan.  
  
 Los procedimientos siguientes describen cómo agregar o eliminar una tarea o un contenedor en el flujo de control de un paquete.  
  
## <a name="add-a-task-or-a-container-to-a-control-flow"></a>Agregar una tarea o contenedor a un flujo de control  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** .  
  
4.  Para abrir el **cuadro de herramientas**, haga clic en **Cuadro de herramientas** en el menú **Ver** .  
  
5.  Expanda **Elementos de flujo de control** y **Tareas de mantenimiento**.  
  
6.  Arrastre tareas y contenedores desde el **Cuadro de herramientas** a la superficie de diseño de la pestaña **Flujo de control** .  
  
7.  Conecte una tarea o contenedor dentro del flujo de control de paquete arrastrando su conector a otro componente en el flujo de control.  
  
8.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados** , en el menú **Archivo** .  
  
## <a name="delete-a-task-or-a-container-from-a-control-flow"></a>Eliminar una tarea o un contenedor de un flujo de control  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo. Realice una de las siguientes operaciones:  
  
    -   Haga clic en la pestaña **Flujo de control** , haga clic con el botón derecho en la tarea o contenedor que quiera eliminar y, después, haga clic en **Eliminar**.  
  
    -   Abra el **Explorador de paquetes**. En la carpeta **Ejecutables** , haga clic con el botón derecho en la tarea o contenedor que quiera eliminar y, después, haga clic en **Eliminar**.  
  
3.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados** , en el menú **Archivo** .  

## <a name="set-the-properties-of-a-task-or-container"></a>Establecer las propiedades de una tarea o un contenedor
Puede establecer la mayoría de las propiedades de tareas y contenedores utilizando la ventana **Propiedades** . Las excepciones son propiedades de colecciones de tareas y propiedades que son demasiado complejas como para establecerse mediante la ventana **Propiedades** . Por ejemplo, no puede configurar el enumerador que usa el contenedor de bucles Foreach en la ventana **Propiedades** . Debe usar un editor de tareas o contenedores para establecer estas propiedades complejas. La mayoría de los editores de tareas y contenedores tienen varios nodos y cada nodo contiene propiedades relacionadas. El nombre del nodo indica el sujeto de las propiedades que contiene el nodo.  
  
 Los procedimientos siguientes describen cómo establecer las propiedades de una tarea o de un contenedor utilizando las ventanas **Propiedades** o el correspondiente editor de tareas y contenedores.  
  
### <a name="set-the-properties-of-a-task-or-container-with-the-properties-window"></a>Establecer las propiedades de una tarea o un contenedor con la ventana Propiedades  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** .  
  
4.  En la superficie de diseño de la pestaña **Flujo de control** , haga clic con el botón derecho en la tarea o el contenedor y, después, haga clic en **Propiedades**.  
  
5.  En la ventana **Propiedades** , actualice los valores de las propiedades.  
  
    > [!NOTE]  
    >  La mayoría de las propiedades se pueden establecer escribiendo un valor directamente en el cuadro de texto o seleccionando un valor de una lista. Sin embargo, algunas propiedades son más complejas y cuentan con un editor de propiedades personalizadas. Para establecer la propiedad, haga clic en el cuadro de texto y, después, haga clic en el botón Generar **(…)** para abrir el editor personalizado.  
  
6.  Opcionalmente, puede crear expresiones de propiedades para actualizar dinámicamente las propiedades de la tarea o del contenedor. Para más información, vea [Agregar o cambiar una expresión de propiedad](../../integration-services/expressions/add-or-change-a-property-expression.md).  
  
7.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados** , en el menú **Archivo** .  
  
### <a name="set-the-properties-of-a-task-or-container-with-the-task-or-container-editor"></a>Establecer las propiedades de una tarea o un contenedor con un editor de tareas o contenedores  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** .  
  
4.  En la superficie de diseño de la pestaña **Flujo de control** , haga clic con el botón derecho en la tarea o en el contenedor y, después, haga clic en **Editar** para abrir el editor de tareas o contenedores correspondiente.  
  
     Para más información sobre cómo configurar el contenedor de bucles For, vea [Configurar un contenedor de bucles For](http://msdn.microsoft.com/library/b9cd7ea7-b198-4a35-8b16-6acf09611ca5).  
  
     Para más información sobre cómo configurar el contenedor de bucles Foreach, vea [Configurar un contenedor de bucles Foreach](http://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25).  
  
    > [!NOTE]  
    >  El contenedor de secuencias no dispone de ningún editor personalizado.  
  
5.  Si el editor de tareas o de contenedores tiene varios nodos, haga clic en el nodo que contiene la propiedad que desea establecer.  
  
6.  Opcionalmente, haga clic en **Expresiones** y, en la página **Expresiones** , cree expresiones de propiedades para actualizar dinámicamente las propiedades de la tarea o del contenedor. Para más información, vea [Agregar o cambiar una expresión de propiedad](../../integration-services/expressions/add-or-change-a-property-expression.md).  
  
7.  Actualice el valor de las propiedades.  
  
8.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados** , en el menú **Archivo** .  
  
## <a name="see-also"></a>Ver también  
 [Tareas de Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Contenedores de Integration Services](../../integration-services/control-flow/integration-services-containers.md)   
 [Flujo de control](../../integration-services/control-flow/control-flow.md)  
  
  
