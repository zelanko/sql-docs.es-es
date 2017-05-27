---
title: Visor de Ayuda para SQL Server | Microsoft Docs
ms.custom: 
ms.date: 02/15/2017
ms.prod: sql-non-specified
ms.technology: server-general
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2014
- SQL Server 2016
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: fc2435ccea3b01328c3c4623e62fbf12ee53e400
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="help-viewer-for-sql-server"></a>Visor de Ayuda para SQL Server
  
  
  
Este artículo le guiará por los pasos necesarios para instalar la Ayuda local y mostrar la Ayuda local y en línea. En el artículo se describe el Visor de Ayuda de Microsoft 1.1 y 2.2 y se incluye documentación para [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] y [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]. 

>[!IMPORTANT]
>El Visor de Ayuda no admite la configuración del proxy ni tampoco el formato ISO.  

>**F1 y la Ayuda**
>>Cuando se presiona F1, aparece en pantalla el tema correspondiente. El tema no se puede mostrar en la Ayuda local.

## <a name="includesscurrentmdincludessscurrent-mdmd-and-help-viewer-22"></a>[!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] y el Visor de Ayuda 2.2  
El Visor de Ayuda 2.2 está disponible en [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] Management Studio a partir de la versión preliminar de abril de 2016 (13.0.12500.29) y en Visual Studio 2015.  

