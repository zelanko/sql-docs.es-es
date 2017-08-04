---
title: "Editor de la tarea de correo (página correo) enviar | Documentos de Microsoft"
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
- sql13.dts.designer.sendmailtask.mail.f1
helpviewer_keywords:
- Send Mail Task Editor
ms.assetid: adb385d5-ef24-4d18-b9ea-b39e00a7075e
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0c630d4044cf083e80b25ea2aac60b74a5bc9d7e
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="send-mail-task-editor-mail-page"></a>Editor de la tarea Enviar correo (página Correo)
  Use la página **Correo** del cuadro de diálogo **Editor de la tarea Enviar correo** para especificar los destinatarios, el tipo de mensaje y la prioridad de un mensaje. También puede adjuntar archivos al mensaje. El texto del mensaje puede consistir en una cadena que proporcione, una conexión de archivo a un archivo con el texto o el nombre de una variable con el texto.  
  
 Para obtener información acerca de esta tarea, vea [Send Mail Task](../../integration-services/control-flow/send-mail-task.md).  
  
## <a name="options"></a>Opciones  
 **SMTPConnection**  
 Seleccione un administrador de conexión de SMTP en la lista o haga clic en  **\<nueva conexión... >** para crear una nueva conexión de administrador.  
  
> [!IMPORTANT]  
>  El administrador de conexiones SMTP solo es compatible con la autenticación anónima y la autenticación de Windows. No admite la autenticación básica.  
  
 **Temas relacionados:** [Administrador de conexiones SMTP](../../integration-services/connection-manager/smtp-connection-manager.md)  
  
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
  
|Value|Description|  
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
 Escriba el texto del mensaje, o bien haga clic en el botón Examinar (…) y escriba el mensaje en el cuadro de diálogo **Origen del mensaje** .  
  
### <a name="messagesourcetype--file-connection"></a>MessageSourceType = Conexión de archivos  
 **MessageSource**  
 Seleccione un administrador de conexión de archivos en la lista o haga clic en \< **nueva conexión...** > para crear una nueva conexión de administrador.  
  
 **Temas relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### <a name="messagesourcetype--variable"></a>MessageSourceType = Variable  
 **MessageSource**  
 Seleccione una variable en la lista o haga clic en \< **nueva variable...** > para crear una nueva variable.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Agregar variable](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Enviar correo electrónico de Editor de la tarea &#40; Página general &#41;](../../integration-services/control-flow/send-mail-task-editor-general-page.md)   
 [Página Expresiones](../../integration-services/expressions/expressions-page.md)  
  
  
