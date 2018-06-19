---
title: Configurar las direcciones URL del servidor de informes (Administrador de configuración de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Report Server Windows service, virtual directories
- report servers [Reporting Services], virtual directories
- virtual directories [Reporting Services]
ms.assetid: a0134ef0-086c-443e-93b9-7213a3d76393
caps.latest.revision: 10
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 9d49d5cae66834cd9cfd304198fc4f677020fe75
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35322324"
---
# <a name="configure-report-server-urls--ssrs-configuration-manager"></a>Configurar las direcciones URL del servidor de informes (Administrador de configuración de SSRS)
  En [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], las direcciones URL se usan para obtener acceso al servicio web del servidor de informes y al [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]. Para poder usar cualquier aplicación, debe configurar al menos una dirección URL para el servicio web y otra para el [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] indica valores predeterminados para ambas direcciones URL de la aplicación que mejor funcionan en la mayoría de los escenarios de implementación, incluso en las implementaciones en paralelo con otros servicios web y aplicaciones.  
  
-   Si instaló la configuración predeterminada, las direcciones URL se crearon utilizando automáticamente los valores predeterminados.  
  
-   Si usa la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para crear o modificar las direcciones URL, puede aceptar los valores predeterminados para una dirección URL o especificar valores personalizados. Cuando se define la dirección URL, en la página aparece un vínculo de prueba de la misma, para que se pueda confirmar inmediatamente que los valores que se especificaron producen una conexión válida. Para obtener instrucciones paso a paso sobre cómo configurar y probar una dirección URL, vea [Configurar una dirección URL &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md).  
  
## <a name="defining-a-report-server-url"></a>Definir una dirección URL del servidor de informes  
 La dirección URL identifica con precisión la ubicación de una instancia de una aplicación del servidor de informes en la red. Al crear una dirección URL del servidor de informes, debe especificar las partes siguientes.  
  
|Parte|Descripción|  
|----------|-----------------|  
|Nombre de host|Una red TCP/IP utiliza una dirección IP para identificar de forma única un dispositivo en la red. Hay una dirección IP física para cada tarjeta adaptadora de red que esté instalada en un equipo. Si la dirección IP se resuelve como un encabezado de host, puede especificar el encabezado de host. Si está implementando el servidor de informes en una red corporativa, puede utilizar el nombre de red del equipo.|  
|Puerto|Un puerto TCP es un extremo en el dispositivo. El servidor de informes escuchará las solicitudes en un puerto designado.|  
|Directorio virtual|Varios servicios web o aplicaciones a menudo comparten un puerto. Por esta razón, la dirección URL de un servidor de informes siempre incluye un directorio virtual que corresponde a la aplicación que obtiene la solicitud. Debe especificar nombres de directorio virtual únicos para cada aplicación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que escuche en la misma dirección IP y puerto.|  
|Configuración SSL|Las direcciones URL en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se pueden configurar para utilizar un certificado SSL existente que se instalara anteriormente en el equipo. Para obtener más información, vea [Configurar conexiones SSL en un servidor de informes en modo nativo](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md) en Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
  
## <a name="default-urls"></a>Direcciones URL predeterminadas  
 Al obtener acceso a un servidor de informes o al [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] a través de su dirección URL, esta debería incluir el nombre de host y no la dirección IP. En una red TCP/IP, la dirección IP se resolverá como un nombre de host (o el nombre de red del equipo). Si usó los valores predeterminados para configurar las direcciones URL, debería poder tener acceso al servicio web del servidor de informes mediante direcciones URL que especifiquen el nombre de equipo u host local como el nombre de host:  
  
-   `http://<computername>/reportserver`  
  
-   `http://localhost/reportserver`  
  
 La configuración que hace que estas direcciones URL estén disponibles aparece en la tabla siguiente. En esta tabla se muestran los valores predeterminados que habilitan una conexión del servidor de informes a través de direcciones URL que incluyan un nombre de host:  
  
|Parte|Valor|Explicación|  
|----------|-----------|-----------------|  
|Dirección IP|Todas asignadas|El servicio de nombres de dominio de la red resuelve el nombre de host de la dirección URL como la dirección IP del equipo. Siempre que la dirección IP se especifique en la dirección URL que defina, una solicitud que se envíe a un host concreto alcanzará su destino pretendido.|  
|Puerto|80|El puerto 80 es el predeterminado para las conexiones TCP/IP en un equipo. Dado que el servidor de informes escucha en el puerto 80, puede omitir el número de puerto de la dirección URL. Si especifica otro puerto, debe especificarlo en la dirección URL.|  
|Directorio virtual|ReportServer|Observe que las dos direcciones URL del ejemplo incluyen el nombre del directorio virtual. A menos que personalice la definición de dirección URL, siempre debe especificar en la dirección URL el nombre del directorio virtual de la aplicación.|  
  
> [!NOTE]  
>  Una reserva de direcciones URL subyacente permite que se use cualquier nombre de host válido en una dirección  URL. La herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] crea una reserva de direcciones URL en HTTP.SYS utilizando la sintaxis que permite que las variaciones del nombre de host se resuelvan en una instancia del servidor de informes determinada. Para obtener más información sobre las reservas de direcciones URL, vea [Acerca de las reservas y el registro de direcciones URL &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md).  
  
