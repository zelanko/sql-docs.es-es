---
description: Usar mensajes
title: Usar mensajes | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- messages [SMO]
ms.assetid: 4037a866-4826-4c1f-890c-e7e3658adf13
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8fae0c31778304c9bca4b9680451e9574ecf29dd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498513"
---
# <a name="using-messages"></a>Usar mensajes
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  En SMO, los mensajes del sistema se representan mediante el <xref:Microsoft.SqlServer.Management.Smo.SystemMessageCollection> objeto que pertenece al objeto de **servidor** . Dado que los mensajes del sistema no se pueden modificar, las propiedades del objeto **SystemMessage** son de solo lectura.  
  
 El objeto <xref:Microsoft.SqlServer.Management.Smo.UserDefinedMessageCollection> representa los mensajes definidos por el usuario mediante programación en SMO. Los mensajes definidos por el usuario existentes se pueden detectar realizando una iteración en la colección. Los nuevos mensajes definidos por el usuario se pueden crear creando instancias de un nuevo objeto **UserDefinedMessage** y estableciendo las propiedades adecuadas.  
  
## <a name="examples"></a>Ejemplos  
 Para los siguientes ejemplos de código, deberá seleccionar el entorno de programación, la plantilla de programación y el lenguaje de programación en los que crear su aplicación. Para obtener más información, vea [crear un proyecto de Visual C&#35; SMO en Visual Studio .net](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="finding-a-particular-system-message-in-visual-basic"></a>Buscar un mensaje del sistema determinado en Visual Basic  
 En el ejemplo de código se muestra cómo identificar un mensaje del sistema por número de identificador y cómo mostrar el mensaje.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference an existing system message using the ItemByIdAndLanguage method.
Dim msg As SystemMessage
msg = srv.SystemMessages.ItemByIdAndLanguage(14126, "us_english")
'Display the message ID and  text.
Console.WriteLine(msg.ID.ToString + " " + msg.Text)
```
  
## <a name="finding-a-particular-system-message-in-visual-c"></a>Buscar un mensaje del sistema determinado en Visual C#  
 En el ejemplo de código se muestra cómo identificar un mensaje del sistema por número de identificador y cómo mostrar el mensaje.  
  
```csharp  
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
  
```powershell  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\  
$srv = get-item default  
  
#Get the message 14126 in US English and display it  
$msg = $srv.SystemMessages.ItemByIdAndLanguage(14126, "us_english")  
$msg.ID.ToString() + " "+ $msg.Text  
```  
  
## <a name="adding-a-new-user-defined-message-in-visual-basic"></a>Agregar un nuevo mensaje definido por el usuario en Visual Basic  
 En el ejemplo de código se muestra cómo crear un mensaje definido por el usuario con un identificador mayor que 50000.  
  
```VBNET  
Dim mysrv As Server  
mysrv = New Server  
Dim udm As UserDefinedMessage  
udm = New UserDefinedMessage(mysrv, 50003, "us_english", 16, "Test message")  
udm.Create()  
```  
  
## <a name="adding-a-new-user-defined-message-in-visual-c"></a>Agregar un nuevo mensaje definido por el usuario en Visual C#  
 En el ejemplo de código se muestra cómo crear un mensaje definido por el usuario con un identificador mayor que 50000.  
  
```csharp  
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
  
```powershell  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Create a new message  
  
$udm = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedMessage -argumentlist `  
$srv, 50030, "us_english", 16, "Test message"  
$udm.Create()  
$msg = $srv.UserDefinedMessages.ItemByIdAndLanguage(50030, "us_english");  
$msg  
```  
  
  
