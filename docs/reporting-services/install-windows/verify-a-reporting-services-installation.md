---
title: "Comprobar la instalación de Reporting Services | Documentos de Microsoft"
ms.custom: 
ms.date: 06/03/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- checking report server installations
- verifying report server installations
- Report Designer [Reporting Services], verifying installations
- installing Reporting Services, verifying installations
- Report Manager [Reporting Services], verifying installations
- report servers [Reporting Services], verifying installations
- Setup [Reporting Services], verifying installations
ms.assetid: 82a51a99-66f0-4b0c-b05b-07d22387adb0
caps.latest.revision: 45
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a5849b6240557cd1682d08210f256e0edabfa70b
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="verify-a-reporting-services-installation"></a>Comprobar una instalación de Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] pueden instalarse de uno de dos modos, Nativo o SharePoint. Los pasos que debería seguir para comprobar la instalación dependen del modo del servidor de informes.  
  
##  <a name="bkmk_sharepointmode"></a> Comprobar la instalación en modo de SharePoint  
  
### <a name="to-verify-the-reporting-services-service"></a>Para comprobar el servicio Reporting Services  
  
1.  En Administración central de SharePoint, haga clic en **Administrar los servicios del servidor** , en el grupo **Configuración del sistema** .  
  
2.  Compruebe que se instala el **Servicio SQL Server Reporting Services** y que está en el estado **En ejecución** .  
  
     Si no ve el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en la lista, compruebe que el servicio está instalado. Para obtener más información, vea [Instalación del primer servidor de informes en modo de SharePoint](http://msdn.microsoft.com/en-us/b29d0f45-0068-4c84-bd7e-5b8a9cd1b538).  
  
### <a name="to-verify-the-service-application"></a>Para comprobar la aplicación de servicio  
  
1.  Para comprobar desde Administración central que tiene al menos una aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , haga clic en **Administrar aplicaciones de servicio** en el grupo **Administración de aplicaciones** .  
  
2.  Compruebe si hay una aplicación de servicio de tipo **Aplicación del servicio SQL Server Reporting Services** y un proxy de aplicación correspondiente.  
  
3.  Haga clic **cerca** del nombre de la aplicación de servicio y, a continuación, haga clic en **Propiedades** en la barra de herramientas de SharePoint.  Si hace clic en el nombre de la aplicación de servicio, se abrirán las páginas de Administración de la aplicación de servicio, no la página de propiedades.  
  
4.  Compruebe que la **Asociación de aplicaciones web** esté configurada para apuntar a la aplicación web deseada.  
  
### <a name="to-verify-the-site-collection-feature"></a>Para comprobar la característica de colección de sitios  
  
1.  En la configuración del sitio, haga clic en **Características de la colección de sitios** en el grupo **Administración de la colección de sitios** .  
  
2.  Compruebe que la **Característica de integración del servidor de informes** está activa.  
  
### <a name="to-verify-reporting-server-content-types"></a>Para comprobar los tipos de contenido del servidor de informes  
  
1.  Para comprobar o agregar los tipos de contenido del servidor de informes [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , vea [Add Reporting Services Content Types to a SharePoint Library (Agregar los tipos de contenido de Reporting Services a una biblioteca de SharePoint)](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  
### <a name="to-verify-you-can-launch-report-builder"></a>Para comprobar que puede iniciar el Generador de informes  
  
1.  Desde una biblioteca de documentos, haga clic en **Documentos** en la cinta de opciones de SharePoint.  
  
2.  Haga clic en **Nuevo documento** y en **Informe del Generador de informes**. Si no ve esta opción, revise el procedimiento anterior para agregar los tipos de contenido del servidor de informes a una biblioteca.  
  
### <a name="create-a-basic-report"></a>Crear un informe básico  
  
1.  En una biblioteca de documentos de SharePoint, cree un informe básico de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que solo contenga un cuadro de texto, por ejemplo un título. El informe no contiene ningún origen de datos o conjuntos de datos. El objetivo es comprobar que puede abrir el Generador de informes y obtener una vista previa de un informe básico.  
  
2.  Guarde el informe en la biblioteca de documentos y ejecútelo desde la biblioteca. Para obtener más información sobre cómo crear informes con el Generador de informes, vea [Start Report Builder (Iniciar el Generador de informes)](http://msdn.microsoft.com/en-us/8c8c7d2e-b315-418d-bf65-90e7685e4259).  
  
### <a name="reporting-services-samples"></a>Ejemplos de Reporting Services  
  
1.  Complete uno de los tutoriales de Reporting Services. Para obtener más información, vea [tutoriales de Reporting Services &#40; SSRS &#41; ](../../reporting-services/reporting-services-tutorials-ssrs.md).  
  
2.  Descargue la base de datos de ejemplo de Adventure Works y los informes de ejemplo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de CodePlex. Para obtener más información, vea [Ejemplos de informes de AdventureWorks](https://msftrsprodsamples.codeplex.com/wikipage?title=SS2012!AdventureWorks2012%20Report%20Samples&referringTitle=Home).  
  
##  <a name="bkmk_nativemode"></a> Comprobar una instalación en modo nativo  
 Cuando instale un servidor de informes en modo nativo mediante la configuración personalizada, el programa de instalación instalará e implementará el servidor. Puede comprobar si el programa de instalación ha implementado el servidor de informes realizando unas sencillas pruebas. Debe ser un administrador local para poder realizar estos pasos. Para permitir que otros usuarios realicen estas pruebas, deberá configurar el acceso al servidor de informes para estos usuarios.  
  
### <a name="to-verify-that-the-report-server-is-installed-and-running"></a>Para comprobar que el servidor de informes está instalado y funciona  
  
1.  Ejecute la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y conéctese a la instancia del servidor de informes recién instalada. La página Dirección URL del servicio web incluye un vínculo al servicio web del servidor de informes. Haga clic en el vínculo para comprobar que puede tener acceso al servidor. Si la base de datos del servidor de informes no está configurada, haga eso primero antes de hacer clic en el vínculo.  
  
2.  Abra las aplicaciones de la consola Servicios y compruebe que se está ejecutando el servicio Servidor de informes. Para ver el estado del servicio del servidor de informes, haga clic en **Inicio**, seleccione **Panel de control**, haga doble clic en **Herramientas administrativas**y, después, en **Servicios**. Cuando aparezca la lista de servicios, desplácese a **Servidor de informes (MSSQLSERVER)**. El estado debe ser **Iniciado**.  
  
3.  Abra un explorador y escriba la dirección URL del servidor de informes en la barra de direcciones. La dirección está formada por el nombre del servidor y el nombre del directorio virtual que haya especificado para el servidor de informes durante la instalación. De manera predeterminada, el directorio virtual del servidor de informes se denomina **ReportServer**. Puede usar la siguiente dirección URL para comprobar la instalación del servidor de informes: http://*\<nombre_equipo >*/ReportServer*\<_nombre >*. La dirección URL será distinta si el servidor de informes se instala como una instancia con nombre. Para obtener más información sobre el formato de dirección URL, vea [configurar direcciones URL de servidor de informes &#40; Administrador de configuración de SSRS &#41; ](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md). Si eres un administrador local en Windows Vista o Windows Server 2008, consulte [configurar un servidor de informes de modo nativo para la administración Local &#40; SSRS &#41; ](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
4.  Ejecute informes para probar el funcionamiento del servidor de informes. Para este paso, puede crear un informe de muestra con el tutorial. Para obtener más información, vea [crear un informe de tabla básico &#40; Tutorial de SSRS &#41; ](../../reporting-services/create-a-basic-table-report-ssrs-tutorial.md).  
  
### <a name="to-verify-that-the-includessrswebportalincludesssrswebportalmd-is-installed-and-running"></a>Para comprobar que el [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] está instalado y funciona  
  
1.  Abra un explorador y escriba la dirección URL del Portal web en la barra de direcciones. La dirección está compuesta del nombre del servidor y el nombre del directorio virtual que ha especificado para el [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] durante la instalación, o en la página Dirección URL del Portal web en la herramienta Configuración de Reporting Services. De forma predeterminada, el directorio virtual del [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] es **Reports**. Puede usar la dirección URL siguiente para comprobar la instalación del [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] :  
  
     http://*\<nombre_equipo >*/Reports*\<_nombre >*.  
  
2.  Use el [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] para crear una carpeta nueva o cargar un archivo para probar si se pasan definiciones a la base de datos del servidor de informes. Si estas operaciones son correctas, la conexión funciona.  
  
     Para obtener más información, vea [Portal Web &#40; Modo nativo de SSRS &#41; ](http://msdn.microsoft.com/en-us/7349e626-6ed5-4d21-b05f-cf042ad9ad70).  
  
### <a name="to-verify-that-report-designer-is-installed-and-running"></a>Para comprobar que el Diseñador de informes está instalado y funciona  
  
1.  Abra [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]y cree un proyecto nuevo basado en un tipo de proyecto de servidor de informes. Para obtener más información sobre cómo utilizar el Asistente para proyectos de servidor de informes, consulte [Reporting Services en SQL Server Data Tools &#40; SSDT &#41; ](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md) en libros en pantalla de SQL Server.  
  
2.  Si ha instalado ejemplos de informe, abra los archivos de proyectos de informe de ejemplo y publique los informes en un servidor de informes.  
  
## <a name="see-also"></a>Vea también  
 [Solucionar problemas en una instalación de Reporting Services](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)   
 [Causa y resolución de errores de servicios](../../reporting-services/troubleshooting/cause-and-resolution-of-reporting-services-errors.md)  
  
  

