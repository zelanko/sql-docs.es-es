---
title: 'Tutorial: Cómo buscar e iniciar herramientas de Reporting Services (SSRS) | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Builder 1.0, locating and starting tool
- Reporting Services, tutorials
- Reporting Services, tools
- Reporting Services Configuration tool
- Business Intelligence Development Studio, locating and starting tool
- Model Designer [Reporting Services], locating and starting tool
- Report Designer [Reporting Services], tutorials
- tools [Reporting Services]
- tutorials [Reporting Services]
- Report Manager [Reporting Services]
ms.assetid: 51ad69d8-fe92-4662-a7cd-d235692f0c03
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4edd0b6e3928a2bc3a280403a87eda5bb797e620
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66099480"
---
# <a name="tutorial-how-to-locate-and-start-reporting-services-tools-ssrs"></a>Tutorial: Cómo buscar e iniciar herramientas de Reporting Services (SSRS)
  En este tutorial se presentan las herramientas utilizadas para configurar un servidor de informes, administrar las operaciones y el contenido del servidor de informes, y crear y publicar informes. La finalidad de este tutorial es ayudar a los nuevos usuarios a comprender cómo encontrar y abrir las distintas herramientas. Si ya está familiarizado con estas herramientas, puede pasar a los otros tutoriales que le ayudarán a adquirir conocimientos para utilizar [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Para obtener más información sobre otros tutoriales, vea [Reporting Services tutoriales &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md).  
  
 En este tema:  
  
-   [Administrador de configuración de Reporting Services (modo nativo)](#bkmk_configuration_manager)  
  
-   [Administrador de informes (modo nativo)](#bkmk_report_manager)  
  
-   [Management Studio](#bkmk_managements_studio)  
  
-   [Herramientas de datos de SQL Server con el Diseñador de informes y el Asistente para informes](#bkmk_ssdt)  
  
-   [Generador de informes](#bkmk_report_builder)  
  
##  <a name="reporting-services-configuration-manager-native-mode"></a><a name="bkmk_configuration_manager"></a>Administrador de configuración de Reporting Services (modo nativo)  
 Use el administrador de configuración en modo nativo para completar el siguiente: , , , , , y.  
  
-   Especifique la cuenta de servicio.  
  
-   Cree o actualice la base de datos del servidor de informes.  
  
-   Modifique las propiedades de conexión.  
  
-   Especifique las direcciones URL.  
  
-   Administre las claves de cifrado.  
  
-   Configure el procesamiento desatendido de informes y la entrega de informes por correo electrónico.  
  
 **Instalación:** [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] se instala al instalar el modo nativo de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] . Para más información, vea [Instalar el servidor de informes en modo nativo de Reporting Services](../install-windows/install-reporting-services-native-mode-report-server.md).  
  
#### <a name="to-start-the-reporting-services-configuration-manager"></a>Para iniciar el Administrador de configuración de Reporting Services  
  
1.  En la pantalla Inicio de Windows, `reporting` escriba y en los resultados de búsqueda de **aplicaciones** , haga clic en **Administrador de configuración de Reporting Services**.  
  
     ![administrador de configuración de Reporting Services al inicio](../media/bi-ssrs-configmanager-win8-startscreen.gif "administrador de configuración de Reporting Services al inicio")  
  
     **De**  
  
     Haga clic en **Inicio**, en **Programas**, [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], **Herramientas de configuración**y, por último, en **Administrador de configuración de Reporting Services**.  
  
     Se abrirá el cuadro de diálogo **Selección de instancia de instalación del servidor de informes** para que seleccione la instancia del servidor de informes que desee configurar.  
  
2.  En **Nombre del servidor**, especifique el nombre del equipo en el que está instalada la instancia del servidor de informes. De manera predeterminada aparece el nombre del equipo local, pero también puede escribir el nombre de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] remota.  
  
     Si especifica un equipo remoto, haga clic en **Buscar** para establecer una conexión. Previamente, debe haber configurado el servidor de informes para la administración remota. Para obtener más información, vea [Configurar un servidor de informes para la administración remota](../report-server/configure-a-report-server-for-remote-administration.md).  
  
3.  En **Nombre de instancia**, elija la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] que desee configurar. En la lista solo aparecen instancias del servidor de informes de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]y [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . No es posible configurar versiones anteriores de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
4.  Haga clic en **Conectar**.  
  
5.  Para comprobar que se haya iniciado la herramienta, compare sus resultados con los de la siguiente imagen:  
  
     ![Herramienta de configuración de Reporting Services](../media/rs-ui-reportserverconfigkatmai.gif "Herramienta de configuración de Reporting Services")  
  
 **Próximos pasos:** [Configurar y administrar un servidor de informes &#40;modo nativo de SSRS&#41;](../report-server/configure-and-administer-a-report-server-ssrs-native-mode.md) y [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
##  <a name="report-manager-native-mode"></a><a name="bkmk_report_manager"></a>Administrador de informes (modo nativo)  
 Use [Administrador de informes &#40;modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md) para establecer permisos, administrar suscripciones y programaciones, y trabajar con informes. También puede utilizar el Administrador de informes para ver informes.  
  
 **Instalación:** Administrador de informes se instala al instalar [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] el modo nativo de: [instalar Reporting Services servidor de informes en modo nativo](../install-windows/install-reporting-services-native-mode-report-server.md)  
  
 Antes de abrir el Administrador de informes, debe contar con los permisos suficientes (en un principio, solo los miembros del grupo de administradores locales poseen permisos que conceden acceso a las características del Administrador de informes). El Administrador de informes proporciona distintas páginas y opciones, según las asignaciones de roles del usuario actual. Los usuarios que no poseen permisos verán una página vacía. Los usuarios que posean permisos para ver informes contarán con vínculos en los que podrán hacer clic para abrir los informes. Para obtener más información sobre permisos, vea [Roles y permisos &#40;Reporting Services&#41;](../security/roles-and-permissions-reporting-services.md).  
  
#### <a name="to-start-report-manager"></a>Para iniciar el Administrador de informes  
  
1.  Abra el explorador. Para obtener información sobre los exploradores y las versiones de exploradores admitidos, consulte [Planning for Reporting Services and Power View Browser Support &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md).  
  
2.  En la barra de direcciones del explorador web, escriba la dirección URL del Administrador de informes. De forma predeterminada, la dirección URL es **http://\<ServerName>/Reports**. Puede utilizar la herramienta de configuración de Reporting Services para confirmar el nombre del servidor y la dirección URL. Para obtener más información sobre las direcciones URL que se usan en [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], vea [Configurar las direcciones URL del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../install-windows/configure-report-server-urls-ssrs-configuration-manager.md).  
  
3.  El Administrador de informes se abre en una ventana de explorador. La página de inicio es la carpeta Inicio. Según los permisos que posea, podrá ver otras carpetas, hipervínculos a informes y archivos de recursos dentro de la página de inicio. También puede ver otros botones y comandos en la barra de herramientas.  
  
4.  Si ejecuta Administrador de informes en el servidor de informes local, vea [configurar un servidor de informes en modo nativo para la administración local &#40;SSRS&#41;](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
 **Pasos siguientes:** [configurar administrador de informes &#40;modo nativo&#41;](../report-server/configure-web-portal.md).  
  
##  <a name="management-studio"></a><a name="bkmk_managements_studio"></a> Management Studio  
 Los administradores del servidor de informes pueden utilizar [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para administrar un servidor de informes junto con otros servidores de componentes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para más información, consulte [Use SQL Server Management Studio](../../database-engine/use-sql-server-management-studio.md).  
  
#### <a name="to-start-sql-server-management-studio"></a>Para iniciar SQL Server Management Studio  
  
1.  En la pantalla Inicio de Windows `sql server` , escriba y, en los resultados de búsqueda de **aplicaciones** , haga clic en **SQL Server Management Studio**.  
  
     ![Management Studio desde la pantalla de Inicio de Windows](../media/bi-ssms-win8-startscreen.gif "Management Studio desde la pantalla de Inicio de Windows")  
  
     **De**  
  
     Haga clic en **Inicio**, en **Todos los programas**, en [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]y, después, en **SQL Server Management Studio**. Aparecerá el cuadro de diálogo **Conectar con el servidor** .  
  
2.  Si no se muestra el cuadro de diálogo **Conectar con el servidor** , en el **Explorador de objetos**, haga clic en **Conectar** y luego seleccione **Reporting Services**.  
  
3.  En la lista **Tipo de servidor** , seleccione **Reporting Services**. Si [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] no está instalado, no aparecerá en la lista.  
  
4.  En la lista **Nombre del servidor** , seleccione una instancia del servidor de informes. La lista incluye instancias locales. También puede escribir el nombre de una instancia remota de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
5.  Haga clic en **Conectar**. Puede expandir el nodo raíz para establecer propiedades del servidor, modificar definiciones de roles o desactivar características del servidor de informes.  
  
##  <a name="sql-server-data-tools-with-report-designer-and-report-wizard"></a><a name="bkmk_ssdt"></a>SQL Server Data Tools con Diseñador de informes y el Asistente para informes  
 El Diseñador de informes está disponible en [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] - Business Intelligence para Visual Studio 2012. La superficie de diseño de la herramienta incluye ventanas con pestañas, asistentes y menús que se utilizan para el acceso a características de creación de informes. La herramienta de diseñador de informes está disponible al elegir un proyecto del servidor de informes o una plantilla del Asistente del servidor de informes. Para más información, vea [Reporting Services en SQL Server Data Tools &#40;SSDT&#41;](reporting-services-in-sql-server-data-tools-ssdt.md).  
  
#### <a name="to-start-report-designer"></a>Para iniciar el Diseñador de informes  
  
1.  En la pantalla de inicio de Windows, escriba **data** y en los resultados de búsqueda de **Aplicaciones** , haga clic en **SQL Server Data Tools para Visual Studio 2012**.  
  
     **De**  
  
     Haga clic en **Inicio**, seleccione **Todos los programas**, [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]y, a continuación, haga clic en **Herramientas de datos de SQL Server (SSDT)**.  
  
2.  En el menú **Archivo** , seleccione **Nuevo**y haga clic en **Proyecto**.  
  
3.  En la lista **Tipos de proyecto** , haga clic en **Proyectos de Business Intelligence**.  
  
4.  En la lista **Plantillas** , haga clic en **Proyecto de servidor de informes**. El siguiente diagrama muestra cómo aparecen las plantillas de proyecto en el cuadro de diálogo:  
  
     ![Cuadro de diálogo Nueva plantilla de proyecto](../media/rs-ui-newrsproject.gif "Cuadro de diálogo Nueva plantilla de proyecto")  
  
5.  Escriba un nombre y ubicación para el proyecto, o haga clic en **Examinar** y seleccione una ubicación.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)][!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] se abre con [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] la página de inicio. El Explorador de soluciones proporciona categorías para crear informes y orígenes de datos. Puede utilizar estas categorías para crear nuevos informes y orígenes de datos. Las ventanas con pestañas aparecen cuando crea una definición de informe. Las ventanas con pestañas son Datos, Diseño y Vista previa.  
  
 Para empezar a crear su primer informe, vea [Crear un informe de tabla básico &#40;Tutorial de SSRS&#41;](../create-a-basic-table-report-ssrs-tutorial.md). Para obtener más información sobre los diseñadores de consultas que puede usar en Diseñador de informes, consulte [herramientas de diseño de consultas en Diseñador de informes SQL Server Data Tools &#40;SSRS&#41;](../report-data/query-design-tools-ssrs.md).  
  
##  <a name="report-builder"></a>Generador de informes de <a name="bkmk_report_builder"></a>  
 Use [Generador de informes &#40;SSRS&#41;](report-builder-authoring-environment-ssrs.md) para crear informes en un [!INCLUDE[msCoName](../../includes/msconame-md.md)] entorno de creación de tipo Office. Puede personalizar y actualizar todos los informes existentes, independientemente de que se hayan creado en el Diseñador de informes o en las versiones anteriores del Generador de informes. Póngase en contacto con el administrador para obtener información sobre la ubicación del archivo ReportBuilder3.msi que necesitará ejecutar para instalar el Generador de informes en su equipo local.  
  
 **Instalación:** la versión ClickOnce del generador de informes se instala con el modo nativo o el modo de SharePoint de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] . La versión independiente del Generador de informes se descarga por separado.  Vea [instalar la versión independiente de Generador de informes &#40;Generador de informes&#41;](../install-windows/install-report-builder.md)  
  
#### <a name="to-start-report-builder-clickonce-from-report-manager-native-mode"></a>Para iniciar el Generador de informes ClickOnce desde el Administrador de informes (modo nativo)  
  
1.  En el explorador web, escriba la dirección URL del Administrador de informes para el servidor de informes. De forma predeterminada, la dirección URL es http://\<*nombreDeServidor*>/reports. Se abre el Administrador de informes.  
  
2.  Haga clic en **Generador de informes**.  
  
     El Generador de informes se abre y puede crear un informe o abrirlo en el servidor de informes.  
  
#### <a name="to-start-report-builder-clickonce-using-a-url"></a>Para iniciar el Generador de informes ClickOnce mediante una dirección URL  
  
1.  En el explorador web, escriba la siguiente dirección URL en la barra de direcciones:  
  
     **http://\<ServerName>/ReportServer/ReportBuilder/ReportBuilder_3_0_0_0. Application**  
  
2.  Presione ENTRAR.  
  
     El Generador de informes se abre y puede crear un informe o abrirlo en el servidor de informes.  
  
#### <a name="to-start-report-builder-clickonce-in-reporting-services-sharepoint-mode"></a>Para iniciar el Generador de informes ClickOnce en el modo de SharePoint de Reporting Services  
  
1.  Vaya al sitio que contenga la biblioteca donde desee crear un informe nuevo.  
  
2.  Abra la biblioteca.  
  
3.  En el menú **Nuevo** , haga clic en **Informe del Generador de informes**.  
  
     El Generador de informes se abre y puede crear un informe o abrirlo en el servidor de informes.  
  
#### <a name="to-start-report-builder-stand-alone"></a>Para iniciar el Generador de informes independiente  
  
1.  En la ventana de inicio de Windows, escriba **generador de informes** y haga clic en **Generador de informes 3.0**.  
  
     **De**  
  
     En el menú Inicio, haga clic en **Todos los programas**y, a continuación, haga clic en **Microsoft SQL Server 2014 Report Builder**.  
  
2.  Haga clic en **Generador de informes**.  
  
     Se abrirá el Generador de informes y podrá crear o abrir un informe.  
  
3.  Haga clic en **Ayuda del Generador de informes** para abrir la documentación del Generador de informes.  
  
## <a name="see-also"></a>Consulte también  
 [Instalación, desinstalación y compatibilidad Generador de informes](../install-uninstall-and-report-builder-support.md)   
 [Reporting Services la instalación en modo de SharePoint &#40;SharePoint 2010 y SharePoint 2013&#41;](../install-windows/install-reporting-services-sharepoint-mode.md)   
 [Reporting Services servidor de informes](../reporting-services-report-server.md)   
 [Herramientas de diseño de consultas en Diseñador de informes SQL Server Data Tools &#40;SSRS&#41;](../report-data/query-design-tools-ssrs.md)   
 [Tutoriales de Reporting Services &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)  
  
  
