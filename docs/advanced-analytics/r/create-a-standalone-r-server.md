---
title: Crear un R Server independiente | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 408e2503-5c7d-4ec4-9d3d-bba5a8c7661d
caps.latest.revision: 35
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4f39a03ecf7b74e0e1305d692a71c28609c80bf0
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-standalone-r-server"></a>Crear un R Server independiente

El programa de instalación de SQL Server incluye la opción para instalar un servidor que se ejecuta fuera de SQL Server de aprendizaje automático. 

Esta opción puede ser útil si tiene que desarrollar soluciones de R de alto rendimiento en Windows y, a continuación, compartir las soluciones en otras plataformas. También puede utilizar la opción de servidor para configurar un entorno para compilar soluciones para admite la ejecución de estos contextos de proceso remoto:
  
  + Una instancia de SQL Server que ejecuta R Services
  + Una instancia de R Server con un clúster de Hadoop o Spark
  + Análisis en base de datos de Teradata
  + R Server en ejecución en Linux 

Este tema describe los pasos de configuración en el programa de instalación de SQL Server para Microsoft R Server y servidor de aprendizaje de máquina de Microsoft.

## <a name="which-should-i-install"></a>¿Lo que debo instalar?

**Microsoft R Server** se ofrece por primera vez como parte de SQL Server 2016 y es compatible con el lenguaje R. La última versión de Microsoft R Server era 9.0.1.
En SQL Server de 2017 cambió R Server **aprendizaje de máquina de Microsoft Server**, con compatibilidad para Python agregada. La versión más reciente del servidor de aprendizaje de máquina de Microsoft es 9.1.0.

Microsoft R Server y servidor de aprendizaje de máquina de Microsoft requieren Enterprise Edition.

