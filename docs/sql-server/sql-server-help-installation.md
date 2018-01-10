---
title: Visor de Ayuda y contenido de ayuda de SQL Server | Microsoft Docs
ms.custom: 
ms.date: 12/15/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-non-specified
ms.technology: server-general
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2014
- SQL Server 2016
- SQL Server 2017
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
caps.latest.revision: "8"
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 679d0fb003a8a59185d860a125cfdd8b5601367c
ms.sourcegitcommit: f2fde1c324466530f92006561a9a29decb711e1b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2017
---
# <a name="sql-server-offline-help-and-help-viewer"></a>Visor de Ayuda y ayuda sin conexión de SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Puede usar el Visor de Ayuda en SQL Server Management Studio (SSMS) o Visual Studio (VS) para descargar e instalar paquetes de ayuda de SQL Server de orígenes en línea o de un disco para poder verlos sin conexión. En este artículo se describen las herramientas para instalar el Visor de Ayuda, cómo instalar contenido de ayuda sin conexión y cómo ver la ayuda para [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)], SQL Server 2016 y SQL Server 2017.

> [!NOTE]
> Las ayudas de SQL Server 2016 y 2017 están combinadas, aunque algunos temas solo se aplican a una versión. Esto se indica en dichos temas. La mayoría de los temas se aplican a ambas versiones.

## <a name="install-the-help-viewer"></a>Instalar el Visor de Ayuda

El Visor de Ayuda tiene dos versiones: la versión 2.x es compatible con la ayuda de SQL Server 2016 y 2017, mientras que la versión 1.x es compatible con la ayuda de [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)]. El Visor de Ayuda no admite la configuración del proxy ni tampoco el formato ISO. 

El Visor de Ayuda se puede instalar con las siguientes herramientas: 

|**Herramienta que instala el Visor de Ayuda**|**Versión del Visor de Ayuda que se instala**|
|---------|---------|
|[SQL Server Management Studio 17.x](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)| v2.2|
|[SQL Server Data Tools para Visual Studio 2015](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)| v2.2|
|Visual Studio 2017* | v2.3|
|Visual Studio 2015 | v2.2|
|SQL Server 2014 Management Studio | v1.x|
|Versiones anteriores de Visual Studio | v1.x|
|SQL Server 2016 | v1.x|

\* Para instalar el Visor de Ayuda con Visual Studio 2017, en la pestaña Componentes individuales del instalador de Visual Studio, seleccione **Visor de Ayuda** en Herramientas de código y haga clic en **Instalar**. 

>[!NOTE]
> - SQL Server 2016 instala el Visor de Ayuda 1.1, que no admite la ayuda de SQL Server 2016. 
> - Si instala SQL Server 2017 no se instalará el Visor de Ayuda.
> - El Visor de Ayuda v2.x también puede ser compatible con la ayuda de [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] si instala el contenido desde un disco.

## <a name="use-help-viewer-v2x"></a>Uso del Visor de Ayuda v2.x

SSMS 17.x y VS 2015 y 2017 usan el Visor de Ayuda 2.x, que es compatible con la ayuda de SQL Server 2016 y 2017. 

**Para descargar e instalar contenido de ayuda sin conexión con el Visor de Ayuda v2.x**

1. En SSMS o VS, haga clic en **Agregar y quitar contenido de la Ayuda** en el menú Ayuda. 

   ![Agregar y quitar contenido de HelpViewer2](../sql-server/media/sql-server-help-installation/addremovecontent.png)  

   El Visor de Ayuda se abre en la pestaña Administrar contenido.  
   
