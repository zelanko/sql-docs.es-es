---
title: Autorización en Reporting Services | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- authorization [Reporting Services]
ms.assetid: 15fc1c7b-560c-4737-b126-e0d428a1b530
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2210d5eb5997ec66e707a90cdc52dc24328e6f6f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193360"
---
# <a name="authorization-in-reporting-services"></a>La autorización en Reporting Services
  La autorización es el proceso de determinar si se debería conceder a una identidad el tipo solicitado de acceso a un recurso determinado en la base de datos del servidor de informes. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] utiliza una arquitectura de autorización basada en roles que concede a los usuarios acceso a un recurso determinado según la asignación de roles del usuario para la aplicación. Las extensiones de seguridad para [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] contienen una implementación de un componente de autorización que se utiliza para conceder acceso a los usuarios una vez autenticados en el servidor de informes. La autorización se invoca cuando un usuario intenta realizar una operación en el sistema o en un elemento del servidor de informes a través del acceso de dirección URL y la API SOAP. Esto es posible a través de la interfaz de extensión de seguridad **IAuthorizationExtension2**. Según se ha indicado previamente, todas las extensiones heredan de **IExtension** la interfaz básica de cualquier extensión que implemente. **IExtension** e **IAuthorizationExtension2** son miembros del espacio de nombres **Microsoft.ReportingServices.Interfaces**.  
  
## <a name="checking-access"></a>Comprobar el acceso  
 En la autorización, la clave de cualquier implementación de seguridad personalizada es la comprobación del acceso, que se implementa en el método <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A>. Cada vez que un usuario intenta una operación en el servidor de informes, se llama a <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A>. El método <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A> se sobrecarga para cada tipo de operación. En las operaciones de carpeta, un ejemplo de comprobación de acceso podría ser similar a la siguiente:  
  
```  
// Overload for Folder operations  
public bool CheckAccess(  
   string userName,   
   IntPtr userToken,   
   byte[] secDesc,   
   FolderOperation requiredOperation)  
{  
   // If the user is the administrator, allow unrestricted access.  
   if (userName == m_adminUserName)   
      return true;  
  
   AceCollection acl = DeserializeAcl(secDesc);  
   foreach(AceStruct ace in acl)  
   {  
         if (userName == ace.PrincipalName)  
         {  
            foreach(FolderOperation aclOperation in   
               ace.FolderOperations)  
            {  
               if (aclOperation == requiredOperation)  
                     return true;  
            }  
         }  
   }  
   return false;  
}  
```  
  
 El servidor de informes llama al método <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A> pasando el nombre del usuario que ha iniciado sesión, un token de usuario, el descriptor de seguridad para el elemento y la operación solicitada. Ahora se comprobaría si el descriptor de seguridad tiene el nombre de usuario y el permiso adecuados para completar la solicitud y, a continuación, se devolvería **true** para indicar que se concede el acceso o **false** para indicar que se deniega.  
  
## <a name="security-descriptors"></a>Descriptor de seguridad  
 Al establecer directivas de autorización en los elementos de la base de datos del servidor de informes, una aplicación cliente (como el Administrador de informes) envía información del usuario a la extensión de seguridad junto con una directiva de seguridad para el elemento. Esta directiva de seguridad e información de usuario se conocen en conjunto como un descriptor de seguridad. Un descriptor de seguridad contiene la información siguiente para un elemento de la base de datos del servidor de informes:  
  
-   El grupo o usuario que tiene algún tipo de permiso para realizar las operaciones en el elemento.  
  
-   El tipo de elemento.  
  
-   Una lista de control de acceso discrecional (DACL) que controla el acceso al elemento.  
  
 Los descriptores de seguridad se crean utilizando los métodos <xref:ReportService2010.ReportingService2010.SetPolicies%2A> y <xref:ReportService2010.ReportingService2010.SetSystemPolicies%2A> del servicio web.  
  
### <a name="authorization-flow"></a>Flujo de la autorización  
 La extensión de seguridad configurada actualmente para ejecutarse en el servidor controla la autorización de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. La autorización se basa en los roles y está limitada a los permisos y operaciones que proporciona la arquitectura de seguridad de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] . El diagrama siguiente describe el proceso para autorizar a los usuarios para operar en los elementos de la base de datos del servidor de informes:  
  
 ![Flujo de autorización de seguridad de Reporting Services](../../../reporting-services/extensions/security-extension/media/rosettasecurityextensionauthorizationflow.gif "Flujo de autorización de seguridad de Reporting Services")  
  
 Como se muestra en este diagrama, la autorización sigue esta secuencia:  
  
1.  Una vez autenticadas, las aplicaciones cliente realizan las solicitudes al servidor de informes a través de los métodos de servicio web de Reporting Services. Un vale de autenticación se pasa al servidor de informes en forma de una cookie en el encabezado HTTP de cada solicitud web.  
  
2.  La cookie se valida antes de cualquier comprobación de acceso.  
  
3.  Una vez validada la cookie, el servidor de informes llama a <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension.GetUserInfo%2A> y se proporciona una identidad al usuario.  
  
4.  El usuario intenta una operación a través del servicio web de Reporting Services.  
  
5.  El servidor de informes llama al método <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A>.  
  
6.  Se recupera el descriptor de seguridad y se pasa a una implementación de extensión de seguridad personalizada de <xref:Microsoft.ReportingServices.Interfaces.IAuthorizationExtension.CheckAccess%2A>. En este punto, el usuario, grupo o equipo se comparan con el descriptor de seguridad del elemento al que se va a tener acceso y se les autoriza a realizar la operación solicitada.  
  
7.  Si se autoriza al usuario, el servicio web realiza la operación y devuelve una respuesta a la aplicación que realiza la llamada.  
  
  