+ [Instalar a Microsoft R Server (independiente) utilizando el programa de instalación de SQL Server](#bkmk_installRServer)
+ [Instalar a Microsoft Server de aprendizaje de máquina (independiente) mediante el programa de instalación de SQL Server](#bkmk_installRServer) 

  El programa de instalación requiere una licencia de SQL Server. Las actualizaciones normalmente se alinean con la cadencia de lanzamiento de SQL Server. Esto garantiza que las herramientas de desarrollo estén sincronizadas con la versión que se ejecuta en el contexto de proceso de SQL Server.

+ [Instalar a R Server para Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)

  Con esta opción, el servidor de R se instala mediante la directiva de soporte técnico de ciclo de vida moderna. También puede ejecutar a este instalador después de la instalación para actualizar una instancia de SQL Server 2016. Actualmente, se _no_ instalar Python admite el uso de esta opción. Para obtener Python, debe instalar el servidor de aprendizaje de máquina mediante el programa de instalación de SQL Server 2017.

##  <a name="bkmk_installRServer"></a>Cómo instalar Microsoft Machine Learning Server (independiente)
  
1. Si ha instalado una versión anterior de Microsoft R Server, se recomienda desinstalarlo primero.

2. Ejecute el programa de instalación de SQL Server 2017.
  
3. Haga clic en el **instalación** pestaña y seleccione **instalación nuevo servidor de aprendizaje de máquina (independiente)**.

4. Una vez completada la comprobación de reglas, acepte los términos de licencia de SQL Server y seleccione una nueva instalación.

5. En el **selección de características** lo siguiente de la página Opciones ya deberían estar seleccionadas:
    
    - Microsoft Machine Learning Server (independiente)
    
    - R y Python se selecciona de forma predeterminada.
    
    El resto de opciones se deben omitir.

6.  Acepte los términos de licencia para descargar e instalar los componentes de aprendizaje automático. Un contrato de licencia independiente es necesario para Microsoft R Open y Python. 
    
    Si el botón **Aceptar** no está disponible, puede hacer clic en **Siguiente**. 
    
    La instalación de estos componentes (y todos los requisitos previos que necesiten) puede tardar varios minutos. 
    
    Si el equipo no tiene acceso a Internet, debe descargar a los instaladores de componentes de antemano. Para obtener más información, consulte [componentes de aprendizaje automático de instalación sin acceso a Internet](./installing-ml-components-without-internet-access.md). 
    
7.  En la página **Listo para instalar** , compruebe las opciones seleccionadas y haga clic en **Instalar**.


Para obtener más información sobre la instalación automatizada o sin conexión, consulte [Instalar Microsoft R Server desde la línea de comandos](../../advanced-analytics/r-services/install-microsoft-r-server-from-the-command-line.md).

###  <a name="bkmk_installRServer"></a> Instalar Microsoft R Server (independiente)  

1. Si ha instalado una versión anterior de Microsoft R Server o cualquier versión de las herramientas de Revolution Analytics, debe desinstalar primero.  Consulte [Actualizar desde una versión anterior de Microsoft R Server](#bkmk_Uninstall).

2. Ejecute el programa de instalación de SQL Server 2016. Se recomienda que instale Service Pack 1 o posterior.

3. En la pestaña **Instalación** , haga clic en **New R Server (Standalone) installation** (Instalación de nuevo R Server (independiente)).
    
     ![Opción de configuración para R Server independiente](media/rsql-rstandalonesetup.png "Opción de configuración para R Server independiente")
    
4.  En la página **Selección de características** , la siguiente opción ya debería estar seleccionada:
    
    **R Server (Standalone)**  
    
    El resto de opciones se deben omitir. No instale el motor de base de datos de SQL Server o SQL Server R Services.
    
5.  Acepte los términos de licencia para descargar e instalar Microsoft R Open. Si el botón **Aceptar** no está disponible, puede hacer clic en **Siguiente**. 
    
    La instalación de estos componentes (y todos los requisitos previos que necesiten) puede tardar varios minutos.
    
6.  En la página **Listo para instalar** , compruebe las opciones seleccionadas y haga clic en **Instalar**.  


### <a name="upgrade-an-existing-r-server-to-901"></a>Actualizar un servidor existente de R a 9.0.1

Si ha instalado una versión anterior de Microsoft R Server (independiente) se puede actualizar la instancia para usar versiones más recientes de los componentes de R. La actualización cambia también el servidor de directiva de soporte técnico de ciclo de vida moderna. Esto permite que la instancia se actualicen con más frecuencia, en una programación diferente de versiones de SQL Server.

1. Instale Microsoft R Server (independiente) si aún no lo ha instalado.

2. Descargar el instalador independiente basado en Windows desde las ubicaciones siguientes: [ejecutar Microsoft R Server para Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#howtoinstall).

3. Ejecute el programa de instalación y siga [estas instrucciones](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#download-r-server-installer).


### <a name="change-in-default-folder-for-r-packages"></a>Cambiar carpeta de forma predeterminada en paquetes de R

Cuando se instala mediante el programa de instalación de SQL Server, se instalan las bibliotecas de R en una carpeta asociada a la versión de SQL Server que utilizó para el programa de instalación. En esta carpeta también encontrará datos de ejemplo, documentación sobre los paquetes base de R y documentación sobre las herramientas y el tiempo de ejecución de R.

**R Server (independiente) con la instalación mediante SQL Server 2016**

`C:\Program Files\Microsoft SQL Server\130\R_SERVER`

**R Server (independiente) con la instalación mediante SQL Server 2017**

`C:\Program Files\Microsoft SQL Server\140\R_SERVER`

**El programa de instalación con el instalador independiente de Windows**

Sin embargo, si se instalan mediante el instalador independiente de Windows, o si se actualiza mediante el instalador independiente de Windows, las bibliotecas de R se mueven a la carpeta del servidor de R siguiente:

`C:\Program Files\Microsoft\R Server\R_SERVER`
      
**En las bases de datos de servicios de instalación de R Services o de aprendizaje automático**

Si ha instalado una instancia de SQL Server con R Services (In-Database) o servicios de aprendizaje de máquina (In-Database), y esa instancia se encuentra en el mismo equipo, las bibliotecas de R y herramientas se instalan de forma predeterminada en una carpeta diferente:

`C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES`

No llame directamente a los paquetes o a las utilidades de R asociados a la instancia de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Si el servidor de R y R Services están instalados en el mismo equipo, cuando necesita ejecutar RGui u otras herramientas, use las herramientas de R y los paquetes instalados en la carpeta R_SERVER.


### <a name="development-tools"></a>Herramientas de desarrollo

IDE de desarrollo no se instala como parte del programa de instalación. No se requieren herramientas adicionales, tal y como se incluyen todas las herramientas estándares que se proporcionan con una distribución de R o Python.

Le recomendamos que intente la la nueva versión de [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)], como Visual Studio es compatible con herramientas de R y Python, así como SQL Server y BI. Sin embargo, puede usar cualquier entorno de desarrollo preferido, incluido RStudio.

## <a name="troubleshooting"></a>Solucionar problemas  

### <a name="incompatible-version-of-r-client-and-r-server"></a>Versión incompatible del Cliente de R y R Server

Si instala la versión más reciente del Cliente de Microsoft R y lo usa para ejecutar R en SQL Server mediante un contexto de proceso remoto, podría aparecer el error siguiente:

*Está ejecutando la versión 9.0.0 del cliente de Microsoft R en el equipo, que es incompatible con la versión del servidor 8.0.3 de Microsoft R. Download and install a compatible version.* (Está ejecutando la versión 9.0.0 del Cliente de Microsoft R en el equipo, que es incompatible con Microsoft R Server versión 8.0.3. Descargue e instale una versión compatible).

Normalmente, la versión de R que se instala con SQL Server R Services se actualiza cuando se publican versiones de servicio. Para garantizar que siempre tenga las versiones más actualizadas de los componentes de R, instale todos los Service Pack. Para que haya compatibilidad con Cliente de Microsoft R 9.0.0, debe instalar las actualizaciones que se describen en este [artículo de soporte técnico](https://support.microsoft.com/kb/3210262). 


### <a name="installing-microsoft-r-server-on-an-instance-of-sql-server-installed-on-windows-core"></a>Instalar Microsoft R Server en una instancia de SQL Server instalada en Windows Core

En la versión RTM de SQL Server 2016, se produjo un problema conocido al agregar Microsoft R Server en una instancia de la edición de Windows Server Core. Esto se ha solucionado.

Si se produce este problema, puede aplicar la revisión que se describe en [KB3164398](https://support.microsoft.com/kb/3164398) para agregar la característica R a la instancia existente en Windows Server Core.   Para obtener más información, consulte [No se puede instalar Microsoft R Server (independiente) en un sistema operativo Windows Server Core](https://support.microsoft.com/kb/3168691).


###  <a name="bkmk_Uninstall"></a> Actualizar desde una versión anterior de Microsoft R Server

Si ha instalado una versión preliminar de Microsoft R Server, debe desinstalarla para poder actualizar a una versión más reciente.

**Para desinstalar R Server (independiente)**

1.  En el **Panel de control**, haga clic en **Agregar o quitar programas**y seleccione `Microsoft SQL Server 2016 <version number>`.  
  
2.  En el cuadro de diálogo con opciones para **Agregar**, **Reparar**o **Quitar** componentes, seleccione **Quitar**.  
  
3.  En la página **Seleccionar características** , en **Características compartidas**, seleccione **R Server (independiente)**. Haga clic en **Siguiente**y, después, haga clic en **Finalizar** para desinstalar los componentes seleccionados.  
   
### <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>La instalación no puede llevarse a cabo y se genera el siguiente error: "Only one Revolution Enterprise product can be installed at a time." (Solo se puede instalar de cada vez un producto Revolution Enterprise).

Es posible que se produzca este error si tiene una instalación anterior de productos Revolution Analytics o una versión preliminar de SQL Server R Services. Debe desinstalar todas las versiones anteriores para poder instalar una versión más reciente de Microsoft R Server. No se admite la instalación en paralelo con otras versiones de herramientas de Revolution Enterprise.

En cambio, se admiten las instalaciones en paralelo cuando se usa R Server (independiente) con [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] o SQL Server 2016.

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


