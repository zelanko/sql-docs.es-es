---
title: Autenticación con el servidor de informes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- connections [Reporting Services], configuring
- connections [Reporting Services], accounts
- Windows authentication [Reporting Services]
- authentication [Reporting Services]
- Forms authentication
ms.assetid: 753c2542-0e97-4d8f-a5dd-4b07a5cd10ab
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: decf2cbed48af0dcc00867a5f4d68b5d7c8958de
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66102187"
---
# <a name="authentication-with-the-report-server"></a>Autenticación con el servidor de informes
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRs) proporciona varias opciones configurables para autenticar usuarios y aplicaciones cliente en el servidor de informes. De forma predeterminada, el servidor de informes usa la autenticación de Windows integrada y supone que existen relaciones de confianza donde el cliente y los recursos de red están en el mismo dominio o en un dominio de confianza. En función de la topología de red y las necesidades de su organización, puede personalizar el protocolo de autenticación que se usa para la autenticación integrada de Windows, usar la autenticación básica o usar una extensión personalizada basada en formularios de autenticación que proporcione. Cada uno de los tipos de autenticación puede activarse o desactivarse individualmente. Puede habilitar más de un tipo de autenticación si desea que el servidor de informes acepte solicitudes de varios tipos.  
  
> [!NOTE]  
>  IIS proporcionaba toda la compatibilidad con la autenticación en las versiones anteriores de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. IIS no se usa a partir de la versión [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] . 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] controla todas las solicitudes de autenticación internamente.  
  
 Todos los usuarios o aplicaciones que soliciten acceso al contenido y las operaciones del servidor de informes deben autenticarse para que se permita el acceso.  
  
