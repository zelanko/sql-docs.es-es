---
title: Configurar un servidor de informes en modo nativo para la administración local (SSRS) | Microsoft Docs
ms.date: 05/28/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- UAC
- installing Reporting Services
- Windows Vista
- Localhost
- windows server 2008
- Vista
ms.assetid: 312c6bb8-b3f7-4142-a55f-c69ee15bbf52
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 35355b32c8e4b59618cf146d9de04f3242ec6e6a
ms.sourcegitcommit: fc0eb955b41c9c508a1fe550eb5421c05fbf11b4
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/30/2019
ms.locfileid: "66403264"
---
# <a name="configure-a-native-mode-report-server-for-local-administration-ssrs"></a>Configurar un servidor de informes en modo nativo para la administración local (SSRS)
  La implementación de un servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en uno de los sistemas operativos siguientes requiere más pasos de configuración si desea administrar la instancia del servidor de informes localmente. En este tema, se describe cómo configurar el servidor de informes para la administración local. Si aún no tiene instalado o configurado el servidor de informes, vea [Instalar SQL Server desde el Asistente para la instalación &#40;programa de instalación&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md) y [Administrar un servidor de informes en modo nativo de Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md).  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
  
-   [!INCLUDE[winblue_server_2](../../includes/winblue-server-2-md.md)]  
  
-   [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]  
  
-   [!INCLUDE[win8](../../includes/win8-md.md)]  
  
-   [!INCLUDE[win8srv](../../includes/win8srv-md.md)]  
  
-   [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]  
  
-   [!INCLUDE[win7](../../includes/win7-md.md)]  
  
-   [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]  
  
 Puesto que los sistemas operativos indicados limitan los permisos, los miembros del grupo local Administradores ejecutan la mayoría de las aplicaciones como si usaran la cuenta de usuario estándar.  
  
 Aunque esta práctica mejora la seguridad global del sistema, impide que utilice las asignaciones de roles predefinidas e integradas que Reporting Services crea para los administradores locales.  
  
-   [Información general de los cambios de configuración](#bkmk_configuraiton_overview)  
  
-   [Para configurar el servidor de informes local y la administración del portal web](#bkmk_configure_local_server)  
  
-   [Para configurar SQL Server Management Studio (SSMS) para la administración del servidor de informes local](#bkmk_configure_ssms)  
  
-   [Para configurar SQL Server Data Tools (SSDT) para publicar en un servidor de informes local](#bkmk_configure_ssdt)  
  
-   [Información adicional](#bkmk_addiitonal_informaiton)  
  
##  <a name="bkmk_configuraiton_overview"></a> Información general de los cambios de configuración  
 Los cambios de configuración siguientes configuran el servidor de forma que pueda usar los permisos de usuario estándar para administrar el contenido y las operaciones del servidor de informes:  
  
-   Agrega direcciones URL de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a los sitios de confianza. De forma predeterminada, cuando Internet Explorer se ejecuta en los sistemas operativos enumerados lo hace en **Modo protegido**, una característica que impide que las solicitudes del explorador lleguen a los procesos de alto nivel que se ejecutan en el mismo equipo. Puede deshabilitar el modo protegido para las aplicaciones del servidor de informes agregándolas como sitios de confianza.  
  
-   Crea asignaciones de roles que le conceden, como administrador del servidor de informes, permiso para administrar el contenido y las operaciones sin tener que utilizar la característica **Ejecutar como administrador** de Internet Explorer. Mediante la creación de asignaciones de roles para su cuenta de usuario de Windows, obtiene acceso a un servidor de informes con los permisos Administrador de contenido y Administrador del sistema a través de las asignaciones de roles explícitas que reemplazan a las asignaciones de roles predefinidas e integradas, que Reporting Services crea.  
  
##  <a name="bkmk_configure_local_server"></a> Para configurar el servidor de informes local y la administración del portal web  
 Complete los pasos de configuración de esta sección si va a examinar un servidor de informes local y ve errores similares a los siguientes:  
  
-   El usuario `'Domain\[user name]`' no tiene los permisos requeridos. Compruebe que se han concedido suficientes permisos y que se han tratado las restricciones del control de cuentas de usuario (UAC) de Windows.  
  
###  <a name="bkmk_site_settings"></a> Configuración de sitios de confianza en el explorador  
  
1.  Abra una ventana del explorador con los permisos Ejecutar como administrador. En el menú **Inicio**, haga clic con el botón derecho en **Internet Explorer** y seleccione **Ejecutar como administrador**.  
  
2.  Seleccione **Sí** cuando se le solicite para continuar.  
  
3.  En la dirección URL, escriba la URL del portal web. Para obtener instrucciones, consulte [El portal web de un servidor de informes &#40;modo nativo de SSRS&#41;](../../reporting-services/web-portal-ssrs-native-mode.md).  
  
4.  Haga clic en **Herramientas**.  
  
5.  Haga clic en **Opciones de Internet**.  
  
6.  Haga clic en **Seguridad**.  
  
7.  Haga clic en **Sitios de confianza**.  
  
8.  Haga clic en **Sitios**.  
  
9. Agregue `https://<your-server-name>`.  
  
10. Desactive la casilla **Requerir comprobación del servidor (https:) para todos los sitios de esta zona** si no usa HTTP en el sitio predeterminado.  
  
11. Haga clic en **Agregar**.  
  
12. Seleccione **Aceptar**.  
  
###  <a name="bkmk_configure_folder_settings"></a> Configuración de la carpeta del portal web  
  
1.  En el portal web, en la página principal, haga clic en **Administrar carpeta**.  
  
2.  En la página **Administrar carpeta**, haga clic en **Seguridad** y, a continuación, seleccione **Agregar grupo o usuario**.  
  
3.  En la página **Nueva asignación de roles**, en el campo **Grupo o usuario**, escriba su cuenta de usuario de Windows en este formato: `<domain>\<user>`.  
  
5.  Seleccione **Administrador de contenido**.  
  
6.  Seleccione **Aceptar**.  
  
###  <a name="bkmk_configure_site_settings"></a> Configuración del sitio del portal web  
  
1.  Abra el explorador con privilegios administrativos y vaya al portal web, `https://<server name>/reports`.  
  
2.  Seleccione el icono de engranaje en la fila superior de la página principal y, a continuación, **Configuración del sitio** en el menú desplegable. 
  
    ![Icono de engranaje](../media/ssrsgearmenu.png).
    >[!TIP]  
    >**Nota:** Si no ve la opción **Configuración del sitio**, cierre y vuelva a abrir el explorador y vaya al portal web con privilegios administrativos.  
  
3.  En la página Configuración del sitio, seleccione **Seguridad** y, a continuación, seleccione **Agregar grupo o usuario**.  
  
4.  En el campo **Nombre de grupo o de usuario** , escriba su cuenta de usuario de Windows en este formato: `<domain>\<user>`.  

5.  Seleccione **Administrador del sistema**.  
  
6.  Seleccione **Aceptar**.  
  
7.  Cierre el portal web.  
  
8. Vuelva a abrir el portal web en Internet Explorer, sin usar **Ejecutar como administrador**.  
  
##  <a name="bkmk_configure_ssms"></a> Para configurar SQL Server Management Studio (SSMS) para la administración del servidor de informes local  
 De forma predeterminada, no puede tener acceso a todas las propiedades del servidor de informes disponibles en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] a menos que inicie [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] con privilegios administrativos.  
  
 **Para configurar asignaciones de roles de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]** no es necesario iniciar [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] con permisos elevados todas las veces:  
  
-   En el menú **Inicio**, haga clic con el botón derecho en **Microsoft SQL Server[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]** y, a continuación, haga clic en **Ejecutar como administrador**.  
  
-   Conéctese al servidor local de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   En el nodo **Seguridad** , haga clic en **Roles del sistema**.  
  
-   Haga clic con el botón derecho en **Administrador del sistema** y, después, haga clic en **Propiedades**.  
  
-   En la página **Propiedades de rol del sistema** , seleccione **Ver propiedades del servidor de informes**. Seleccione todas las demás propiedades que desee asociar a miembros del rol de administradores del sistema.  
  
-   Haga clic en **Aceptar**.  
  
-   Cerrar [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]  
  
-   Para agregar un usuario al rol del sistema "administrador del sistema", consulte la anterior sección [Configuración del sitio del portal web](#bkmk_configure_site_settings) en este artículo.  
  
 Ahora, cuando abra [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] y no seleccione explícitamente **Ejecutar como administrador** tendrá acceso a las propiedades del servidor de informes.  
  
##  <a name="bkmk_configure_ssdt"></a> Para configurar SQL Server Data Tools (SSDT) para publicar en un servidor de informes local  
 Si instaló [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] en uno de los sistemas operativos enumerados en la primera sección de este tema y desea que SSDT interactúe con un servidor de informes local en modo nativo, aparecerán errores con los permisos a menos que abra [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] con permisos elevados o que configure roles de Reporting Services. Por ejemplo, si no tiene los permisos necesarios, encontrará problemas similares a los siguientes:  
  
-   Cuando intenta implementar elementos de informe en el servidor de informes local, aparece un mensaje de error similar al siguiente en la ventana **Lista de errores** :  
  
    -   Los permisos otorgados al usuario "Dominio\\<nombre de usuario\>" son insuficientes para realizar esta operación.  
  
 **Para ejecutar SSDT con permisos elevados cada vez que lo abre:**  
  
1.  En la pantalla de inicio, seleccione **Microsoft SQL Server** y después haga clic con el botón derecho en **SQL Server Data Tools**. Haga clic en **Ejecutar como administrador**  
  
2.  Seleccione **Sí** cuando se le solicite para continuar.  
  
Ahora debe poder implementar informes y otros elementos en un servidor de informes local.  
  
 **Para configurar asignaciones de roles de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no es necesario iniciar SSDT con permisos elevados todas las veces:**  
  
-   Consulte las secciones [Configuración de carpetas del portal web](#bkmk_configure_folder_settings) y [Configuración del sitio del portal web](#bkmk_configure_site_settings) en este tema.  
  
##  <a name="bkmk_addiitonal_informaiton"></a> Información adicional  
 Un paso de configuración frecuente adicional relacionado con la administración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] consiste en abrir el puerto 80 en Firewall de Windows para permitir el acceso al equipo servidor de informes. Para obtener instrucciones, consulte [Configure a Firewall for Report Server Access](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).  
  
## <a name="see-also"></a>Vea también  
 [Administración de un servidor de informes en modo nativo de Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  
  
  
