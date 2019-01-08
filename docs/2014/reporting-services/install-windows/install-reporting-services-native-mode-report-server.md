---
title: Instalar el servidor de informes de modo nativo de servicios de informes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- default configuration [Reporting Services]
- report servers [Reporting Services], default configurations
- installation options [Reporting Services]
ms.assetid: 8f25e6dc-b753-400e-9e9a-50f4f35bf6c4
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 39f3b68f816594d275f48723865c7497f5352fbb
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52527708"
---
# <a name="install-reporting-services-native-mode-report-server"></a>Instalar el servidor de informes en modo nativo de Reporting Services
  Un servidor de informes en modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se puede instalar desde el Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o desde la línea de comandos. En el Asistente para la instalación, puede seleccionar 1) instalar archivos y configurar el servidor con los valores predeterminados o 1) instalar solo los archivos y el Asistente para la instalación no configura el servidor. En este tema se examina la *configuración predeterminada para el modo nativo* donde el programa de instalación instala y configura una instancia del servidor de informes. Cuando finalice el programa de instalación, el servidor de informes estará en ejecución y listo para ser utilizado. Un servidor de informes en modo nativo se ejecuta como servidor de aplicaciones independiente. El modo nativo es el modo de servidor predeterminado.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] |  
  
##  <a name="bkmk_top"></a> En este tema  
  
