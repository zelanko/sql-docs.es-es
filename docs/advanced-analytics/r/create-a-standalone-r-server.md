---
title: "Instalar R Server independiente o independiente de servidor de aprendizaje de máquina | Documentos de Microsoft"
ms.custom: 
ms.date: 11/16/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 408e2503-5c7d-4ec4-9d3d-bba5a8c7661d
caps.latest.revision: "35"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 5c27e75bf6248ebb403235e339750cf935ee3a3d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone"></a>Instalar servidor de aprendizaje de máquina (independiente) o R Server (independiente)

El programa de instalación de SQL Server incluye la opción para instalar un servidor que se ejecuta fuera de SQL Server de aprendizaje automático. Esta opción puede ser útil si tiene que desarrollar soluciones de aprendizaje de máquina de alto rendimiento que pueda usar contextos de proceso remoto o que se pueden implementar en varias plataformas, como:
  
  + Una instancia de SQL Server 2016 o 2017 de SQL Server donde está habilitado el aprendizaje automático
  + Una instancia de servidor de R o servidor de aprendizaje de máquina en un clúster de Hadoop o Spark
  + Servidor de R o servidor de aprendizaje de máquina en Linux

Este artículo describe cómo usar el programa de instalación de SQL Server para instalar la versión independiente del servidor de aprendizaje de máquina o Microsoft R Server. Si tiene una edición Enterprise o Software Assurance, instalar al servidor de aprendizaje automático de independiente es gratuito.