## <a name="server-side-permissions-on-a-report-server-url"></a>Permisos del lado servidor en una dirección URL del servidor de informes  
 Los permisos de cada extremo de la dirección URL se conceden exclusivamente a la cuenta de servicio del servidor de informes. Solo esta cuenta tiene derechos para aceptar las solicitudes que se dirigen a la dirección URL de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Las listas de control de acceso discrecional (DACL, Discretionary Access Control List) se crean y mantienen para la cuenta cuando se configura la identidad del servicio a través del programa de instalación o de la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Si cambia la cuenta de servicio, la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] actualizará todas las reservas de direcciones URL que creó para recopilar información de las cuentas nuevas. Para obtener más información, vea [Sintaxis de reserva de direcciones URL &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md).  
  
## <a name="authenticating-client-requests-sent-to-a-report-server-url"></a>Autenticar las solicitudes de cliente que se envían a la dirección URL de un servidor de informes  
 De forma predeterminada, el tipo de autenticación que se admite en los extremos de una dirección URL es la de Windows. Ésta es la extensión de seguridad predeterminada. Si está implementando un proveedor de autenticación de formularios o personalizado, debe modificar la configuración de la autenticación en el servidor de informes. Si lo desea, también puede cambiar la configuración de la autenticación de Windows para que coincida con el subsistema de autenticación que se use en la red. Para obtener más información, vea [Autenticación con el servidor de informes](../../reporting-services/security/authentication-with-the-report-server.md) en Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="in-this-section"></a>En esta sección  
 [Configurar una dirección URL &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
 En este tema se proporcionan instrucciones para establecer y modificar una reserva de direcciones URL en la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 [Acerca de las reservas y el registro de direcciones URL &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md)  
 Las direcciones URL se utilizan para tener acceso a las aplicaciones e informes. En este tema se explican las direcciones URL de las aplicaciones, las direcciones URL predeterminadas y cómo funcionan las reservas de direcciones URL y el registro en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Sintaxis de reserva de direcciones URL &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md)  
 Las reservas de direcciones URL predeterminadas que usa [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] son válidas para la mayoría de los escenarios. Sin embargo, si desea restringir el acceso o extender la implementación para habilitar el acceso a Internet o a una extranet, es posible que tenga que personalizar la configuración para que cumpla sus requisitos. En este tema se describe la sintaxis de una reserva de direcciones URL y se proporcionan recomendaciones para crear reservas personalizadas para una implementación.  
  
 [Direcciones URL en archivos de configuración &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)  
 El archivo RSReportServer.config contiene varias entradas para las reservas de direcciones URL y las direcciones URL que se usan en el [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] y en la distribución del correo electrónico del servidor de informes. En este tema se resume la configuración de las direcciones URL que permite comprender cómo se comparan.  
  
 [Reservas de direcciones URL para implementaciones del servidor de informes de varias instancias &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/url-reservations-for-multi-instance-report-server-deployments.md)  
 Al instalar varias instancias de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en un único equipo, aumenta la probabilidad de encontrar direcciones URL duplicadas al registrar una dirección URL. Para evitar estos errores, siga las recomendaciones de este tema para crear reservas de direcciones URL específicas de una instancia.  
  
## <a name="see-also"></a>Ver también  
 [Configurar una dirección URL &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) 
