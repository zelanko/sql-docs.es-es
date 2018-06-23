---
title: Editor de la tarea servicio Web (página entrada) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.webservicestask.input.f1
helpviewer_keywords:
- Web Service Task Editor
ms.assetid: 93529c88-f540-47f2-a10a-12c87318ed6f
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 8f458f4a2898915102ab2a05b04fb7ba223c5e30
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200157"
---
# <a name="web-service-task-editor-input-page"></a>Editor de la tarea Servicio web (página Entrada)
  Use la página **Entrada** del cuadro de diálogo **Editor de la tarea Servicio web** para especificar el servicio web, el método web y los valores que se deben proporcionar como entrada para el método web. Los valores se pueden proporcionar mediante la especificación directa de cadenas o la selección de variables en la columna Valor.  
  
 Para obtener información sobre esta tarea, vea [Tarea Servicio web](control-flow/web-service-task.md).  
  
## <a name="options"></a>Opciones  
 **ssNoVersion**  
 Seleccione en la lista un servicio web para ejecutar el método web.  
  
 **Método**  
 Seleccione en la lista un método web para la tarea que se va a ejecutar.  
  
 **Documentación del método web**  
 Escriba una descripción del método web o haga clic en el botón Examinar **(…)** y escriba una descripción en el cuadro de diálogo **Documentación del método web** .  
  
 **Nombre**  
 Muestra los nombres de las entradas del método web.  
  
 **Tipo**  
 Muestra los tipos de datos de las entradas.  
  
> [!NOTE]  
>  La tarea Servicio web solo admite parámetros de los tipos de datos siguientes: tipos primitivos tales como enteros y cadenas; matrices y secuencias de tipos primitivos, y enumeraciones.  
  
 **Variable**  
 Active las casillas para utilizar variables que proporcionen entradas.  
  
 **Value**  
 Si las casillas de Variable están activadas, seleccione las variables de la lista para proporcionar entradas; en caso contrario, escriba los valores que se usarán en las entradas.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de la tarea servicio Web &#40;página General&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor de la tarea servicio Web &#40;generan las páginas&#41;](../../2014/integration-services/web-service-task-editor-output-page.md)   
 [Página Expresiones](expressions/expressions-page.md)  
  
  