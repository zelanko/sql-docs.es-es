---
title: Agregar o eliminar tareas o contenedores en un flujo de control | Microsoft Docs
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
- containers [Integration Services], adding
- adding tasks
- adding containers
- tasks [Integration Services], adding
ms.assetid: 653084c6-87a3-45d5-b458-914ecf24d56a
caps.latest.revision: 44
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1546a8bf4d0da741d63cb8bd8d4b2f849cf921d2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37256941"
---
# <a name="add-or-delete-a-task-or-a-container-in-a-control-flow"></a>Agregar o eliminar tareas o contenedores en un flujo de control
  Cuando se trabaja en el diseñador de flujo de control, el cuadro de herramientas del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] enumera las tareas que proporciona [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para generar flujo de control en un paquete. Para obtener más información sobre el cuadro de herramientas, vea [SSIS Toolbox](../ssis-toolbox.md).  
  
 Un paquete puede incluir varias instancias de la misma tarea. Cada instancia de una tarea se identifica de forma exclusiva en el paquete y cada instancia se puede configurar de forma diferente.  
  
 Si se elimina una tarea, las restricciones de precedencia que conectan la tarea a otras tareas y contenedores en el flujo de control también se eliminan.  
  
 Los procedimientos siguientes describen cómo agregar o eliminar una tarea o un contenedor en el flujo de control de un paquete.  
  
### <a name="to-add-a-task-or-a-container-to-a-control-flow"></a>Para agregar una tarea o contenedor a un flujo de control  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** .  
  
4.  Para abrir el **cuadro de herramientas**, haga clic en **Cuadro de herramientas** en el menú **Ver** .  
  
5.  Expanda **Elementos de flujo de control** y **Tareas de mantenimiento**.  
  
6.  Arrastre tareas y contenedores desde el **Cuadro de herramientas** a la superficie de diseño de la pestaña **Flujo de control** .  
  
7.  Conecte una tarea o contenedor dentro del flujo de control de paquete arrastrando su conector a otro componente en el flujo de control.  
  
8.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
### <a name="to-delete-a-task-or-a-container-from-a-control-flow"></a>Para eliminar una tarea o un contenedor de un flujo de control  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo. Realice una de las siguientes operaciones:  
  
    -   Haga clic en la pestaña **Flujo de control** , haga clic con el botón derecho en la tarea o contenedor que quiera eliminar y, después, haga clic en **Eliminar**.  
  
    -   Abra el **Explorador de paquetes**. En la carpeta **Ejecutables** , haga clic con el botón derecho en la tarea o contenedor que quiera eliminar y, después, haga clic en **Eliminar**.  
  
3.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
## <a name="see-also"></a>Vea también  
 [Tareas de Integration Services](integration-services-tasks.md)   
 [Contenedores de Integration Services](integration-services-containers.md)   
 [Flujo de control](control-flow.md)  
  
  