> [![Descargar SSMS](../release-notes/media/download.png)](https://msdn.microsoft.com/library/mt238290.aspx)Descargar la versión más reciente de **[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)**  

**Para instalar la Ayuda local para su uso con el Visor de Ayuda 2.2**  
1. Abra el Visor de Ayuda 2.2. Para ello, inicie SQL Server Management Studio o Visual Studio y haga clic en **Agregar y quitar contenido de la Ayuda** en el menú **Ayuda**.  
2. Haga clic en la pestaña **Administrar contenido**.  
3. Para instalar la Ayuda desde un origen en línea, haga clic en **En línea** en el área **Origen de la instalación**.  
![HelpViewer2_ManageContent_OnlineSource](../release-notes/media/helpviewer2-managecontent-onlinesource.png)  
7. Haga clic en **Agregar** junto a la documentación que quiera instalar y en **Actualizar**.  
![HelpViewer2_ManageContent_AddContent](../release-notes/media/helpviewer2-managecontent-addcontent.png)     
  
   >[!IMPORTANT] 
   >En SQL Server Management Studio y Visual Studio, la aplicación del Visor de Ayuda puede bloquearse mientras se agrega la documentación. Haga lo siguiente para solucionar este problema. Para obtener más información sobre este problema, vea [Visual Studio Help Viewer freezes](https://msdn.microsoft.com/library/mt654096.aspx)(El Visor de Ayuda de Visual Studio se bloquea).  
   >>Abra el archivo %LOCALAPPDATA%\Microsoft\HelpViewer2.2\HlpViewer_SSMS16_en-US.settings | HlpViewer_VisualStudio14_en-US.settings en el Bloc de notas y cambie la fecha en el siguiente código a una fecha en el futuro. Este archivo solo está disponible en el equipo local si se tiene instalado Visual Studio. 
   >>>Última actualización de la caché="31/12/2017 00:00:00"  
  
    La tabla de contenido del panel izquierdo se actualiza automáticamente para incluir la documentación que se ha agregado.  
![HelpViewer2_withContentInstalled](../release-notes/media/helpviewer2-withcontentinstalled.png)

1. (Opcional) En el cuadro **Ruta de acceso del almacén local** de la pestaña **Administrar contenido** se muestra el lugar en el que está instalada la documentación en el equipo local. Para moverla a una ubicación diferente, haga clic en **Mover**, escriba una ruta de carpeta en el campo **A** del cuadro de diálogo **Mover contenido** y, después, haga clic en **Aceptar**.

   ![HelpViewer2_MoveContent_Dialog](../release-notes/media/helpviewer2-move-content-dialog.png)

   Una vez que se haya movido el contenido, se muestra la nueva ubicación en la **Ruta de acceso del almacén local**.
      
   >[!IMPORTANT]
   > Si aparece un mensaje que indica que se ha producido un error en la operación de mover, cierre el cuadro de mensaje, cierre el Visor de Ayuda y, después, vuelva a abrir el Visor de Ayuda. La nueva ubicación del contenido debería aparecer ahora en la **Ruta de acceso del almacén local**.   
  
**Para mostrar la Ayuda local o en línea en SQL Server Management Studio**  
* Para ver la Ayuda local, haga clic en **Agregar y quitar contenido de la Ayuda** en el menú **Ayuda** y, después, haga clic en la pestaña **Página principal del Visor de Ayuda** para ver la documentación.  
    >[!NOTE]
    >El texto de la **Página principal del Visor de Ayuda** cambia en función del tema en el que se haya hecho clic en la tabla de contenido.   
* Para ver la Ayuda en línea, haga clic en **Ver Ayuda** en el menú **Ayuda**. La documentación se muestra en un explorador.  
![HelpViewer2_SSMS_ChooseOnlineORLocalHelp](../release-notes/media/helpviewer2-ssms-chooseonlineorlocalhelp.png)  
  
  
**Para mostrar la Ayuda local o en línea en Visual Studio**  
* Haga clic en **Establecer preferencias de la Ayuda** en el menú **Ayuda** y realice una de las acciones siguientes.  
   * Haga clic en **Iniciar en el explorador** para ver la Ayuda en línea. Al hacer clic en **Ver Ayuda** en el menú **Ayuda**, la documentación se muestra en un explorador.  
   * Haga clic en **Iniciar en el Visor de Ayuda** para ver la Ayuda local. Al hacer clic en **Ver Ayuda** en el menú **Ayuda**, la documentación se muestra en el Visor de Ayuda.  
     
     ![HelpViewer2_VisualStudio_ChooseOnlineORLocalHelp](../release-notes/media/helpviewer2-visualstudio-chooseonlineorlocalhelp.png)  
  
  
## <a name="includesssql14mdincludessssql14-mdmd-and-help-viewer-11"></a>[!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] y el Visor de Ayuda 1.1  
 El Visor de Ayuda 1.1 está disponible en [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] Management Studio y en versiones de Visual Studio anteriores a Visual Studio 2012.   
 
>[!NOTE]
> También puede ver la Ayuda local de [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] mediante el Visor de Ayuda 2.2, pero únicamente si selecciona **Instalar contenido desde disco**. El Visor de Ayuda 2.2 está disponible en [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] Management Studio a partir de la versión preliminar de abril de 2016 (13.0.12500.29) y en Visual Studio 2015. 
   
**Para instalar la Ayuda local para su uso con el Visor de Ayuda 1.1**  
1. Vaya al [sitio de descarga](https://www.microsoft.com/en-us/download/details.aspx?id=42557) del contenido de Ayuda y haga clic en **Descargar**.  
2. Haga clic en **Guardar** en el cuadro de mensaje para guardar el archivo SQLServer2014Documentation_*.exe en el equipo.  
   >[!NOTE]
   >Para entornos restringidos con firewall y proxy, guarde la descarga en una unidad USB u otro medio portátil que se pueda llevar al entorno.   
3. Haga doble clic en el archivo .exe para desempaquetar el archivo de contenido de Ayuda y guarde el archivo en una carpeta local o compartida.  
4. Abra el **Administrador de bibliotecas de Ayuda**. Para ello, inicie SQL Server Management Studio o Visual Studio y haga clic en **Administrar configuración de la Ayuda** en el menú **Ayuda**.  
7. Haga clic en **Instalar contenido desde disco** y vaya a la carpeta en la que ha desempaquetado el archivo de contenido de Ayuda.  
  
Seleccione Instalar contenido desde disco.  |Vaya al archivo de contenido de Ayuda.   
---------|---------  
![HelpLibraryManager_MainPage_InstallFromDisk](../release-notes/media/helplibrarymanager-mainpage-installfromdisk.png)    | ![HelpLibraryManager_InstallContentFromDisk_dialog1](../release-notes/media/helplibrarymanager-installcontentfromdisk-dialog1.png)          
  
>[!IMPORTANT]
> Para no instalar contenido de Ayuda local que solo tenga una tabla de contenido parcial, use la opción **Instalar contenido desde disco** en el **Administrador de bibliotecas de Ayuda**.  
>>Si ha usado la opción **Instalar contenido desde Internet** y el Visor de Ayuda muestra una tabla de contenido parcial, vea los pasos para solucionar problemas en esta [entrada de blog](https://blogs.msdn.microsoft.com/womeninanalytics/2016/06/21/troubleshoot-local-help-for-sql-server-2014/). 

8. Haga clic en el archivo HelpContentSetup.msha, en **Abrir** y en **Siguiente**.  
9. Haga clic en **Agregar** junto a la documentación que quiera instalar y en **Actualizar**.  
  
   ![HelpLibraryManager_InstallContentFromDisk_dialog2](../release-notes/media/helplibrarymanager-installcontentfromdisk-dialog2.png)  
10. Haga clic en **Finalizar** y en **Salir**. Después, haga clic en **Ver Ayuda** en el menú **Ayuda** para abrir el Visor de Ayuda y ver el contenido. El contenido que ha instalado debería aparecer en la tabla de contenido, en el panel izquierdo.  
  
    ![HelpViewer1_withContentInstalled_ZoomedIn](../release-notes/media/helpviewer1-withcontentinstalled-zoomedin.png)  
  
**Para mostrar la Ayuda local o en línea**  
1. Haga clic en **Administrar configuración de la Ayuda** en el menú **Ayuda** para abrir el **Administrador de bibliotecas de Ayuda**.  
2. En el cuadro de diálogo **Administrador de bibliotecas de Ayuda**, haga clic en **Elegir Ayuda en línea o local**.  
  
   ![HelpLibraryManager_MainPage_ChooseOnlineORLocal.png](../release-notes/media/helplibrarymanager-mainpage-chooseonlineorlocal.png.png)  
3. Realice una de las siguientes acciones y, después, haga clic en **Aceptar** y en **Salir**.  
   * Haga clic en **I want to use online help** (Quiero usar la Ayuda en línea).  
   * Haga clic en **I want to use local help** (Quiero usar la Ayuda local).  
  
   ![HelpLibraryManager_ChooseOnlineORLocalHelp_OnlineHelpSelected_dialog](../release-notes/media/helplibrarymanager-chooseonlineorlocalhelp-onlinehelpselected-dialog.png)  
  
Si ha seleccionado usar la Ayuda en línea, al hacer clic en **Ver Ayuda** en el menú **Ayuda**, el explorador se abrirá y mostrará el artículo [Libros en pantalla de SQL Server 2014](https://msdn.microsoft.com/library/ms130214(v=sql.120).aspx) en MSDN. Si ha seleccionado usar la Ayuda local, al hacer clic en **Ver Ayuda** se iniciará el Visor de Ayuda.  

## <a name="additional-information"></a>Información adicional
[Visor de Ayuda de Microsoft (Visual Studio 2015)](https://msdn.microsoft.com/library/hh580782.aspx)

