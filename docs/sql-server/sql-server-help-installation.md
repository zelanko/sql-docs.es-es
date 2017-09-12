---
title: "Visor de Ayuda y contenido sin conexión para SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 06/27/2017
ms.prod: sql-non-specified
ms.technology: server-general
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2014
- SQL Server 2016
- SQL Server 2017
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
caps.latest.revision: 8
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: b8e93b7afb8845398e23ca52c5c3f3bf3901898c
ms.contentlocale: es-es
ms.lasthandoff: 09/08/2017

---
# <a name="help-viewer-and-offline-content-for-sql-server"></a>Visor de Ayuda y contenido sin conexión para SQL Server
  
  
  
Este artículo muestra cómo instalar el Visor de Ayuda y ver la documentación de SQL Server sin conexión. El artículo cubre documentación para [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)], SQL Server 2016 y SQL Server 2017. 

## <a name="install-help-viewer"></a>Instalar el Visor de Ayuda
En la tabla siguiente se indican las herramientas que instalan el Visor de Ayuda en función de la versión de SQL Server que use. Instale una de las herramientas enumeradas para instalar el Visor de Ayuda.


|**Versión de SQL Server**|**Herramientas que instalan el Visor de Ayuda**|**Versión instalada del Visor de Ayuda**|
|---------|---------|---------|
|SQL Server 2017<br>SQL Server 2016     |   [Versión más reciente de SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)<br><br>[Versión más reciente de SQL Server Data Tools para Visual Studio 2015](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)<br><br>Visual Studio 2017 (*solo admite SQL Server 2016*)  |  v2.x       |
|SQL Server 2014    | SQL Server 2014 Management Studio<br><br>Versiones de Visual Studio anteriores a Visual Studio 2012        |  v1.x       |


> [!IMPORTANT]
> SQL Server 2016 instala el Visor de Ayuda 1.1, que no se puede usar para ver documentación de SQL Server 2016 y 2017.
> <br>
> <br>
> SQL Server 2017 no instala el Visor de Ayuda.
> <br>
> <br>
> Para instalar el Visor de Ayuda con Visual Studio 2017, haga clic en la pestaña **Componentes individuales** del programa **Instalador de Visual Studio**, haga clic en **Visor de Ayuda** en la categoría **Herramientas de código** y luego haga clic en **Instalar**. 
> <br>
> <br>
> Puede ver la Ayuda local de [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] mediante el Visor de Ayuda 2.x, pero únicamente si selecciona **Instalar contenido desde disco**. 


## <a name="sql-server-2016-sql-server-2017-offline-content"></a>Contenido sin conexión de SQL Server 2016 y SQL Server 2017  
 
