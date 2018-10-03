---
title: Usar el correo electrónico de base de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- e-mail [SMO]
- Database Mail [SMO]
- mail [SMO]
ms.assetid: 7605390f-b485-48cc-8d97-e364a066067b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fcf6e57ed33e0799ae61610fdb15bd59aea45de8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48221575"
---
# <a name="using-database-mail"></a>Utilizar el correo electrónico de base de datos
  En SMO, el objeto <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> referenciado por la propiedad <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> representa el subsistema del correo electrónico de base de datos. Mediante el objeto <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> de SMO, puede configurar el subsistema del correo electrónico de base de datos y administrar los perfiles y cuentas de correo. SMO <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> objeto pertenece a la `Server` objeto, lo que significa que el ámbito de las cuentas de correo está en el nivel de servidor.  
  
## <a name="examples"></a>Ejemplos  
 Para utilizar cualquier ejemplo de código que se proporcione, deberá elegir el entorno de programación, la plantilla de programación y el lenguaje de programación con los que crear su aplicación. Para obtener más información, consulte [crear un proyecto de Visual Basic SMO en Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) o [crear un Visual C&#35; proyecto SMO en Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
 Para los programas que utilizan [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] correo electrónico de base de datos, debe incluir el `Imports` instrucción para calificar el espacio de nombres de correo electrónico. Inserte la instrucción después de las demás instrucciones `Imports`, antes de cualquier declaración de la aplicación, como:  
  
 `Imports Microsoft.SqlServer.Management.Smo`  
  
 `Imports Microsoft.SqlServer.Management.Common`  
  
 `Imports Microsoft.SqlServer.Management.Smo.Mail`  
  
## <a name="creating-a-database-mail-account-by-using-visual-basic"></a>Crear una cuenta de correo electrónico de base de datos utilizando Visual Basic  
 En este ejemplo de código se muestra cómo crear una cuenta de correo electrónico en SMO. El Correo electrónico de base de datos está representado por el objeto <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> y está referenciado por la propiedad <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> del objeto <xref:Microsoft.SqlServer.Management.Smo.Server>. SMO puede utilizarse para configurar mediante programación el Correo electrónico de base de datos, pero no puede usarse para enviar o administrar el correo electrónico recibido.  
  
 VB.NET  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBMail1](SMO How to#SMO_VBMail1)]  -->  
  
## <a name="creating-a-database-mail-account-by-using-visual-c"></a>Crear una cuenta de correo electrónico de base de datos utilizando Visual C#  
 En este ejemplo de código se muestra cómo crear una cuenta de correo electrónico en SMO. El Correo electrónico de base de datos está representado por el objeto <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> y está referenciado por la propiedad <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> del objeto <xref:Microsoft.SqlServer.Management.Smo.Server>. SMO puede utilizarse para configurar mediante programación el Correo electrónico de base de datos, pero no puede usarse para enviar o administrar el correo electrónico recibido.  
  
```csharp  
{  
         //Connect to the local, default instance of SQL Server.  
         Server srv = default(Server);   
           srv = new Server();   
           //Define the Database Mail service with a SqlMail object variable   
           //and reference it using the Server Mail property.   
           SqlMail sm;   
           sm = srv.Mail;   
           //Define and create a mail account by supplying the Database Mail  
           //service, name, description, display name, and email address  
           //arguments in the constructor.   
           MailAccount a = default(MailAccount);   
           a = new MailAccount(sm, "AdventureWorks2012 Administrator", "AdventureWorks2012 Automated Mailer", "Mail account for administrative e-mail.", "dba@Adventure-Works.com");   
           a.Create();    
}  
```  
  
## <a name="creating-a-database-mail-account-by-using-powershell"></a>Crear una cuenta de correo electrónico de base de datos utilizando PowerShell  
 En este ejemplo de código se muestra cómo crear una cuenta de correo electrónico en SMO. El Correo electrónico de base de datos está representado por el objeto <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> y está referenciado por la propiedad <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> del objeto <xref:Microsoft.SqlServer.Management.Smo.Server>. SMO puede utilizarse para configurar mediante programación el Correo electrónico de base de datos, pero no puede usarse para enviar o administrar el correo electrónico recibido.  
  
 PowerShell  
  
```powershell  
#Connect to the local, default instance of SQL Server.  
  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Define the Database Mail; reference it using the Server Mail property.  
$sm = $srv.Mail  
  
#Define and create a mail account by supplying the Database Mail service,  
#name, description, display name, and email address arguments in the constructor.  
$a = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Mail.MailAccount -argumentlist $sm, `  
"Adventure Works Administrator", "Adventure Works Automated Mailer",`  
 "Mail account for administrative e-mail.", "dba@Adventure-Works.com"  
$a.Create()  
```  
  
  
