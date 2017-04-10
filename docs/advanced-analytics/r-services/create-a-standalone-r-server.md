---
title: "Crear un R Server independiente | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 408e2503-5c7d-4ec4-9d3d-bba5a8c7661d
caps.latest.revision: 35
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 27
---
# Crear un R Server independiente
  El programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye la opción de instalar **Microsoft R Server (independiente)**. Esta opción le permite desarrollar soluciones de R de alto rendimiento en Windows al conectarse a la base de datos u origen de datos de su elección. Microsoft R Server solo está disponible en la edición Enterprise.  
  
 Al instalar Microsoft R Server, obtendrá las mismas herramientas de conectividad y paquetes de R mejorados que se proporcionan en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], pero no se requiere una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y la ejecución de scripts de R se realiza en el equipo independiente, no en la base de datos.  
  
> [!NOTE]  
>  Microsoft R Server ahora también está disponible mediante una instalación simplificada que inscribe la instancia en la [directiva moderna de ciclo de vida](https://support.microsoft.com/help/447912). Esta oferta de compatibilidad garantiza que siempre use la versión más reciente de R. Para obtener más información sobre el uso de la instalación simplificada, consulte [Run Microsoft R Server for Windows](https://msdnstage.redmond.corp.microsoft.com/microsoft-r/rserver-install-windows?branch=r-server-nov16-dev) (Ejecutar Microsoft R Server para Windows).
>  
> Si instala Microsoft R Server mediante la instalación simplificada, también puede convertir cualquier instancia especificada de R Services para que use la nueva directiva de compatibilidad y obtener actualizaciones más frecuentes de componentes de R. Para obtener más información, consulte [Use sqlBindR.exe to upgrade an instance of R Services](http://www.bing.com) (Usar sqlBindR.exe para actualizar una instancia de R Services).   
  
##  <a name="a-namebkmkinstallrservicesindatabasea-install-microsoft-r-server-standalone"></a><a name="bkmk_installRServicesInDatabase"></a> Instalar Microsoft R Server (independiente)  
  
1.  Si ya ha instalado una versión anterior de Microsoft R Server, debe desinstalarla.  Consulte [Actualizar desde una versión anterior de Microsoft R Server](#bkmk_Uninstall). 

2. Ejecute el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  En la pestaña **Instalación** , haga clic en **New R Server (Standalone) installation** (Instalación de nuevo R Server (independiente)).  
  
     ![Setup option for R Server Standalone](../../advanced-analytics/r-services/media/rsql-rstandalonesetup.png "Setup option for R Server Standalone")  
  
3.  En la página **Selección de características** , la siguiente opción ya debería estar seleccionada:  
  
    -   **R Server (Standalone)**  
  
         Esta opción instala características compartidas, incluidos paquetes base y herramientas de R de código abierto, así como paquetes de R mejorados y herramientas de conectividad proporcionadas por Microsoft R.  
  
     El resto de opciones se deben omitir.  
  
4.  Acepte los términos de licencia para descargar e instalar Microsoft R Open. Si el botón **Aceptar** no está disponible, puede hacer clic en **Siguiente**. La instalación de estos componentes (y todos los requisitos previos que necesiten) puede tardar varios minutos.   
  
5.  En la página **Listo para instalar**, compruebe las opciones seleccionadas y haga clic en **Instalar**.  
  
> [!TIP]
> Para obtener más información sobre la instalación automatizada o sin conexión, consulte [Instalar Microsoft R Server desde la línea de comandos](../../advanced-analytics/r-services/install-microsoft-r-server-from-the-command-line.md).

  
## <a name="what-is-installed-and-where-to-find-r-packages"></a>Qué está instalado y dónde encontrar paquetes de R  
 Microsoft R Server incluye los paquetes base de R y una serie de paquetes de R mejorados que admiten el procesamiento en paralelo, el rendimiento mejorado y la conectividad con orígenes de datos, incluidos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y Hadoop.  
  
-   **Paquetes de R**  
  
     Las bibliotecas de R se instalan junto con otras herramientas y utilidades que se instalan con Microsoft SQL Server 2016. Por ejemplo:  
  
     `C:\Program Files\Microsoft SQL Server\130\R_SERVER`  
  
     Además, en esta carpeta encontrará documentación sobre los paquetes base de R, datos de ejemplo y documentación sobre las herramientas y el tiempo de ejecución de R.  
  
    > [!NOTE]  
    >  Si ha instalado una instancia de SQL Server con R Services (en bases de datos) en el mismo equipo, las bibliotecas y las herramientas de R se instalarán en una carpeta diferente: `C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES`.  
    >   
    >  No use los paquetes o las utilidades de R asociados a la instancia de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Use siempre las herramientas y los paquetes de R de la carpeta R_SERVER.  
  
-   **Herramientas de R**  
  
     No se instala un IDE de desarrollo de R como parte de la instalación. Puede instalar RStudio, [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] u otro entorno de desarrollo que prefiera.  
  
     No se requieren herramientas adicionales. Todas las herramientas base estándar de R están incluidas en `C:\Program Files\Microsoft SQL Server\130\R_SERVER\bin`.  
  
     Para obtener más información, consulte [Instalar o configurar herramientas de R](../../advanced-analytics/r-services/setup-or-configure-r-tools.md).  


 
## <a name="troubleshooting"></a>Solucionar problemas  

### <a name="incompatible-version-of-r-client-and-r-server"></a>Versión incompatible del Cliente de R y R Server

Si instala la versión más reciente del Cliente de Microsoft R y lo usa para ejecutar R en SQL Server mediante un contexto de proceso remoto, podría aparecer el error siguiente:

*You are running version 9.0.0 of Microsoft R client on your computer, which is incompatible with the Microsoft R server version 8.0.3. Download and install a compatible version.* (Está ejecutando la versión 9.0.0 del Cliente de Microsoft R en el equipo, que es incompatible con Microsoft R Server versión 8.0.3. Descargue e instale una versión compatible).

Normalmente, la versión de R que se instala con SQL Server R Services se actualiza cuando se publican versiones de servicio. Para garantizar que siempre tenga las versiones más actualizadas de los componentes de R, instale todos los Service Pack. Para que haya compatibilidad con Cliente de Microsoft R 9.0.0, debe instalar las actualizaciones que se describen en este [artículo de soporte técnico](https://support.microsoft.com/kb/3210262). 


### <a name="installing-microsoft-r-server-on-an-instance-of-sql-server-installed-on-windows-core"></a>Instalar Microsoft R Server en una instancia de SQL Server instalada en Windows Core
En la versión de lanzamiento de SQL Server 2016, se producía un problema al agregar Microsoft R Server a una instancia de la edición Windows Server Core. Esto se ha solucionado. 

Si se produce este problema, puede aplicar la revisión que se describe en [KB3164398](https://support.microsoft.com/kb/3164398) para agregar la característica R a la instancia existente en Windows Server Core.   Para obtener más información, consulte [No se puede instalar Microsoft R Server (independiente) en un sistema operativo Windows Server Core](https://support.microsoft.com/kb/3168691).


###  <a name="a-namebkmkuninstalla-upgrading-from-an-older-version-of-microsoft-r-server"></a><a name="bkmk_Uninstall"></a> Actualizar desde una versión anterior de Microsoft R Server  
 Si ha instalado una versión preliminar de Microsoft R Server, debe desinstalarla para poder actualizar a una versión más reciente.  
  
**Para desinstalar R Server (independiente)**  
  
1.  En el **Panel de control**, haga clic en **Agregar o quitar programas** y seleccione `Microsoft SQL Server 2016 <version number>`.  
  
2.  En el cuadro de diálogo con opciones para **Agregar**, **Reparar** o **Quitar** componentes, seleccione **Quitar**.  
  
3.  En la página **Seleccionar características**, en **Características compartidas**, seleccione **R Server (independiente)**. Haga clic en **Siguiente** y, después, haga clic en **Finalizar** para desinstalar los componentes seleccionados.  
   
### <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>La instalación no puede llevarse a cabo y se genera el siguiente error: "Only one Revolution Enterprise product can be installed at a time." (Solo se puede instalar de cada vez un producto Revolution Enterprise).  
Es posible que se produzca este error si tiene una instalación anterior de productos Revolution Analytics o una versión preliminar de SQL Server R Services. Debe desinstalar todas las versiones anteriores para poder instalar una versión más reciente de Microsoft R Server. No se admite la instalación en paralelo con otras versiones de herramientas de Revolution Enterprise.  

En cambio, se admiten las instalaciones en paralelo cuando se usa R Server (independiente) con [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y 
  
### <a name="unable-to-uninstall-older-components"></a>No se pueden desinstalar componentes anteriores   
  
Si tiene problemas para quitar una versión anterior, puede que deba editar el Registro para quitar las claves relacionadas.  

> [!IMPORTANT]
> Este problema se produce únicamente si ha instalado una versión preliminar de Microsoft R Server o una versión CTP de SQL Server 2016 R Services.
  
1. Abra el Registro de Windows y busque esta clave: `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`.  
2. Elimine todas las entradas siguientes, si están presentes, y si la clave solo contiene el valor `sEstimatedSize2`:  
  
    -   E0B2C29E-B8FC-490B-A043-2CAE75634972        (para 8.0.2)  
  
    -   46695879-954E-4072-9D32-1CC84D4158F4        (para 8.0.1)  
  
    -   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B        (para 8.0.0)  
  
    -   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A        (para 7.5.0)  
  
## <a name="see-also"></a>Vea también  
 [Microsoft R Server](../../advanced-analytics/r-services/r-server-standalone.md)  
  
  