---
title: Agregar, eliminar, cambiar el ámbito de Variable definido por el usuario en un paquete | Microsoft Docs
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
- variables [Integration Services], adding
ms.assetid: cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e
caps.latest.revision: 46
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2fdccdecea434aa3fe56c362f932b3ba0da396b3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37213605"
---
# <a name="add-delete-change-scope-of-user-defined-variable-in-a-package"></a>Agregar, eliminar, cambiar el ámbito de la variable definida por el usuario en un paquete
  Estos procedimientos describen cómo agregar, eliminar y cambiar el ámbito de una variable definida por el usuario en un paquete usando la ventana **Variables**.  
  
 Para obtener más información sobre el ámbito de las variables, vea [Integration Services &#40;SSIS&#41; Variables](integration-services-ssis-variables.md).  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] También proporciona variables del sistema que hacen que la información del sistema disponibles en tiempo de ejecución y se pueden utilizar en contenedores como paquetes y controladores de eventos. Las variables del sistema no se pueden eliminar.  
  
### <a name="to-add-a-variable"></a>Para agregar una variable  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] con el que desea trabajar.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  En el diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] , siga uno de estos procedimientos para definir el ámbito de la variable:  
  
    -   Para establecer el ámbito en el paquete, haga clic en cualquier lugar de la superficie de diseño de la pestaña **Flujo de control** .  
  
    -   Para establecer el ámbito en un controlador de eventos, seleccione un ejecutable y un controlador de eventos en la superficie de diseño de la pestaña **Controlador de eventos** .  
  
    -   Para establecer el ámbito en una tarea o un contenedor, en la superficie de diseño de la pestaña **Flujo de control** o **Controlador de eventos** , haga clic en una tarea o un contenedor.  
  
4.  En el menú **SSIS** , haga clic en **Variables**. También puede ver la ventana **Variables** si asigna el comando View.Variables a una combinación de teclas que desee en la página **Teclado** del cuadro de diálogo **Opciones** .  
  
5.  En la ventana **Variables** , haga clic en el icono **Agregar variable** . Se agregará la nueva variable a la lista.  
  
6.  Opcionalmente, haga clic en el icono **Opciones de cuadrícula** , seleccione las columnas adicionales que desee mostrar en el cuadro de diálogo **Opciones de cuadrícula de variables** y haga clic en **Aceptar**.  
  
7.  O bien, establezca las propiedades de una variable. Para obtener más información, vea [Establecer las propiedades de una variable definida por el usuario](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md).  
  
8.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
### <a name="to-delete-a-variable"></a>Para eliminar una variable  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga clic con el botón secundario en el paquete para abrirlo.  
  
3.  En el menú **SSIS** , haga clic en **Variables**. También puede ver la ventana **Variables** si asigna el comando View.Variables a una combinación de teclas que desee en la página **Teclado** del cuadro de diálogo **Opciones** .  
  
4.  Seleccione la variable que desee eliminar y haga clic en **Eliminar variable**.  
  
     Si no ve la variable en la ventana Variables, haga clic en **Opciones de cuadrícula** y seleccione **Mostrar variables de todos los ámbitos**.  
  
5.  Si se abre el cuadro de diálogo **Confirmar eliminación de variables** , haga clic en **Sí** para confirmar.  
  
6.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
### <a name="to-change-the-scope-of-a-variable"></a>Para cambiar el ámbito de una variable  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga clic con el botón secundario en el paquete para abrirlo.  
  
3.  En el menú **SSIS** , haga clic en **Variables**. También puede ver la ventana **Variables** si asigna el comando View.Variables a una combinación de teclas que desee en la página **Teclado** del cuadro de diálogo **Opciones** .  
  
4.  Seleccione la variable y haga clic en **Mover variable**.  
  
     Si no ve la variable en la ventana Variables, haga clic en **Opciones de cuadrícula** y seleccione **Mostrar variables de todos los ámbitos**.  
  
5.  En el cuadro de diálogo **Seleccionar nuevo ámbito** , seleccione el paquete o un contenedor, una tarea o un controlador de eventos en el paquete, para cambiar el ámbito de la variable.  
  
6.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
## <a name="see-also"></a>Vea también  
 [Servicios de integración &#40;SSIS&#41; Variables](integration-services-ssis-variables.md)   
 [Usar Variables en paquetes](../../2014/integration-services/use-variables-in-packages.md)   
 [Establecer las propiedades de una Variable definida por el usuario](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md)   
 [Uso de los valores de variables y parámetros en un paquete secundario](../../2014/integration-services/use-the-values-of-variables-and-parameters-in-a-child-package.md)  
  
  
