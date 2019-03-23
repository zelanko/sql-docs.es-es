---
title: Pestaña controladores de eventos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.eventhandlerwindow.f1
ms.assetid: 94fc8916-8032-490c-b9d5-ded8b6217e49
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2f13aa09f7b424da63348c5363bc6d5077ed9f2c
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58380743"
---
# <a name="event-handlers-tab"></a>Pestaña Controladores de eventos
  Utilice la pestaña **Controladores de eventos** del Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] para generar un flujo de control en un paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Un controlador de eventos se ejecuta en respuesta a un evento generado por el paquete o por una tarea o un contenedor de un paquete.  
  
## <a name="options"></a>Opciones  
 **Executable**  
 Seleccione el ejecutable para el cual desea generar un controlador de eventos. El ejecutable puede ser el paquete, o una tarea o contenedores del paquete.  
  
 **Controlador de eventos**  
 Seleccione un tipo de controlador de eventos. Cree el controlador de eventos arrastrando los elementos desde el **Cuadro de herramientas**.  
  
 **Eliminar**  
 Seleccione un controlador de eventos y elimínelo del paquete haciendo clic en **Eliminar**.  
  
 **Haga clic aquí para crear un \<nombre de controlador de eventos > para el ejecutable \<nombre del archivo ejecutable >**  
 Haga clic aquí para crear el controlador de eventos.  
  
 Cree el flujo de control arrastrando objetos gráficos que representan contenedores y tareas de [!INCLUDE[ssIS](../includes/ssis-md.md)] desde el **Cuadro de herramientas** a la superficie de diseño de la pestaña **Controladores de eventos** y, a continuación, conecte los objetos utilizando las restricciones de precedencia para definir la secuencia en que se ejecutan.  
  
 Además, para agregar anotaciones, haga clic con el botón derecho en la superficie de diseño y, después, en el menú, haga clic en **Agregar anotación**.  
  
## <a name="see-also"></a>Vea también  
 [Controladores de eventos de Integration Services &#40;SSIS&#41;](integration-services-ssis-event-handlers.md)   
 [Flujo de control](control-flow/control-flow.md)   
 [Diseñador SSIS](ssis-designer.md)   
 [Controladores de eventos de Integration Services &#40;SSIS&#41;](integration-services-ssis-event-handlers.md)  
  
  