2. Para instalar el último paquete de contenido de ayuda, seleccione **En línea** en Origen de la instalación.
   
   ![HelpViewer2_ManageContent_OnlineSource](../sql-server/media/sql-server-help-installation/helpviewer2-managecontent-onlinesource.png)  
   
   >[!NOTE]
   > Para instalar contenido desde el disco (ayuda de SQL Server 2014), seleccione **Disco** en Origen de la instalación y especifique la ubicación del disco.
   
   En Ruta de acceso del almacén local de la pestaña Administrar contenido se muestra dónde se instalará el contenido en el equipo local. Si quiere cambiar la ubicación, haga clic en **Mover**, indique otra ruta de acceso de carpeta en el campo **A** y haga clic en **Aceptar**.
   Si se produce un error de instalación de ayuda después de cambiar la ruta de acceso del almacén local, cierre y vuelva a abrir el Visor de Ayuda, asegúrese de que se muestra la nueva ubicación en Ruta de acceso del almacén local y vuelva a intentar realizar la instalación.

3. Haga clic en **Agregar** al lado de cada paquete de contenido (libro) que quiera instalar. 
   Para instalar todo el contenido de ayuda de SQL Server, agregue los 13 libros de SQL Server. 
   
4. Haga clic en **Actualizar** en la parte inferior derecha. 
   La tabla de contenido de ayuda de la parte izquierda se actualizará automáticamente con los libros agregados. 
   
   ![HelpViewer2_ManageContent_AddContent](../sql-server/media/sql-server-help-installation/helpviewer2-managecontent-addcontent.png)     
   
> [!NOTE]
> No todos los títulos de nodos superiores de la tabla de contenido de SQL Server coinciden exactamente con los nombres de los libros de ayuda descargables correspondientes. Los títulos de la TDC están relacionados con los nombres de libros de la siguiente forma:

| Panel de contenido | Libro de SQL Server |
|-----|-----|
|Referencia del lenguaje de Analysis Services | Referencia del lenguaje de Analysis Services (MDX)|
|Referencia de expresiones de análisis de datos (DAX) | Referencia de expresiones de análisis de datos (DAX)|
|Referencia de Extensiones de minería de datos (DMX) | Referencia de Extensiones de minería de datos (DMX)|
|Guías del desarrollador para SQL Server | Referencia para desarrolladores de SQL Server|
|Descargar SQL Server Management Studio | SQL Server Management Studio|
|Getting started with machine learning in SQL Server (Introducción al aprendizaje automático en SQL Server) | Microsoft Machine Learning Services|
|Power Query M Reference (Referencia de Power Query M) | Power Query M Reference (Referencia de Power Query M)|
|Controladores de SQL Server | Controladores de conexión de SQL Server|
|SQL Server en Linux | SQL Server en Linux|
|Documentación técnica de SQL Server | Documentación técnica de SQL Server (SSIS, SSRS, motor de base de datos, instalación)|
|Herramientas y utilidades de Azure SQL Database | Herramientas de SQL Server|
|Referencia de Transact-SQL (motor de base de datos) | Referencia de Transact-SQL|
|Referencia del lenguaje XQuery (SQL Server) | Referencia del lenguaje XQuery (SQL Server)|

