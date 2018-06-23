---
title: Pestaña controladores de eventos | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.eventhandlerwindow.f1
ms.assetid: 94fc8916-8032-490c-b9d5-ded8b6217e49
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 49b6145f29fac5088d44e6e82f6dcd3eb491556a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105170"
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
  
 **Haga clic aquí para crear un \<nombre del controlador de eventos > para el ejecutable \<nombre del archivo ejecutable >**  
 Haga clic aquí para crear el controlador de eventos.  
  
 Cree el flujo de control arrastrando objetos gráficos que representan contenedores y tareas de [!INCLUDE[ssIS](../includes/ssis-md.md)] desde el **Cuadro de herramientas** a la superficie de diseño de la pestaña **Controladores de eventos** y, a continuación, conecte los objetos utilizando las restricciones de precedencia para definir la secuencia en que se ejecutan.  
  
 Además, para agregar anotaciones, haga clic con el botón derecho en la superficie de diseño y, después, en el menú, haga clic en **Agregar anotación**.  
  
## <a name="see-also"></a>Vea también  
 [Controladores de eventos de Integration Services &#40;SSIS&#41;](integration-services-ssis-event-handlers.md)   
 [Flujo de control](control-flow/control-flow.md)   
 [Diseñador SSIS](ssis-designer.md)   
 [Servicios de integración &#40;SSIS&#41; controladores de eventos](integration-services-ssis-event-handlers.md)  
  
  