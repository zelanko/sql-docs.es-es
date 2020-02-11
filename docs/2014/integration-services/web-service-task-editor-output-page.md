---
title: Editor de la tarea servicio Web (página salida) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.webservicestask.output.f1
helpviewer_keywords:
- Web Service Task Editor
ms.assetid: 73c83969-7b0e-479d-a436-0a46b2068d01
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7924570253bf2f805d91c4dfabc3d5facf44cccc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66054471"
---
# <a name="web-service-task-editor-output-page"></a>Editor de la tarea Servicio web (página Salida)
  Use la página **Salida** del cuadro de diálogo **Editor de la tarea Servicio web** para indicar dónde desea almacenar el resultado devuelto por el método web.  
  
 Para obtener información sobre esta tarea, vea [Tarea Servicio web](control-flow/web-service-task.md).  
  
## <a name="static-options"></a>Opciones estáticas  
 **OutputType**  
 Seleccione el tipo de almacenamiento que desea usar para almacenar los resultados. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Conexión de archivos**|Almacene los resultados en un archivo. Si selecciona este valor, se mostrará la opción dinámica **Archivo**.|  
|**Variable**|Almacene los resultados en una variable. Si selecciona este valor, se mostrará la opción dinámica **Variable**.|  
  
## <a name="outputtype-dynamic-options"></a>Opciones dinámicas de OutputType  
  
### <a name="outputtype--file-connection"></a>OutputType = Conexión de archivos  
 **Archivo**  
 Seleccione un administrador de conexiones de archivos de la lista, o bien haga clic en \<**Nueva conexión…**> para crear un administrador de conexiones.  
  
 **Temas relacionados:** [Administrador de conexiones de archivos](connection-manager/file-connection-manager.md), [Editor del administrador de conexiones de archivos](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="outputtype--variable"></a>OutputType = Variable  
 **Variable**  
 Seleccione una variable de la lista o haga \<clic en **nueva variable...**> para crear una nueva variable.  
  
 **Temas relacionados:**  [Integration Services &#40;SSIS&#41; variables](integration-services-ssis-variables.md), [Agregar variable](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de la tarea servicio Web &#40;página general&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor de la tarea servicio Web &#40;página de entrada&#41;](../../2014/integration-services/web-service-task-editor-input-page.md)   
 [Página Expresiones](expressions/expressions-page.md)  
  
  
