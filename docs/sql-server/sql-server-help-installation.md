---
title: Visor de Ayuda y contenido de ayuda de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 12/10/2019
ms.prod: sql
ms.technology: ''
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ad4d98af834e482005e354b2dcd5ce2c52f2fd42
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "75251466"
---
# <a name="sql-server-offline-help-and-help-viewer"></a>Visor de Ayuda y ayuda sin conexión de SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Puede usar la aplicación Visor de Ayuda de Microsoft para descargar e instalar los paquetes de ayuda de SQL Server desde el disco o desde orígenes en línea. Después, puede ver el contenido sin conexión. El Visor de ayuda se instala con varias herramientas. En este artículo se describen las herramientas para instalar el Visor de Ayuda, cómo instalar contenido de ayuda sin conexión y cómo ver la ayuda.

Se necesita acceso a Internet para descargar el contenido de Visor de Ayuda. Después, podrá migrar el contenido a un equipo que no tenga acceso a Internet.

>[!NOTE]
> Para obtener el contenido local para las versiones actuales de SQL Server, instale la versión actual de SQL Server Management Studio [SQL Server Management Studio 18.x](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="what-tools-install-the-help-viewer-versions"></a>¿Qué herramientas instalan las versiones del Visor de ayuda?

Hay dos versiones principales del Visor de Ayuda de Microsoft.  Las versiones 1.x y 2.x. Cada versión admite distintas versiones del contenido de SQL Server.  El formato de los libros sin conexión ha cambiado con el paso del tiempo y las versiones anteriores de Visor de Ayuda no son compatibles con las versiones más recientes de los libros.

|**Conjunto de contenido**|**Herramientas que instalan el Visor de Ayuda**|**Versión de Visor de Ayuda**|
|-|-|-|
|SQL Server 2019 <br><br><br>SQL Server 2017 <br>SQL Server 2016 | [Visual Studio 2019 (\*1)](https://docs.microsoft.com/visualstudio/install/install-visual-studio?view=vs-2019) <br>[SQL Server Management Studio 18.x](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) <br><br>[Visual Studio 2017 (\*1)](https://docs.microsoft.com/visualstudio/install/install-visual-studio?view=vs-2017) <br>[SQL Server Management Studio 17.x](https://docs.microsoft.com/sql/ssms/release-notes-ssms?view=sql-server-2017#download-ssms-1791) <br>[SQL Server Data Tools para Visual Studio 2015](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt) <br>Visual Studio 2015 | v2.3 <br><br><br>v2.2 |
|SQL Server 2014<br>SQL Server 2012|Programa de instalación de SQL Server 2016 (\*2)<br>SQL Server 2014 Management Studio<br>Programa de instalación de SQL Server 2014 (\*2)<br>SQL Server Management Studio 2012<br>Programa de instalación de SQL Server 2012 (\*2)| v1.x|
| | | |

(\*1) Para instalar el Visor de Ayuda con Visual Studio 2019 o 2017, en la pestaña **Componentes individuales** del Instalador de Visual Studio, seleccione **Code Tools** \> **Visor de Ayuda** \> **Instalar**.

(\*2) Indica la opción **Componentes de documentación** en el programa de instalación de SQL Server.

>[!NOTE]
> - SQL Server 2016 instala el Visor de Ayuda 1.1, que no admite el contenido de ayuda de SQL Server 2016. Para ver el contenido de SQL Server 2016, necesita la versión v2.x de Visor de ayuda. Para obtener más información, vea las [Notas de la versión de SQL Server 2016](sql-server-2016-release-notes.md).
> - El Visor de ayuda 2.x puede mostrar la documentación de las versiones de 2014 a 2019 de SQL Server, como mínimo.
> - Una manera fácil de obtener el Visor de Ayuda 2.3 o posterior es descargar primero la versión más reciente de `SSMS.exe`, que es gratuita. Y, a continuación, use el menú **Ayuda** de SSMS.
> - A partir de SQL Server 2017, el Visor de Ayuda no se puede instalar desde el programa de instalación de SQL Server.

## <a name="use-help-viewer-v2x"></a>Uso del Visor de Ayuda v2.x

Para este enfoque, se recomienda el Visor de Ayuda 2.3 o posterior. El menú **Ayuda** de la [versión más reciente de SSMS.exe](../ssms/download-sql-server-management-studio-ssms.md) es para la versión 2.3 o posterior.

### <a name="to-download-and-install-offline-help-content-with-help-viewer-v2x"></a>Para descargar e instalar contenido de ayuda sin conexión con el Visor de Ayuda v2.x

1. En SSMS o VS, haga clic en **Agregar y quitar contenido de la Ayuda** en el menú Ayuda. 

   ![Agregar y quitar contenido de HelpViewer2](../sql-server/media/sql-server-help-installation/addremovecontent.png)  

   El Visor de Ayuda se abre en la pestaña Administrar contenido.  
   
2. Para instalar el último paquete de contenido de ayuda, seleccione **En línea** en Origen de la instalación.
   
   ![HelpViewer2_ManageContent_OnlineSource](../sql-server/media/sql-server-help-installation/helpviewer2-managecontent-onlinesource.png)  
   
   >[!NOTE]
   > Para instalar contenido desde el disco (ayuda de SQL Server 2014), seleccione **Disco** en Origen de la instalación y especifique la ubicación del disco.
   
   En "Ruta de acceso del almacén local" de la pestaña "Administrar contenido", se muestra dónde se instalará el contenido en el equipo local. Para cambiar la ubicación, haga clic en **Mover**, especifique otra ruta de carpeta en el campo **A** y, después, haga clic en **Aceptar**.
   Si se produce un error en la instalación de la Ayuda después de cambiar la ruta de acceso del almacén local, cierre y vuelva a abrir el Visor de ayuda. Compruebe que la nueva ubicación aparece en la ruta de acceso del almacén local y vuelva a intentar realizar la instalación.

3. Haga clic en **Agregar** al lado de cada paquete de contenido (libro) que quiera instalar. 
   Para instalar todo el contenido de ayuda de SQL Server, agregue los 13 libros de SQL Server. 
   
4. Haga clic en **Actualizar** en la parte inferior derecha. 
   La tabla de contenido de ayuda de la parte izquierda se actualizará automáticamente con los libros agregados. 
   
   ![HelpViewer2_ManageContent_AddContent](../sql-server/media/sql-server-help-installation/helpviewer2-managecontent-addcontent.png)     
   
> [!NOTE]
> No todos los títulos de nodos superiores de la tabla de contenido de SQL Server coinciden exactamente con los nombres de los libros de ayuda descargables correspondientes. Los títulos de la TDC están relacionados con los nombres de libros de la siguiente forma:

(*) Contenido de la primera versión de disponibilidad general del contenido de SQL Server 2017, así como contenido de 2016 anterior. Estos libros se quitarán, ya que los libros completos y separados de SQL Server 2016 y 2017 contienen ediciones de contenido realizadas en enero de 2019.  

| | Panel de contenido | Libro de SQL Server |
|-----|-----|-----|
|*|Referencia del lenguaje de Analysis Services | Referencia del lenguaje de Analysis Services (MDX)|
|*|Referencia de expresiones de análisis de datos (DAX) | Referencia de expresiones de análisis de datos (DAX)|
|*|Referencia de Extensiones de minería de datos (DMX) | Referencia de Extensiones de minería de datos (DMX)|
|*|Getting started with Machine learning in SQL Server (Introducción al aprendizaje automático en SQL Server) | Microsoft Machine Learning Services|
|*|Referencia de Power Query M | Referencia de Power Query M|
||Documentación de SQL Server 2016 | Documentación de SQL Server 2016|
||Documentación de SQL Server 2017| Documentación de SQL Server 2017|
|*|Guías del desarrollador para SQL Server | Referencia para desarrolladores de SQL Server|
|*|Descargar SQL Server Management Studio | SQL Server Management Studio|
|*|Página principal de la programación de clientes de Microsoft SQL Server | Controladores de conexión de SQL Server|
|*|SQL Server en Linux | SQL Server en Linux|
|*|Documentación técnica de SQL Server | Documentación técnica de SQL Server (SSIS, SSRS, motor de base de datos, instalación)|
|*|Herramientas y utilidades de Azure SQL Database | Herramientas de SQL Server|
|*|Referencia de Transact-SQL (motor de base de datos) | Referencia de Transact-SQL|
|*|Referencia del lenguaje XQuery (SQL Server) | Referencia del lenguaje XQuery (SQL Server)|
| &nbsp; | &nbsp; | &nbsp; |

> [!NOTE]
> Si el Visor de Ayuda se bloquea al agregar contenido, cambie la línea Cache LastRefreshed="\<mm/dd/yyyy> 00:00:00" en los archivos %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings o HlpViewer_VisualStudiox_en-US.settings a una fecha en el futuro. Para obtener más información sobre este problema, vea [Visual Studio Help Viewer freezes](/visualstudio/welcome-to-visual-studio)(El Visor de Ayuda de Visual Studio se bloquea).

### <a name="to-view-offline-help-content-in-ssms-with-help-viewer-v2x"></a>Para ver contenido de ayuda en línea en SSMS con el Visor de Ayuda v2.x

Para ver la ayuda instalada en SSMS, presione Ctrl+Alt+F1 o seleccione **Agregar o quitar contenido** en el menú Ayuda para iniciar el Visor de Ayuda. 

   ![Agregar y quitar contenido de HelpViewer2](../sql-server/media/sql-server-help-installation/addremovecontent.png)  

Este se abrirá en la pestaña Administrar contenido, con la tabla de contenido de ayuda instalada en el panel izquierdo. Haga clic en los artículos de la tabla de contenido para que se muestren en el panel de la derecha.
> [!TIP]
> Si el panel de contenido no está visible, haga clic en Contenido en el margen izquierdo. Haga clic en el icono de chincheta para mantener el panel de contenido abierto.  

   ![Visor de Ayuda v2.x con contenido](../sql-server/media/sql-server-help-installation/helpviewer2-withcontentinstalled.png)

### <a name="to-view-offline-help-content-in-vs-with-help-viewer-v2x"></a>Para ver contenido de ayuda sin conexión en VS con el Visor de Ayuda v2.x

Para ver la ayuda instalada en Visual Studio:
1. Seleccione **Establecer preferencias de la Ayuda** en el menú Ayuda y seleccione **Iniciar en el Visor de Ayuda**. 

   ![Visor de Ayuda, Establecer preferencias de la Ayuda, Ayuda de VS](../sql-server/media/sql-server-help-installation/launchviewer.png)

2. Haga clic en **Ver Ayuda** en el menú Ayuda para que se muestre el contenido en el Visor de Ayuda. 

   ![Ver Ayuda](../sql-server/media/sql-server-help-installation/viewhelp.png)

   La tabla de contenido de ayuda se muestra en la parte izquierda y el artículo de ayuda seleccionado en la parte derecha.
  
## <a name="use-help-viewer-v1x"></a>Uso del Visor de Ayuda v1.x

En esta sección, realizará los siguientes pasos generales:

- Descargue manualmente los libros sin conexión de SQL Server 2014, que son un total de cuatro.
- Use el menú **Ayuda** de SSMS o VS para iniciar el Visor de Ayuda.
- Finalmente, se indica al Visor de Ayuda dónde está el archivo `*.msha` de SQL Server 2014 en la unidad de disco duro local.

Las versiones anteriores de SSMS y VS ofrecían las versiones 1.x del Visor de Ayuda. La versión 1.x puede mostrar los libros sin conexión para las versiones 2012 y 2014 de SQL Server. Sin embargo, la 1.x no puede mostrar el libro sin conexión de SQL Server 2016 o posterior.

El Visor de Ayuda 2.3 también puede mostrar los libros sin conexión de SQL Server 2014, después de descargar los libros sin conexión de SQL Server 2014 en el disco duro local.

### <a name="to-download-and-install-offline-help-content-with-help-viewer-v1x"></a>Para descargar e instalar contenido de ayuda sin conexión con el Visor de Ayuda v1.x

Este proceso usa el Visor de Ayuda 1.x para descargar la ayuda de SQL Server 2014 del Centro de descarga de Microsoft e instalarla en el equipo.

1. Vaya al sitio de descarga [Product Documentation for Microsoft SQL Server 2014](https://www.microsoft.com/download/details.aspx?id=42557) (Documentación de producto para Microsoft SQL Server 2014) y haga clic en **Descargar**.

2. Haga clic en **Guardar** en el cuadro de mensaje para guardar el archivo *SQLServer2014Documentation\_\*.exe* en el equipo.

   > [!NOTE]
   > Para entornos restringidos con firewall y proxy, guarde la descarga en una unidad USB u otro medio portátil que se pueda llevar al entorno.

3. Haga doble clic en el archivo .exe para desempaquetar el archivo de contenido de ayuda y guarde el archivo en una carpeta local o compartida.

4. Inicie SSMS o VS, y haga clic en **Administrar configuración de la Ayuda** en el menú Ayuda para abrir el **Administrador de bibliotecas de Ayuda**.

5. Haga clic en **Instalar contenido desde disco** y vaya a la carpeta en la que ha desempaquetado el archivo de contenido de ayuda.

   ![HelpLibraryManager_MainPage_InstallFromDisk](../sql-server/media/sql-server-help-installation/helplibrarymanager-mainpage-installfromdisk.png)

   ![HelpLibraryManager_InstallContentFromDisk_dialog1](../sql-server/media/sql-server-help-installation/helplibrarymanager-installcontentfromdisk-dialog1.png)

   > [!IMPORTANT]
   > Para no instalar contenido de ayuda local que solo tenga una tabla de contenido parcial, debe usar la opción **Instalar contenido desde disco** en el **Administrador de bibliotecas de Ayuda**.  Si ha usado **Instalar contenido desde Internet** y el Visor de Ayuda muestra una tabla de contenido parcial, vea los pasos para solucionar problemas en esta [entrada de blog](https://blogs.msdn.microsoft.com/womeninanalytics/2016/06/21/troubleshoot-local-help-for-sql-server-2014/).

6. Haga clic en el archivo `HelpContentSetup.msha`, en **Abrir** y, a continuación, en **Siguiente**.

7. Haga clic en **Agregar** junto a la documentación que quiera instalar y en **Actualizar**.

   ![HelpLibraryManager_InstallContentFromDisk_dialog2](../sql-server/media/sql-server-help-installation/helplibrarymanager-installcontentfromdisk-dialog2.png)

8. Haga clic en **Finalizar** y, después, en **Salir**.

### <a name="to-view-offline-help-content-with-help-viewer-v1x"></a>Para ver contenido de ayuda sin conexión con el Visor de Ayuda v1.x

1. Para ver la ayuda instalada, abra el **Administrador de bibliotecas de Ayuda**, haga clic en **Elegir Ayuda en línea o local** y luego en **Usar Ayuda local**.

2. Abra el Visor de Ayuda para ver el contenido al hacer clic en **Ver Ayuda** en el menú **Ayuda**. El contenido instalado se muestra en el panel de la izquierda.

   ![HelpViewer1_withContentInstalled_ZoomedIn](../sql-server/media/sql-server-help-installation/helpviewer1-withcontentinstalled-zoomedin.png)  

## <a name="view-online-help"></a>Ver ayuda en línea

La ayuda en línea siempre mostrará el contenido más actualizado. 

### <a name="to-view-sql-server-online-help-in-ssms-17x"></a>Para ver ayuda en línea de SQL Server en SSMS 17.x

- Haga clic en **Ver ayuda** en el menú **Ayuda**. La documentación de SQL Server 2016 y 2017 más reciente de [https://docs.microsoft.com/sql/sql-server/](https://docs.microsoft.com/sql/sql-server/) se muestra en un explorador.

   ![Ver Ayuda](../sql-server/media/sql-server-help-installation/viewhelp.png)

### <a name="to-view-visual-studio-online-help-in-visual-studio"></a>Para ver ayuda en línea de Visual Studio en Visual Studio

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

Al presionar F1 o al hacer clic en **Ayuda** o en el icono **?** de un cuadro de diálogo en SSMS o VS, aparecerá un artículo de ayuda en línea contextual en el explorador o en el Visor de Ayuda.

### <a name="to-view-f1-help"></a>Para ver la ayuda de F1

1. En el menú Ayuda, haga clic en **Establecer preferencias de la Ayuda** y seleccione **Iniciar en el explorador** o **Iniciar en el Visor de Ayuda**.
2. Presione F1, o bien haga clic en **Ayuda** o en **?** . en los cuadros de diálogo en los que estén disponibles para ver artículos en línea contextuales en el entorno elegido.

> [!NOTE]
> La ayuda de F1 solo funciona cuando está conectado a Internet. No hay ningún origen sin conexión para la ayuda de F1.

## <a name="systems-without-internet-access"></a>Sistemas sin acceso a Internet
Después de descargar los libros sin conexión en un sistema que tenga acceso a Internet, siga este procedimiento para migrar el contenido a un sistema que no tenga conexión a Internet.

  >[!NOTE]
  >En el sistema sin conexión tendrá que instalar software compatible con el Visor de ayuda, como SQL Server Management Studio.

1. Abra el Visor de ayuda (Ctrl + Alt + F1).
1. Seleccione la documentación que le interese. Por ejemplo, filtre por SQL y seleccione la documentación técnica de SQL Server.
1. Identifique la ruta de acceso física de los archivos en disco, que se puede encontrar en **Ruta de acceso del almacén local**.
1. Vaya hasta esta ubicación mediante el explorador del sistema de archivos.
    1.  La ubicación predeterminada es `C:\Program Files (x86)\Microsoft SQL Server\140\Tools\Binn\ManagementStudio\Extensions\Application`
1. Seleccione las tres carpetas (**ContentStore**, **Incoming**, **IndexStore**) y cópielas en la misma ubicación en el sistema sin conexión. Es posible que tenga que usar un dispositivo de medios provisional, como un CD o USB.
1. Una vez que se hayan movido estos archivos, inicie el Visor de ayuda en el sistema sin conexión y la documentación técnica de SQL Server estará disponible.

![physical-location-of-offline-content.png](media/sql-server-help-installation/physical-location-of-offline-content.png)

## <a name="next-steps"></a>Pasos siguientes
[Visor de Ayuda de Microsoft (Visual Studio)](/visualstudio/ide/microsoft-help-viewer)  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