## <a name="authentication-types"></a>Tipos de autenticación  
 Todos los usuarios o aplicaciones que soliciten el acceso al contenido y las operaciones del servidor de informes deben autenticarse mediante el tipo de autenticación configurado en el servidor de informes para que se permita el acceso. En la tabla siguiente se describen los tipos de autenticación que admite [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
|Nombre del tipo de autenticación|Valor del nivel de autenticación HTTP|Se usa de forma predeterminada|Descripción|  
|-----------------------------|-------------------------------------|---------------------|-----------------|  
|RSWindowsNegotiate|Negotiate|Sí|Intenta usar primero la autenticación integrada Kerberos para Windows, pero vuelve a NTLM si Active Directory no puede conceder un vale para la solicitud de cliente al servidor de informes. Negotiate solamente volverá a NTLM si el vale no está disponible. Si el primer intento provoca un error en lugar de indicar que no se encuentra un vale, el servidor de informes no hace un segundo intento.|  
|RSWindowsNTLM|NTLM|Sí|Usa la autenticación integrada NTLM para Windows.<br /><br /> Las credenciales no se delegarán ni suplantarán en otras solicitudes. Las solicitudes subsiguientes seguirán una nueva secuencia de desafío-respuesta. Según la configuración de seguridad de la red, podría pedirse a un usuario las credenciales o la solicitud de autenticación se administrará de forma transparente.|  
|RSWindowsKerberos|Kerberos|No|Usa la autenticación integrada Kerberos para Windows. Para configurar Kerberos, debe colocar los nombres principales del servicio del servidor (SPN) para las cuentas de servicio, lo que requiere privilegios de administrador de dominio. Si configura la delegación de identidad con Kerberos, el token del usuario que solicita un informe también se puede usar en una conexión adicional a los orígenes de datos externos que proporcionan datos a los informes.<br /><br /> Antes de especificar RSWindowsKerberos, asegúrese de que el tipo de explorador que usa lo admite realmente. Si utiliza Internet Explorer, la autenticación Kerberos solo se admite a través de Negotiate. Internet Explorer no formulará ninguna solicitud de autenticación que especifique Kerberos directamente.|  
|RSWindowsBasic|Básica|No|La autenticación básica se define en el protocolo HTTP y solo se puede usar para autenticar las solicitudes HTTP para el servidor de informes.<br /><br /> Las credenciales se pasan en la solicitud HTTP en la codificación Base64. Si usa la autenticación básica, utilice el Nivel de sockets seguros (SSL) para cifrar la información de la cuenta de usuario antes de enviarse a través de la red. SSL proporciona un canal cifrado para enviar una solicitud de conexión del cliente al servidor de informes a través de una conexión HTTP TCP/IP. Para obtener más información, vea el tema relativo al [uso de SSL para cifrar datos confidenciales](https://go.microsoft.com/fwlink/?LinkId=71123) en el sitio web de [!INCLUDE[msCoName](../../includes/msconame-md.md)] TechNet.|  
|Personalizado|(Anónima)|No|La autenticación anónima indica al servidor de informes que omita el encabezado de autenticación de una solicitud HTTP. El servidor de informes acepta todas las solicitudes, pero llama a una autenticación de formularios [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] Forms personalizada que el usuario proporciona para autenticar al usuario.<br /><br /> Especifique `Custom` únicamente si está implementando un módulo de autenticación personalizada que administra todas las solicitudes de autenticación en el servidor de informes. No puede utilizar el tipo de autenticación Custom con la extensión de la autenticación de Windows predeterminada.|  
  
## <a name="unsupported-authentication-methods"></a>Métodos de autenticación no admitidos  
 No se admiten los métodos de autenticación y solicitudes siguientes.  
  
|Método de autenticación|Explicación|  
|---------------------------|-----------------|  
|Anónimas|El servidor de informes no aceptará las solicitudes no autenticadas de un usuario anónimo, salvo en las implementaciones que incluyan una extensión de autenticación personalizada.<br /><br /> El Generador de informes aceptará las solicitudes sin autenticar si habilita el acceso del mismo en un servidor de informes que esté configurado para la autenticación básica.<br /><br /> En todos los demás casos, las solicitudes anónimas se rechazan y se genera un error de acceso denegado de estado 401 de HTTP antes de que la solicitud llegue a [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]. Los clientes que reciben este error deben volver a formular la solicitud con un tipo de autenticación válido.|  
|Tecnologías de inicio de sesión único (SSO)|No hay ninguna compatibilidad nativa para las tecnologías de inicio de sesión único en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Si desea utilizar una tecnología de inicio de sesión único, debe crear una extensión de autenticación personalizada.<br /><br /> El entorno host del servidor de informes no admite los filtros ISAPI. Si la tecnología SSO que usa se implementa como un filtro ISAPI, considere usar la compatibilidad integrada de ISA Server para el protocolo RADIUS o RSASecueID. De lo contrario, puede crear un ISAPI de ISA Server o un HTTPModule para RS, pero se recomienda usar ISA Server directamente.|  
|Passport|No se admite en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|Implícita|No se admite en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
## <a name="configuration-of-authentication-settings"></a>Configuración de los valores de autenticación  
 La configuración de la autenticación se establece para la seguridad predeterminada cuando la dirección URL del servidor de informes está reservada. Si modifica estos valores incorrectamente, el servidor de informes devolverá errores de acceso denegado HTTP 401 para las solicitudes HTTP que no se puedan autenticar. La elección de un tipo de autenticación requiere saber si la autenticación de Windows se admite en la red. Se debe especificar al menos un tipo de autenticación. Se pueden especificar varios tipos de autenticación para RSWindows. Los tipos de autenticación de RSWindows ( `RSWindowsBasic`es `RSWindowsNTLM`decir `RSWindowsKerberos`,,, y **RSWindowsNegotiate**) se excluyen mutuamente con Custom.  
  
> [!IMPORTANT]  
>  Reporting Services no valida la configuración que se especifique para determinar si es correcta en un entorno informático. Es posible que la seguridad predeterminada no funcione en una instalación o que se especifique una configuración que no sea válida en una infraestructura de seguridad. Por esta razón, es importante que pruebe cuidadosamente la implementación del servidor de informes en un entorno de pruebas controlado antes de hacer que esté disponible en una organización mayor.  
  
 El servicio web del servidor de informes y el Administrador de informes siempre utilizan el mismo tipo de autenticación. No puede configurar tipos de autenticación diferentes para las áreas de características del servicio del servidor de informes. Si tiene una implementación escalada, asegúrese de duplicar todos los cambios en todos los nodos de la implementación. No puede configurar nodos diferentes en la misma implementación escalada para utilizar tipos de autenticación diferentes.  
  
 El procesamiento en segundo plano no acepta solicitudes de los usuarios finales, aunque autentica todas las solicitudes para la ejecución desatendida. Siempre usa la autenticación de Windows y autentica las solicitudes mediante el servicio del servidor de informes o la cuenta de ejecución desatendida si está configurada.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Configurar la autenticación de Windows en el servidor de informes](configure-windows-authentication-on-the-report-server.md)  
  
-   [Configuración de la autenticación básica en el servidor de informes](configure-basic-authentication-on-the-report-server.md)  
  
-   [Configuración de la autenticación de formularios o personalizada en el servidor de informes](configure-custom-or-forms-authentication-on-the-report-server.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripciones de las tareas|Vínculos|  
|-----------------------|-----------|  
|Configurar el tipo de autenticación integrada de Windows.|[Configurar la autenticación de Windows en el servidor de informes](configure-windows-authentication-on-the-report-server.md)|  
|Configurar el tipo de autenticación básica.|[Configuración de la autenticación básica en el servidor de informes](configure-basic-authentication-on-the-report-server.md)|  
|Configurar la autenticación de formularios o, de lo contrario, un tipo de autenticación personalizada.|[Configuración de la autenticación de formularios o personalizada en el servidor de informes](configure-custom-or-forms-authentication-on-the-report-server.md)|  
|Permitir al administrador de informes controlar el escenario de autenticación personalizada.|[Configurar el Administrador de informes para pasar cookies de autenticación personalizadas](configure-the-web-portal-to-pass-custom-authentication-cookies.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Conceder permisos en un servidor de informes en modo nativo](granting-permissions-on-a-native-mode-report-server.md)   
 [Archivo de configuración RSReportServer](../report-server/rsreportserver-config-configuration-file.md)   
 (create-and-manage-role-assignments.md)   
 [Especificar información de credenciales y conexión para los orígenes de datos de informes](../report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
 [Implementar una extensión de seguridad](../extensions/security-extension/implementing-a-security-extension.md)   
 [Configurar conexiones SSL en un servidor de informes en modo nativo](configure-ssl-connections-on-a-native-mode-report-server.md)   
 [Configurar el acceso a Generador de informes](../report-server/configure-report-builder-access.md)   
 [Información general de extensiones de seguridad](../extensions/security-extension/security-extensions-overview.md)   
 [Autenticación en Reporting Services](../extensions/security-extension/authentication-in-reporting-services.md)   
 [La autorización en Reporting Services](../extensions/security-extension/authorization-in-reporting-services.md)  
  
  