> [!NOTE]
> Si el Visor de Ayuda se bloquea al agregar contenido, cambie la línea Cache LastRefreshed="\<mm/dd/yyyy> 00:00:00" en los archivos %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings o HlpViewer_VisualStudiox_en-US.settings a una fecha en el futuro. Para obtener más información sobre este problema, vea [Visual Studio Help Viewer freezes](https://msdn.microsoft.com/en-us/library/dd831853.aspx)(El Visor de Ayuda de Visual Studio se bloquea).

**Para ver contenido de ayuda en línea en SSMS con el Visor de Ayuda v2.x**

Para ver la ayuda instalada en SSMS, presione Ctrl+Alt+F1 o seleccione **Agregar o quitar contenido** en el menú Ayuda para iniciar el Visor de Ayuda. 

   ![Agregar y quitar contenido de HelpViewer2](../sql-server/media/sql-server-help-installation/addremovecontent.png)  

Este se abrirá en la pestaña Administrar contenido, con la tabla de contenido de ayuda instalada en el panel izquierdo. Haga clic en los temas de la tabla de contenido para que se muestren en el panel derecho. 
> [!TIP]
> Si el panel de contenido no está visible, haga clic en Contenido en el margen izquierdo. Haga clic en el icono de chincheta para mantener el panel de contenido abierto.  

   ![Visor de Ayuda v2.x con contenido](../sql-server/media/sql-server-help-installation/helpviewer2-withcontentinstalled.png)

**Para ver contenido de ayuda sin conexión en VS con el Visor de Ayuda v2.x**

Para ver la ayuda instalada en Visual Studio:
1. Seleccione **Establecer preferencias de la Ayuda** en el menú Ayuda y seleccione **Iniciar en el Visor de Ayuda**. 

   ![Visor de Ayuda, Establecer preferencias de la Ayuda, Ayuda de VS](../sql-server/media/sql-server-help-installation/launchviewer.png)

2. Haga clic en **Ver Ayuda** en el menú Ayuda para que se muestre el contenido en el Visor de Ayuda. 

   ![Ver Ayuda](../sql-server/media/sql-server-help-installation/viewhelp.png)

   La tabla de contenido de ayuda se muestra en la parte izquierda y el tema de ayuda seleccionado en la parte derecha. 
   
## <a name="use-help-viewer-v1x"></a>Uso del Visor de Ayuda v1.x

Las versiones anteriores de SSMS y VS usan el Visor de Ayuda 1.x, que es compatible con la ayuda de SQL Server 2014. 

**Para descargar e instalar contenido de ayuda sin conexión con el Visor de Ayuda v1.x**

Este proceso usa el Visor de Ayuda 1.x para descargar la ayuda de SQL Server 2014 del Centro de descarga de Microsoft e instalarla en el equipo.

1. Vaya al sitio de descarga [Product Documentation for Microsoft SQL Server 2014](https://www.microsoft.com/en-us/download/details.aspx?id=42557) (Documentación de producto para Microsoft SQL Server 2014) y haga clic en **Descargar**.  
2. Haga clic en **Guardar** en el cuadro de mensaje para guardar el archivo *SQLServer2014Documentation\_\*.exe* en el equipo.  
   
   >[!NOTE]
   >Para entornos restringidos con firewall y proxy, guarde la descarga en una unidad USB u otro medio portátil que se pueda llevar al entorno.   
   
3. Haga doble clic en el archivo .exe para desempaquetar el archivo de contenido de ayuda y guarde el archivo en una carpeta local o compartida.  
4. Inicie SSMS o VS, y haga clic en **Administrar configuración de la Ayuda** en el menú Ayuda para abrir el **Administrador de bibliotecas de Ayuda**.  
5. Haga clic en **Instalar contenido desde disco** y vaya a la carpeta en la que ha desempaquetado el archivo de contenido de ayuda.  
   
   ![HelpLibraryManager_MainPage_InstallFromDisk](../sql-server/media/sql-server-help-installation/helplibrarymanager-mainpage-installfromdisk.png)
   
   ![HelpLibraryManager_InstallContentFromDisk_dialog1](../sql-server/media/sql-server-help-installation/helplibrarymanager-installcontentfromdisk-dialog1.png)
   
   > [!IMPORTANT]
   > Para no instalar contenido de ayuda local que solo tenga una tabla de contenido parcial, debe usar la opción **Instalar contenido desde disco** en el **Administrador de bibliotecas de Ayuda**.  Si ha usado **Instalar contenido desde Internet** y el Visor de Ayuda muestra una tabla de contenido parcial, vea los pasos para solucionar problemas en esta [entrada de blog](https://blogs.msdn.microsoft.com/womeninanalytics/2016/06/21/troubleshoot-local-help-for-sql-server-2014/). 
   
8. Haga clic en el archivo HelpContentSetup.msha, en **Abrir** y en **Siguiente**.  
9. Haga clic en **Agregar** junto a la documentación que quiera instalar y en **Actualizar**.  
   
   ![HelpLibraryManager_InstallContentFromDisk_dialog2](../sql-server/media/sql-server-help-installation/helplibrarymanager-installcontentfromdisk-dialog2.png)  
   
10. Haga clic en **Finalizar** y, después, en **Salir**.

**Para ver contenido de ayuda sin conexión con el Visor de Ayuda v1.x**

11. Para ver la ayuda instalada, abra el **Administrador de bibliotecas de Ayuda**, haga clic en **Elegir Ayuda en línea o local** y luego en **Usar Ayuda local**.
12. Abra el Visor de Ayuda para ver el contenido al hacer clic en **Ver Ayuda** en el menú **Ayuda**. El contenido instalado se muestra en el panel de la izquierda.  
   
   ![HelpViewer1_withContentInstalled_ZoomedIn](../sql-server/media/sql-server-help-installation/helpviewer1-withcontentinstalled-zoomedin.png)  
   
## <a name="view-online-help"></a>Ver ayuda en línea

La ayuda en línea siempre mostrará el contenido más actualizado. 

**Para ver ayuda en línea de SQL Server en SSMS 17.x**

- Haga clic en **Ver ayuda** en el menú **Ayuda**. La documentación más reciente de SQL Server 2016 y 2017 de [https://docs.microsoft.com/sql/https://docs.microsoft.com/es-es/sql/sql-server/sql-server-technical-documentation](https://docs.microsoft.com/en-us/sql/sql-server/sql-server-technical-documentation) se mostrará en un explorador. 

   ![Ver Ayuda](../sql-server/media/sql-server-help-installation/viewhelp.png)

**Para ver ayuda en línea de Visual Studio en Visual Studio**

1. Seleccione **Establecer preferencias de la Ayuda** en el menú Ayuda y seleccione **Iniciar en el explorador** o **Iniciar en el Visor de Ayuda**. 
2. Haga clic en **Ver ayuda** en el menú Ayuda. La ayuda más reciente de Visual Studio se mostrará en el entorno seleccionado. 

**Para ver ayuda en línea con Visor de Ayuda v1.x**

1. Haga clic en **Administrar configuración de la Ayuda** en el menú Ayuda para abrir el **Administrador de bibliotecas de Ayuda**.  
2. En el cuadro de diálogo Administrador de bibliotecas de Ayuda, haga clic en **Elegir Ayuda en línea o local**.  
   
   ![HelpLibraryManager_MainPage_ChooseOnlineORLocal.png](../sql-server/media/sql-server-help-installation/helplibrarymanager-mainpage-chooseonlineorlocal.png.png)  
   
3. Haga clic en **I want to use online help** (Usar ayuda en línea), en **Aceptar** y luego en **Salir**.  
   
   ![HelpLibraryManager_ChooseOnlineORLocalHelp_OnlineHelpSelected_dialog](../sql-server/media/sql-server-help-installation/helplibrarymanager-chooseonlineorlocalhelp-onlinehelpselected-dialog.png)
   
4. Abra el Visor de Ayuda para ver el contenido al hacer clic en **Ver Ayuda** en el menú **Ayuda**. 

## <a name="view-f1-help"></a>Ver la Ayuda de F1

Al presionar F1 o al hacer clic en **Ayuda** o en el icono **?** de un cuadro de diálogo en SSMS o VS, aparecerá un tema de ayuda en línea contextual en el explorador o en el Visor de Ayuda. 

**Para ver la ayuda de F1**

1. Seleccione **Establecer preferencias de la Ayuda** en el menú Ayuda y seleccione **Iniciar en el explorador** o **Iniciar en el Visor de Ayuda**. 
2. Presione F1 o haga clic en **Ayuda** o en **?** en los cuadros de diálogo en los que estén disponibles para ver temas en línea contextuales en el entorno elegido.

>  [!NOTE]
>  La ayuda de F1 solo funciona cuando está conectado a Internet. No hay ningún origen sin conexión para la ayuda de F1. 
   

## <a name="next-steps"></a>Pasos siguientes
[Visor de Ayuda de Microsoft (Visual Studio)](/visualstudio/ide/microsoft-help-viewer)  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
