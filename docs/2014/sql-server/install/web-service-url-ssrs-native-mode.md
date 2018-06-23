---
title: Dirección URL del servicio (modo nativo de SSRS) Web | Documentos de Microsoft
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL12.rsconfigtool.reportservervirtualdirectory.F1
helpviewer_keywords:
- Reporting Services, Web service
ms.assetid: 9d210b5d-2a08-4e56-a4f5-c16715b00d79
caps.latest.revision: 9
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 317a351878dbaf0d022ec1a170ac460fefac5985
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200465"
---
# <a name="web-service-url-ssrs-native-mode"></a>Dirección URL del servicio web (Modo nativo de SSRS)
  Utilice la página Dirección URL del servicio web para configurar o modificar la dirección URL que se usa para tener acceso al servidor de informes. Se creará una *reserva de direcciones URL* dependiendo de la dirección URL que especifique. La reserva de direcciones URL define la sintaxis y las reglas de todas las direcciones URL que se pueden utilizar posteriormente para tener acceso al servicio web del servidor de informes. Especifica el prefijo, host, puerto y directorio virtual para el servicio web del servidor de informes. Según cómo especifique el host, podría haber varias direcciones URL posibles para una única reserva. El valor predeterminado para el host especifica un carácter comodín seguro. Un carácter comodín seguro permite especificar en una dirección URL cualquier nombre de host que se pueda resolver como el equipo que hospeda el servidor de informes. Para obtener más información acerca de la configuración de dirección URL y las reservas, consulte [configurar una dirección URL &#40;Administrador de configuración de SSRS&#41; ](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) y [configurar direcciones URL de servidor de informes &#40;Administrador de configuración de SSRS&#41; ](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md).  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Para abrir esta página, inicie la [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager y haga clic en **dirección URL del servicio Web** en el panel de navegación. Para obtener más información, vea [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
 Esta página proporciona los valores que se suelen usar en las direcciones URL del servidor de informes. Si desea crear más direcciones URL, usar los encabezados de host o especificar la dirección IP en un formato determinado, haga clic en **Avanzadas**.  
  
 Un vínculo al servicio web aparecerá en esta página después de hacer clic en **Aplicar**. Si hace clic en este vínculo antes de que se cree la base de datos del servidor de informes, puede aparecer un error "Página no encontrada". Este error ya no aparecerá una vez que se configure la base de datos. Para más información, vea [Crear una base de datos del servidor de informes de modo nativo &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).  
  
 Si vuelve a instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y encontrar que se producen errores al intentar utilizar el valor de dirección IP predeterminada de todas asignadas y el puerto 80, normalmente puede resolver el error volviendo a crear la dirección URL después de reiniciar el servicio.  
  
## <a name="options"></a>Opciones  
 **Directorio virtual**  
 Especifica el nombre del directorio virtual para el servicio web del servidor de informes. Solo puede tener un nombre de directorio virtual para cada instancia del servicio web del servidor de informes del mismo equipo.  
  
 **Dirección IP**  
 Identifica el equipo del servidor de informes en una red TCP/IP. Los valores válidos incluyen:  
  
-   **Todas asignadas** especifica que cualquiera de las direcciones IP que están asignadas al equipo se puede utilizar en una dirección URL que señale a una aplicación de servidor de informes. Este valor también abarca nombres de host descriptivos (como nombres de equipo) que un servidor de nombres de dominio puede resolver en una dirección IP que se asigna al equipo. Éste es el valor predeterminado de una dirección URL de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   **Todas sin asignar** especifica que el servidor de informes aceptará cualquier solicitud que no tenga una coincidencia exacta para la dirección IP o nombre de host. No utilice este valor si otra aplicación web ya está utilizándolo. Si hace esto, interrumpirá el servicio para la otra aplicación.  
  
-   **127.0.0.1** se utilizan para tener acceso al host local. Admite la administración local en el equipo del servidor de informes. Si selecciona solo este valor, únicamente los usuarios que hayan iniciado sesión de forma local en el equipo servidor de informes tendrán acceso a la aplicación.  
  
-   *Nnn.nnn.nnn.nnn* es la dirección IPv4 de una tarjeta adaptadora de red del equipo. Si la red usa direccionamiento IPv6, la dirección IP será un valor de 128 bits de 8 campos de 4 bytes similar con el siguiente formato: \<encabezado >:*nnnn*  
  
     Si tiene varias tarjetas, verá una dirección IP para cada una. Si selecciona solo este valor, limitará el acceso de la aplicación únicamente a la dirección IP (y a cualquier nombre de host que un servidor de nombres de dominio asigne a esa dirección). No puede utilizar el host local para tener acceso a un servidor de informes y no puede utilizar las direcciones IP de otras tarjetas de adaptadores de red que estén instalados en el equipo del servidor de informes.  
  
 **Puerto TCP**  
 Especifica el puerto en el que el servidor de informes supervisa las solicitudes HTTP de las direcciones URL que incluyen el nombre de directorio virtual del servidor de informes.  
  
 **Certificado SSL**  
 Enlaza un certificado a la dirección IP que especificó. El certificado debe estar instalado y configurado en el equipo. Reporting Services no proporciona características para administrar certificados. El certificado se debe emitir para un nombre de host o un nombre de equipo que se resuelva como la dirección IP. Por ejemplo, para usar un certificado emitido para http://salesreports, la dirección IP especificada debe resolverse en un servidor denominado "salesreports".  
  
 Si usa un certificado, debe modificar el `UrlRoot` de archivos de configuración en el archivo RSReportServer.config para que especifica el nombre completo del equipo para el que se ha registrado el certificado. Para obtener más información, vea [Configurar conexiones SSL en un servidor de informes en modo nativo](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md) en Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Puerto SSL**  
 Especifica el puerto para las conexiones SSL.  
  
 **Direcciones URL**  
 Muestra las direcciones URL definidas para la instancia actual del servidor de informes.  
  
 **Avanzadas**  
 Haga clic para crear más direcciones URL para la instancia de la aplicación actual.  
  
> [!NOTE]  
>  Si tiene enlaces SSL y reservas de direcciones URL existentes y desea cambiar el enlace SSL para, por ejemplo, usar otro certificado o encabezado de host, se recomienda que complete los pasos siguientes por orden:  
>   
>  1.  Quite primero todas las reservas de direcciones URL.  
> 2.  A continuación, quite todos los enlaces SSL.  
> 3.  Después, vuelva a crear las direcciones URL y los enlaces SSL.  
>   
>  El procedimiento anterior se puede realizar mediante el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
>   
>  Microsoft Windows admite un enlace para cada combinación de dirección IP y puerto. Si configura un servidor de informes de forma que use un valor de encabezado de host específico y el certificado de la combinación de puerto-dirección IP se envía también a un valor de encabezado de host diferente, aparecerá en el explorador una advertencia en la que se indica que el certificado no coincide con la dirección URL que se está usando.  
>   
>  Para corregir el problema, elimine todos los enlaces y, a continuación, cree nuevos enlaces con una configuración única, o configure los registros de direcciones URL de Reporting Services con caracteres comodín.  
  
## <a name="see-also"></a>Vea también  
 [Temas de Ayuda de F1 de administrador de configuración de Reporting Services &#40;modo nativo de SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Configurar las direcciones URL del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  