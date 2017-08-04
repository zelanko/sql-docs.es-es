---
title: "Depurar un Script estableciendo puntos de interrupción en una tarea Script y componente de Script | Documentos de Microsoft"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- breakpoints [Integration Services]
- scripts [Integration Services], breakpoints
ms.assetid: 6c03464f-3f7d-4882-b7f8-8e396f8e2944
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 96815b337311c4ba8d16e10c25891c728e7a0c74
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="debug-a-script-by-setting-breakpoints-in-a-script-task-and-script-component"></a>Depurar un script estableciendo puntos de interrupción en una tarea Script y un componente Script
  Este procedimiento describe cómo establecer puntos de interrupción en los scripts que se utilizan en la tarea Script y en el componente Script.  
  
 Después de establecer puntos de interrupción en la secuencia de comandos, el **establecer puntos de interrupción - \<nombre de objeto >** cuadro de diálogo muestra los puntos de interrupción, junto con los puntos de interrupción integrados.  
  
> [!IMPORTANT]  
>  En determinadas circunstancias, se omiten los puntos de interrupción en la tarea Script y el componente de script. Para obtener más información, consulte el **depurar la tarea Script** sección [codificar y depurar la tarea Script](../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md) y **depurar el componente de secuencia de comandos** sección [codificar y depurar el componente de Script](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="to-set-a-breakpoint-in-script"></a>Para establecer un punto de interrupción en un script  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  Haga doble clic en el paquete que contiene el script en la que desea establecer puntos de interrupción.  
  
3.  Para abrir la tarea de secuencia de comandos, haga clic en el **flujo de Control** ficha y, a continuación, haga doble clic en la tarea de secuencia de comandos.  
  
4.  Para abrir el componente de Script, haga clic en el **de flujo de datos** ficha y, a continuación, haga doble clic en el componente de Script.  
  
5.  Haga clic en **Script** y, a continuación, haga clic en **editar Script**.  
  
6.  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools para aplicaciones (VSTA), busque la línea del script en el que desea establecer un punto de interrupción, haga clic en esa línea, seleccione **punto de interrupción**y, a continuación, haga clic en **Insertar punto de interrupción**.  
  
     El icono de punto de interrupción aparece en la línea de código.  
  
7.  En el menú **Archivo** , haga clic en **Salir**.  
  
8.  Haga clic en **Aceptar**.  
  
9. Para guardar el paquete, haga clic en **Guardar los elementos seleccionados** , en el menú **Archivo** .  
  
  