+ [Instalar R Server](#bkmk_installRServer) -utiliza el programa de instalación de SQL Server 2016
+ [Instalar el servidor de aprendizaje de máquina](#bkmk_installMLServer) -utiliza el programa de instalación de SQL Server 2017
+ [Actualizar una instancia existente de Microsoft R Server](#bkmk_upgrade)
+ [Ayuda para decidir lo que desea instalar](#bkmk_tips)

##  <a name="bkmk_installMLServer"></a>Instalar Server (independiente) de aprendizaje automático

Esta característica requiere una licencia Enterprise o un equivalente para **SQL Server 2017**.

Si ha instalado una versión anterior de Microsoft R Server, se recomienda desinstalarlo primero.

Si el equipo no tiene acceso a Internet, debe descargar a los instaladores de componentes de antemano. Para obtener más información, consulte [instalación de componentes de aprendizaje de máquina sin acceso a internet](./installing-ml-components-without-internet-access.md).

1. Ejecute el programa de instalación de SQL Server 2017.

2. Haga clic en el **instalación** pestaña y seleccione **instalación nuevo servidor de aprendizaje de máquina (independiente)**.
    
     ![Instalación independiente de servidor de aprendizaje de máquina](media/2017setup-installation-page-mlsvr.png "iniciar la instalación de servidor independiente de aprendizaje de máquina")

3. Una vez completada la comprobación de reglas, acepte los términos de licencia de SQL Server y seleccione una nueva instalación.

4. En el **selección de características** página siguiente ya deberían estar seleccionadas opciones:

    - Microsoft Machine Learning Server (independiente)

    - R y Python se selecciona de forma predeterminada. Puede anular la selección de cualquiera de estos lenguajes, pero se recomienda que instale al menos uno de los idiomas admitidos.

     ![Instalación independiente de servidor de aprendizaje de máquina](media/2017setup-features-page-mlsvr-rpy.png "iniciar la instalación de servidor independiente de aprendizaje de máquina")
    
    El resto de opciones se deben omitir. 
    
    > [!NOTE]
    > Evitar la instalación de la **características compartidas** si el equipo ya tiene servicios de aprendizaje de máquina instalado para el análisis de bases de datos de SQL Server. Esto crea bibliotecas duplicadas.
    > 
    > Además, mientras que los scripts de R o Python que se ejecutan en SQL Server se administran mediante SQL Server para no tener que entrar en conflicto con la memoria utilizada por otros servicios de motor de base de datos, el servidor de aprendizaje de máquina independiente no tiene estas restricciones y puede interferir con otras operaciones de base de datos . Por último, acceso remoto a través de la sesión RDP, que se suele utilizar para la puesta en marcha, suele estar bloqueado por los administradores de base de datos.
    > 
    > Por estos motivos, generalmente recomendamos que instale el servidor de aprendizaje de máquina (independiente) en un equipo independiente de servicios de aprendizaje de máquina de SQL Server.

5.  Acepte los términos de licencia para descargar e instalar los componentes de aprendizaje automático. Si instala ambos lenguajes, un contrato de licencia independiente es necesario para Microsoft R y Python.
    
     ![Contrato de licencia de Python](media/2017setup-python-license.png "Python del acuerdo de licencia")
    
    Instalación de estos componentes y los requisitos previos que necesiten, podría llevar algún tiempo. Si el botón **Aceptar** no está disponible, puede hacer clic en **Siguiente**.

6.  En la página **Listo para instalar** , compruebe las opciones seleccionadas y haga clic en **Instalar**.

Para obtener más información acerca de la instalación automatizada o fuera de línea, consulte [instalar Microsoft R Server desde la línea de comandos](../../advanced-analytics/r/install-microsoft-r-server-from-the-command-line.md).

##  <a name="bkmk_installRServer"></a> Instalar Microsoft R Server (independiente)

Esta característica requiere una licencia Enterprise o un equivalente para **SQL Server 2016**.

Si ha instalado cualquier versión anterior de las herramientas de Revolution Analytics o paquetes, debe desinstalarlas primero. Vea [actualizar desde una versión anterior de Microsoft R Server](#bkmk_Uninstall).

1. Ejecute el programa de instalación de SQL Server 2016. Se recomienda que instale Service Pack 1 o posterior.

2. En el **instalación** , haga clic en **instalación de nuevo R Server (independiente)**.
    
     ![Iniciar el programa de instalación de R Server independiente](media/2016-setup-installation-rsvr.png "iniciar el programa de instalación de R Server independiente")
    
3.  En la página **Selección de características** , la siguiente opción ya debería estar seleccionada:
    
    **R Server (Standalone)**  
    
    ![Las selecciones para R Server independiente de características](media/2016setup-rserver-features.png "selecciones para R Server independiente de características")
    
    El resto de opciones se deben omitir. 
    
    > [!NOTE]
    > Evitar la instalación de la **características compartidas** si está ejecutando el programa de instalación en un equipo cuando R Services ya está instalado para el análisis de bases de datos de SQL Server. Esto crea bibliotecas duplicadas.
    > 
    > Mientras que los scripts de R que se ejecutan en SQL Server se administran mediante SQL Server para no tener que entrar en conflicto con la memoria utilizada por otros servicios de motor de base de datos, la R Server independiente no tiene estas restricciones y puede interferir con otras operaciones de base de datos.
    > 
    > Por lo general, se recomienda que instale el servidor de aprendizaje de máquina (independiente) en un equipo independiente de servicios de aprendizaje de máquina de SQL Server.

4.  Acepte los términos de licencia para descargar e instalar Microsoft R Open. Si el botón **Aceptar** no está disponible, puede hacer clic en **Siguiente**.
    
    Instalación de estos componentes y los requisitos previos que necesiten, podría llevar algún tiempo.
    
5.  En la página **Listo para instalar** , compruebe las opciones seleccionadas y haga clic en **Instalar**.

## <a name="bkmk_upgrade"></a>Actualizar una instancia existente del servidor de R

Si instaló una versión anterior de Microsoft R Server (independiente), puede actualizar la instancia para usar versiones más recientes de los componentes de R. La actualización también cambia la directiva de soporte técnico para usar la directiva del ciclo de vida de Software modernas admite. Esto permite que la instancia se actualicen con más frecuencia, en una programación diferente de versiones de SQL Server.

1. Descargar el instalador independiente basado en Windows desde las ubicaciones siguientes: 

    + [Instalar para Windows Server de aprendizaje automático](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
    + [Instalar a R Server 9.1 para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)

2. Ejecute el programa de instalación y siga las instrucciones. En la página donde seleccionar las características que se va a instalar, seleccione cada instancia del servidor de R que desea actualizar.

## <a name ="bkmk_tips"></a>Seguimiento y sugerencias de instalación

Esta sección proporciona información adicional relacionada con el programa de instalación.

### <a name="which-version-should-i-install"></a>¿Qué versión debo instalar?

+ **Microsoft R Server** se ofrece por primera vez como parte de SQL Server 2016 y es compatible con el lenguaje R. La última versión de Microsoft R Server era 9.0.1.

+ **Aprendizaje de máquina de Microsoft Server** es la versión más reciente, que se lanzó con SQL Server 2017 y cuenta con muchas actualizaciones, incluida la compatibilidad con Python. Se ha publicado la actualización acumulativa 1 para SQL Server 2017, que incluye la versión 9.2.1.24 del servidor de aprendizaje de máquina. Se recomienda esta actualización si desea que las API de Python más reciente.

+ **Realizar una actualización en contexto**: el programa de instalación requiere una licencia de SQL Server y las actualizaciones normalmente se alinean con el ritmo de lanzamientos de SQL Server. Esto garantiza que las herramientas de desarrollo estén sincronizadas con la versión que se ejecuta en el contexto de proceso de SQL Server. Sin embargo, puede usar al instalador independiente basado en Windows para obtener las actualizaciones más frecuentes, bajo la directiva de soporte técnico de ciclo de vida de Software modernas. También puede usar a este instalador para actualizar una instancia de SQL Server 2016 o 2017 de SQL Server.

### <a name="default-installation-folders"></a>Carpetas de instalación predeterminadas

Al instalar el servidor de R o servidor de aprendizaje de máquina mediante el programa de instalación de SQL Server, se instalan las bibliotecas de R en una carpeta asociada a la versión de SQL Server que utilizó para el programa de instalación. En esta carpeta, también encontrará documentación de las herramientas de R y en tiempo de ejecución, documentación de los paquetes de base de R y datos de ejemplo.

Sin embargo, si se instalan mediante el instalador independiente de Windows, o si se actualiza mediante el instalador independiente de Windows, se instalan las bibliotecas de R en una carpeta diferente.

Solo sirven de referencia, si ha instalado una instancia de SQL Server con R Services (In-Database) o servicios de aprendizaje de máquina (In-Database), y esa instancia está en el mismo equipo, las bibliotecas de R y herramientas se instalan de forma predeterminada en una carpeta diferente.

En la tabla siguiente se enumera las rutas de acceso para cada instalación.

|Versión| Método de instalación | Carpeta predeterminada|
|----|----|----|
|R Server (Standalone) |Asistente para la instalación de SQL Server 2016|`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|R Server (Standalone) |Instalador independiente de Windows|`C:\Program Files\Microsoft\R Server\R_SERVER`|
|Machine Learning Server (independiente) |  Asistente para la instalación de SQL Server 2017 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER`|
|Machine Learning Server (independiente) |  Instalador independiente de Windows |`C:\Program Files\Microsoft\R Server\R_SERVER`|
|R Services (en bases de datos) |Asistente para la instalación de SQL Server 2016|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|
|Machine Learning Services (en base de datos) |Asistente para la instalación de SQL Server 2017|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES` o `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |

### <a name="development-tools"></a>Herramientas de desarrollo

IDE de desarrollo no se instala como parte del programa de instalación. No se requieren herramientas adicionales, tal y como se incluyen todas las herramientas estándares que se proporcionan con una distribución de R o Python.

Se recomienda que pruebe la nueva versión de [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]. Visual Studio admite tanto R y Python, así como herramientas de desarrollo de base de datos, conectividad con SQL Server y herramientas de BI. Sin embargo, puede usar cualquier entorno de desarrollo preferido, incluido RStudio.

## <a name="troubleshooting"></a>Solucionar problemas

En esta sección se enumera algunos problemas comunes para tener en cuenta al instalar el servidor de aprendizaje de máquina o R Server.

### <a name="incompatible-version-of-r-client-and-r-server"></a>Versión incompatible del Cliente de R y R Server

Si instala al cliente de Microsoft R y utilizarlo para ejecutar R en un contexto de proceso de SQL Server remoto, podría obtener un error similar al siguiente:

*Está ejecutando la versión 9.0.0 del cliente de Microsoft R en el equipo, que es incompatible con la versión 8.0.3 de Microsoft R Server. Download and install a compatible version.* (Está ejecutando la versión 9.0.0 del Cliente de Microsoft R en el equipo, que es incompatible con Microsoft R Server versión 8.0.3. Descargue e instale una versión compatible).

En SQL Server 2016, era necesario que la versión de R que se estaba ejecutando en SQL Server R Services ser exactamente igual que las bibliotecas de cliente de Microsoft R. Ese requisito se ha quitado en versiones posteriores. Sin embargo, se recomienda que siempre obtener las últimas versiones de los componentes de aprendizaje automático e instale todos los service packs. 

Si tiene una versión anterior de Microsoft R Server y necesita garantizar su compatibilidad con el cliente de Microsoft R 9.0.0, instale las actualizaciones que se describen en este [artículo de soporte técnico](https://support.microsoft.com/kb/3210262).

### <a name="installing-microsoft-r-server-on-an-instance-of-sql-server-installed-on-windows-core"></a>Instalar Microsoft R Server en una instancia de SQL Server instalada en Windows Core

En la versión RTM de SQL Server 2016, se produjo un problema conocido al agregar Microsoft R Server en una instancia de la edición de Windows Server Core. Esto se ha solucionado.

Si se produce este problema, puede aplicar la revisión que se describe en [KB3164398](https://support.microsoft.com/kb/3164398) para agregar la característica de R a la instancia existente en Windows Server Core.   Para obtener más información, consulte [No se puede instalar Microsoft R Server (independiente) en un sistema operativo Windows Server Core](https://support.microsoft.com/kb/3168691).

###  <a name="bkmk_Uninstall"></a>Actualizar desde una versión anterior de Microsoft R Server

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

[Machine Learning Server (independiente)](../../advanced-analytics/r/r-server-standalone.md)
