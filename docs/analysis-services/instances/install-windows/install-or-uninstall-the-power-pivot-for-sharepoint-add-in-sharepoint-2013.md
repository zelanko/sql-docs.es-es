---
title: "Instalar o desinstalar el complemento Power Pivot para SharePoint (SharePoint 2013) | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fe13ce8b-9369-4126-928a-9426f9119424
caps.latest.revision: 28
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 28
---
# Instalar o desinstalar el complemento Power Pivot para SharePoint (SharePoint 2013)
  [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] es una colección de componentes de servidor de aplicaciones y servicios back-end que ofrecen acceso a datos de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] en una granja de [!INCLUDE[SPS2013](../../../includes/sps2013-md.md)]. El complemento [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint (**spPowerpivot.msi**) es un paquete de instalación que se usa para instalar los componentes de servidor de aplicaciones.  
  
-   El complemento no es necesario para las implementaciones de SharePoint 2010.  
  
-   El complemento no es obligatorio en una implementación de servidor única que incluya SharePoint 2013 y [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en modo de SharePoint. Los componentes que instala el complemento se incluyen al instalar un servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en modo de SharePoint. Para ver diagramas de implementaciones de ejemplo con el complemento, vea [Topologías de implementación para las características BI de SQL Server en SharePoint](../Topic/Deployment%20Topologies%20for%20SQL%20Server%20BI%20Features%20in%20SharePoint.md).  
  
 **Nota** : en este tema se describe la instalación de los archivos de solución de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] y de la herramienta de configuración de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013. Una vez efectuada la instalación, vea el siguiente tema para obtener información sobre la herramienta de configuración y otras características adicionales: [Configuración de PowerPivot e implementación de soluciones &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md).  
  
 Para obtener información sobre cómo descargar **spPowerPivot.msi**, consulte [Microsoft® SQL Server® 2014 Power Pivot® para Microsoft SharePoint®](http://go.microsoft.com/fwlink/?LinkID=324854).  
  
 **En este tema:**  
  
-   [Información previa](#bkmk_background)  
  
-   [¿Dónde instalar spPowerPivot.msi?](#bkmk_where_to_install)  
  
-   [Requisitos y requisitos previos](#bkmk_prereq)  
  
-   [Para instalar Power Pivot para SharePoint](#bkmk_install)  
  
-   [Implementar los archivos de solución de SharePoint con la Herramienta de configuración de Power Pivot para SharePoint 2013](#bkmk_deploy_solution)  
  
-   [Desinstalar o reparar el complemento](#bkmk_remove_addin)  
  
||  
|-|  
|**[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2013|  
  
##  <a name="bkmk_background"></a> Información previa  
  
-   **Servidor de aplicaciones:** [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] en SharePoint 2013 incluye el uso de libros como un origen de datos, actualización de datos programada y el Panel de administración de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
     [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] es un paquete de Windows Installer de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] (**spPowerpivot.msi**) que implementa las bibliotecas cliente de Analysis Services y copia los archivos de instalación de [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] al equipo. El instalador no implementa ni configura características de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] en SharePoint. Se instalan los componentes siguientes de manera predeterminada:  
  
    -   [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 2013. Este componente incluye scripts de PowerShell (archivos .ps1), paquetes de solución de SharePoint (.wsp) y la herramienta de configuración de [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] para SharePoint 2013 para implementar [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] en una granja de SharePoint 2013.  
  
    -   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Proveedor OLE DB para Analysis Services (MSOLAP).  
  
    -   Proveedor de datos de ADOMD.NET.  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Analysis Management Objects.  
  
-   **Servicios backend** : si usa [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel con el fin de crear libros que contienen datos analíticos, debe tener Excel Services configurado con un servidor de BI que ejecute [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en modo de SharePoint para obtener acceso a esos datos en un entorno de servidor. Puede ejecutar el programa de instalación de SQL Server en un equipo que tenga instalado SharePoint Server 2013 o en un equipo diferente que no tenga ningún software de SharePoint. Analysis Services no tiene ninguna dependencia en SharePoint.  
  
     Para obtener información acerca de la instalación, la desinstalación y la configuración de los servicios back-end, vea lo siguiente:  
  
    -   [Instalación de Analysis Services en el modo PowerPivot](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
    -   [Desinstalar Power Pivot para SharePoint](../../../sql-server/install/uninstall-power-pivot-for-sharepoint.md)  
  
##  <a name="bkmk_where_to_install"></a> ¿Dónde instalar spPowerPivot.msi?  
 Se recomienda instalar **spPowerPivot.msi** en todos los servidores de la granja de servidores de SharePoint para mantener la coherencia de la configuración, incluidos los servidores de aplicaciones y los servidores front-end web. El paquete del instalador incluye los proveedores de datos de Analysis Services y la herramienta de configuración de [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)]. Al instalar **spPowerPivot.msi** puede personalizar la instalación si excluye componentes individuales.  
  
 **Proveedores de datos** : varias tecnologías de SharePoint y SQL Server usan los proveedores de datos de Analysis Services, incluidos Excel Services, PerformancePoint Services y Power View. La instalación de **spPowerPivot.msi** en todos los servidores de SharePoint asegura que todo el conjunto de proveedores de datos de Analysis Services y la conectividad de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] están disponibles de forma coherente en toda la granja de servidores.  
  
> [!NOTE]  
>  Debe instalar los proveedores de datos de Analysis Services en un servidor de SharePoint 2013 mediante **spPowerPivot.msi**. No se admiten otros paquetes de instalador disponibles en el Feature Pack de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] porque estos paquetes no incluyen los archivos auxiliares de SharePoint 2013 que los proveedores de datos necesitan en este entorno.  
  
 **Herramienta de configuración:** la herramienta de configuración de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013 solo es necesaria en uno de los servidores de SharePoint. Sin embargo, en granjas con varios servidores se recomienda instalar la herramienta de configuración al menos en dos servidores para poder tener acceso a dicha herramienta si uno de los dos servidores está sin conexión.  
  
##  <a name="bkmk_prereq"></a> Requisitos y requisitos previos  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SharePoint Server 2013.  
  
-   **spPowerPivot.msi** solo es de 64 bits, de acuerdo con los requisitos de productos y tecnologías de SharePoint.  
  
-   Un servidor de [!INCLUDE[ssASCurrent](../../../includes/ssascurrent-md.md)] en modo de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Excel Services usará la instancia de SQL Server Analysis Services como servidor de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Analysis Services se puede ejecutar en un equipo local o remoto.  
  
-   **Permisos:** para instalar [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)], el usuario actual debe ser administrador del equipo y miembro de un grupo de administradores de la granja de servidores de SharePoint.  
  
-   Para obtener más información sobre los requisitos y los requisitos previos de [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)], vaya a [Requisitos de hardware y software para el servidor de Analysis Services en modo de SharePoint](../Topic/Hardware%20and%20Software%20Requirements%20for%20Analysis%20Services%20Server%20in%20SharePoint%20Mode.md).  
  
##  <a name="bkmk_install"></a> Para instalar Power Pivot para SharePoint  
 El paquete del instalador **spPowerpivot.msi** admite tanto una interfaz gráfica de usuario como un modo de línea de comandos. Ambos métodos de instalación necesitan que se ejecute el archivo .msi con privilegios de administrador. Una vez efectuada la instalación, vea el siguiente tema para obtener información sobre la herramienta de configuración y otras características adicionales: [Configuración de PowerPivot e implementación de soluciones &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md).  
  
### Instalación mediante la interfaz de usuario  
 Para instalar [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] con la interfaz gráfica de usuario, complete los pasos siguientes:  
  
1.  Ejecute **SpPowerPivot.msi**.  
  
2.  En la página de bienvenida, haga clic en **Siguiente** .  
  
3.  Examine y acepte el contrato de licencia y, a continuación, haga clic en **Siguiente**.  
  
4.  En la página **Selección de características** , todas las características están seleccionadas de forma predeterminada.  
  
5.  Haga clic en **Siguiente**.  
  
6.  Haga clic en **Instalar** para finalizar la instalación.  
  
### Instalación desde la línea de comandos  
 Para realizar una instalación desde la línea de comandos, abra un símbolo del sistema con permisos administrativos y ejecute **spPowerPivot.msi**. Por ejemplo:  
  
 `Msiexec.exe /i SpPowerPivot.msi`.  
  
 Para crear un registro de instalación, use los modificadores de registro de MsiExec estándar. En el ejemplo siguiente se crea el archivo de registro “Install_Log.txt” mediante el modificador de registro detallado “v”.  
  
```  
Msiexec.exe /i SpPowerPivot.msi /L v c:\test\Install_Log.txt  
```  
  
### Instalación silenciosa desde la línea de comandos para scripting  
 Puede usar los modificadores **/q** o **/quiet** para realizar una instalación "silenciosa" que no mostrará cuadros de diálogos ni advertencias. La instalación silenciosa es útil si desea incluir en el script la instalación del complemento.  
  
> [!IMPORTANT]  
>  Si usa el modificador **q** para una instalación silenciosa desde la línea de comandos, el contrato de licencia para el usuario final no se mostrará. Independientemente del método de instalación, el uso de este software se rige por un contrato de licencia y usted es responsable de su cumplimiento.  
  
 **Para realizar una instalación silenciosa:**  
  
1.  Abra un símbolo del sistema **con permisos de administrador**.  
  
2.  Ejecute el siguiente comando:  
  
    ```  
    Msiexec.exe /i spPowerPivot.msi /q  
    ```  
  
### Instalación desde la línea de comandos para incluir componentes específicos  
 La herramienta de configuración de [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] no se necesita en todos los servidores de SharePoint, pero se recomienda instalarla al menos en dos servidores para que la herramienta de configuración esté disponible cuando se necesite.  
  
 Al instalar el paquete spPowerPivot.msi puede usar las opciones de línea de comandos e instalar elementos específicos, como los proveedores de datos y no la herramienta de configuración de [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] . La siguiente línea de comandos es un ejemplo de cómo instalar todos los componentes salvo la herramienta de configuración:  
  
```  
Msiexec /i spPowerPivot.msi AGREETOLICENSE="yes" ADDLOCAL=” SQL_OLAPDM,SQL_ADOMD,SQL_AMO,SQLAS_SP_Common”  
```  
  
|Opción|Descripción|  
|------------|-----------------|  
|Analysis_Server_SP_addin|[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Configuración|  
|SQL_OLAPDM|MSOLAP|  
|SQL_ADOMD|Proveedor de ADOMD.net|  
|SQL_AMO|Proveedor AMO|  
|SQLAS_SP_Common|Componentes comunes de Analysis Services para SharePoint 2013|  
  
##  <a name="bkmk_deploy_solution"></a> Implementar los archivos de solución de SharePoint con la Herramienta de configuración de Power Pivot para SharePoint 2013  
 Tres de los archivos copiados al disco duro por spPowerPivot.msi son archivos de solución de SharePoint. El ámbito de un archivo de solución es el nivel de aplicación web, mientras que el ámbito de los demás archivos es el nivel de granja. Los archivos son los siguientes:  
  
-   `PowerPivotFarmSolution.wsp`  
  
-   `PowerPivotFarm14Solution.wsp`  
  
-   `PowerPivotWebApplicationSolution.wsp`  
  
 Los archivos de solución se copian a la siguiente carpeta:  
  
 `ssInstallPathTools\PowerPivotTools\SPAddinConfiguration\Resources`  
  
 Después de la instalación .msi, ejecute la Herramienta de configuración de [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] para configurar e implementar las soluciones de la granja de servidores de SharePoint.  
  
 **Para iniciar la herramienta de configuración:**  
  
 En la pantalla de inicio de Windows, escriba "power" y en los resultados de la búsqueda de Aplicaciones, haga clic en **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013**. Tenga en cuenta que los resultados de la búsqueda pueden incluir dos vínculos porque el programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instala distintas herramientas de configuración de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2010 y SharePoint 2013. Asegúrese de iniciar la herramienta de configuración de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013.  
  
 ![dos herramientas de configuración de PowerPivot](../../../analysis-services/instances/install-windows/media/as-powerpivot-configtools-bothicons.gif "dos herramientas de configuración de PowerPivot")  
  
 **o**  
  
1.  Vaya a **Iniciar**, **Todos los programas**.  
  
2.  Haga clic en [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)].  
  
3.  Haga clic en **Herramientas de configuración**.  
  
4.  Haga clic en **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013**.  
  
 Para obtener más información acerca de la herramienta de configuración, vea [Power Pivot Configuration Tools](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
##  <a name="bkmk_remove_addin"></a> Desinstalar o reparar el complemento  
  
> [!CAUTION]  
>  Si desinstala **spPowerPivot.msi** , se desinstalarán los proveedores de datos y la herramienta de configuración. La desinstalación de los proveedores de datos puede provocar que el servidor no pueda conectarse a [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)].  
  
 Puede desinstalar o reparar [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] mediante uno de los métodos siguientes:  
  
1.  **Panel de control de Windows:** seleccione [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]**[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013**. Haga clic en **Desinstalar** o en **Reparar**.  
  
2.  Ejecute el paquete spPowerPivot.msi y seleccione la opción **Quitar** o la opción **Reparar** .  
  
 **Línea de comandos:** para reparar o desinstalar [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013 mediante la línea de comandos, abra un símbolo del sistema **con permisos de administrador** y ejecute uno de los comandos siguientes:  
  
-   Para reparar, ejecute el siguiente comando:  
  
    ```  
    msiexec.exe /f spPowerPivot.msi  
    ```  
  
 O BIEN  
  
-   Para desinstalar, ejecute el siguiente comando:  
  
    ```  
    msiexec.exe /uninstall spPowerPivot.msi  
    ```  
  
  