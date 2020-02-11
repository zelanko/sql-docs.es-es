---
title: Editor de la tarea servicio Web (página general) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.webservicestask.general.f1
helpviewer_keywords:
- Web Service Task Editor
ms.assetid: 4d7df283-430d-4f0f-9dd4-5909554cd5eb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c6f993f1f2386782bf8225f22b285b9385e2f8e3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66054540"
---
# <a name="web-service-task-editor-general-page"></a>Editor de la tarea Servicio web (página General)
  Use la página **General** del cuadro de diálogo **Editor de la tarea Servicio web** para especificar un administrador de conexiones de HTTP, especificar la ubicación del archivo de Lenguaje de descripción de servicios web (WSDL) que usa la tarea Servicio web, describir la tarea Servicios web y descargar el archivo WSDL.  
  
 Para obtener más información sobre esta tarea, vea [Tarea Servicio web](control-flow/web-service-task.md).  
  
## <a name="options"></a>Opciones  
 **HTTPConnection**  
 Seleccione un administrador de conexiones de la lista, o bien haga clic en \<**Nueva conexión…**> para crear uno.  
  
> [!IMPORTANT]  
>  El administrador de conexiones HTTP solo es compatible con la autenticación anónima y la autenticación básica. No es compatible con la autenticación de Windows.  
  
 **Temas relacionados:**  [Administrador de conexiones http](connection-manager/http-connection-manager.md), [Editor del administrador de conexiones http página de &#40;Server&#41;](../../2014/integration-services/http-connection-manager-editor-server-page.md)  
  
 **WSDLFile**  
 Escriba la ruta de acceso completa de un archivo WSDL local del equipo, o bien haga clic en el botón Examinar **(…)** y busque el archivo.  
  
 Si ya ha descargado manualmente el archivo WSDL en el equipo, seleccione este archivo. Sin embargo, si el archivo WSDL todavía no se ha descargado, siga estos pasos:  
  
-   Cree un archivo vacío que tenga la extensión ".wsdl".  
  
-   Seleccione este archivo vacío para la opción **WSDLFile** .  
  
-   Establezca el valor de **OverwriteWSDLFile** en `True` para permitir que el archivo vacío se SOBRESCRIBA con el archivo WSDL real.  
  
-   Haga clic en **Descargar WSDL** para descargar el archivo WSDL real y sobrescribir el archivo vacío.  
  
    > [!NOTE]  
    >  La opción **Descargar WSDL** no se habilita hasta que se proporciona el nombre de un archivo local existente en el cuadro **WSDLFile** .  
  
 **OverwriteWSDLFile**  
 Indica si el archivo WSDL de la tarea Servicio web se puede sobrescribir.  
  
 Si tiene previsto descargar el archivo WSDL mediante el botón **Descargar WSDL** , establezca este valor en `True`.  
  
 **Nombre**  
 Proporcione un nombre único para la tarea Servicio web. Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Descripción**  
 Escriba una descripción de la tarea Servicio web.  
  
 **Descargar WSDL**  
 Descarga el archivo WSDL.  
  
 Este botón no se habilita hasta que se proporciona el nombre de un archivo local existente en el cuadro **WSDLFile** .  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de la tarea servicio Web &#40;página de entrada&#41;](../../2014/integration-services/web-service-task-editor-input-page.md)   
 [Editor de la tarea servicio Web &#40;página salida&#41;](../../2014/integration-services/web-service-task-editor-output-page.md)   
 [Página Expresiones](expressions/expressions-page.md)  
  
  
