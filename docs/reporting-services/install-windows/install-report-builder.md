---
title: Instalar el Generador de informes | Microsoft Docs
ms.custom: 
ms.date: 09/22/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 6b2291bb-1d20-4d08-81cb-a16dd8e01faf
caps.latest.revision: "20"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Active
ms.openlocfilehash: 395ec440e3cae0ac4013edc9c35af36e32a73d0c
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2018
---
# <a name="install-report-builder"></a>Install Report Builder
  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] es una aplicación independiente que el usuario o un administrador pueden instalar en el equipo. Puede instalarlo desde el Centro de descarga de Microsoft, desde un servidor de informes de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] o desde un sitio de SharePoint integrado con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Un administrador normalmente instala y configura [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], concede permiso para descargar [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] desde el portal web y administra carpetas y permisos a los informes, los elementos de informe y los conjuntos de datos compartidos guardados en el servidor de informes. Para más información sobre la administración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vea [Servidor de informes de Reporting Services &#40;modo nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md).  
  
## <a name="install-includessrbnoversionincludesssrbnoversion-mdmd-from--a--web-portal-or-sharepoint-library"></a>Instalar [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] desde un portal web o una biblioteca de SharePoint 
  
 Puede iniciar el [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] desde un portal web de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o desde un sitio de SharePoint integrado con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para obtener información, vea [Iniciar el Generador de informes](../../reporting-services/report-builder/start-report-builder.md).  
  
### <a name="sharepoint-site-integrated-with-includessrsnoversionincludesssrsnoversion-mdmd"></a>Sitio de SharePoint integrado con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]
  
 En un sitio de SharePoint integrado con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], si en el menú **Nuevo documento** no aparece **Informe del Generador de informes**, **Modelo del Generador de informes**y **Orígenes de datos de informe**, será necesario agregar sus tipos de contenido a la biblioteca de SharePoint. Para obtener más información, vea [Add Reporting Services Content Types to a SharePoint Library (Agregar los tipos de contenido de Reporting Services a una biblioteca de SharePoint)](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).  
 