-   [¿Qué es la configuración predeterminada?](#bkmk_whatisdefaultconfiguration)  
  
-   [Cuándo se debe instalar la configuración predeterminada para el modo nativo](#bkmk_whentoinstalldefaultconfig)  
  
-   [Requisitos](#bkmk_requirements)  
  
-   [Reservas de dirección URL predeterminada](#bkmk_defaultURLreservations)  
  
-   [Instalar el modo nativo mediante el Asistente para la instalación de SQL Server](#bkmk_installwithwizard)  
  
-   [Instalar el modo nativo mediante la línea de comandos](#bkmk_commandline)  
  
##  <a name="bkmk_whatisdefaultconfiguration"></a> ¿Qué es la configuración predeterminada?  
 El programa de instalación instala las siguientes características de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] al seleccionar la configuración predeterminada para la opción en modo nativo:  
  
-   El Servicio del servidor de informes (que incluye el servicio web del servidor de informes, la aplicación de procesamiento en segundo plano y el Administrador de informes)  
  
-   El Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   Las utilidades de línea de comandos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (rsconfig.exe, rskeymgmt.exe y rs.exe)  
  
 Esta opción no se aplica a las características compartidas como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], que se deben especificar como elementos independientes si desea instalarlos.  
  
 El programa de instalación configura lo siguiente en una instalación del servidor de informes en modo nativo:  
  
-   La cuenta de servicio del servicio web del servidor de informes.  
  
-   Dirección URL del servicio web del servidor de informes.  
  
-   La dirección URL del Administrador de informes.  
  
-   La base de datos del servidor de informes.  
  
-   Acceso de la cuenta del servicio a las bases de datos del servidor de informes.  
  
-   Conexión DSN para las bases de datos del servidor de informes.  
  
 El programa de instalación no configura la cuenta de ejecución desatendida, el correo electrónico del servidor de informes, la copia de seguridad de las claves de cifrado ni una implementación escalada. Puede usar el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para configurar estas propiedades. Para obtener más información, vea [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
##  <a name="bkmk_whentoinstalldefaultconfig"></a> Cuándo se debe instalar la configuración predeterminada para el modo nativo  
 Una configuración predeterminada instala [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en un estado operativo para que se pueda utilizar el servidor de informes inmediatamente una vez finalizada la instalación. Especifique este modo si desea ahorrar pasos eliminando las tareas de configuración necesarias que de otro modo tendría que realizar en la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Instalar la configuración predeterminada no garantiza que el servidor de informes vaya a funcionar una vez finalizada la instalación. Las direcciones URL predeterminadas podrían no registrarse cuando el servicio se inicie. Siempre pruebe la instalación para comprobar que el servicio se inicia y se ejecuta como debería.  
  
##  <a name="bkmk_requirements"></a> Requisitos  
 La opción de configuración predeterminada usa los valores predeterminados con el fin de establecer la configuración básica necesaria para hacer que un servidor de informes esté operativo. Tiene los requisitos siguientes:  
  
-   El hardware debe cumplir los requisitos mínimos de hardware y software para ejecutar Microsoft SQL Server. Para obtener más información, vea [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] se deben instalar juntos en la misma instancia. La instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] hospeda la base de datos del servidor de informes que el programa de instalación crea y configura.  
  
-   La cuenta de usuario utilizada para ejecutar el programa de instalación debe ser miembro del grupo local de administradores y tener permiso para obtener acceso y crear las bases de datos en la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] que hospeda las bases de datos del servidor de informes.  
  
-   El programa de instalación debe poder utilizar los valores predeterminados para reservar las direcciones URL que proporcionan acceso al servidor de informes y al Administrador de informes. Estos valores son el puerto 80, un carácter comodín seguro y los nombres de directorios virtuales con el formato **ReportServer_\<***nombre_instancia***>** y **Reports_\<***nombre_instancia***>**.  
  
-   El programa de instalación debe poder utilizar los valores predeterminados para crear las bases de datos del servidor de informes. Estos valores son **ReportServer** y **ReportServerTempDB**. Si tiene bases de datos de una instalación anterior, el programa de instalación se bloqueará porque no puede configurar el servidor de informes en la configuración predeterminada del modo nativo. Debe cambiar el nombre, mover o eliminar las bases de datos para desbloquear la instalación.  
  
 Si el equipo no cumple todos los requisitos para una instalación predeterminada, debe instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en el modo de solo archivos y, a continuación, usar el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para configurarlo una vez finalizada la instalación.  
  
 No intente reconfigurar el equipo solo para permitir que continúe una instalación predeterminada. Si lo hace, podrían necesitarse varias horas de trabajo, lo que elimina en efecto el ahorro de tiempo que la opción de instalación proporciona. La solución mejor es instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en el modo de solo archivos y, a continuación, configurar el servidor de informes para utilizar valores concretos.  
  
##  <a name="bkmk_defaultURLreservations"></a> Reservas de dirección URL predeterminada  
 Las reservas de direcciones URL están compuestas de un prefijo, un nombre de host, un puerto y un directorio virtual:  
  
|Parte|Descripción|  
|----------|-----------------|  
|Prefijo|El prefijo predeterminado es HTTP. Si instaló anteriormente un certificado de Capa de sockets seguros (SSL), el programa de instalación intentará crear reservas de direcciones URL que usen el prefijo HTTPS.|  
|Nombre de host|El nombre de host predeterminado es un carácter comodín (+) seguro. Especifica que el servidor de informes aceptará cualquier solicitud HTTP en el puerto designado para cualquier nombre de host que se resuelve en el equipo, incluidos http://\<nombreDeEquipo > / reportserver, http://localhost/reportserver, o http://\<direcciónIP > / ReportServer.|  
|Puerto|El puerto predeterminado es 80. Tenga en cuenta que si utiliza cualquier puerto distinto del 80, tendrá que agregarlo explícitamente a la dirección URL cuando abra una aplicación web de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en una ventana del explorador.|  
|Directorio virtual|De forma predeterminada, los directorios virtuales se crean en el formato de ReportServer_\<*instance_name*> para el servicio Web del servidor de informes y Reports_\<*instance_name*> Administrador de informes. Para el servicio web del servidor de informes, el nombre del directorio virtual predeterminado es **reportserver**. Para el Administrador de informes, el directorio virtual predeterminado es **reports**.|  
  
 Un ejemplo de cadena de dirección URL completa podría ser el siguiente:  
  
-   http://+:80/reportserver, proporciona acceso al servidor de informes.  
  
-   http://+:80/reports, proporciona acceso al administrador de informes.  
  
##  <a name="bkmk_installwithwizard"></a> Instalar el modo nativo mediante el Asistente para la instalación de SQL Server  
 En la lista siguiente se describen los pasos y las opciones específicos de  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que se seleccionan en el Asistente para la instalación de SQL Server. En la lista no se describe cada página que aparece en el asistente para la instalación, solo las páginas relacionadas con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que forman parte de una instalación de modo nativo.  
  
1.  En la página **Rol de instalación** , seleccione **Instalación de características de SQL Server**.  
  
     ![Instalación de la característica de SQL Server para el rol de instalación](../../../2014/sql-server/install/media/rs-setuprole.gif "Instalación de la característica de SQL Server para el rol de instalación")  
  
2.  En la página **Selección de características** , seleccione lo siguiente:  
  
    -   **Servicios de Motor de base de datos**, a menos que ya esté instalada anteriormente una instancia del motor de base de datos.  
  
    -   **Reporting Services: nativo**.  
  
    -   **Herramientas de administración - básica**. Las herramientas de administración no se requieren pero se recomiendan a menos que tenga otra instalación de herramientas de administración. La opción de configuración predeterminado dará como resultado un servidor de informes funciona, pero es posible que desee cambiar las opciones de configuración en una fecha posterior. Algunas opciones, como "Mis informes" se administran a través de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]  
  
     ![Selección del modo nativo de SSRS en Selección de características](../../../2014/sql-server/install/media/rs-setupfeatureselection-native-withcircles.gif "Selección del modo nativo de SSRS en Selección de características")  
  
3.  Si piensa usar la característica de suscripción de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , en la página **Configuración del servidor** , compruebe que Agente SQL Server está configurado para el tipo de inicio **Automático** .  
  
4.  En la página **Configuración de Reporting Services** , seleccione **Instalar y configurar**.  
  
     ![Configuración del modo nativo de SSRS](../../../2014/sql-server/install/media/rs-setupconfiguration-native-with-circles.gif "Configuración del modo nativo de SSRS")  
  
5.  Una vez completado el asistente para la instalación de SQL Server, compruebe la instalación de modo nativo predeterminada con los siguientes pasos básicos.  
  
    -   Abra el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y confirme que se puede conectar con el servidor de informes.  
  
    -   Abra el explorador con privilegios de administrador y conéctese al Administrador de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , por ejemplo `http://loclahost/Reports`.  
  
    -   Abra el explorador con privilegios de administrador y conéctese a la página del servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Por ejemplo,  `http://loclahost/ReportServer`  
  
 Para obtener más información, consulte la sección Nativo de los dos temas siguientes:  
  
 [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)  
  
 [Solución de problemas en una instalación de Reporting Services](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)  
  
##  <a name="bkmk_commandline"></a> Instalar el modo nativo mediante la línea de comandos  
 El ejemplo siguiente incluye el Servicio [!INCLUDE[ssDE](../../includes/ssde-md.md)] porque se requiere para una configuración predeterminada.  
  
```  
setup /q /ACTION=install /FEATURES=SQL,RS,TOOLS /INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS"   
/RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /SQLSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /AGTSVCACCOUNT="NT AUTHORITY\NETWORK   
SERVICE" /RSSVCSTARTUPTYPE="Manual" /RSINSTALLMODE="DefaultNativeMode"  
```  
  
 Para obtener más información y ejemplos, vea [símbolo instalación de Reporting Services SharePoint Mode y modo nativo](../../reporting-services/install-windows/install-reporting-services-at-the-command-prompt.md) y [instalar SQL Server 2014 desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)  
  
## <a name="see-also"></a>Vea también  
 [Solucionar problemas en una instalación de Reporting Services](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)   
 [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
 [Configurar la cuenta de servicio del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Configurar las direcciones URL del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configurar una conexión a la base de datos del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Instalación de solo archivos &#40;Reporting Services&#41;](../../reporting-services/install-windows/files-only-installation-reporting-services.md)   
 [Inicializar un servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [Configurar conexiones SSL en un servidor de informes en modo nativo](../security/configure-ssl-connections-on-a-native-mode-report-server.md)   
 [Configurar las direcciones URL del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configurar los permisos y las cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [Inicio rápido de instalación de SQL Server 2014](../../../2014/getting-started/quick-start-installation-of-sql-server-2014.md)  
  
  
