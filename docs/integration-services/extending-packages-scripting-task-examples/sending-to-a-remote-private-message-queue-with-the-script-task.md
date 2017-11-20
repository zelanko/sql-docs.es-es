---
title: Enviar a una cola de mensajes privada remota con la tarea Script | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting-task-examples
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], remote private message queues
- Message Queue task [Integration Services]
- Script task [Integration Services], examples
ms.assetid: 636314fd-d099-45cd-8bb4-f730d0a06739
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5ab9314ef0825486914d1801bfa2b9613883b43e
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="sending-to-a-remote-private-message-queue-with-the-script-task"></a>Enviar a una cola de mensajes privada remota con la tarea Script
  Message Queue Server (también conocido como MSMQ) facilita a los desarrolladores la comunicación rápida y confiable con los programas de aplicación mediante el envío y la recepción de mensajes. Una cola de mensajes se puede encontrar en el equipo local o en un equipo remoto y puede ser pública o privada. En [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], el administrador de conexiones MSMQ y la tarea Cola de mensajes no admiten el envío a una cola privada en un equipo remoto. Sin embargo, si se utiliza la tarea Script, resulta sencillo enviar un mensaje a una cola privada remota.  
  
> [!NOTE]  
>  Si desea crear una tarea que pueda reutilizar más fácilmente en varios paquetes, considere la posibilidad de utilizar el código de este ejemplo de tarea Script como punto inicial de una tarea personalizada. Para más información, vea [Desarrollar una tarea personalizada](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="description"></a>Description  
 En el ejemplo siguiente se usa un administrador de conexiones MSMQ existente, así como los objetos y métodos del espacio de nombres System.Messaging, para enviar el texto contenido en una variable de paquete a una cola de mensajes privada remota. La llamada al método M:Microsoft.SqlServer.Dts.ManagedConnections.MSMQConn.AcquireConnection(System.Object) del Administrador de conexiones MSMQ devuelve un **MessageQueue** cuyos **enviar** método lleva a cabo esta tarea.  
  
#### <a name="to-configure-this-script-task-example"></a>Para configurar este ejemplo de tarea Script  
  
1.  Cree un administrador de conexiones MSMQ con el nombre predeterminado. Establezca la ruta de acceso de una cola privada remota válida, con el formato siguiente:  
  
    ```  
    FORMATNAME:DIRECT=OS:<computername>\private$\<queuename>  
    ```  
  
2.  Crear un [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] variable denominada **MessageText** de tipo **cadena** para pasar el texto del mensaje en la secuencia de comandos. Escriba un mensaje predeterminado como valor de la variable.  
  
3.  Agregue una tarea Script a la superficie de diseño y modifíquela. En el **Script** pestaña de la **Editor de la tarea de secuencia de comandos**, agregar el `MessageText` variable la **ReadOnlyVariables** propiedad que se va a hacer la variable esté disponible dentro de la secuencia de comandos .  
  
4.  Haga clic en **editar Script** para abrir el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] herramientas para el editor de secuencias de comandos de aplicaciones (VSTA).  
  
5.  Agregar una referencia en el proyecto de script para la **System.Messaging** espacio de nombres.  
  
6.  Reemplace el contenido de la ventana de script con el código de la sección siguiente.  
  
## <a name="code"></a>código  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports System.Messaging  
  
Public Class ScriptMain  
  
    Public Sub Main()  
  
        Dim remotePrivateQueue As MessageQueue  
        Dim messageText As String  
  
        remotePrivateQueue = _  
            DirectCast(Dts.Connections("Message Queue Connection Manager").AcquireConnection(Dts.Transaction), _  
            MessageQueue)  
        messageText = DirectCast(Dts.Variables("MessageText").Value, String)  
        remotePrivateQueue.Send(messageText)  
  
        Dts.TaskResult = ScriptResults.Success  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.Messaging;  
  
public class ScriptMain  
{  
  
    public void Main()  
        {  
  
            MessageQueue remotePrivateQueue = new MessageQueue();  
            string messageText;  
  
            remotePrivateQueue = (MessageQueue)(Dts.Connections["Message Queue Connection Manager"].AcquireConnection(Dts.Transaction) as MessageQueue);  
            messageText = (string)(Dts.Variables["MessageText"].Value);  
            remotePrivateQueue.Send(messageText);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [Tarea Cola de mensajes](../../integration-services/control-flow/message-queue-task.md)  
  
  

