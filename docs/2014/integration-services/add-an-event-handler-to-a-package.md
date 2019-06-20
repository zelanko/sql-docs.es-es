---
title: Agregar un controlador de eventos a un paquete | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- event handlers [Integration Services], creating
ms.assetid: 5e56885d-8658-480a-bed9-3f2f8003fd78
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 589d90b52647241b22929473efc9c6e54eb3b75f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062029"
---
# <a name="add-an-event-handler-to-a-package"></a>agregar un controlador de eventos a un paquete
  En tiempo de ejecución, los contenedores y tareas producen eventos. Puede crear controladores de eventos personalizados que respondan a estos eventos ejecutando un flujo de trabajo cuando se produce el evento. Por ejemplo, puede crear un controlador de eventos que envíe un mensaje de correo electrónico cuando una tarea genera un error.  
  
 Un controlador de eventos es similar a un paquete. Al igual que un paquete, un controlador de eventos puede proporcionar un ámbito para variables, e incluye un flujo de control y flujos de datos opcionales. Puede generar controladores de eventos para paquetes, el contenedor de bucles Foreach, el contenedor de bucles For, el contenedor de secuencias y todas las tareas.  
  
 Puede crear controladores de eventos mediante la superficie de diseño de la pestaña **Controladores de eventos** en el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 Cuando la pestaña **Controladores de eventos** se encuentra activa, los nodos **Elementos de flujo de control** y **Tareas del plan de mantenimiento** del cuadro de herramientas en el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] contienen la tarea y los contenedores para generar el flujo de control en el controlador de eventos. Los nodos **Orígenes de flujo de datos**, **Transformaciones**y **Destinos de flujo de datos** contienen los orígenes de datos, transformaciones y destinos para generar los flujos de datos en el controlador de eventos. Para obtener más información, consulte [Control Flow](control-flow/control-flow.md) y [Data Flow](data-flow/data-flow.md).  
  
 La pestaña **Controlador de eventos** también incluye el área de Administradores de **conexión** , donde se crean y modifican los administradores de conexión que usan los controladores de eventos para conectarse a los servidores y orígenes de datos. Para obtener más información, vea [Crear administradores de conexiones](../../2014/integration-services/create-connection-managers.md).  
  
### <a name="to-create-an-event-handler"></a>Para crear un controlador de eventos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Controladores de eventos** .  
  
     ![Captura de pantalla de la superficie de diseño con el controlador de eventos](media/eventhandlers.gif "Screenshot of design surface with event handler")  
  
     La creación del flujo de control y de los flujos de datos en un controlador de eventos se asemeja a la creación del flujo de control y de los flujos de datos en un paquete. Para obtener más información, consulte [Control Flow](control-flow/control-flow.md) y [Data Flow](data-flow/data-flow.md).  
  
4.  En la lista **Ejecutable** , seleccione el ejecutable para el que desee crear un controlador de eventos.  
  
5.  En la lista **Controlador de eventos** , seleccione el controlador que desee crear.  
  
6.  Haga clic en el vínculo en la superficie de diseño de la pestaña **Controlador de eventos** .  
  
7.  Agregue elementos del flujo de control al controlador de eventos y conecte elementos mediante una restricción de precedencia, arrastrando la restricción de un elemento del flujo de control a otro. Para más información, consulte [Control Flow](control-flow/control-flow.md).  
  
8.  De forma opcional, puede agregar una tarea Flujo de datos y, en la superficie de diseño de la pestaña **Flujo de datos** , crear un flujo de datos para el controlador de eventos. Para más información, consulte [Data Flow](data-flow/data-flow.md).  
  
9. En el menú **Archivo** , haga clic en **Guardar los elementos seleccionados** para guardar el paquete.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Integration Services](../../2014/integration-services/sql-server-integration-services.md)   
 [Registro de Integration Services &#40;SSIS&#41;](performance/integration-services-ssis-logging.md)  
  
  
