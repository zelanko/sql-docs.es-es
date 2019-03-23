---
title: Editor (página salida) de la tarea servicio Web | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.webservicestask.output.f1
helpviewer_keywords:
- Web Service Task Editor
ms.assetid: 73c83969-7b0e-479d-a436-0a46b2068d01
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4cfeac28676dc8134c7eedf1e4b27901e0f053dc
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58377933"
---
# <a name="web-service-task-editor-output-page"></a>Editor de la tarea Servicio web (página Salida)
  Use la página **Salida** del cuadro de diálogo **Editor de la tarea Servicio web** para indicar dónde desea almacenar el resultado devuelto por el método web.  
  
 Para obtener información sobre esta tarea, vea [Tarea Servicio web](control-flow/web-service-task.md).  
  
## <a name="static-options"></a>Opciones estáticas  
 **OutputType**  
 Seleccione el tipo de almacenamiento que desea usar para almacenar los resultados. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Conexión de archivos**|Almacene los resultados en un archivo. Si selecciona este valor, se mostrará la opción dinámica **Archivo**.|  
|**Variable**|Almacene los resultados en una variable. Si selecciona este valor, se mostrará la opción dinámica **Variable**.|  
  
## <a name="outputtype-dynamic-options"></a>Opciones dinámicas de OutputType  
  
### <a name="outputtype--file-connection"></a>OutputType = Conexión de archivos  
 **Archivo**  
 Seleccione un administrador de conexiones de archivos de la lista, o bien haga clic en \<**Nueva conexión…**> para crear un administrador de conexiones.  
  
 **Temas relacionados:** [Administrador de conexiones de archivos](connection-manager/file-connection-manager.md), [Editor del Administrador de conexiones de archivos](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="outputtype--variable"></a>OutputType = Variable  
 **Variable**  
 Seleccione una variable de la lista, o bien haga clic en \<**Nueva variable…**> para crear una.  
  
 **Temas relacionados:**  [Servicios de integración &#40;SSIS&#41; Variables](integration-services-ssis-variables.md), [agregar Variable](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de la tarea Servicio web &#40;página General&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor de la tarea Servicio web &#40;página Entrada&#41;](../../2014/integration-services/web-service-task-editor-input-page.md)   
 [Página Expresiones](expressions/expressions-page.md)  
  
  
