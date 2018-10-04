---
title: Comprobar una instalación de Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- checking report server installations
- verifying report server installations
- Report Designer [Reporting Services], verifying installations
- installing Reporting Services, verifying installations
- Report Manager [Reporting Services], verifying installations
- report servers [Reporting Services], verifying installations
- Setup [Reporting Services], verifying installations
ms.assetid: 82a51a99-66f0-4b0c-b05b-07d22387adb0
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e1ea6363f2acb76d7c95fb6d2e8f7c0e9dbdbc6a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48108935"
---
# <a name="verify-a-reporting-services-installation"></a>Verify a Reporting Services Installation
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] pueden instalarse de uno de dos modos, Nativo o SharePoint. Los pasos que debería seguir para comprobar la instalación dependen del modo del servidor de informes.  
  
 Este tema contiene la información siguiente:  
  
-   [Comprobar la instalación del modo de SharePoint](#bkmk_sharepointmode)  
  
-   [Comprobar una instalación en modo nativo](#bkmk_nativemode)  
  
##  <a name="bkmk_sharepointmode"></a> Comprobar la instalación en modo de SharePoint  
  
#### <a name="to-verify-the-reporting-services-service"></a>Para comprobar el servicio Reporting Services  
  
1.  En Administración central de SharePoint, haga clic en **Administrar los servicios del servidor** , en el grupo **Configuración del sistema** .  
  
2.  Compruebe que se instala el **Servicio SQL Server Reporting Services** y que está en el estado **En ejecución** .  
  
     Si no ve el servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en la lista, compruebe que el servicio está instalado. Para obtener más información, vea la sección "Instalar e iniciar the Reporting Services SharePoint Service" de [instalar Reporting Services SharePoint Mode for SharePoint 2010](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md).  
  
#### <a name="to-verify-the-service-application"></a>Para comprobar la aplicación de servicio  
  
1.  Para comprobar desde Administración central que tiene al menos una aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , haga clic en **Administrar aplicaciones de servicio** en el grupo **Administración de aplicaciones** .  
  
2.  Compruebe si hay una aplicación de servicio de tipo **Aplicación del servicio SQL Server Reporting Services** y un proxy de aplicación correspondiente.  
  
3.  Haga clic **cerca** del nombre de la aplicación de servicio y, a continuación, haga clic en **Propiedades** en la barra de herramientas de SharePoint.  Si hace clic en el nombre de la aplicación de servicio, se abrirán las páginas de Administración de la aplicación de servicio, no la página de propiedades.  
  
4.  Compruebe que la **Asociación de aplicaciones web** esté configurada para apuntar a la aplicación web deseada.  
  
#### <a name="to-verify-the-site-collection-feature"></a>Para comprobar la característica de colección de sitios  
  
1.  En la configuración del sitio, haga clic en **Características de la colección de sitios** en el grupo **Administración de la colección de sitios** .  
  
2.  Compruebe que la **Característica de integración del servidor de informes** está activa.  
  
#### <a name="to-verify-reporting-server-content-types"></a>Para comprobar los tipos de contenido del servidor de informes  
  
1.  Para comprobar o agregar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] tipos de contenido del servidor de informes, vea [agregar tipos de contenido de servidor de informes en una biblioteca &#40;Reporting Services en modo integrado de SharePoint&#41;](../add-reporting-services-content-types-to-a-sharepoint-library.md).  
  
#### <a name="to-verify-you-can-launch-report-builder"></a>Para comprobar que puede iniciar el Generador de informes  
  
1.  Desde una biblioteca de documentos, haga clic en **Documentos** en la cinta de opciones de SharePoint.  
  
2.  Haga clic en **Nuevo documento** y en **Informe del Generador de informes**. Si no ve esta opción, revise el procedimiento anterior para agregar los tipos de contenido del servidor de informes a una biblioteca.  
  
#### <a name="create-a-basic-report"></a>Crear un informe básico  
  
1.  En una biblioteca de documentos de SharePoint, cree un informe básico de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que solo contenga un cuadro de texto, por ejemplo un título. El informe no contiene ningún origen de datos o conjuntos de datos. El objetivo es comprobar que puede abrir el Generador de informes y obtener una vista previa de un informe básico.  
  
2.  Guarde el informe en la biblioteca de documentos y ejecútelo desde la biblioteca. Para obtener más información sobre cómo crear informes con el Generador de informes, vea [Iniciar el Generador de informes (Generador de informes)](http://technet.microsoft.com/library/ms159221.aspx).  
  
#### <a name="reporting-services-samples"></a>Ejemplos de Reporting Services  
  
1.  Complete uno de los tutoriales de Reporting Services. Para más información, vea [Tutoriales de Reporting Services &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md).  
  
2.  Descargue la base de datos de ejemplo de Adventure Works y los informes de ejemplo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de CodePlex. Para obtener más información, vea [Ejemplos de informes de AdventureWorks](https://msftrsprodsamples.codeplex.com/wikipage?title=SS2012!AdventureWorks2012%20Report%20Samples&referringTitle=Home).  
  
##  <a name="bkmk_nativemode"></a> Comprobar una instalación en modo nativo  
 Cuando instale un servidor de informes en modo nativo mediante la configuración personalizada, el programa de instalación instalará e implementará el servidor. Puede comprobar si el programa de instalación ha implementado el servidor de informes realizando unas sencillas pruebas. Debe ser un administrador local para poder realizar estos pasos. Para permitir que otros usuarios realicen estas pruebas, deberá configurar el acceso al servidor de informes para estos usuarios.  
  
#### <a name="to-verify-that-the-report-server-is-installed-and-running"></a>Para comprobar que el servidor de informes está instalado y funciona  
  
1.  Ejecute la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y conéctese a la instancia del servidor de informes recién instalada. La página Dirección URL del servicio web incluye un vínculo al servicio web del servidor de informes. Haga clic en el vínculo para comprobar que puede tener acceso al servidor. Si la base de datos del servidor de informes no está configurada, haga eso primero antes de hacer clic en el vínculo.  
  
2.  Abra las aplicaciones de la consola Servicios y compruebe que se está ejecutando el servicio Servidor de informes. Para ver el estado del servicio del servidor de informes, haga clic en **Inicio**, seleccione **Panel de control**, haga doble clic en **Herramientas administrativas**y, después, en **Servicios**. Cuando aparezca la lista de servicios, desplácese a **Servidor de informes (MSSQLSERVER)**. El estado debe ser **Iniciado**.  
  
3.  Abra un explorador y escriba la dirección URL del servidor de informes en la barra de direcciones. La dirección está formada por el nombre del servidor y el nombre del directorio virtual que haya especificado para el servidor de informes durante la instalación. De manera predeterminada, el directorio virtual del servidor de informes se denomina **ReportServer**. Puede usar la siguiente dirección URL para comprobar la instalación del servidor de informes: http://*\<nombre de equipo>*/ReportServer*\<_nombre de instancia>*. La dirección URL será distinta si el servidor de informes se instala como una instancia con nombre. Para más información sobre el formato de las direcciones URL, vea [Configurar las direcciones URL del servidor de informes &#40;Administrador de configuración de SSRS&#41;](configure-report-server-urls-ssrs-configuration-manager.md). Si es un administrador local en Windows Vista o Windows Server 2008, vea [Configurar un servidor de informes en modo nativo para la administración local &#40;SSRS&#41;](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
4.  Ejecute informes para probar el funcionamiento del servidor de informes. Para este paso, puede crear un informe de muestra con el tutorial. Para más información, vea [Crear un informe de tabla básico &#40;Tutorial de SSRS&#41;](../create-a-basic-table-report-ssrs-tutorial.md).  
  
#### <a name="to-verify-that-report-manager-is-installed-and-running"></a>Para comprobar que el Administrador de informes está instalado y funciona  
  
1.  Abra un explorador y escriba la dirección URL del Administrador de informes en la barra de direcciones. La dirección está compuesta del nombre del servidor y el nombre del directorio virtual que se especificó para el Administrador de informes durante la instalación, o en la página Dirección URL del Administrador de informes en la herramienta Configuración de Reporting Services. De manera predeterminada, el directorio virtual del Administrador de informes es **Reports**. Puede utilizar la dirección URL siguiente para comprobar la instalación del Administrador de informes:  
  
     http://*\<nombre del equipo>*/Reports*\<_nombre de instancia>*.  
  
2.  Utilice el Administrador de informes para crear una carpeta o cargue un archivo para probar si se pasan definiciones a la base de datos del servidor de informes. Si estas operaciones son correctas, la conexión funciona.  
  
     Para más información, vea [Administrador de informes &#40;Modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
#### <a name="to-verify-that-report-designer-is-installed-and-running"></a>Para comprobar que el Diseñador de informes está instalado y funciona  
  
1.  Abra [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]y cree un proyecto nuevo basado en un tipo de proyecto de servidor de informes. Para más información sobre cómo usar el Asistente de proyectos de servidor de informes, vea [Reporting Services en SQL Server Data Tools &#40;SSDT&#41;](../tools/reporting-services-in-sql-server-data-tools-ssdt.md) en los Libros en pantalla de SQL Server.  
  
2.  Si ha instalado ejemplos de informe, abra los archivos de proyectos de informe de ejemplo y publique los informes en un servidor de informes.  
  
## <a name="see-also"></a>Vea también  
 [Solución de problemas de una instalación de Reporting Services](troubleshoot-a-reporting-services-installation.md)   
 [Causa y resolución de errores de Reporting Services](../troubleshooting/cause-and-resolution-of-reporting-services-errors.md)  
  
  
