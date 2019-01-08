---
title: Establecer las propiedades de una tarea o contenedor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- tasks [Integration Services], properties
ms.assetid: 52d47ca4-fb8c-493d-8b2b-48bb269f859b
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8fc33585e165b8cdac2f7d46c322741b3eb1756c
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52503729"
---
# <a name="set-the-properties-of-a-task-or-container"></a>Establecer las propiedades de tareas o contenedores
  Puede establecer la mayoría de las propiedades de tareas y contenedores utilizando la ventana **Propiedades** . Las excepciones son propiedades de colecciones de tareas y propiedades que son demasiado complejas como para establecerse mediante la ventana **Propiedades** . Por ejemplo, no puede configurar el enumerador que usa el contenedor de bucles Foreach en la ventana **Propiedades** . Debe usar un editor de tareas o contenedores para establecer estas propiedades complejas. La mayoría de los editores de tareas y contenedores tienen varios nodos y cada nodo contiene propiedades relacionadas. El nombre del nodo indica el sujeto de las propiedades que contiene el nodo.  
  
 Los procedimientos siguientes describen cómo establecer las propiedades de una tarea o de un contenedor utilizando las ventanas **Propiedades** o el correspondiente editor de tareas y contenedores.  
  
### <a name="to-set-the-properties-of-a-task-or-container-by-using-the-properties-window"></a>Para establecer las propiedades de una tarea o de un contenedor mediante la ventana Propiedades  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** .  
  
4.  En la superficie de diseño de la pestaña **Flujo de control** , haga clic con el botón derecho en la tarea o el contenedor y, después, haga clic en **Propiedades**.  
  
5.  En la ventana **Propiedades** , actualice los valores de las propiedades.  
  
    > [!NOTE]  
    >  La mayoría de las propiedades se pueden establecer escribiendo un valor directamente en el cuadro de texto o seleccionando un valor de una lista. Sin embargo, algunas propiedades son más complejas y cuentan con un editor de propiedades personalizadas. Para establecer la propiedad, haga clic en el cuadro de texto y, después, haga clic en el botón Generar **(…)** para abrir el editor personalizado.  
  
6.  Opcionalmente, puede crear expresiones de propiedades para actualizar dinámicamente las propiedades de la tarea o del contenedor. Para más información, vea [Agregar o cambiar una expresión de propiedad](expressions/add-or-change-a-property-expression.md).  
  
7.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
### <a name="to-set-the-properties-of-a-task-or-container-by-using-a-task-or-container-editor"></a>Para establecer las propiedades de una tarea o de un contenedor mediante un editor de tareas o contenedores  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** .  
  
4.  En la superficie de diseño de la pestaña **Flujo de control** , haga clic con el botón derecho en la tarea o en el contenedor y, después, haga clic en **Editar** para abrir el editor de tareas o contenedores correspondiente.  
  
     Para más información sobre cómo configurar el contenedor de bucles For, vea [Configurar un contenedor de bucles For](control-flow/for-loop-container.md).  
  
     Para más información sobre cómo configurar el contenedor de bucles Foreach, vea [Configurar un contenedor de bucles Foreach](control-flow/foreach-loop-container.md).  
  
    > [!NOTE]  
    >  El contenedor de secuencias no dispone de ningún editor personalizado.  
  
5.  Si el editor de tareas o de contenedores tiene varios nodos, haga clic en el nodo que contiene la propiedad que desea establecer.  
  
6.  Opcionalmente, haga clic en **Expresiones** y, en la página **Expresiones** , cree expresiones de propiedades para actualizar dinámicamente las propiedades de la tarea o del contenedor. Para más información, vea [Agregar o cambiar una expresión de propiedad](expressions/add-or-change-a-property-expression.md).  
  
7.  Actualice el valor de las propiedades.  
  
8.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
## <a name="see-also"></a>Vea también  
 [Tareas de Integration Services](control-flow/integration-services-tasks.md)   
 [Contenedores de Integration Services](control-flow/integration-services-containers.md)  
  
  
