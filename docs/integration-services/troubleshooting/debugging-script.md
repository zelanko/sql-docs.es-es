---
title: Depurar script | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Script task [Integration Services], debugging
- debugging [Integration Services], scripts
- scripts [Integration Services], debugging
ms.assetid: fddf57d8-8607-4f88-85a0-1b683087b491
author: janinezhang
ms.author: janinez
ms.openlocfilehash: a8dee34e6d2bb7cfb858ee1f10378d5ac4916f9b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67945577"
---
# <a name="debugging-script"></a>Depurar script

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Escribe los scripts que la tarea Script y el componente Script usan, en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools para aplicaciones (VSTA).  
  
 EN VSTA se establecen y programan los puntos de interrupción. Puede administrar los puntos de interrupción en VSTA, pero también puede administrar los puntos de interrupción mediante el cuadro de diálogo **Establecer puntos de interrupción** que proporciona el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Para más información, consulte [Debugging Control Flow](../../integration-services/troubleshooting/debugging-control-flow.md).  
  
 El cuadro de diálogo **Establecer puntos de interrupción** incluye los puntos de interrupción del script. Estos puntos de interrupción aparecen en la parte inferior de la lista de puntos de interrupción, y muestran el número de línea y el nombre de la función en que aparece el punto de interrupción. Es posible eliminar un punto de interrupción de script en el cuadro de diálogo **Establecer puntos de interrupción** .  
  
 En tiempo de ejecución, los puntos de interrupción establecidos en líneas de código del script se integran con los puntos de interrupción establecidos en el paquete o las tareas y contenedores del paquete. El depurador puede ejecutarse desde un punto de interrupción en el script hasta un conjunto de puntos de interrupción en el paquete, tarea o contenedor, y viceversa. Por ejemplo, un paquete puede tener puntos de interrupción establecidos en las condiciones de interrupción que se producen cuando el paquete recibe los eventos **OnPreExecute** y **OnPostExecute** y también puede tener una tarea Script que tiene puntos de interrupción en líneas de su script. En este escenario, el paquete puede suspender la ejecución en la condición de interrupción asociada al evento **OnPreExecute** , ejecutar los puntos de interrupción en el script y finalmente ejecutarse en la condición de interrupción asociada con el evento **OnPostExecute** .  
  
 Para obtener más información acerca de cómo depurar la tarea Script y el componente Script, vea [Coding and Debugging the Script Task](../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md) y [Coding and Debugging the Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="to-set-a-breakpoint-in-visual-studio-for-applications"></a>Para establecer un punto de interrupción en Visual Studio para Aplicaciones  
  
-   [Depurar un script estableciendo puntos de interrupción en una tarea Script y un componente Script](../../integration-services/extending-packages-scripting/debug-a-script-by-setting-breakpoints-in-a-script-task-and-script-component.md)  
  
## <a name="see-also"></a>Consulte también  
 [Herramientas para solucionar problemas con el desarrollo de paquetes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)  
  
  