**Para instalar el contenido sin conexión**  
1. Abra el Visor de Ayuda. Para ello, inicie SQL Server Management Studio o Visual Studio y haga clic en **Agregar y quitar contenido de la Ayuda** en el menú **Ayuda**.  
2. Haga clic en la pestaña **Administrar contenido**.  
3. Para instalar la Ayuda desde un origen en línea, haga clic en **En línea** en el área **Origen de la instalación**.  
![HelpViewer2_ManageContent_OnlineSource](../sql-server/media/helpviewer2-managecontent-onlinesource.png)  
7. Haga clic en **Agregar** junto a la documentación que quiera instalar y en **Actualizar**.  
![HelpViewer2_ManageContent_AddContent](../sql-server/media/helpviewer2-managecontent-addcontent.png)     
  
   >[!IMPORTANT] 
   >En SQL Server Management Studio y Visual Studio, la aplicación del Visor de Ayuda puede bloquearse mientras se agrega la documentación. Haga lo siguiente para solucionar este problema. Para obtener más información sobre este problema, vea [Visual Studio Help Viewer freezes](https://msdn.microsoft.com/library/mt654096.aspx)(El Visor de Ayuda de Visual Studio se bloquea).  
   >>Abra el archivo %LOCALAPPDATA%\Microsoft\HelpViewer2.2\HlpViewer_SSMS16_en-US.settings | HlpViewer_VisualStudio14_en-US.settings en el Bloc de notas y cambie la fecha en el siguiente código a una fecha en el futuro. Este archivo solo está disponible en el equipo local si se tiene instalado Visual Studio. 
   >>>Última actualización de la caché="31/12/2017 00:00:00"  
  
    La tabla de contenido del panel izquierdo se actualiza automáticamente para incluir la documentación que se ha agregado.  
![HelpViewer2_withContentInstalled](../sql-server/media/helpviewer2-withcontentinstalled.png)

1. (Opcional) En el cuadro **Ruta de acceso del almacén local** de la pestaña **Administrar contenido** se muestra el lugar en el que está instalada la documentación en el equipo local. Para moverla a una ubicación diferente, haga clic en **Mover**, escriba una ruta de carpeta en el campo **A** del cuadro de diálogo **Mover contenido** y, después, haga clic en **Aceptar**.

   ![HelpViewer2_MoveContent_Dialog](../sql-server/media/helpviewer2-move-content-dialog.png)

   Una vez que se haya movido el contenido, se muestra la nueva ubicación en la **Ruta de acceso del almacén local**.
      
   >[!IMPORTANT]
   > Si aparece un mensaje que indica que se ha producido un error en la operación de mover, cierre el cuadro de mensaje, cierre el Visor de Ayuda y, después, vuelva a abrir el Visor de Ayuda. La nueva ubicación del contenido debería aparecer ahora en la **Ruta de acceso del almacén local**.   
 
## <a name="includesssql14mdincludessssql14-mdmd-offline-content"></a>[!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] Contenido sin conexión 
 
  
**Para instalar el contenido sin conexión**  
1. Vaya al [sitio de descarga](https://www.microsoft.com/en-us/download/details.aspx?id=42557) del contenido de Ayuda y haga clic en **Descargar**.  
2. Haga clic en **Guardar** en el cuadro de mensaje para guardar el archivo SQLServer2014Documentation_*.exe en el equipo.  

 Para entornos restringidos con firewall y proxy, guarde la descarga en una unidad USB u otro medio portátil que se pueda llevar al entorno.   

3. Haga doble clic en el archivo .exe para desempaquetar el archivo de contenido de Ayuda y guarde el archivo en una carpeta local o compartida.  
4. Abra el **Administrador de bibliotecas de Ayuda**. Para ello, inicie SQL Server Management Studio o Visual Studio y haga clic en **Administrar configuración de la Ayuda** en el menú **Ayuda**.  
5. Haga clic en **Instalar contenido desde disco** y vaya a la carpeta en la que ha desempaquetado el archivo de contenido de Ayuda.  
  
     Seleccione Instalar contenido desde disco.  |Vaya al archivo de contenido de Ayuda.   
     ---------|---------  
     ![HelpLibraryManager_MainPage_InstallFromDisk](../sql-server/media/helplibrarymanager-mainpage-installfromdisk.png)    | ![HelpLibraryManager_InstallContentFromDisk_dialog1](../sql-server/media/helplibrarymanager-installcontentfromdisk-dialog1.png)          
  
     >[!IMPORTANT]
     > Para no instalar contenido de Ayuda local que solo tenga una tabla de contenido parcial, use la opción **Instalar contenido desde disco** en el **Administrador de bibliotecas de Ayuda**.  
     >>Si ha usado la opción **Instalar contenido desde Internet** y el Visor de Ayuda muestra una tabla de contenido parcial, vea los pasos para solucionar problemas en esta [entrada de blog](https://blogs.msdn.microsoft.com/womeninanalytics/2016/06/21/troubleshoot-local-help-for-sql-server-2014/). 

8. Haga clic en el archivo HelpContentSetup.msha, en **Abrir** y en **Siguiente**.  
9. Haga clic en **Agregar** junto a la documentación que quiera instalar y en **Actualizar**.  
  
   ![HelpLibraryManager_InstallContentFromDisk_dialog2](../sql-server/media/helplibrarymanager-installcontentfromdisk-dialog2.png)  
10. Haga clic en **Finalizar** y en **Salir**.
11. Vuelva a abrir el **Administrador de bibliotecas de Ayuda**, haga clic en **Elegir Ayuda en línea o local** y luego en **Usar Ayuda local**.
12. Abra el Visor de Ayuda para ver el contenido al hacer clic en **Ver Ayuda** en el menú **Ayuda**. El contenido que ha instalado debería aparecer en la tabla de contenido, en el panel izquierdo.  
  
    ![HelpViewer1_withContentInstalled_ZoomedIn](../sql-server/media/helpviewer1-withcontentinstalled-zoomedin.png)  
  
## <a name="view-online-content-in-help-viewer"></a>Ver el contenido en línea en el Visor de Ayuda

En el Visor de Ayuda v2.x, puede ver el contenido en línea mediante una de las siguientes acciones.

- En SQL Server Management Studio, haga clic en **Ver Ayuda** en el menú **Ayuda**. La documentación se muestra en un explorador.
![HelpViewer2_SSMS_ChooseOnlineORLocalHelp](../sql-server/media/helpviewer2-ssms-chooseonlineorlocalhelp.png)

- En Visual Studio, haga clic en **Establecer preferencias de la Ayuda** en el menú **Ayuda** y luego en **Iniciar en el explorador**. Al hacer clic en **Ver Ayuda** en el menú **Ayuda**, la documentación se muestra en un explorador.

![HelpViewer2_VisualStudio_ChooseOnlineORLocalHelp](../sql-server/media/helpviewer2-visualstudio-chooseonlineorlocalhelp.png)   

En el Visor de Ayuda v1.x, puede ver el contenido en línea si hace lo siguiente.
1. Haga clic en **Administrar configuración de la Ayuda** en el menú **Ayuda** para abrir el **Administrador de bibliotecas de Ayuda**.  
2. En el cuadro de diálogo **Administrador de bibliotecas de Ayuda**, haga clic en **Elegir Ayuda en línea o local**.  
  
   ![HelpLibraryManager_MainPage_ChooseOnlineORLocal.png](../sql-server/media/helplibrarymanager-mainpage-chooseonlineorlocal.png.png)  
3. Haga clic en **I want to use online help** (Quiero usar la Ayuda en línea), en **Aceptar** y luego en **Salir**.  

   ![HelpLibraryManager_ChooseOnlineORLocalHelp_OnlineHelpSelected_dialog](../sql-server/media/helplibrarymanager-chooseonlineorlocalhelp-onlinehelpselected-dialog.png)

## <a name="f1-help-and-other-tips"></a>Ayuda F1 y otras sugerencias

Cuando se presiona F1, aparece en pantalla el tema correspondiente. El tema no se puede mostrar en la Ayuda local.

Además, el Visor de Ayuda no admite la configuración del proxy ni tampoco el formato ISO. 

## <a name="additional-information"></a>Información adicional
[Visor de Ayuda de Microsoft (Visual Studio 2015)](https://msdn.microsoft.com/library/hh580782.aspx)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
