---
title: Usar el cifrado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- database master key [SMO]
- cryptography [SMO]
- cryptography [SQL Server], SMO
- encryption keys [SMO]
- encryption [SQL Server], SMO
- encryption [SMO]
- certificates [SMO]
- service master key [SMO]
ms.assetid: 405e0ed7-50a9-430e-a343-471f54b4af76
author: stevestein
ms.author: sstein
ms.openlocfilehash: ea79d34a5c0e8f8d51ce38db799f88c8aa981dd0
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85003584"
---
# <a name="using-encryption"></a>Utilizar el cifrado
  En SMO, el objeto <xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey> representa la clave maestra de servicio. La propiedad <xref:Microsoft.SqlServer.Management.Smo.Server.ServiceMasterKey%2A> del objeto <xref:Microsoft.SqlServer.Management.Smo.Server> hace referencia a esto. Se puede regenerar utilizando el método <xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey.Regenerate%2A>.  
  
 El objeto<xref:Microsoft.SqlServer.Management.Smo.MasterKey> representa la clave maestra de la base de datos. La propiedad <xref:Microsoft.SqlServer.Management.Smo.MasterKey.IsEncryptedByServer%2A> indica si se cifra la clave maestra de base de datos utilizando la clave maestra de servicio. La copia cifrada en la base de datos maestra se actualiza automáticamente siempre que se cambia la clave maestra de base de datos.  
  
 Es posible quitar el cifrado de la clave de servicio utilizando el método <xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A> y cifrar la clave maestra de base de datos con una contraseña. En esa situación, tendrá que abrir explícitamente la clave maestra de base de datos antes de tener acceso a las claves privadas que ha protegido.  
  
 Cuando una base de datos se adjunta a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], debe proporcionar la contraseña para la clave maestra de base de datos o ejecutar el método <xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A> para hacer que una copia no cifrada de la clave maestra de base de datos esté disponible para el cifrado con la clave maestra de servicio. Se recomienda este paso para evitar la necesidad de abrir explícitamente la clave maestra de base de datos.  
  
 El método <xref:Microsoft.SqlServer.Management.Smo.MasterKey.Regenerate%2A> regenera la clave maestra de base de datos. Si se vuelve a generar la clave maestra de base de datos, todas las claves cifradas con ella se descifran y, a continuación, vuelve a cifrarlas con la nueva clave maestra de base de datos. El método <xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A> quita el cifrado de la clave maestra de base de datos mediante la clave maestra de servicio. <xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A> hace que se cifre una copia de la clave maestra utilizando la clave maestra de servicio y la almacena en la base de datos actual y en la base de datos maestra.  
  
 En SMO, el objeto <xref:Microsoft.SqlServer.Management.Smo.Certificate> representa los certificados. El objeto <xref:Microsoft.SqlServer.Management.Smo.Certificate> tiene propiedades que especifican la clave pública, el nombre del asunto, el período de validez e información sobre el emisor. El permiso para tener acceso al certificado se controla utilizando los métodos `Grant`, `Revoke` y `Deny`.  
  
## <a name="example"></a>Ejemplo  
 Para el siguiente ejemplo de código, deberá seleccionar el entorno de programación, la plantilla de programación y el lenguaje de programación en los que crear su aplicación. Para obtener más información, vea [crear un proyecto de Visual Basic SMO en Visual Studio .net](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) y [crear un proyecto de Visual C&#35; SMO en Visual Studio .net](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="adding-a-certificate-in-visual-basic"></a>Agregar un certificado en Visual Basic  
 En el ejemplo de código se crea un certificado simple con una contraseña de cifrado. A diferencia de otros objetos, el método <xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A> tiene varias sobrecargas. La sobrecarga utilizada en el ejemplo crea un nuevo certificado con una contraseña de cifrado.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCertificate1](SMO How to#SMO_VBCertificate1)]  -->  
  
## <a name="adding-a-certificate-in-visual-c"></a>Agregar un certificado en Visual C#  
 En el ejemplo de código se crea un certificado simple con una contraseña de cifrado. A diferencia de otros objetos, el método <xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A> tiene varias sobrecargas. La sobrecarga utilizada en el ejemplo crea un nuevo certificado con una contraseña de cifrado.  
  
```csharp
{  
            //Connect to the local, default instance of SQL Server.   
            {  
                Server srv = new Server();  
  
                //Reference the AdventureWorks2012 database.   
                Database db = srv.Databases["AdventureWorks2012"];  
  
                //Define a Certificate object variable by supplying the parent database and name in the constructor.   
                Certificate c = new Certificate(db, "Test_Certificate");  
  
                //Set the start date, expiry date, and description.   
                System.DateTime dt;  
                DateTime.TryParse("January 01, 2010", out dt);  
                c.StartDate = dt;  
                DateTime.TryParse("January 01, 2015", out dt);  
                c.ExpirationDate = dt;  
                c.Subject = "This is a test certificate.";  
                //Create the certificate on the instance of SQL Server by supplying the certificate password argument.   
                c.Create("pGFD4bb925DGvbd2439587y");  
            }  
        }   
```  
  
## <a name="adding-a-certificate-in-powershell"></a>Agregar un certificado en PowerShell  
 En el ejemplo de código se crea un certificado simple con una contraseña de cifrado. A diferencia de otros objetos, el método <xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A> tiene varias sobrecargas. La sobrecarga utilizada en el ejemplo crea un nuevo certificado con una contraseña de cifrado.  
  
```powershell
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item AdventureWorks2012  
  
#Create a certificate
$c = New-Object -TypeName Microsoft.SqlServer.Management.Smo.Certificate -ArgumentList $db, "Test_Certificate"  
$c.StartDate = "January 01, 2010"  
$c.Subject = "This is a test certificate."  
$c.ExpirationDate = "January 01, 2015"  
  
#Create the certificate on the instance of SQL Server by supplying the certificate password argument.  
$c.Create("pGFD4bb925DGvbd2439587y")
```  
  
## <a name="see-also"></a>Consulte también  
 [Uso de claves de cifrado](using-encryption.md)  
