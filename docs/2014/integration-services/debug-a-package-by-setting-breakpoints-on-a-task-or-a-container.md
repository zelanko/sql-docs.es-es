---
title: Depurar un paquete estableciendo puntos de interrupción en una tarea o un contenedor | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- containers [Integration Services], breakpoints
- breakpoints [Integration Services]
- tasks [Integration Services], breakpoints
ms.assetid: e7fa106a-2221-403a-bb74-efc9f12bb450
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 6535657a5b193b92b76fd32fee9497e8ef76580e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203232"
---
# <a name="debug-a-package-by-setting-breakpoints-on-a-task-or-a-container"></a>Depurar un paquete estableciendo puntos de interrupción en una tarea o un contenedor
  Este procedimiento describe cómo establecer puntos de interrupción en un paquete, una tarea, un contenedor de bucles For o Foreach o un contenedor de secuencias.  
  
### <a name="to-set-breakpoints-in-a-package-a-task-or-a-container"></a>Para establecer puntos de interrupción en un paquete, una tarea o un contenedor  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  Haga doble clic en el paquete en el que desee establecer puntos de interrupción.  
  
3.  En el Diseñador SSIS, siga estos pasos:  
  
    -   Para establecer puntos de interrupción en el objeto de paquete, haga clic en la pestaña **Flujo de control** , coloque el cursor en cualquier lugar del fondo de la superficie de diseño, haga clic con el botón derecho y, después, haga clic en **Editar puntos de interrupción**.  
  
    -   Para establecer puntos de interrupción en un flujo de control de paquete, haga clic en la pestaña **Flujo de control** , haga clic con el botón derecho en una tarea, un contenedor de bucles For o Foreach o un contenedor de secuencias y, después, haga clic en **Editar puntos de interrupción**.  
  
    -   Para establecer puntos de interrupción en un controlador de eventos, haga clic en la pestaña **Controlador de eventos** , haga clic con el botón derecho en una tarea, un contenedor de bucles For o Foreach o un contenedor de secuencias y, después, haga clic en **Editar puntos de interrupción**.  
  
4.  En el cuadro de diálogo **Establecer puntos de interrupción \<nombre de contenedor>**, seleccione los puntos de interrupción que quiere habilitar.  
  
5.  Opcionalmente, modifique el tipo y la cantidad de número de llamadas para cada punto de interrupción.  
  
6.  Para guardar el paquete, haga clic en **Guardar los elementos seleccionados** , en el menú **Archivo** .  
  
## <a name="see-also"></a>Vea también  
 [Solución de problemas de herramientas de desarrollo de paquetes](troubleshooting/troubleshooting-tools-for-package-development.md)   
 [Depurar un Script estableciendo puntos de interrupción en una tarea Script y componente de Script](data-flow/transformations/script-component.md)   
 [Codificar y depurar la tarea de secuencia de comandos](control-flow/script-task.md)   
 [Codificar y depurar el componente de script](extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  