## <a name="install-includessrbnoversionincludesssrbnoversion-mdmd-with-system-center-configuration-manager"></a>Instalar [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] con System Center Configuration Manager 
  
 Un administrador también puede usar software como System Center Configuration Manager para insertar el programa en su equipo. Para obtener información sobre la forma de usar software específico para instalar el [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)], consulte la documentación del software. Para más información, consulte el [sitio de System Center Configuration Manager](https://www.microsoft.com/en-us/cloud-platform/system-center-configuration-manager).  
  
> [!IMPORTANT]  
>  Las características de seguridad de Windows Vista y Windows 7 exigen permisos elevados para ejecutar operaciones de línea de comandos y solicitarán permiso para ejecutar la línea de comandos. La instalación no es silenciosa. Para que la instalación sea silenciosa, es necesario ejecutar la línea de comandos como administrador.  
  
## <a name="system-requirements"></a>Requisitos del sistema
  
 Consulte la sección **System Requirements** (Requisitos del sistema) en la [página de descarga del Generador de informes](http://go.microsoft.com/fwlink/?LinkID=734968) en el Centro de descarga de Microsoft.
  
##  <a name="download"></a> Para instalar el [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] desde el sitio de descarga  
  
1.  En la [página del Generador de informes del Centro de descarga de Microsoft](http://go.microsoft.com/fwlink/?LinkID=734968) , haga clic en **Download**(Descargar).  
  
2.  Cuando haya acabado la descarga del [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] , haga clic en  **Ejecutar**.  
  
     De este modo se inicia el Asistente para el [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] de SQL Server.  
  
3.  Acepte los términos del contrato de licencia y haga clic en **Siguiente**.  
  
4.  En la página **Servidor de destino predeterminado** , puede especificar la dirección URL al servidor de informes de destino si difiere del valor predeterminado. Haga clic en **Siguiente**.  
  
    > [!NOTE]  
    >  Si tiene previsto trabajar con el [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] cuando esté conectado a un servidor de informes, conviene que especifique en este momento la dirección URL al servidor. También puede hacerlo desde el cuadro de diálogo **Opciones** del [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)].  
  
5.  Haga clic en **Instalar** para completar la instalación del [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)].  
  
## <a name="to-install-includessrbnoversionincludesssrbnoversion-mdmd-from-a-share"></a>Para instalar el [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] desde un recurso compartido  
  
1.  Póngase en contacto con el administrador para obtener información sobre la ubicación del archivo ReportBuilder3.msi que necesitará ejecutar para instalar el [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] en el equipo local.  
  
2.  Busque el archivo ReportBuilder3.msi, el paquete de Windows Installer (MSI) para [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]y haga clic en él.  
  
     De este modo se inicia el Asistente para el [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] de SQL Server.  
  
3.  Complete el resto de los pasos de [To install Report Builder from the download site](#download).  
  
## <a name="to-install-includessrbnoversionincludesssrbnoversion-mdmd-from-the-command-line"></a>Para instalar el [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] desde la línea de comandos 

 También puede realizar una instalación de línea de comandos del [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] y especificar argumentos para personalizar la instalación. Además de los parámetros estándar intrínsecos de MSI, puede usar los parámetros personalizados que proporciona el [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] : RBINSTALLDIR y REPORTSERVERURL. RBINSTALLDIR especifica la carpeta de instalación raíz para el [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]. REPORTSERVERURL especifica el servidor de informes predeterminado que usa el [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] para guardar los informes en el servidor.  
  
 Si quiere realizar una instalación completamente silenciosa, sin ninguna interacción con la interfaz de usuario, especifique la opción **/quiet** . Por diseño, la marca de la opción quiet suprime los errores de instalación. Por lo tanto, es recomendable que, cuando use la opción quiet, incluya la opción **/l** que especifica el registro.   
  
1.  En la [página del Generador de informes del Centro de descarga de Microsoft](http://go.microsoft.com/fwlink/?LinkID=734968), haga clic en **Download**(Descargar).  
  
2.  Después de haya acabado la descarga del [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] , haga clic en  **Guardar**.  
  
3.  En el menú **Inicio** , haga clic en **Ejecutar**.  
  
4.  En el cuadro **Abrir** , escriba **cmd.**  
  
5.  En la ventana del símbolo del sistema, vaya a la carpeta en la que haya guardado ReportBuilder3.msi.  
  
6.  Escriba un comando con el formato siguiente:  
  
     `msiexec/i ReportBuilder3.msi /option [value] [/option [value]]`  
  
     Las dos opciones específicas para la instalación del [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] son: RBINSTALLDIR y REPORTSERVERURL. No hace falta que incluya estos argumentos en la línea de comandos. El siguiente es el comando de línea base:  
  
     `msiexec /i ReportBuilder3_x86.msi /quiet`  
  
7.  Para ejecutar el comando, pulse ENTRAR.  
  
## <a name="set-includessrbnoversionincludesssrbnoversion-mdmd-defaults"></a>Establecer los valores predeterminados del [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]  
  
-   Después de instalar el [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)], puede establecer algunas opciones predeterminadas. Haga clic en **Archivo** > **Opciones**.  
  
     Lo más útil es establecer el portal web de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o el sitio de SharePoint predeterminados. Para obtener más información, consulte [Set default options for Report Builder](../../reporting-services/report-builder/set-default-options-for-report-builder.md).  
  
-   Haga clic en **Generador de informes** .  
  
     Si no ve el servidor de informes en la lista de servidores existentes, cierre el cuadro de diálogo **Abrir informe** y haga clic en **Conectar** en la parte inferior del [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] para conectarse al servidor.  
  
## <a name="see-also"></a>Ver también  
 [Iniciar el Generador de informes](../../reporting-services/report-builder/start-report-builder.md)   
 [Desinstalación del Generador de informes](../../reporting-services/install-windows/uninstall-report-builder.md)  
  
  
