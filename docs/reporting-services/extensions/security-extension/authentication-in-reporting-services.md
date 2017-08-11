---
title: "Autenticación en Reporting Services | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- security [Reporting Services], authentication
- forms-based authentication [Reporting Services]
- authentication [Reporting Services]
- custom authentication [Reporting Services]
ms.assetid: 103ce1f9-31d8-44bb-b540-2752e4dcf60b
caps.latest.revision: 25
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 6926d7787a715ab9183763939ca78ed192d0e251
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="authentication-in-reporting-services"></a>Autenticación de Windows en Reporting Services
  La autenticación es el proceso de establecer el derecho de un usuario en una identidad. Hay muchas técnicas que puede utilizar para autenticar a un usuario. La manera más común es mediante contraseñas. Por ejemplo, al implementar la autenticación de formularios, desea una implementación que consulte las credenciales (normalmente con alguna interfaz que solicita un nombre de inicio de sesión y una contraseña) de los usuarios y, a continuación, valida los usuarios con un almacén de datos, como una tabla de base de datos o un archivo de configuración. Si no se pueden validar las credenciales, se produce un error en el proceso de autenticación y el usuario asumirá una identidad anónima.  
  
## <a name="custom-authentication-in-reporting-services"></a>Autenticación personalizada en Reporting Services  
 En [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], el sistema operativo Windows administra la autenticación de los usuarios a través de la seguridad integrada o de la recepción explícita y la validación de las credenciales del usuario. La autenticación personalizada se puede desarrollar en [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] para admitir esquemas de autenticación adicionales. Esto se posibilita a través de la interfaz de extensión de la seguridad <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension2>. Todas las extensiones heredan de la interfaz base <xref:Microsoft.ReportingServices.Interfaces.IExtension> para cualquier extensión que implemente y use el servidor de informes. <xref:Microsoft.ReportingServices.Interfaces.IExtension>, así como <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension2>, son miembros del espacio de nombres <xref:Microsoft.ReportingServices.Interfaces>.  
  
 Para autenticar con un servidor de informes en [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], se usa principalmente el método <xref:ReportService2010.ReportingService2010.LogonUser%2A>. Este miembro del servicio web de Reporting Services se puede utilizar con el objeto de pasar las credenciales del usuario a un servidor de informes para la validación. Implementa la extensión de seguridad subyacente **IAuthenticationExtension2.LogonUser** que contiene el código de autenticación personalizado. En el ejemplo de autenticación de formularios, **LogonUser**, que realiza una comprobación de autenticación con las credenciales proporcionadas y un almacén de usuario personalizado en una base de datos. Un ejemplo de una implementación de **LogonUser** tiene este aspecto:  
  
```  
public bool LogonUser(string userName, string password, string authority)  
{  
   return AuthenticationUtilities.VerifyPassword(userName, password);  
}  
  
```  
  
 La función de ejemplo siguiente se utiliza para comprobar las credenciales proporcionadas:  
  
```  
  
internal static bool VerifyPassword(string suppliedUserName,  
   string suppliedPassword)  
{   
   bool passwordMatch = false;  
   // Get the salt and pwd from the database based on the user name.  
   // See "How To: Use DPAPI (Machine Store) from ASP.NET," "How To:  
   // Use DPAPI (User Store) from Enterprise Services," and "How To:  
   // Create a DPAPI Library" for more information about how to use  
   // DPAPI to securely store connection strings.  
   SqlConnection conn = new SqlConnection(  
      "Server=localhost;" +   
      "Integrated Security=SSPI;" +  
      "database=UserAccounts");  
   SqlCommand cmd = new SqlCommand("LookupUser", conn);  
   cmd.CommandType = CommandType.StoredProcedure;  
  
   SqlParameter sqlParam = cmd.Parameters.Add("@userName",  
       SqlDbType.VarChar,  
       255);  
   sqlParam.Value = suppliedUserName;  
   try  
   {  
      conn.Open();  
      SqlDataReader reader = cmd.ExecuteReader();  
      reader.Read(); // Advance to the one and only row  
      // Return output parameters from returned data stream  
      string dbPasswordHash = reader.GetString(0);  
      string salt = reader.GetString(1);  
      reader.Close();  
      // Now take the salt and the password entered by the user  
      // and concatenate them together.  
      string passwordAndSalt = String.Concat(suppliedPassword, salt);  
      // Now hash them  
      string hashedPasswordAndSalt =  
         FormsAuthentication.HashPasswordForStoringInConfigFile(  
         passwordAndSalt,  
         "SHA1");  
      // Now verify them. Returns true if they are equal.  
      passwordMatch = hashedPasswordAndSalt.Equals(dbPasswordHash);  
   }  
   catch (Exception ex)  
   {  
       throw new Exception("Exception verifying password. " +  
          ex.Message);  
   }  
   finally  
   {  
       conn.Close();  
   }  
   return passwordMatch;  
}  
```  
  
