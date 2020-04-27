---
title: Ejemplos de tarea Script | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], examples
- examples [Integration Services]
- SSIS Script task, examples
ms.assetid: b0dd77ee-ee11-4cd9-87aa-61dd67f2fe1c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d47fa22b8207facc5b4bc22a4077b8bd81837ec2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62768483"
---
# <a name="script-task-examples"></a>Ejemplos de tarea Script
  La tarea Script es una herramienta con varias funciones que puede utilizar en un paquete para satisfacer casi cualquier requisito que no cumplan las tareas incluidas con [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. En este tema se enumeran los ejemplos de código de la tarea Script que muestran alguna de las funciones disponibles.  
  
> [!NOTE]  
>  Si desea crear tareas que pueda reutilizar más fácilmente en varios paquetes, considere la posibilidad de utilizar el código de estos ejemplos de tarea Script como punto inicial de las tareas personalizadas. Para más información, vea [Desarrollar una tarea personalizada](../extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
### <a name="example-topics"></a>Temas de ejemplo  
 Esta sección contiene ejemplos de código que muestran varios usos de las clases de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que puede incorporar en una tarea Script de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [Detectar un archivo plano vacío con la tarea Script](../extending-packages-scripting-task-examples/detecting-an-empty-flat-file-with-the-script-task.md)  
 Comprueba un archivo plano para determinar si contiene filas de datos, y guarda el resultado en una variable para su uso en una bifurcación del flujo de control.  
  
 [Recopilar una lista para el bucle ForEach con la tarea Script](../extending-packages-scripting-task-examples/gathering-a-list-for-the-foreach-loop-with-the-script-task.md)  
 Recopila una lista de archivos que cumplen los criterios especificados por el usuario y rellena una variable para su uso posterior por parte del enumerador de variable para Foreach.  
  
 [Consultar Active Directory con la tarea Script](../extending-packages-scripting-task-examples/querying-the-active-directory-with-the-script-task.md)  
 Recupera información sobre el usuario de Active Directory basándose en el valor de una variable [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], mediante las clases del espacio de nombres System.DirectoryServices.  
  
 [Supervisar los contadores de rendimiento con la tarea Script](../extending-packages-scripting-task-examples/monitoring-performance-counters-with-the-script-task.md)  
 Crea un contador de rendimiento personalizado que se puede utilizar para realizar el seguimiento del progreso de ejecución de un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], mediante las clases del espacio de nombres System.Diagnostics.  
  
 [Trabajar con imágenes con la tarea Script](../extending-packages-scripting-task-examples/working-with-images-with-the-script-task.md)  
 Comprime las imágenes en el formato JPEG y crea las imágenes en miniatura a partir de ellas, mediante las clases del espacio de nombres System.Drawing.  
  
 [Buscar impresoras instaladas con la tarea Script](../extending-packages-scripting-task-examples/finding-installed-printers-with-the-script-task.md)  
 Busca las impresoras instaladas que admiten un tamaño de papel concreto, mediante las clases del espacio de nombres System.Drawing.Printing.  
  
 [Enviar un mensaje de correo electrónico HTML con la tarea Script](../extending-packages-scripting-task-examples/sending-an-html-mail-message-with-the-script-task.md)  
 Envía un mensaje de correo en formato HTML en lugar de texto simple.  
  
 [Trabajar con archivos de Excel con la tarea Script](../extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
 Enumera las hojas de cálculo de un archivo de Excel y comprueba la existencia de una hoja de cálculo concreta.  
  
 [Enviar a una cola de mensajes privada remota con la tarea Script](../extending-packages-scripting-task-examples/sending-to-a-remote-private-message-queue-with-the-script-task.md)  
 Envía un mensaje a una cola de mensajes privada remota.  
  
### <a name="other-examples"></a>Otros ejemplos  
 Los siguientes temas también contienen ejemplos de código para su uso con la tarea Script.  
  
 [Usar variables en la tarea Script](../extending-packages-scripting/task/using-variables-in-the-script-task.md)  
 Solicita al usuario confirmación de si el paquete debe continuar ejecutándose, basándose en el valor de una variable de paquete que puede superar el límite especificado en otra variable.  
  
 [Conectarse a orígenes de datos de la tarea Script](../extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)  
 Recupera una conexión o información de conexión de los administradores de conexión definidos en el paquete.  
  
 [Provocar eventos en la tarea Script](../extending-packages-scripting/task/raising-events-in-the-script-task.md)  
 Produce un error, una advertencia o un mensaje informativo basándose en el estado de conexión a Internet en el servidor.  
  
 [Registrar en la tarea Script](../extending-packages-scripting/task/logging-in-the-script-task.md)  
 Registra el número de elementos procesados por la tarea para los proveedores de registro habilitados.  
  
![Integration Services icono (pequeño)](../media/dts-16.gif "Icono de Integration Services (pequeño)")  **Manténgase al día con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
  
