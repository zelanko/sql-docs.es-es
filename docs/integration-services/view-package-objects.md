---
title: Ver objetos de paquete | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, properties
- properties [Integration Services]
- Package Explorer window [Integration Services]
- packages [Integration Services], properties
- explorer view [Integration Services]
- SSIS packages, properties
- viewing package objects
- SQL Server Integration Services packages, properties
ms.assetid: a85c0245-0a68-4eb0-83b1-9b11df80bd10
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 99fdafa44320ca37700ddb3e424518212156b688
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67945389"
---
# <a name="view-package-objects"></a>Ver objetos de paquete

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  En el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] , la pestaña **Explorador de paquetes** proporciona una vista de explorador del paquete. La vista refleja la jerarquía de contenedores de la arquitectura de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . El contenedor de paquetes se encuentra en la parte superior de la jerarquía y puede expandir el paquete para ver las conexiones, ejecutables, controladores de eventos, proveedores de registro, restricciones de precedencia y variables del paquete.  
  
 Los ejecutables, que son los contenedores y las tareas del paquete, pueden incluir controladores de eventos, restricciones de precedencia y variables. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] admite una jerarquía anidada de contenedores, y los contenedores de bucles For, bucles Foreach y secuencias pueden incluir otros ejecutables.  
  
 Si un paquete incluye un flujo de datos, el **Explorador de paquetes** incluye la tarea Flujo de datos y una carpeta **Componentes** que enumera los componentes de flujo de datos.  
  
 Desde la pestaña **Explorador de paquetes** , puede eliminar objetos en un paquete y obtener acceso a la ventana **Propiedades** para ver las propiedades del objeto.  
  
 El siguiente diagrama muestra una vista de árbol de un paquete simple.  
  
 ![Captura de pantalla de la pestaña Explorador de paquetes](../integration-services/media/packageexplorer.gif "Screenshot of the Package Explorer tab")  
  
## <a name="view-the-package-structure-and-content"></a>Ver la estructura y el contenido de los paquetes  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea ver en el **Explorador de paquetes**.  
  
2.  Haga clic en la pestaña **Explorador de paquetes** .  
  
3.  Para ver el contenido de las carpetas **Variables**, **Restricciones de precedencia**, **Controladores de eventos**, **Administradores de conexión**, **Proveedores de registro**, o **Ejecutables** , expanda cada carpeta.  
  
4.  Según la estructura del paquete, expanda las carpetas del siguiente nivel.  
  
## <a name="view-the-properties-of-a-package-object"></a>Ver las propiedades de un objeto de paquete
  
-   Haga clic con el botón derecho en un objeto y haga clic en **Propiedades** para abrir la ventana **Propiedades** .  
  
## <a name="delete-an-object-in-a-package"></a>Eliminar un objeto en un paquete  
  
-   Haga clic con el botón derecho en un objeto y luego haga clic en **Eliminar**. 
 
## <a name="see-also"></a>Consulte también  
 [Tareas de Integration Services](../integration-services/control-flow/integration-services-tasks.md)   
 [Contenedores de Integration Services](../integration-services/control-flow/integration-services-containers.md)   
 [Restricciones de precedencia](../integration-services/control-flow/precedence-constraints.md)   
 [Variables de Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-variables.md)   
 [Controladores de eventos de Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-event-handlers.md)   
 [Registro de Integration Services &#40;SSIS&#41;](../integration-services/performance/integration-services-ssis-logging.md)  
  
  
