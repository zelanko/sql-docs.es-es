---
title: Uso de mensajes | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- messages [SMO]
ms.assetid: 4037a866-4826-4c1f-890c-e7e3658adf13
caps.latest.revision: 38
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3301f223875c75e91b13c2103087df21dd5f3ad0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199318"
---
# <a name="using-messages"></a>Usar mensajes
  En SMO, el objeto <xref:Microsoft.SqlServer.Management.Smo.SystemMessageCollection> que pertenece al objeto `Server` representa los mensajes del sistema. Dado que los mensajes del sistema no se pueden modificar, las propiedades del objeto `SystemMessage` son de solo lectura.  
  
 El objeto <xref:Microsoft.SqlServer.Management.Smo.UserDefinedMessageCollection> representa los mensajes definidos por el usuario mediante programación en SMO. Los mensajes definidos por el usuario existentes se pueden detectar realizando una iteración en la colección. Los nuevos mensajes definidos por el usuario se pueden crear creando instancias de un nuevo objeto `UserDefinedMessage` y estableciendo las propiedades adecuadas.  
  
## <a name="examples"></a>Ejemplos  
 Para los siguientes ejemplos de código, deberá seleccionar el entorno de programación, la plantilla de programación y el lenguaje de programación en los que crear su aplicación. Para obtener más información, consulte [crear un proyecto de Visual Basic SMO en Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) y [crear a Visual C&#35; proyecto SMO en Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="finding-a-particular-system-message-in-visual-basic"></a>Buscar un mensaje del sistema determinado en Visual Basic  
 En el ejemplo de código se muestra cómo identificar un mensaje del sistema por número de identificador y cómo mostrar el mensaje.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBMessages1](SMO How to#SMO_VBMessages1)]  -->  
  
## <a name="finding-a-particular-system-message-in-visual-c"></a>Buscar un mensaje del sistema determinado en Visual C#  
 En el ejemplo de código se muestra cómo identificar un mensaje del sistema por número de identificador y cómo mostrar el mensaje.  
  
```  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
            //Reference an existing system message using the   
            //ItemByIdAndLanguage method.   
            SystemMessage msg = default(SystemMessage);  
            msg = srv.SystemMessages.ItemByIdAndLanguage(14126, "us_english");  
            //Display the message ID and text.   
            Console.WriteLine(msg.ID.ToString() + " " + msg.Text);  
        }  
```  
  
## <a name="finding-a-particular-system-message-in-powershell"></a>Buscar un mensaje del sistema determinado en PowerShell  
 En el ejemplo de código se muestra cómo identificar un mensaje del sistema por número de identificador y cómo mostrar el mensaje.  
  
```  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\  
$srv = get-item default  
  
#Get the message 14126 in US English and display it  
$msg = $srv.SystemMessages.ItemByIdAndLanguage(14126, "us_english")  
$msg.ID.ToString() + " "+ $msg.Text  
```  
  
## <a name="adding-a-new-user-defined-message-in-visual-basic"></a>Agregar un nuevo mensaje definido por el usuario en Visual Basic  
 En el ejemplo de código se muestra cómo crear un mensaje definido por el usuario con un identificador mayor que 50000.  
  
```  
Dim mysrv As Server  
mysrv = New Server  
Dim udm As UserDefinedMessage  
udm = New UserDefinedMessage(mysrv, 50003, "us_english", 16, "Test message")  
udm.Create()  
```  
  
## <a name="adding-a-new-user-defined-message-in-visual-c"></a>Agregar un nuevo mensaje definido por el usuario en Visual C#  
 En el ejemplo de código se muestra cómo crear un mensaje definido por el usuario con un identificador mayor que 50000.  
  
```  
{  
  
            Server mysrv = new Server();  
  
            UserDefinedMessage udm = new UserDefinedMessage(mysrv, 50030, "us_english",16, "Test message");  
            udm.Create();  
             UserDefinedMessage  msg = mysrv.UserDefinedMessages.ItemByIdAndLanguage(50030, "us_english");  
            //Display the message ID and text.   
            Console.WriteLine(msg.ID.ToString() + " " + msg.Text);  
  
        }  
```  
  
## <a name="adding-a-new-user-defined-message-in-powershell"></a>Agregar un nuevo mensaje definido por el usuario en PowerShell  
 En el ejemplo de código se muestra cómo crear un mensaje definido por el usuario con un identificador mayor que 50000.  
  
```  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Create a new message  
  
$udm = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedMessage -argumentlist `  
$srv, 50030, "us_english", 16, "Test message"  
$udm.Create()  
$msg = $srv.UserDefinedMessages.ItemByIdAndLanguage(50030, "us_english");  
$msg  
```  
  
  