---
description: Solución de problemas en una instalación de Reporting Services
title: Solución de problemas en una instalación de Reporting Services | Microsoft Docs
ms.date: 01/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.assetid: e2536f7f-d90c-4571-9ffd-6bbfe69018d6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1cc420302bb8d1610adcc1848fda226c4c55b492
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472476"
---
# <a name="troubleshoot-a-reporting-services-installation"></a>Solución de problemas en una instalación de Reporting Services

  Si no puede instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] debido a los errores que se producen durante la instalación, siga las instrucciones de este artículo para abordar las condiciones que probablemente ocasionen esos errores.  
  
 Para obtener información sobre otros errores y problemas relacionados con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] vea [Troubleshoot SSRS issues and errors.](https://social.technet.microsoft.com/wiki/contents/articles/ssrs-troubleshooting-issues-and-errors.aspx) (Solución de problemas y errores de SSRS)  
  
 Examine las [notas de la versión en línea](https://go.microsoft.com/fwlink/?linkid=236893) en caso de que el problema que tiene se describa en las notas de la versión.  
  
##  <a name="check-setup-logs"></a><a name="bkmk_setuplogs"></a> Examinar los registros de instalación  
 Los errores de configuración se registran en los archivos de registro de la carpeta **[!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Setup Bootstrap\Log** . Se crea una subcarpeta cada vez que se ejecuta el programa de instalación. El nombre de la subcarpeta indica la hora y la fecha en que se ejecutó el programa de instalación. Para obtener instrucciones sobre cómo ver los archivos de registro de instalación, vea [Ver y leer los archivos de registro de instalación de SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
-   Los archivos de registro incluyen una recopilación de archivos.  
  
-   Abra el archivo *_summary.txt para ver información del producto, componente e instancia.  
  
-   Abra el archivo *_errorlog.txt para ver información de los errores generados durante la instalación.  
  
-   Abra el archivo *_RS\_\*_ComponentUpdateSetup.log para ver información sobre la instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
##  <a name="check-prerequisites"></a><a name="bkmk_prereq"></a> Comprobar los requisitos previos  
 El programa de instalación comprueba si se cumplen los requisitos previos automáticamente. Sin embargo, al solucionar problemas de instalación, es útil saber qué requisitos comprueba dicho programa.  
  
-   Los requisitos relacionados con las cuentas que se necesitan para ejecutar el programa de instalación incluyen la pertenencia al grupo local de administradores. El programa de instalación debe tener permiso para agregar archivos y valores del Registro, crear grupos de seguridad locales y establecer permisos fijos. Si está instalando una configuración predeterminada, el programa de instalación debe tener permiso para crear una base de datos del servidor de informes en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la que esté efectuando la instalación.  
  
-   El sistema operativo debe admitir HTTP.SYS 1.1.  
  
-   El servicio HTTP debe estar habilitado y ejecutándose.  
  
-   El Coordinador de transacciones distribuidas (DTC) se debe estar ejecutando si también está instalando el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Authz.dll debe encontrarse en la carpeta System32.  
  
 El programa de instalación ya no comprueba Internet Information Services (IIS) ni [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] requiere MDAC 2.0 y [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] versión 2.0; el programa de instalación los instalará si no están en el equipo.  

::: moniker range="=sql-server-2016"
  
##  <a name="troubleshoot-problems-with-sharepoint-mode-installations"></a><a name="bkmk_tshoot_sharepoint"></a> Solucionar los problemas de las instalaciones en modo de SharePoint  
  
-   [El Administrador de configuración del servidor de informes no se inicia](#bkmk_configmanager_notstart)  
  
-   [No ve el servicio SQL Server Reporting Services en Administración central de SharePoint después de instalar SQL Server 2016 SSRS en modo de SharePoint](#bkmk_no_ssrs_service)  
  
-   [Los cmdlets de PowerShell de Reporting Services no están disponibles y no se reconocen los comandos](#bkmk_cmdlets_not_recognized)  
  
-   [Aparece un mensaje de error que indica que la dirección URL no está configurada](#bkmk_URL_not_configured)  
  
-   [El programa de instalación produce errores en un equipo con SharePoint instalado pero que no está configurado](#bkmk_sharepoint_not_confiugred)  
  
-   [La página Administración central de SharePoint está en blanco](#bkmk_central_admin_blank)  
  
-   [Ve un mensaje de error al intentar crear un nuevo informe del Generador de informes](#bkmk_reportbuilder_newreport_error)  
  
-   [Ve un mensaje de error que indica que RS_SHP no se admite con PREPAREIMAGE](#bkmk_RS_SHP_notsupported)  

### <a name="report-server-configuration-manager-does-not-start"></a><a name="bkmk_configmanager_notstart"></a> El Administrador de configuración del servidor de informes no se inicia

 **Descripción:** este problema se debe al diseño de SQL Server 2012 y versiones posteriores. Reporting Services está estructurado para la arquitectura de servicios de SharePoint. El Administrador de configuración ya no es necesario para configurar y administrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint.  
  
 **Solución alternativa:** use la Administración central de SharePoint para configurar un servidor de informes en modo de SharePoint. Para obtener más información, vea [Administrar una aplicación de servicio de SharePoint para Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).  
  
 ![Icono de flecha usado con el vínculo Volver al principio](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio") [Solucionar los problemas de las instalaciones en modo de SharePoint](#bkmk_tshoot_sharepoint)  
  
###  <a name="you-do-not-see-the-sql-server-reporting-services-service-in-sharepoint-central-administration-after-installing-sql-server-2016-ssrs-in-sharepoint-mode"></a><a name="bkmk_no_ssrs_service"></a> No ve el servicio SQL Server Reporting Services en Administración central de SharePoint después de instalar SQL Server 2016 SSRS en modo de SharePoint  
 **Descripción:** si, después de haber instalado correctamente SQL Server 2016 Reporting Services en el modo de SharePoint y el complemento de SQL Server 2016 Reporting Services para SharePoint 2013/2016, no ve "SQL Server Reporting Services" en los dos menús siguientes, significa que el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no se ha registrado:  
  
-   Administración central de SharePoint 2013/2016 -> “Administración de aplicaciones” -> página “Administrar servicios en el servidor”  
  
-   Administración central de SharePoint 2013/2016 -> "Administración de aplicaciones" -> "Administrar aplicaciones de servicio" ->menú "Nuevo"  
  
 **Solución alternativa:** para registrar e iniciar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint Services, siga estos pasos:  
  
1.  En el equipo que ejecuta Administración central de SharePoint 2013/2016  
  
    1.  Abra el Shell de administración de SharePoint 2013/2016 con privilegios de administrador. Haga clic con el botón derecho en el icono y haga clic en **Ejecutar como administrador**. Ejecute los tres siguientes cmdlets desde el shell:  
  
    2.  ```  
        Install-SPRSService  
        ```  
  
    3.  ```  
        Install-SPRSServiceProxy  
        ```  
  
    4.  ```  
        Get-SPServiceInstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
        ```  
  
2.  Compruebe el estado del servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] como "**Iniciado**" en la página: Administración central de SharePoint 2013/2016 -> "**Administración de aplicaciones**" -> página "**Administrar servicios en el servidor**"  
  
 ![Icono de flecha usado con el vínculo Volver al principio](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio") [Solucionar los problemas de las instalaciones en modo de SharePoint](#bkmk_tshoot_sharepoint)  
  
###  <a name="reporting-services-powershell-cmdlets-are-not-available-and-commands-are-not-recognized"></a><a name="bkmk_cmdlets_not_recognized"></a> Los cmdlets de PowerShell de Reporting Services no están disponibles y no se reconocen los comandos  
 **Descripción:** al intentar ejecutar un cmdlet de PowerShell de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], aparece un mensaje de error similar al siguiente:  
  
-   El término “Install-SPRSServiceInstall-SPRSService” **no se reconoce** como nombre de un cmdlet, función, archivo de script o programa ejecutable. Compruebe si escribió correctamente el nombre o, si incluyó una ruta de acceso, compruebe que dicha ruta es correcta e inténtelo de nuevo. At line:1 char:39+ Install-SPRSServiceInstall-SPRSService <<<<    + CategoryInfo          : ObjectNotFound: (Install-SPRSServiceInstall-SPRSService:String) [], CommandNotFoundExcep  
  
 **Solución alternativa:** realice una de las acciones siguientes:  
  
-   Ejecute el complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para productos de SharePoint. **rssharepoint.msi**.  
  
-   Instale [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint desde los medios de instalación de SQL Server.  
  
 Si el **Shell de administración de SharePoint 2013/2016** está abierto cuando completa una de las soluciones alternativas, cierre y vuelva a abrir el shell de administración.  
  
 Vea los siguientes artículos para más información:  
  
-   [Dónde encontrar el complemento Reporting Services para Productos de SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
-   [Instalación del primer servidor de informes en modo de SharePoint](install-the-first-report-server-in-sharepoint-mode.md)  
  
 ![Icono de flecha usado con el vínculo Volver al principio](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio") [Solucionar los problemas de las instalaciones en modo de SharePoint](#bkmk_tshoot_sharepoint)  
  
###  <a name="you-see-an-error-message-indicating-the-url-is-not-configured"></a><a name="bkmk_URL_not_configured"></a> Aparece un mensaje de error que indica que la dirección URL no está configurada  
 **Descripción:** verá un mensaje de error similar al siguiente:  
  
 Esta funcionalidad de SQL Server Reporting Services (SSRS) no se admite. Use Administración central para comprobar y corregir los problemas siguientes:
 
 - No se ha configurado una dirección URL del servidor de informes. Use la página Integración de SSRS para configurarla.
 
 - El proxy de aplicación del servicio SSRS no está configurado. Use las páginas de aplicación del servicio SSRS para configurar el proxy.
 
 - La aplicación del servicio SSRS no está asignada a esta aplicación web. Use las páginas de aplicación de servicios de SSRS para asociar el proxy de aplicación de servicios de SSRS al Grupo de proxy de aplicación para esta aplicación web. 
  
 **Solución alternativa:** el mensaje de error contiene tres pasos sugeridos para corregir este problema. La primera sugerencia del mensaje "No se ha configurado una dirección URL del servidor de informes." es pertinente cuando se integra con la versión del servidor de informes anterior a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. La configuración de SharePoint para las versiones del servidor de informes anteriores se completa en la página **Configuración de aplicación general** , mediante **SQL Server Reporting Services (2008 y 2008 R2)**.  
  
 **Más información:** este mensaje de error aparecerá si intenta usar cualquier funcionalidad de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que requiere una conexión al servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Esto incluye:  
  
-   Abrir el Generador de informes de SQL Server desde una biblioteca de documentos de SharePoint.  
  
-   Administrar suscripciones.  
  
-   Administrar una aplicación de servicio.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio") [Solucionar los problemas de las instalaciones en modo de SharePoint](#bkmk_tshoot_sharepoint)  
  
###  <a name="setup-fails-on-a-computer-with-sharepoint-installed-but-it-is-not-configured"></a><a name="bkmk_sharepoint_not_confiugred"></a> El programa de instalación produce errores en un equipo con SharePoint instalado pero que no está configurado  
 **Descripción** : si selecciona instalar el modo SharePoint de Reporting Services en un equipo que tiene SharePoint instalado pero no configurado, verá un mensaje similar al siguiente y la instalación se detendrá:  
  
 El programa de instalación de SQL Server ha dejado de funcionar  
  
 **Solución alternativa:** configure SharePoint y, a continuación, ejecute la instalación de SQL Server.  
  
 **Más información:** al instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en una instalación de SharePoint existente, el programa de instalación intenta instalar e iniciar el servicio de SharePoint [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Si SharePoint no está configurado, la instalación del servicio da error e impide que el programa de instalación se complete.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio") [Solucionar los problemas de las instalaciones en modo de SharePoint](#bkmk_tshoot_sharepoint)  
  
###  <a name="sharepoint-central-administration-page-is-blank"></a><a name="bkmk_central_admin_blank"></a> La página Administración central de SharePoint está en blanco  
 **Descripción:** pudo instalar SharePoint 2013/2016 correctamente, sin errores de instalación. Sin embargo, al ir a Administración Central, solo ve una página en blanco:  
  
 **Solución alternativa:** este problema no es específico de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , sino que está relacionado con la configuración de permisos de la instalación de SharePoint global. Estas son algunas sugerencias:  
  
-   Revise el artículo de SharePoint sobre los entornos de desarrollo. [Configurar un entorno de desarrollo general para SharePoint](/sharepoint/dev/general-development/set-up-a-general-development-environment-for-sharepoint)  
  
-   Revisar la exposición en el foro: [Administración central devuelve una página en blanco después de la instalación en Windows 7](https://social.technet.microsoft.com/Forums/en/sharepoint2010setup/thread/a422a3c8-39f6-4b9e-988a-4c4d1e745694)  
  
-   La cuenta de servicio que usa para los servicios de SharePoint, como el Servicio de Administración central de SharePoint 2013/2016, debería tener los privilegios de administrador en el sistema operativo local.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio") [Solucionar los problemas de las instalaciones en modo de SharePoint](#bkmk_tshoot_sharepoint)  
  
###  <a name="you-see-an-error-message-when-you-try-to-create-a-new-report-builder-report"></a><a name="bkmk_reportbuilder_newreport_error"></a> Ve un mensaje de error al intentar crear un nuevo informe del Generador de informes  
 **Descripción:** ve un mensaje de error similar al siguiente al intentar crear un informe del Generador de informes dentro de una biblioteca de documentos:  
  
 No se admite esta funcionalidad porque una aplicación de servicio de SQL Server Reporting Services no existe o una dirección URL del servidor de informes no se ha configurado en Administración central.  
  
 **Solución alternativa:** compruebe que tiene una aplicación de servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y que está configurada correctamente. Para obtener más información, vea [Instalación del primer servidor de informes en modo de SharePoint](install-the-first-report-server-in-sharepoint-mode.md).
  
 ![Icono de flecha usado con el vínculo Volver al principio](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio") [Solucionar los problemas de las instalaciones en modo de SharePoint](#bkmk_tshoot_sharepoint)  
  
###  <a name="you-see-an-error-message-that-rs_shp-is-not-supported-with-prepareimage"></a><a name="bkmk_RS_SHP_notsupported"></a> Ve un mensaje de error que indica que RS_SHP no se admite con PREPAREIMAGE  
 **Descripción:** al intentar ejecutar PREPAREIMAGE para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], aparece un mensaje de error similar al siguiente:  
  
 "La característica especificada "RS_SHP" no se admite al ejecutar la acción PREPAREIMAGE, dado que no es compatible con SysPrep. Quite las características que no son compatibles con SysPrep y ejecute el programa de instalación de nuevo".  
  
 **Solución alternativa:** no hay ninguna. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no admite SYSPREP (PREPAREIMAGE). [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no admite SYSPREP.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio") [Solucionar los problemas de las instalaciones en modo de SharePoint](#bkmk_tshoot_sharepoint)  

::: moniker-end
  
##  <a name="troubleshoot-problems-with-the-native-mode-installations"></a><a name="bkmk_tshoot_native"></a> Solucionar problemas con las instalaciones en modo nativo  
  
###  <a name="performance-counters-are-not-visible-after-upgrading-to-windows-vista-or-windows-server-2008"></a><a name="PerfCounters"></a> Los contadores de rendimiento no son visibles después de actualizar a Windows Vista o Windows Server 2008  
 Si actualiza el sistema operativo a [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] o [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] en un equipo que ejecuta [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], los contadores de rendimiento de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no se establecerán después de la actualización.  
  
#### <a name="to-reinstate-reporting-services-performance-counters"></a>Para restablecer los contadores de rendimiento de Reporting Services  
  
1.  Elimine las claves del Registro siguientes:  
  
    -   **HKLM\SYSTEM\CurrentControlSet\Services\MSRS 2016 Web Service**  
  
    -   **HKLM\SYSTEM\CurrentControlSet\Services\MSRS 2016 Windows Service**  
  
2.  Abra una ventana del símbolo del sistema y escriba el comando siguiente en el símbolo del sistema:  
  
    -   **Ejecute \<** *.NET 4.0 Framework directory* **>\InstallUtil.exe \<** *Report Server Bin directory* **>\ReportingServicesLibrary.dll**.  
  
        > [!NOTE]  
        >  Reemplace \<*.NET 4.0 Framework directory*> por la ruta de acceso física de los archivos de .NET Framework 4.0 y reemplace \<*Report Server Bin directory*> por la ruta de acceso física de los archivos binarios del servidor de informes.  
  
3.  Reinicie el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Para comprobar que los pasos funcionaron, abra un explorador web y vaya a la dirección URL del portal web o del servidor de informes. A continuación, abra el Monitor de rendimiento para comprobar que los contadores funcionan.  
  
#### <a name="to-add-the-performance-registry-keys-again-by-using-registry-editor"></a>Para agregar las claves del Registro de rendimiento con el Editor del Registro  
  
1.  Abra el Editor del Registro:  
  
    1.  Haga clic en **Inicio** y, a continuación, en **Ejecutar**.  
  
    2.  En el cuadro de diálogo **Ejecutar** , en el cuadro **Abrir** , escriba **regedit**.  
  
2.  En el Editor del Registro, seleccione la clave del Registro siguiente: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2016 Web Service\Performance`  
  
3.  Haga clic con el botón derecho en el nodo **Performance** , seleccione **Nuevo** y haga clic en **Valor de cadena múltiple**.  
  
4.  Escriba **Counter Names** y, después, presione Intro.  
  
5.  Repita este paso para agregar la clave de registro **Counter Types** a este nodo.  
  
6.  Desplácese hasta la siguiente clave del Registro: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2016 Web Service\Performance`  
  
7.  Haga clic con el botón derecho en el nodo **Performance** , seleccione **Nuevo** y haga clic en **Valor de cadena múltiple**.  
  
8.  Escriba **Counter Names** y, después, presione Intro.  
  
9. Repita este paso para agregar la clave de registro **Counter Types** a este nodo.  
  
 Después de reparar la instancia de 64 bits o volver a agregar las claves del Registro de forma manual, puede usar el Monitor de rendimiento para configurar los objetos de rendimiento de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que quiera supervisar.  
  
###  <a name="reportserverexternalurl-and-passthroughcookies-configuration-properties-are-not-configured-after-an-upgrade-from-sql-server-2005"></a><a name="ConfigPropsMissing"></a> Las propiedades de configuración ReportServerExternalURL y PassThroughCookies no están configuradas después de actualizar SQL Server 2005  
 Al actualizar desde [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)], el proceso de actualización no configura las propiedades de configuración **ReportServerExternalURL** y **PassThroughCookies** . **ReportServerExternalURL** es una propiedad opcional y se debe establecer únicamente si usa elementos web de SharePoint 2.0 y desea que los usuarios puedan recuperar un informe y abrirlo en una nueva ventana del explorador. Para más información sobre **ReportServerExternalURL**, vea [Direcciones URL en archivos de configuración &#40;Administrador de configuración del servidor de informes&#41;](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md). **PassThroughCookies** solo se requiere cuando se usa el método de autenticación personalizada. Para más información sobre **PassThroughCookies**, vea [Configurar el portal web para pasar cookies de autenticación personalizada](../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md).  
  
> [!NOTE]  
>  Al utilizar la autenticación personalizada, se recomienda que migre la instalación en lugar de actualizarla. Para más información sobre cómo migrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vea [Migrar una instalación de Reporting Services &#40;modo nativo&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md).  
  
 De forma predeterminada, estas propiedades no existen en la configuración de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] . Si configuró estas propiedades en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y continúa requiriendo la funcionalidad que proporcionan, debe agregarlas manualmente al archivo **RSReportServer.config** después del proceso de actualización. Para más información, vea [Modificar un archivo de configuración de Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md).  

### <a name="401-unauthorized-error-when-using-windows-authentication-after-an-upgrade-from-sql-server-2005-to-sql-server-2016"></a><a name="WindowsAuthBreaksAfterUpgrade"></a> 401- Error no autorizado al utilizar la autenticación de Windows después de actualizar SQL Server 2005 a SQL Server 2016

 Si actualiza [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] y usa la autenticación NTLM con una cuenta integrada para la cuenta de servicio del servidor de informes, podría encontrar un error 401-no autorizado al obtener acceso al servidor de informes o al portal web después de la actualización.  
  
 Verá este mensaje debido a un cambio en la configuración de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] predeterminada para la autenticación de Windows. Negotiate se configura cuando la cuenta de servicio del servidor de informes es Servicio de red o Sistema local. NTLM se configura cuando la cuenta del servicio del servidor de informes no es ninguna de esas cuentas integradas. Para corregir este problema después de actualizar, puede modificar el archivo RSReportServer.config y configurar **AuthenticationType** para que sea **RSWindowsNTLM**. Para más información, consulte [Configure Windows Authentication on the Report Server](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md) (Configuración de la autenticación de Windows en el servidor de informes).  

### <a name="uninstalling-32-bit-instance-of-sql-server-2016-reporting-services-in-side-by-side-deployment-with-a-64-bit-instance-breaks-the-64-bit-instance"></a><a name="Uninstall32BitBreaks64Bit"></a> La desinstalación de la instancia de 32 bits de SQL Server 2016 Reporting Services en la implementación paralela con una instancia de 64 bits daña la instancia de 64 bits

 Al instalar una instancia de 32 bits y una instancia de 64 bits de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] en paralelo en un equipo y desinstalar la de 32 bits, se quitan cuatro claves del Registro de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Al quitar estas claves se interrumpe la instancia de 64 bits de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Las claves del Registro de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que se quitan al desinstalar la instancia de 32 bits son:  
  
 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2016 Web Service\Performance:Counter Names` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2016 Windows Service\Performance:Counter Names` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2016 Web Service\Performance:Counter Types` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2016 Windows Service\Performance:Counter Types`  
  
 Para corregir este problema, puede reparar la instancia de 64 bits. Aunque se recomienda usar la reparación, puede volver a agregar las claves del Registro de forma manual mediante el Editor del Registro.  
  
> [!CAUTION]  
>  Una modificación incorrecta del Registro puede provocar daños graves en el sistema. Antes de realizar cambios en el Registro, debe hacer una copia de seguridad de los datos de valor guardados en el equipo.  
  
##  <a name="additional-resources"></a><a name="bkmk_additional"></a> Recursos adicionales  
 A continuación se indican recursos adicionales que puede consultar a modo de ayuda para solucionar problemas:  
  
-   Wiki de TechNet: [Solución de problemas de SQL Server Reporting Services (SSRS) en el modo integrado de SharePoint 2010](https://social.technet.microsoft.com/wiki/contents/articles/troubleshoot-sql-server-reporting-services-ssrs-in-sharepoint-integrated-mode.aspx)  
  
-   [Preguntas y respuestas de Microsoft: SQL Server Reporting Services](/answers/topics/sql-server-reporting-services.html)  
  
-   ¿Tiene algún comentario o más preguntas? Visite [UserVoice de Microsoft SQL Server](https://feedback.azure.com/forums/908035-sql-server).  
  
