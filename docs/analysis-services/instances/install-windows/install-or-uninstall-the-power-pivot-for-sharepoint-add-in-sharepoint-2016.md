---
title: Instalar o desinstalar el PowerPivot para SharePoint complemento (SharePoint 2016) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 34dd07b8-d59d-49ce-bad0-74f40e4db0b8
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1dbd22c1c09de66200cda7300f34666ea453777a
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2016"></a>Instalar o desinstalar el complemento Power Pivot para SharePoint (SharePoint 2016)
  [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] es una colección de componentes de servidor de aplicaciones y servicios back-end que proporcionan acceso a datos de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] en una granja de [!INCLUDE[SPS2016](../../../includes/sps2016-md.md)] . El complemento [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint (**spPowerpivot16.msi**) es un paquete del instalador que se usa para instalar los componentes de servidor de aplicaciones.  
  
 **Nota** : En este tema se describe la instalación de los archivos de solución de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] y de la herramienta de configuración de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2016. Una vez efectuada la instalación, consulte el siguiente tema para obtener información sobre la herramienta de configuración y otras características adicionales: [Configuración de Power Pivot e implementación de soluciones &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md).  
  
 Para obtener información sobre cómo descargar **spPowerPivot16.msi**, consulte [Microsoft® SQL Server® 2016 Power Pivot® de Microsoft SharePoint®](https://www.microsoft.com/download/details.aspx?id=52675).  
  
 **En este tema:**  
  
-   [Información previa](#bkmk_background)  
  
-   [¿Dónde instalar spPowerPivot16.msi?](#bkmk_where_to_install)  
  
-   [Requisitos y requisitos previos](#bkmk_prereq)  
  
-   [Para instalar Power Pivot para SharePoint](#bkmk_install)  
  
-   [Implementar los archivos de solución de SharePoint con la Herramienta de configuración de Power Pivot para SharePoint 2016](#bkmk_deploy_solution)  
  
-   [Desinstalar o reparar el complemento](#bkmk_remove_addin)  
  

**[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2016 
  
##  <a name="bkmk_background"></a> Información previa  
  
-   **Servidor de aplicaciones:** [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] en SharePoint 2016 incluye el uso de libros como un origen de datos, actualización de datos programada y el Panel de administración de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
     [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] es un paquete de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Installer (**spPowerpivot16.msi**) que implementa las bibliotecas cliente de Analysis Services y copia los archivos de instalación de [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] al equipo. El instalador no implementa ni configura características de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] en SharePoint. Se instalan los componentes siguientes de manera predeterminada:  
  
    -   [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)]. Este componente incluye scripts de PowerShell (archivos .ps1), paquetes de solución de SharePoint (.wsp) y la herramienta de configuración de [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] para implementar [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] en una granja de servidores de SharePoint 2016.  
  
    -   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Proveedor OLE DB para Analysis Services (MSOLAP).  
  
    -   Proveedor de datos de ADOMD.NET.  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Analysis Management Objects.  
  
-   **Servicios back-end** : si usa [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel con el fin de crear libros que contengan datos analíticos, debe tener Office Online Server configurado con un servidor de BI que ejecute [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en modo de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para obtener acceso a esos datos en un entorno de servidor. Puede ejecutar el programa de instalación de SQL Server en un equipo que tenga instalado SharePoint Server 2016 o en un equipo diferente que no tenga ningún software de SharePoint. Analysis Services no tiene ninguna dependencia en SharePoint.  
  
     Para obtener información acerca de la instalación, la desinstalación y la configuración de los servicios back-end, vea lo siguiente:  
  
    -   [Instalación de Analysis Services en el modo PowerPivot](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
    -   [Desinstalar Power Pivot para SharePoint](../../../sql-server/install/uninstall-power-pivot-for-sharepoint.md)  
  
##  <a name="bkmk_where_to_install"></a> ¿Dónde instalar spPowerPivot16.msi?  
 Se recomienda instalar **spPowerPivot16.msi** en todos los servidores de la granja de servidores de SharePoint para mantener la coherencia de la configuración, incluidos los servidores de aplicaciones y los servidores front-end web. El paquete del instalador incluye los proveedores de datos de Analysis Services y la herramienta de configuración de [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] . Al instalar **spPowerPivot16.msi** puede personalizar la instalación si excluye los componentes individuales.  
  
 **Proveedores de datos** : varias tecnologías de SharePoint y SQL Server usan los proveedores de datos de Analysis Services, incluidos PerformancePoint Services y Power View. La instalación de **spPowerPivot16.msi** en todos los servidores de SharePoint asegura que todo el conjunto de proveedores de datos de Analysis Services y la conectividad de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] están disponibles de forma coherente en toda la granja de servidores.  
  
> [!NOTE]  
>  Debe instalar los proveedores de datos de Analysis Services en un servidor de SharePoint 2016 mediante **spPowerPivot16.msi**. No se admiten otros paquetes del instalador disponibles en el Feature Pack de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] porque estos paquetes no incluyen los archivos auxiliares de SharePoint 2016 que los proveedores de datos necesitan en este entorno.  
  
 **Herramienta de configuración** : la herramienta de configuración de [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] solo es necesaria en uno de los servidores de SharePoint. Sin embargo, en granjas con varios servidores se recomienda instalar la herramienta de configuración al menos en dos servidores para poder tener acceso a dicha herramienta si uno de los dos servidores está sin conexión.  
  
##  <a name="bkmk_prereq"></a> Requisitos y requisitos previos  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SharePoint Server 2016.  
  
-   **spPowerPivot16.msi** solo es de 64 bits, de acuerdo con los requisitos de los productos y tecnologías de SharePoint.  
  
-   Un servidor en [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] modo. Office Online Server usará la instancia de SQL Server Analysis Services como un servidor de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Analysis Services se puede ejecutar en el servidor local de SharePoint o en un equipo remoto. No se puede instalar en Office Online Server.  
  
-   **Permisos:** para instalar [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)], el usuario actual debe ser administrador del equipo y pertenecer al grupo de administradores de la granja de servidores de SharePoint.  
  
-   Para obtener más información sobre los requisitos y los requisitos previos de [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] , vaya a [Requisitos de hardware y software para el servidor de Analysis Services en modo de SharePoint](http://msdn.microsoft.com/library/fb86ca0a-518c-4c61-ae78-7680c57fae1f).  
  
##  <a name="bkmk_install"></a> Para instalar Power Pivot para SharePoint  
 El paquete del instalador **spPowerpivot16.msi** admite tanto una interfaz gráfica de usuario como un modo de línea de comandos. Ambos métodos de instalación necesitan que se ejecute el archivo .msi con privilegios de administrador. Una vez efectuada la instalación, consulte el siguiente tema para obtener información sobre la herramienta de configuración y otras características adicionales: [Configuración de Power Pivot e implementación de soluciones &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md).  
  
### <a name="user-interface-installation"></a>Instalación mediante la interfaz de usuario  
 Para instalar [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] con la interfaz gráfica de usuario, complete los pasos siguientes:  
  
1.  Ejecute **spPowerPivot16.msi**.  
  
2.  En la página de bienvenida, seleccione **Siguiente** .  
  
3.  Examine y acepte el contrato de licencia y después seleccione **Siguiente**.  
  
4.  En la página **Selección de características** , todas las características están seleccionadas de forma predeterminada.  
  
5.  Seleccione **Siguiente**.  
  
6.  Seleccione **Instalar** para finalizar la instalación.  
  
### <a name="command-line-installation"></a>Instalación desde la línea de comandos  
 Para realizar una instalación desde la línea de comandos, abra un símbolo del sistema con permisos administrativos y después ejecute **spPowerPivot16.msi**. Por ejemplo:  
  
 `Msiexec.exe /i spPowerPivot16.msi`.  
  
 Para crear un registro de instalación, use los modificadores de registro de MsiExec estándar. En el ejemplo siguiente se crea el archivo de registro “Install_Log.txt” mediante el modificador de registro detallado “v”.  
  
```  
Msiexec.exe /i spPowerPivot16.msi /L v c:\test\Install_Log.txt  
```  
  
### <a name="quiet-command-line-installation-for-scripting"></a>Instalación silenciosa desde la línea de comandos para scripting  
 Puede usar los modificadores **/q** o **/quiet** para realizar una instalación "silenciosa" que no mostrará cuadros de diálogos ni advertencias. La instalación silenciosa es útil si desea incluir en el script la instalación del complemento.  
  
> [!IMPORTANT]  
>  Si usa el modificador **q** para una instalación silenciosa desde la línea de comandos, el contrato de licencia para el usuario final no se mostrará. Independientemente del método de instalación, el uso de este software se rige por un contrato de licencia y usted es responsable de su cumplimiento.  
  
 **Para realizar una instalación silenciosa:**  
  
1.  Abra un símbolo del sistema **con permisos de administrador**.  
  
2.  Ejecute el siguiente comando:  
  
    ```  
    Msiexec.exe /i spPowerPivot16.msi /q  
    ```  
  
### <a name="command-line-installation-to-include-specific-components"></a>Instalación desde la línea de comandos para incluir componentes específicos  
 La herramienta de configuración de [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] no se necesita en todos los servidores de SharePoint, pero se recomienda instalarla al menos en dos servidores para que la herramienta de configuración esté disponible cuando se necesite.  
  
 Al instalar spPowerPivot16.msi, puede usar las opciones de la línea de comandos para instalar elementos específicos, como los proveedores de datos, pero no la herramienta de configuración de [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] . La siguiente línea de comandos es un ejemplo de cómo instalar todos los componentes salvo la herramienta de configuración:  
  
```  
Msiexec /i spPowerPivot16.msi AGREETOLICENSE="yes" ADDLOCAL=” SQL_OLAPDM,SQL_ADOMD,SQL_AMO,SQLAS_SP_Common”  
```  
  
|Opción|Descripción|  
|------------|-----------------|  
|Analysis_Server_SP_addin16|[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] Configuración|  
|SQL_OLAPDM|Proveedor OLE DB de Analysis Services para SQL Server 2016|  
|SQL_ADOMD|Proveedor de ADOMD.NET|  
|SQL_AMO|Proveedor de Objetos de administración de análisis (AMO) de SQL Server 2016|  
|SQLAS_SP16_Common|Componentes comunes de Analysis Services para SharePoint 2016|  
  
##  <a name="bkmk_deploy_solution"></a> Implementar los archivos de solución de SharePoint con la Herramienta de configuración de Power Pivot para SharePoint 2016  
 Tres de los archivos copiados al disco duro por spPowerPivot16.msi son archivos de solución de SharePoint. El ámbito de un archivo de solución es el nivel de aplicación web, mientras que el ámbito de los demás archivos es el nivel de granja. Los archivos son los siguientes:  
  
-   `PowerPivot16FarmSolution.wsp`  

-   `PowerPivot16WebApplicationSolution.wsp`  
  
 Los archivos de solución se copian a la siguiente carpeta:  
  
 `ssInstallPathTools\PowerPivotTools\SPAddinConfiguration\Resources`  
  
 Después de la instalación .msi, ejecute la Herramienta de configuración de [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] para configurar e implementar las soluciones de la granja de servidores de SharePoint.  
  
 **Para iniciar la herramienta de configuración:**  
  
 En la pantalla Inicio de Windows, escriba "power" y en los resultados de la búsqueda de Aplicaciones, seleccione **Configuración de [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)]**. Tenga en cuenta que los resultados de la búsqueda pueden incluir dos vínculos porque el programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instala distintas herramientas de configuración de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013 y SharePoint 2016. Asegúrese de iniciar la herramienta de configuración de [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] .  
  
 ![PowerPivot para SharePoint 2016](../../../analysis-services/instances/install-windows/media/powerpivot-for-sharepoint-2016-configuration.png "PowerPivot para SharePoint 2016")  
  
 **Or**  
  
1.  Vaya a **Iniciar**, **Todos los programas**.  
  
2.  Seleccione [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)].  
  
3.  Seleccione **Herramientas de configuración**.  
  
4.  En la página de bienvenida, seleccione **[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] Configuración**.  
  
 Para obtener más información acerca de la herramienta de configuración, vea [Power Pivot Configuration Tools](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
##  <a name="bkmk_remove_addin"></a> Desinstalar o reparar el complemento  
  
> [!CAUTION]  
>  Si desinstala **spPowerPivot16.msi** , se desinstalarán los proveedores de datos y la herramienta de configuración. La desinstalación de los proveedores de datos puede provocar que el servidor no pueda conectarse a [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)].  
  
 Puede desinstalar o reparar [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] mediante uno de los métodos siguientes:  
  
1.  **Panel de control de Windows:** seleccione [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]**[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)]**. Seleccione **Desinstalar** o **Reparar**.  
  
2.  Ejecute spPowerPivot16.msi y seleccione la opción **Quitar** o la opción **Reparar** .  
  
 **Línea de comandos:** para reparar o desinstalar [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] mediante la línea de comandos, abra un símbolo del sistema **con permisos de administrador** y ejecute uno de los comandos siguientes:  
  
-   Para reparar, ejecute el siguiente comando:  
  
    ```  
    msiexec.exe /f spPowerPivot16.msi  
    ```  
  
 o  
  
-   Para desinstalar, ejecute el siguiente comando:  
  
    ```  
    msiexec.exe /uninstall spPowerPivot16.msi  
    ```  
  
  

