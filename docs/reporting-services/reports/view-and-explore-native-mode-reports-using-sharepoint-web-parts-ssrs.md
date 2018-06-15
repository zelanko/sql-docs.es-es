---
title: Ver y explorar los informes en modo nativo usando elementos web de SharePoint (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: reports
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: dee8ee42-156b-43b6-b202-02dfb9404284
caps.latest.revision: 9
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 1072350a30a5f28ac16cda48f72720a383012d02
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33028242"
---
# <a name="view-and-explore-native-mode-reports-using-sharepoint-web-parts-ssrs"></a>Ver y explorar los informes en modo nativo usando elementos web de SharePoint (SSRS)

> [!IMPORTANT]  
>  SQL Server Reporting Services ya no admite el uso de elementos web (RSWebParts.cab) en modo nativo para tener acceso al contenido del servidor de informes en un sitio de SharePoint desde un servidor de informes en modo nativo. Use el [elemento web Visor de informes en un sitio de SharePoint](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md) en su lugar.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona varios elementos web que funcionan con versiones específicas de un servidor de informes y en determinados modos de implementación.  
  
-   **Modo nativo:** si desea tener acceso al contenido del servidor de informes en un sitio de SharePoint desde un servidor de informes en modo nativo, use el Explorador de informes de los elementos web de SharePoint 2.0 incluidos con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. En este tema se proporcionan instrucciones para instalar y usar los elementos web de la versión 2.0.  
  
-   **Modo de SharePoint:** si quiere tener acceso a un servidor de informes que se ejecuta en modo de SharePoint, use los elementos web que instala el complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para los productos de SharePoint. Para más información sobre el complemento, vea [Dónde encontrar el complemento Reporting Services para Productos de SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
> [!NOTE]  
>  El elemento web del visor de informes para el modo nativo (SPViewer.dwp) es un elemento web diferente del que instala el complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para productos de SharePoint (ReportViewer.dwp). Los elementos web tienen implementaciones y esquemas diferentes pero ambos pueden instalarse en la misma granja de SharePoint. Visualmente, puede distinguir los dos elementos web mediante la siguiente característica: el elemento web Visor de informes que se instala mediante el complemento tiene el menú **Acciones** en la barra de herramientas.  
  
 Para más información sobre los modos del servidor de informes, vea [Servidor de informes de Reporting Services](../../reporting-services/report-server-sharepoint/reporting-services-report-server.md).  
  
 En este tema:  
  
-   [Acerca del Explorador de informes y el Visor de informes](#bkmk_aboutwebparts)  
  
-   [Requisitos para usar los elementos web](#bkmk_requirements)  
  
-   [Instalar elementos web](#bkmk_installingwebparts)  
  
-   [Agregar y configurar elementos web](#bkmk_configurewebparts)  
  
##  <a name="bkmk_aboutwebparts"></a> Acerca del Explorador de informes y el Visor de informes  
 El Explorador de informes y el Visor de informes son elementos web de SharePoint 2.0 que se presentaron con el Service Pack 2 (SP2) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y siguen estando disponibles en las versiones actuales.  
  
 Los elementos web proporcionan un método para ver informes y explorar la jerarquía de carpetas del servidor de informes desde un sitio de SharePoint.  
  
 Tenga en cuenta que no se admite la personalización de elementos web. Los elementos web se usan tal cual y no se pueden extender ni modificar.  
  
-   El**Explorador de informes** (SPExplorer.dwp) se conecta al Administrador de informes en el equipo con el servidor de informes. Puede buscar informes disponibles en un servidor de informes y suscribirse a informes individuales. Si el Generador de informes está habilitado y tiene permisos suficientes, puede iniciar el Generador de informes desde el elemento web Explorador de informes.  
  
     El Explorador de informes muestra el contenido de una carpeta mediante una página del Administrador de informes. El acceso a los elementos y carpetas individuales en la jerarquía de carpetas del servidor de informes se controla mediante asignaciones de roles en el servidor de informes. Al seleccionar un informe, se abre en una ventana nueva del explorador. El Visor de HTML del servidor de informes muestra el informe y proporciona la barra de herramientas de informe, pero no el elemento web Visor de informes. Si desea personalizar la configuración de la barra de herramientas, asegúrese de especificar los parámetros de acceso a la dirección URL en el servidor de informes. Para obtener instrucciones, vea [Referencia de parámetros de acceso URL](../../reporting-services/url-access-parameter-reference.md).  
  
-   El**Visor de informes** (SPViewer.dwp) muestra un informe y proporciona una barra de herramientas que puede usar para navegar por las páginas, buscar contenido o exportar el informe. Puede agregar el elemento web Visor de informes a una página de elementos web para mostrar siempre un informe específico en dicha página o **puede conectarlo con el Explorador de informes** para mostrar informes abiertos mediante el elemento web.  
  
##  <a name="bkmk_requirements"></a> Requisitos para usar los elementos web  
 Los requisitos para usar los elementos web Visor de informes y Explorador de informes son:  
  
-   Las versiones admitidas de productos y tecnologías de SharePoint incluyen:  
  
    -   [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 y [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007.  
  
    -   [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] y [!INCLUDE[SPS2010](../../includes/sps2010-md.md)].  
  
-   La versión del servidor de informes en modo nativo debe ser [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o posterior.  
  
-   El servidor de informes se debe ejecutar en modo nativo. **No puede** usar los elementos web del Visor de informes y el Explorador de informes para conectarse a informes o verlos en un servidor de informes que se ejecute en el modo de SharePoint.  
  
-   El Administrador de informes debe estar instalado.  
  
 Los elementos web Explorador de informes y Visor de informes se distribuyen mediante un archivo .cab incluido con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Las instrucciones para instalar, configurar y usar los elementos web se proporcionan en las siguientes secciones de este tema.  
  
##  <a name="bkmk_installingwebparts"></a> Instalar elementos web  
 Los elementos web se suministran a un servidor de SharePoint como un archivo .CAB. Ejecute la herramienta Stsadm.exe de SharePoint en el archivo .cab desde la línea de comandos para instalar los elementos web. Para obtener más información acerca de la herramienta y la implementación de elementos web, vea la documentación de SharePoint.  
  
#### <a name="install-web-parts-using-powershell"></a>Instalar elementos web con PowerShell  
  
1.  Copie el archivo **RSWebParts.cab** en una carpeta del servidor de SharePoint. Puede copiarlo en cualquier carpeta del servidor de SharePoint y, a continuación, eliminarlo una vez instalados los elementos web. De manera predeterminada, SQL Server 2014 Reporting Services y las versiones anteriores instalan el archivo RSWebParts.cab en la siguiente carpeta:  
  
    ```  
    C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Reporting Services\SharePoint  
    ```  
  
2.  En el equipo que tenga la instalación del producto de SharePoint, abra el **Shell de administración de SharePoint 2010** con **privilegios de administrador**.  
  
3.  Ejecute el siguiente comando de PowerShell:  
  
    ```  
    Install-SPWebPartPack -LiteralPath "C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Reporting Services\SharePoint\RSWebParts.cab" -GlobalInstall  
    ```  
  
4.  Debería ver un mensaje similar al siguiente, que indica que el elemento web se implementó.  
  
    > Nombre               Id. solución                                             Implementado  
  
    > ----                    ----------                                              -------\-  
  
    > rswebparts.cab    00000000-0000-0000-0000-000000000000     True  
  
     Para más información sobre cómo usar PowerShell, consulte [Install-SPWebPartPack (http://technet.microsoft.com/library/ff607840.aspx)](http://technet.microsoft.com/library/ff607840.aspx).  
  
#### <a name="install-web-parts-using-stsadmexe"></a>Instalar elementos web con STSADM.exe  
  
1.  Copie el archivo **RSWebParts.cab** en la misma ubicación en el servidor de SharePoint descrita en la sección PowerShell de este documento.  
  
2.  En el equipo en que esté instalado el producto de SharePoint, abra una ventana de símbolo del sistema con privilegios de administrador y navegue hasta la carpeta que contenga la herramienta **Stsadm.exe** . La ruta de acceso predeterminada de [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] es la siguiente:  
  
    > C:\Archivos de programa\Common Files\Microsoft Shared\Web Server Extensions\14\BIN.  
  
3.  Ejecute Stsadm.exe en el archivo .cab con la siguiente sintaxis:  
  
    ```  
    STSADM.EXE -o addwppack -filename "C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Reporting Services\SharePoint\RSWebParts.cab" -globalinstall  
    ```  
  
4.  Debería recibir un mensaje que indique que la operación se completó correctamente.  
  
     Al especificar `-globalinstall` , se agregan los elementos web a la caché de ensamblados global (GAC). Este paso es necesario si desea conectar los elementos web.  
  
##  <a name="bkmk_configurewebparts"></a> Agregar y configurar elementos web  
 Una vez instalados los elementos web, puede agregarlos a una o a varias páginas en un sitio de SharePoint. El usuario debe tener permiso para crear sitios web y agregar contenido.  
  
 El procedimiento siguiente agregará ambos elementos web a una página y, después, conectará el Explorador de informes y el Visor de informes de modo que, cuando haga clic en un informe en el Explorador de informes, se mostrará dentro del Visor de informes.  
  
#### <a name="add-report-viewer"></a>Agregar el Visor de informes  
  
1.  En Acciones del sitio, haga clic en **Editar página**.  
  
2.  En una zona de la página, haga clic en **Agregar elemento web**.  
  
3.  En el cuadro de diálogo **Agregar elementos web** , desplácese a la categoría **Varios** .  
  
4.  Seleccione **Visor de informes**.  
  
    > [!WARNING]  
    >  No seleccione **Visor de informes de SQL Server Reporting Services** . Ese elemento web se registra al instalar el Complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para productos de SharePoint y se usa para ejecutar un servidor de informes en modo de SharePoint. No se puede usar para ver informes en un servidor de informes en modo nativo.  
  
5.  Haga clic en **Agregar**.  
  
6.  Mientras la página está en el modo de edición, haga clic en **Editar elemento web** en el elemento web Visor de informes.  
  
7.  En **Report Manager URL**, escriba una dirección URL a una instancia del Administrador de informes asociada al servidor de informes en modo nativo al que desea tener acceso. De manera predeterminada, la dirección URL del Administrador de informes tiene la siguiente sintaxis: **http://\<nombreDeServidor>/informes**.  
  
8.  En **Ruta de acceso del informe**, especifique una barra diagonal, seguida de la ruta de acceso a la carpeta y el nombre del informe. **No** incluya el nombre del servidor ni el directorio virtual del Administrador de informes. Por ejemplo, para abrir el informe "Company Sales" de la carpeta Adventure Works, especifique **/Adventure Works/Company Sales**. Aquí se proporciona otro ejemplo en el que el informe "Products" está en la carpeta raíz del servidor de informes **/Products**.  
  
9. Haga clic en **Aceptar**.  
  
#### <a name="add-report-explorer-and-connect-to-report-viewer"></a>Agregar el Explorador de informes y conectarse al Visor de informes  
  
1.  En otra zona de la página, haga clic en **Agregar un elemento web** y, en la carpeta Varios haga clic en **Explorador de informes** y haga clic en **Agregar**.  
  
2.  En el menú contextual Elemento web del Explorador de informes, haga clic en **Editar elemento web**.  
  
3.  En **Report Manager URL**, escriba una dirección URL a una instancia del Administrador de informes asociada al servidor de informes en modo nativo al que desea tener acceso.  
  
4.  Además, puede establecer la **Ruta de inicio**. La ruta de inicio es una carpeta de la jerarquía de carpetas del servidor de informes. Puede especificar una ruta de inicio si desea que la página predeterminada sea una carpeta en una posición inferior en la jerarquía de carpetas. La ruta debe comenzar con una barra diagonal. Debe especificar una ruta de acceso completa que empiece por el nodo raíz de la jerarquía de carpetas del servidor de informes, pero que no incluya el nombre del servidor ni el directorio virtual del Administrador de informes. Por ejemplo, para abrir una carpeta llamada Adventure Works justo debajo del nodo raíz, especifique **/Adventure Works** en la ruta de inicio.  
  
5.  Haga clic en **Aceptar**.  
  
6.  El explorador de informes mostrará una lista de los elementos de informes del servidor de informes. De forma predeterminada, si hace clic en el nombre de un informe, abrirá un informe en una nueva ventana. Complete los pasos siguientes si desea conectar el Explorador de informes al Visor de informes de modo que, cuando haga clic en un nombre de informe en el Explorador de informes, se muestra en el Visor de informes.  
  
    1.  En el menú contextual del Explorador de informes, haga clic en **Conexiones**.  
  
    2.  Haga clic en **Mostrar informe en**.  
  
    3.  Haga clic en **Visor de informes**.  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
