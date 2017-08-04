---
title: "Editor de tareas de servicio Web (página General) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.webservicestask.general.f1
helpviewer_keywords:
- Web Service Task Editor
ms.assetid: 4d7df283-430d-4f0f-9dd4-5909554cd5eb
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2c65419846e21225c6b5fe41bc07cfbae6dffe01
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="web-service-task-editor-general-page"></a>Editor de la tarea Servicio web (página General)
  Use la página **General** del cuadro de diálogo **Editor de la tarea Servicio web** para especificar un administrador de conexiones de HTTP, especificar la ubicación del archivo de Lenguaje de descripción de servicios web (WSDL) que usa la tarea Servicio web, describir la tarea Servicios web y descargar el archivo WSDL.  
  
 Para obtener más información sobre esta tarea, vea [Tarea Servicio web](../../integration-services/control-flow/web-service-task.md).  
  
## <a name="options"></a>Opciones  
 **HTTPConnection**  
 Seleccione un administrador de conexiones en la lista o haga clic en \< **nueva conexión...** > para crear una nueva conexión de administrador.  
  
> [!IMPORTANT]  
>  El administrador de conexiones HTTP solo es compatible con la autenticación anónima y la autenticación básica. No es compatible con la autenticación de Windows.  
  
 **Temas relacionados**: [Administrador de conexiones HTTP](../../integration-services/connection-manager/http-connection-manager.md), [Editor del administrador de conexiones HTTP &#40;página Servidor&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md).  
  
 **WSDLFile**  
 Escriba la ruta de acceso completa de un archivo WSDL que sea local en el equipo o haga clic en el botón de exploración **(…)** y busque este archivo.  
  
 Si ya ha descargado manualmente el archivo WSDL en el equipo, seleccione este archivo. Sin embargo, si el archivo WSDL todavía no se ha descargado, siga estos pasos:  
  
-   Cree un archivo vacío que tenga la extensión ".wsdl".  
  
-   Seleccione este archivo vacío para la opción **WSDLFile** .  
  
-   Establezca el valor de **OverwriteWSDLFile** en **True** para permitir que el archivo vacío se sobrescriba con el archivo WSDL real.  
  
-   Haga clic en **Descargar WSDL** para descargar el archivo WSDL real y sobrescribir el archivo vacío.  
  
    > [!NOTE]  
    >  La opción **Descargar WSDL** no se habilita hasta que se proporciona el nombre de un archivo local existente en el cuadro **WSDLFile** .  
  
 **OverwriteWSDLFile**  
 Indica si el archivo WSDL de la tarea Servicio web se puede sobrescribir.  
  
 Si piensa descargar el archivo WSDL utilizando el botón **Descargar WSDL** , establezca este valor en **True**.  
  
 **Nombre**  
 Proporcione un nombre único para la tarea Servicio web. Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Description**  
 Escriba una descripción de la tarea Servicio web.  
  
 **Descargar WSDL**  
 Descarga el archivo WSDL.  
  
 Este botón no se habilita hasta que se proporciona el nombre de un archivo local existente en el cuadro **WSDLFile** .  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de la tarea de servicio & #40 Web; entrada página &#41;](../../integration-services/control-flow/web-service-task-editor-input-page.md)   
 [Editor de la tarea servicio Web &#40; página resultados &#41;](../../integration-services/control-flow/web-service-task-editor-output-page.md)   
 [Página Expresiones](../../integration-services/expressions/expressions-page.md)  
  
  
