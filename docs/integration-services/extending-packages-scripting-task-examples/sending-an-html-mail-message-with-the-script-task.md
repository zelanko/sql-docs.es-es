---
title: "Enviar un mensaje de correo electrónico HTML con la tarea Script | Documentos de Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Send Mail task [Integration Services]
- Script task [Integration Services], examples
- Script task [Integration Services], HTML mail message
ms.assetid: dd2b1eef-b04f-4946-87ab-7bc56bb525ce
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: b5f50a79ca83243ea130c77a0d95ab402ba2d31a
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="sending-an-html-mail-message-with-the-script-task"></a>Enviar un mensaje de correo electrónico HTML con la tarea Script
  La tarea SendMail de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] solamente admite los mensajes de correo en texto sin formato. Sin embargo, puede enviar con facilidad los mensajes de correo HTML mediante la tarea Script y las funciones de correo de .NET Framework.  
  
> [!NOTE]  
>  Si desea crear una tarea que pueda reutilizar más fácilmente en varios paquetes, considere la posibilidad de utilizar el código de este ejemplo de tarea Script como punto inicial de una tarea personalizada. Para más información, vea [Desarrollar una tarea personalizada](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="description"></a>Description  
 En el ejemplo siguiente se usa el **System.Net.Mail** espacio de nombres para configurar y enviar un mensaje de correo electrónico HTML. El script obtiene los campos para, de, asunto y cuerpo del correo electrónico de variables de paquete, se usa para crear un nuevo **MailMessag**e y establece su **IsBodyHtml** propiedad **True**. A continuación, obtiene el nombre del servidor SMTP de otra variable de paquete, inicializa una instancia de **System.Net.Mail.SmtpClient**y llama a su **enviar** método para enviar el mensaje HTML. En el ejemplo se encapsula el mensaje enviando la funcionalidad en una subrutina que se puede reutilizar en otros scripts.  
  
#### <a name="to-configure-this-script-task-example-without-an-smtp-connection-manager"></a>Para configurar este ejemplo de tarea Script sin un administrador de conexiones SMTP  
  
1.  Cree las variables de cadena con nombre `HtmlEmailTo`, `HtmlEmailFrom`y `HtmlEmailSubject`, y asígneles los valores adecuados para un mensaje de pruebas válido.  
  
2.  Cree una variable de cadena con nombre `HtmlEmailBody` y asígnele una cadena de marcado HTML. Por ejemplo:  
  
    ```  
    <html><body><h1>Testing</h1><p>This is a <b>test</b> message.</p></body></html>  
    ```  
  
3.  Cree una variable de cadena con nombre `HtmlEmailServer` y asigne el nombre de un servidor SMTP disponible que acepte mensajes salientes anónimos.  
  
4.  Asigne las cinco de estas variables para el **ReadOnlyVariables** propiedad de una nueva tarea Script.  
  
5.  Importar la **System.Net** y **System.Net.Mail** espacios de nombres en el código.  
  
 En el código de ejemplo de este tema se obtiene el nombre del servidor SMTP de una variable de paquete. Sin embargo, también podría aprovechar un administrador de conexiones SMTP para encapsular la información de conexión y extraer el nombre del servidor del administrador de conexiones en su código. El método <xref:Microsoft.SqlServer.Dts.ManagedConnections.SMTPConn.AcquireConnection%2A> del administrador de conexiones SMTP devuelve a una cadena en el formato siguiente:  
  
 `SmtpServer=smtphost;UseWindowsAuthentication=False;EnableSsl=False;`  
  
 Puede usar el **String.Split** método para separar esta lista de argumentos en una matriz de cadenas individuales en cada punto y coma (;) o igual a iniciar sesión (=) y, a continuación, extraer el segundo argumento (subíndice 1) de la matriz como el nombre del servidor.  
  
#### <a name="to-configure-this-script-task-example-with-an-smtp-connection-manager"></a>Para configurar este ejemplo de tarea Script con un administrador de conexiones SMTP  
  
1.  Modificar la tarea de secuencia de comandos que se configuró anteriormente quitando la `HtmlEmailServer` variable en la lista de **ReadOnlyVariables**.  
  
2.  Reemplace la línea de código que obtiene el nombre de servidor:  
  
    ```  
    Dim smtpServer As String = _  
      Dts.Variables("HtmlEmailServer").Value.ToString  
    ```  
  
     con las siguientes líneas:  
  
    ```  
    Dim smtpConnectionString As String = _  
      DirectCast(Dts.Connections("SMTP Connection Manager").AcquireConnection(Dts.Transaction), String)  
    Dim smtpServer As String = _  
      smtpConnectionString.Split(New Char() {"="c, ";"c})(1)  
    ```  
  
## <a name="code"></a>código  
  
```vb  
Public Sub Main()  
  
  Dim htmlMessageTo As String = _  
    Dts.Variables("HtmlEmailTo").Value.ToString  
  Dim htmlMessageFrom As String = _  
    Dts.Variables("HtmlEmailFrom").Value.ToString  
  Dim htmlMessageSubject As String = _  
    Dts.Variables("HtmlEmailSubject").Value.ToString  
  Dim htmlMessageBody As String = _  
    Dts.Variables("HtmlEmailBody").Value.ToString  
  Dim smtpServer As String = _  
    Dts.Variables("HtmlEmailServer").Value.ToString  
  
  SendMailMessage( _  
      htmlMessageTo, htmlMessageFrom, _  
      htmlMessageSubject, htmlMessageBody, _  
      True, smtpServer)  
  
  Dts.TaskResult = ScriptResults.Success  
  
End Sub  
  
Private Sub SendMailMessage( _  
    ByVal SendTo As String, ByVal From As String, _  
    ByVal Subject As String, ByVal Body As String, _  
    ByVal IsBodyHtml As Boolean, ByVal Server As String)  
  
  Dim htmlMessage As MailMessage  
  Dim mySmtpClient As SmtpClient  
  
  htmlMessage = New MailMessage( _  
    SendTo, From, Subject, Body)  
  htmlMessage.IsBodyHtml = IsBodyHtml  
  
  mySmtpClient = New SmtpClient(Server)  
  mySmtpClient.Credentials = CredentialCache.DefaultNetworkCredentials  
  mySmtpClient.Send(htmlMessage)  
  
End Sub  
```  
  
```csharp  
public void Main()  
        {  
  
            string htmlMessageTo = Dts.Variables["HtmlEmailTo"].Value.ToString();  
            string htmlMessageFrom = Dts.Variables["HtmlEmailFrom"].Value.ToString();  
            string htmlMessageSubject = Dts.Variables["HtmlEmailSubject"].Value.ToString();  
            string htmlMessageBody = Dts.Variables["HtmlEmailBody"].Value.ToString();  
            string smtpServer = Dts.Variables["HtmlEmailServer"].Value.ToString();  
  
            SendMailMessage(htmlMessageTo, htmlMessageFrom, htmlMessageSubject, htmlMessageBody, true, smtpServer);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
        private void SendMailMessage(string SendTo, string From, string Subject, string Body, bool IsBodyHtml, string Server)  
        {  
  
            MailMessage htmlMessage;  
            SmtpClient mySmtpClient;  
  
            htmlMessage = new MailMessage(SendTo, From, Subject, Body);  
            htmlMessage.IsBodyHtml = IsBodyHtml;  
  
            mySmtpClient = new SmtpClient(Server);  
            mySmtpClient.Credentials = CredentialCache.DefaultNetworkCredentials;  
            mySmtpClient.Send(htmlMessage);  
  
        }  
```  
  
## <a name="see-also"></a>Vea también  
 [Tarea Enviar correo](../../integration-services/control-flow/send-mail-task.md)  
  
  

