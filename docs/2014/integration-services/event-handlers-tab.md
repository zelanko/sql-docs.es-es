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
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a258c768f46e2310095c6aadc0c57c65cea2bac6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48131145"
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
 [Servicios de integración &#40;SSIS&#41; controladores de eventos](integration-services-ssis-event-handlers.md)  
  
  
