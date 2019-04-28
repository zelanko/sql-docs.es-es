---
title: Editor de tareas de correo (página correo) enviar | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sendmailtask.mail.f1
helpviewer_keywords:
- Send Mail Task Editor
ms.assetid: adb385d5-ef24-4d18-b9ea-b39e00a7075e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 57b0cfee4c9197a721e132a672e11364e8cd29c7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62889050"
---
# <a name="send-mail-task-editor-mail-page"></a>Editor de la tarea Enviar correo (página Correo)
  Use la página **Correo** del cuadro de diálogo **Editor de la tarea Enviar correo** para especificar los destinatarios, el tipo de mensaje y la prioridad de un mensaje. También puede adjuntar archivos al mensaje. El texto del mensaje puede consistir en una cadena que proporcione, una conexión de archivo a un archivo con el texto o el nombre de una variable con el texto.  
  
 Para obtener información acerca de esta tarea, vea [Send Mail Task](control-flow/send-mail-task.md).  
  
## <a name="options"></a>Opciones  
 **SMTPConnection**  
 Seleccione un administrador de conexiones SMTP de la lista, o bien haga clic en **\<Nueva conexión…>** para crear un administrador de conexiones.  
  
> [!IMPORTANT]  
>  El administrador de conexiones SMTP solo es compatible con la autenticación anónima y la autenticación de Windows. No admite la autenticación básica.  
  
 **Temas relacionados:** [Administrador de conexiones SMTP](connection-manager/smtp-connection-manager.md)  
  
 **De**  
 Especifique la dirección de correo electrónico del remitente.  
  
 **Para**  
 Escriba las direcciones de correo electrónico de los destinatarios, separadas con punto y coma.  
  
 **CC**  
 Escriba las direcciones de correo electrónico de las personas que recibirán una copia del mensaje, separadas con punto y coma.  
  
 **CCO**  
 Escriba las direcciones de correo electrónico de los destinatarios ocultos de copia del mensaje, separadas con punto y coma.  
  
 **Asunto**  
 Escriba el asunto del mensaje de correo electrónico.  
  
 **MessageSourceType**  
 Permite seleccionar el tipo de origen del mensaje. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Entrada directa**|Establezca el origen para el texto del mensaje. Si selecciona este valor, se mostrará la opción dinámica **MessageSource**.|  
|**Conexión de archivos**|Establezca el origen al archivo que incluye el texto del mensaje. Si selecciona este valor, se mostrará la opción dinámica **MessageSource**.|  
|**Variable**|Establezca el origen para la variable que incluye el texto del mensaje. Si selecciona este valor, se mostrará la opción dinámica **MessageSource**.|  
  
 **Prioridad**  
 Establezca la prioridad del mensaje.  
  
 **Datos adjuntos**  
 Escriba los nombres de los archivos de datos adjuntos que desea adjuntar al mensaje de correo electrónico, separados por una barra vertical (|).  
  
> [!NOTE]  
>  Las líneas Para, CC y CCO están limitadas a 256 caracteres según las normas de Internet.  
  
## <a name="messagesourcetype-dynamic-options"></a>Opciones dinámicas de MessageSourceType  
  
### <a name="messagesourcetype--direct-input"></a>MessageSourceType = Entrada directa  
 **MessageSource**  
 Escriba el texto del mensaje, o bien haga clic en el botón Examinar (…) y escriba el mensaje en el cuadro de diálogo **Origen del mensaje**.  
  
### <a name="messagesourcetype--file-connection"></a>MessageSourceType = Conexión de archivos  
 **MessageSource**  
 Seleccione un administrador de conexiones de archivos de la lista, o bien haga clic en \<**Nueva conexión…**> para crear un administrador de conexiones.  
  
 **Temas relacionados:** [Administrador de conexiones de archivos](connection-manager/file-connection-manager.md), [Editor de administrador de conexiones de archivos](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="messagesourcetype--variable"></a>MessageSourceType = Variable  
 **MessageSource**  
 Seleccione una variable de la lista, o bien haga clic en \<**Nueva variable…**> para crear una.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md), [Agregar variable](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de la tarea Enviar correo &#40;página General&#41;](general-page-of-integration-services-designers-options.md)   
 [Página Expresiones](expressions/expressions-page.md)  
  
  
