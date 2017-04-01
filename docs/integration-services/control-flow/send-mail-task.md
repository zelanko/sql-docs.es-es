---
title: "Tarea Enviar correo | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.sendmailtask.f1"
helpviewer_keywords: 
  - "correo [Integration Services]"
  - "Enviar correo, tarea"
  - "electrónico, correo [Integration Services]"
  - "mensajes [Integration Services]"
  - "enviar mensajes"
ms.assetid: fe0b7cbc-fe8e-4fe2-95b4-2953efff5869
caps.latest.revision: 51
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 51
---
# Tarea Enviar correo
  La tarea Enviar correo envía un mensaje de correo electrónico. Un paquete puede utilizar la tarea Enviar correo para enviar mensajes si las tareas del paquete de flujo de trabajo finalizan correctamente o si se producen errores, o para enviar mensajes en respuesta a eventos provocados por el paquete en tiempo de ejecución. Por ejemplo, la tarea puede notificar a un administrador de base de datos si la tarea Copia de seguridad de la base de datos se realizó correctamente o no.  
  
 Puede configurar la tarea Enviar correo de las siguientes maneras:  
  
-   Proporcionar el texto del mensaje de correo electrónico.  
  
-   Especificar el asunto del mensaje de correo electrónico.  
  
-   Establecer el nivel de prioridad del mensaje. La tarea admite tres niveles de prioridad: normal, bajo y alto.  
  
-   Especificar los destinatarios en las líneas Para, CC y CCO. Si la tarea especifica varios destinatarios, deben separarse mediante signos de punto y coma.  
  
    > [!NOTE]  
    >  Las líneas Para, CC y CCO tienen un límite de 256 caracteres cada una, de acuerdo con los estándares de Internet.  
  
-   Incluir archivos adjuntos. Si la tarea especifica varios archivos adjuntos, deben separarse mediante la barra vertical (|).  
  
    > [!NOTE]  
    >  Si cuando se ejecuta el paquete no existe un archivo adjunto, se producirá un error.  
  
-   Especificar el administrador de conexiones SMTP que se va a usar.  
  
    > [!IMPORTANT]  
    >  El administrador de conexiones SMTP solo es compatible con la autenticación anónima y la autenticación de Windows. No admite la autenticación básica.  
  
 El texto del mensaje puede ser una cadena que especifique, una conexión a un archivo que contiene el texto o el nombre de una variable que contiene el texto que se va a enviar. La tarea usa el administrador de conexiones de archivos para conectar con un archivo. Para más información, consulte [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
 La tarea usa el administrador de conexiones SMTP para conectar con un servidor de correo. Para más información, consulte [SMTP Connection Manager](../../integration-services/connection-manager/smtp-connection-manager.md).  
  
## Mensajes de registro personalizados disponibles en la tarea Enviar correo  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea Enviar correo. Para más información, vea [Registro de Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md) y [Mensajes personalizados para registro](../../integration-services/performance/custom-messages-for-logging.md).  
  
|Entrada del registro|Description|  
|---------------|-----------------|  
|**SendMailTaskBegin**|Indica que la tarea comenzó a enviar un mensaje de correo electrónico.|  
|**SendMailTaskEnd**|Indica que la tarea finalizó el envío de un mensaje de correo electrónico.|  
|**SendMailTaskInfo**|Proporciona información descriptiva sobre la tarea.|  
  
## Configurar la tarea Enviar correo  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor de la tarea Enviar correo &#40;página General&#41;](../../integration-services/control-flow/send-mail-task-editor-general-page.md)  
  
-   [Editor de la tarea Enviar correo &#40;página Correo&#41;](../../integration-services/control-flow/send-mail-task-editor-mail-page.md)  
  
-   [Página Expresiones](../../integration-services/expressions/expressions-page.md)  
  
 Para obtener información sobre cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.SendMailTask.SendMailTask>  
  
## Tareas relacionadas  
 Para obtener información sobre cómo establecer estas propiedades en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)], haga clic en [Establecer las propiedades de tareas o contenedores](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md).  
  
## Contenido relacionado  
  
-   Artículo técnico [How to send email with delivery notification in C#](http://go.microsoft.com/fwlink/?LinkId=237625) (Enviar un mensaje de correo electrónico con una notificación de entrega en C#) en shareourideas.com  
  
## Vea también  
 [Tareas de Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Flujo de control](../../integration-services/control-flow/control-flow.md)  
  
  