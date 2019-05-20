---
title: Enviar a una cola de mensajes privada remota con la tarea Script | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], remote private message queues
- Message Queue task [Integration Services]
- Script task [Integration Services], examples
ms.assetid: 636314fd-d099-45cd-8bb4-f730d0a06739
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 13d62d72764060ef924d02ef735ff277d14ca4ed
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2019
ms.locfileid: "65724282"
---
# <a name="sending-to-a-remote-private-message-queue-with-the-script-task"></a>Enviar a una cola de mensajes privada remota con la tarea Script

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Message Queue Server (también conocido como MSMQ) facilita a los desarrolladores la comunicación rápida y confiable con los programas de aplicación mediante el envío y la recepción de mensajes. Una cola de mensajes se puede encontrar en el equipo local o en un equipo remoto y puede ser pública o privada. En [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], el administrador de conexiones MSMQ y la tarea Cola de mensajes no admiten el envío a una cola privada en un equipo remoto. Sin embargo, si se utiliza la tarea Script, resulta sencillo enviar un mensaje a una cola privada remota.  
  
> [!NOTE]  
>  Si desea crear una tarea que pueda reutilizar más fácilmente en varios paquetes, considere la posibilidad de utilizar el código de este ejemplo de tarea Script como punto inicial de una tarea personalizada. Para más información, vea [Desarrollar una tarea personalizada](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="description"></a>Descripción  
 En el ejemplo siguiente se utiliza un administrador de conexiones MSMQ existente, junto con objetos y métodos del espacio de nombres System.Messaging, para enviar el texto contenido en una variable de paquete a una cola de mensajes privada remota. La llamada al método M:Microsoft.SqlServer.Dts.ManagedConnections.MSMQConn.AcquireConnection(System.Object) del administrador de conexiones MSMQ devuelve un objeto **MessageQueue** cuyo método **Send** lleva a cabo esta tarea.  
  
#### <a name="to-configure-this-script-task-example"></a>Para configurar este ejemplo de tarea Script  
  
1.  Cree un administrador de conexiones MSMQ con el nombre predeterminado. Establezca la ruta de acceso de una cola privada remota válida, con el formato siguiente:  
  
    ```  
    FORMATNAME:DIRECT=OS:<computername>\private$\<queuename>  
    ```  
  
2.  Cree una variable [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con el nombre **MessageText** de tipo **String** para pasar el texto del mensaje al script. Escriba un mensaje predeterminado como valor de la variable.  
  
3.  Agregue una tarea Script a la superficie de diseño y modifíquela. En la pestaña **Script** del **Editor de la tarea Script**, agregue la variable `MessageText` a la propiedad **ReadOnlyVariables** para que la variable esté disponible dentro del script.  
  
4.  Haga clic en **Editar script** para abrir el editor de script de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA).  
  
5.  En el proyecto de script, agregue una referencia al espacio de nombres **System.Messaging**.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Tarea Cola de mensajes](../../integration-services/control-flow/message-queue-task.md)  
  
  
