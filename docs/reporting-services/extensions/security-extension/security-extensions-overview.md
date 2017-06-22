---
title: "Información general de las extensiones de seguridad | Documentos de Microsoft"
ms.custom: 
ms.date: 03/15/2017
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
- security [Reporting Services], extensions
ms.assetid: 24ccd795-6506-457c-93ac-6a9dd6bb9a46
caps.latest.revision: 22
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: df3ae2c8b5ccde0beffeb2f3f18d68bdb4c4a782
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="security-extensions-overview"></a>Información general de extensiones de seguridad
  Una extensión de seguridad [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] permite la autenticación y autorización de usuarios o grupos; es decir, les permite a usuarios diferentes iniciar sesión en un servidor de informes y, en función de sus identidades, realizar tareas u operaciones diferentes. De forma predeterminada, [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] utiliza una extensión de autenticación basada en Windows que utiliza los protocolos de cuenta de Windows para comprobar las identidades de los usuarios que indican que tienen cuentas en el sistema. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] utiliza un sistema de seguridad basada en roles para autorizar a los usuarios. El modelo de seguridad basado en roles [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] es similar a los modelos de seguridad basados en roles de otras tecnologías.  
  
 Dado que las extensiones de seguridad están basadas en una API abierta y extensible, puede crear nuevas extensiones de autenticación y de autorización en [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. El siguiente es un ejemplo de una implementación de extensión de seguridad típica que utiliza la autenticación y autorización basadas en formularios:  
  
 ![Proceso de extensión de seguridad de servicios de notificación](../../../reporting-services/extensions/security-extension/media/rosettasecurityextensionflow.gif "proceso de extensión de seguridad de Reporting Services")  
  
 Como se muestra en la ilustración, la autenticación y autorización se producen como sigue:  
  
1.  Un usuario intenta tener acceso al Administrador de informes utilizando una URL y se le redirige a un formulario que recopila las credenciales del usuario para la aplicación cliente.  
  
2.  El usuario envía las credenciales al formulario.  
  
3.  Las credenciales del usuario se envían al servicio web de Reporting Services a través del método <xref:ReportService2010.ReportingService2010.LogonUser%2A>.  
  
4.  El servicio web llama la extensión de seguridad proporcionada por el cliente y comprueba que el nombre de usuario y la contraseña existen en la entidad de seguridad personalizada.  
  
5.  Después de la autenticación, el servicio web crea un vale de autenticación (conocido como una "cookie"), administra el vale y comprueba el rol del usuario para la página Inicio de Administrador de informes.  
  
6.  El servicio web devuelve la cookie al explorador y muestra la interfaz de usuario adecuada en Administrador de informes.  
  
7.  Una vez autenticado el usuario, el explorador realiza las solicitudes a Administrador de informes a la vez que transmite la cookie en el encabezado HTTP. Estas solicitudes son una respuesta a las acciones del usuario dentro de la aplicación Administrador de informes.  
  
8.  La cookie se transmite en el encabezado HTTP al servicio web junto con la operación del usuario solicitada.  
  
9. La cookie se valida y si es válida, el servidor de informes devuelve el descriptor de seguridad y otra información relativa a la operación solicitada desde la base de datos del servidor de informes.  
  
10. Si la cookie es válida, el servidor de informes realiza una llamada a la extensión de seguridad para comprobar si el usuario está autorizado para realizar la operación concreta.  
  
11. Si el usuario está autorizado, el servidor de informes realiza la operación solicitada y devuelve el control al autor de las llamadas.  
  
12. Una vez autenticado el usuario, el acceso URL al servidor de informes utiliza la misma cookie. La cookie se transmite en el encabezado HTTP.  
  
13. El usuario continúa solicitando las operaciones en el servidor de informes hasta que la sesión haya finalizado.  
  
## <a name="when-to-implement-a-security-extension"></a>Cuándo implementar una extensión de seguridad  
 Recomendamos que, siempre que sea posible, se utilice la autenticación de Windows. Sin embargo, la autenticación personalizada y autorización para [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] pueden ser adecuadas en los dos casos siguientes:  
  
-   Tiene una aplicación de Internet o de extranet que no puede utilizar las cuentas de Windows.  
  
-   Tiene usuarios y roles personalizados y necesita proporcionar un esquema de autorización correspondiente en [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Implementar una extensión de seguridad](../../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)   
 [Configurar el Administrador de informes para pasar Cookies de autenticación personalizada](https://msdn.microsoft.com/library/ms345241(v=sql.110).aspx)  
  
  
