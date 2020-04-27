---
title: Tarea Enviar correo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sendmailtask.f1
helpviewer_keywords:
- mail [Integration Services]
- Send Mail task
- e-mail [Integration Services]
- messages [Integration Services]
- sending messages
ms.assetid: fe0b7cbc-fe8e-4fe2-95b4-2953efff5869
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3308899190aa63ebb9be93c4c9af15d5e0f94600
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62830399"
---
# <a name="send-mail-task"></a>Enviar correo, tarea
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
  
 El texto del mensaje puede ser una cadena que especifique, una conexión a un archivo que contiene el texto o el nombre de una variable que contiene el texto que se va a enviar. La tarea usa el administrador de conexiones de archivos para conectar con un archivo. Para más información, consulte [Flat File Connection Manager](../connection-manager/file-connection-manager.md).  
  
 La tarea usa el administrador de conexiones SMTP para conectar con un servidor de correo. Para más información, consulte [SMTP Connection Manager](../connection-manager/smtp-connection-manager.md).  
  
## <a name="custom-logging-messages-available-on-the-send-mail-task"></a>Mensajes de registro personalizados disponibles en la tarea Enviar correo  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea Enviar correo. Para obtener más información, vea [Registro de Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md) y [Mensajes personalizados para registro](../custom-messages-for-logging.md).  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`SendMailTaskBegin`|Indica que la tarea comenzó a enviar un mensaje de correo electrónico.|  
|`SendMailTaskEnd`|Indica que la tarea finalizó el envío de un mensaje de correo electrónico.|  
|`SendMailTaskInfo`|Proporciona información descriptiva sobre la tarea.|  
  
## <a name="configuring-the-send-mail-task"></a>Configurar la tarea Enviar correo  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor de la tarea Enviar correo &#40;página General&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor de la tarea Enviar correo &#40;página Correo&#41;](../send-mail-task-editor-mail-page.md)  
  
-   [Página Expresiones](../expressions/expressions-page.md)  
  
 Para obtener información sobre cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.SendMailTask.SendMailTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obtener información sobre cómo establecer estas propiedades en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en [Establecer las propiedades de tareas o contenedores](../set-the-properties-of-a-task-or-container.md).  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   Artículo técnico [How to send email with delivery notification in C#](https://go.microsoft.com/fwlink/?LinkId=237625)(Enviar un mensaje de correo electrónico con una notificación de entrega en C#) en shareourideas.com  
  
## <a name="see-also"></a>Consulte también  
 [Tareas de Integration Services](integration-services-tasks.md)   
 [Flujo de control](control-flow.md)  
  
  
