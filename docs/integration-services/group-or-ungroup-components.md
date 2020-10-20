---
description: Agrupar o desagrupar componentes
title: Agrupar o desagrupar componentes | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- grouping containers
- tasks [Integration Services], grouping
- containers [Integration Services], grouping
- grouping tasks
ms.assetid: 34320838-c271-4f8c-90b3-1254690890bb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7cd88383577694d5bef248baea5004056d239136
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195214"
---
# <a name="group-or-ungroup-components"></a>Agrupar o desagrupar componentes

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  Las pestañas **Flujo de control**, **Flujo de datos**y **Controladores de eventos** del Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] admiten la agrupación contraíble. Si un paquete tiene muchos componentes, las pestañas pueden estar abarrotadas, lo que dificulta la visión de todos los componentes a la vez y la búsqueda del elemento con el que desea trabajar. La característica de agrupación contraíble puede ahorrar espacio en la superficie de trabajo y facilitar el trabajo con paquetes grandes.  
  
 Se seleccionan los componentes que desea agrupar, los agrupa y luego expande o contrae los grupos para facilitar su trabajo. Al expandir un grupo se proporciona acceso a las propiedades de los componentes del grupo. Las restricciones de precedencia que conectan las tareas y contenedores se incluyen automáticamente en el grupo.  
  
 A continuación se presentan las consideraciones para la agrupación de componentes.  
  
-   Para agrupar componentes, el flujo de control, el flujo de datos o el controlador de eventos deben contener más de un componente.  
  
-   Los grupos también pueden anidarse, permitiendo la creación de grupos dentro de grupos. La superficie de diseño puede implementar varios grupos no anidados, pero un componente solamente puede pertenecer a un grupo, a menos que los grupos estén anidados.  
  
-   Cuando se guarda un paquete, el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] guarda la agrupación, pero la agrupación no tiene ningún efecto sobre la ejecución de paquetes. La capacidad para agrupar componentes es una característica de tiempo de diseño que no afecta al comportamiento de tiempo de ejecución del paquete.  
  
### <a name="to-group-components"></a>Para agrupar componentes  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control**, **Flujo de datos**o **Controladores de eventos** .  
  
4.  En la superficie de diseño de la pestaña, seleccione los componentes que quiera agrupar, haga clic con el botón derecho en un componente que haya seleccionado y, después, haga clic en **Agrupar**.  
  
5.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
### <a name="to-ungroup-components"></a>Para desagrupar componentes  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control**, **Flujo de datos**o **Controladores de eventos** .  
  
4.  En la superficie de diseño de la pestaña, seleccione el grupo que contenga el componente que quiera desagrupar, haga clic con el botón derecho y, después, haga clic en **Desagrupar**.  
  
5.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
## <a name="see-also"></a>Consulte también  
 [Agregar o eliminar tareas o contenedores en un flujo de control](../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [Conectar tareas y contenedores mediante una restricción de precedencia predeterminada](./control-flow/precedence-constraints.md)  
  