## <a name="authentication-flow"></a>Flujo de autenticación  
 El servicio Web de Reporting Services proporciona extensiones de autenticación personalizadas para habilitar la autenticación de formularios mediante el portal web y el servidor de informes.  
  
 El método <xref:ReportService2010.ReportingService2010.LogonUser%2A> del servicio web de Reporting Services se utiliza para enviar las credenciales al servidor de informes para la autenticación. El servicio web utiliza los encabezados HTTP para pasar un vale de autenticación (conocido como "cookie") del servidor al cliente para las solicitudes de inicio de sesión validadas.  
  
 La ilustración siguiente describe el método para autenticar a los usuarios en el servicio web cuando la aplicación se implementa con un servidor de informes configurado para utilizar una extensión de autenticación personalizada.  
  
 ![Flujo de autenticación de seguridad de servicios de Reporting](../../../reporting-services/extensions/security-extension/media/rosettasecurityextensionauthenticationflow.gif "flujo de autenticación de seguridad de Reporting Services")  
  
 Como se muestra en la figura 2, el proceso de autenticación es el siguiente:  
  
1.  Una aplicación cliente llama al método <xref:ReportService2010.ReportingService2010.LogonUser%2A> del servicio web para autenticar a un usuario.  
  
2.  El servicio Web realiza una llamada a la <xref:ReportService2010.ReportingService2010.LogonUser%2A> método de la extensión de seguridad, en concreto, la clase que implementa **IAuthenticationExtension2**.  
  
3.  La implementación de <xref:ReportService2010.ReportingService2010.LogonUser%2A> valida el nombre de usuario y la contraseña en el almacén del usuario o la entidad de seguridad.  
  
4.  Tras una autenticación correcta, el servicio web crea una cookie y la administra para la sesión.  
  
5.  El servicio web devuelve el vale de autenticación a la aplicación que realiza la llamada en el encabezado HTTP.  
  
 Cuando el servicio web autentica correctamente a un usuario a través de la extensión de seguridad, genera una cookie que se utiliza para las solicitudes subsiguientes. La cookie puede no conservarse dentro de la entidad de seguridad personalizada porque el servidor de informes no posea la entidad de seguridad. El método del servicio web <xref:ReportService2010.ReportingService2010.LogonUser%2A> devuelve la cookie y se utiliza en las siguientes llamadas al método de servicio web y en el acceso URL.  
  
> [!NOTE]  
>  Para evitar poner en peligro la cookie durante la transmisión, las cookies de autenticación que devuelve <xref:ReportService2010.ReportingService2010.LogonUser%2A> se deberían transmitir protegidas utilizando el cifrado de Capa de sockets seguros (SSL).  
  
 Si tiene acceso al servidor de informes a través del acceso URL cuando se instala una extensión de seguridad personalizada, Internet Information Services (IIS) y [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] administran automáticamente la transmisión del vale de autenticación. Si va a tener acceso al servidor de informes a través de la API SOAP, la implementación de la clase de proxy debe incluir compatibilidad adicional para administrar el vale de autenticación. Para obtener más información sobre cómo utilizar la API SOAP y administrar el vale de autenticación, vea "Usar el servicio web con seguridad personalizada".  
  
## <a name="forms-authentication"></a>Autenticación de formularios  
 La autenticación de formularios es un tipo de autenticación de [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] en la que un usuario no autenticado se dirige a un formulario HTML. Cuando el usuario proporciona las credenciales, el sistema emite una cookie que contiene un vale de autenticación. En las solicitudes posteriores, el sistema comprueba primero la cookie para ver si el servidor de informes autenticó ya al usuario.  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] se puede extender para admitir la autenticación de formularios utilizando las interfaces de extensibilidad de seguridad disponibles a través de la API de Reporting Services. Si extiende [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] para utilizar la autenticación de formularios, utilice Capa de sockets seguros (SSL) para todas las comunicaciones con el servidor de informes, con el fin de evitar que los usuarios malintencionados obtengan acceso a la cookie de otro usuario. SSL permite que los clientes y un servidor de informes se autentiquen entre sí y asegurarse de que ningún otro equipo pueda leer el contenido de las comunicaciones entre los dos equipos. Todos los datos enviados desde un cliente a través de una conexión SSL se cifran para que los usuarios malintencionados no puedan interceptar las contraseñas o los datos que se envían a un servidor de informes.  
  
 La autenticación de formularios se implementa generalmente para admitir cuentas y la autenticación para plataformas distintas de Windows. Cuando un usuario solicita acceso a un servidor de informes, se presenta una interfaz gráfica y las credenciales proporcionadas se envían a una entidad de seguridad para la autenticación.  
  
 La autenticación de formularios requiere que una persona esté presente para escribir las credenciales. En las aplicaciones desatendidas que se comunican directamente con el servicio web de Reporting Services, la autenticación de formularios se debe combinar con un esquema de autenticación personalizada.  
  
 La autenticación de formularios es adecuada para [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] cuando:  
  
-   Necesita almacenar y autenticar a los usuarios que no tienen cuentas de Windows de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] y  
  
-   Necesita proporcionar su propio formulario de interfaz de usuario como una página de inicio de sesión entre las diferentes páginas de un sitio web.  
  
 Considere lo siguiente al escribir una extensión de seguridad personalizada que admita la autenticación de formularios:  
  
-   Si utiliza la autenticación de formularios, el acceso anónimo debe habilitarse en el directorio virtual del servidor de informes en Internet Information Services (IIS).  
  
-   La autenticación de [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] debe establecerse en la autenticación de formularios. La autenticación de [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] se configura en el archivo Web.config para el servidor de informes.  
  
-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] puede autenticar y autorizar a los usuarios con la autenticación de Windows o la autenticación personalizada, pero no con ambos. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] no admite el uso simultáneo de varias extensiones de seguridad.  
  
## <a name="see-also"></a>Vea también  
 [Implementación de una extensión de seguridad](../../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)  
  
  
