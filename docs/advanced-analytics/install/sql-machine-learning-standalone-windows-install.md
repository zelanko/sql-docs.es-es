---
title: Instalación de Machine Learning Server (independiente)
description: Configure un servidor de aprendizaje automático independiente para Python y R. Un servidor instalar instalado mediante el programa de instalación de SQL Server equivale funcionalmente a las versiones de Microsoft Machine Learning Server que no son de marca SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/03/2020
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 319ae61fbdca64bc6f27143bdd4a42aec635d129
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "79285929"
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone-using-sql-server-setup"></a>Instalación de Machine Learning Server (independiente) o R Server (independiente) con el programa de instalación de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
El programa de instalación de SQL Server incluye una opción de **características compartidas** para instalar un servidor aprendizaje automático independiente que se ejecuta fuera de SQL Server. Se denomina **Machine Learning Server (independiente)** e incluye Python y R. 
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
El programa de instalación de SQL Server incluye una opción de **características compartidas** para instalar un servidor aprendizaje automático independiente que se ejecuta fuera de SQL Server. En SQL Server 2016, esta característica se denomina **R Server (independiente)** .  
::: moniker-end

Un servidor independiente instalado mediante el programa de instalación de SQL Server equivale funcionalmente a las versiones de [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server) que no son de marca SQL, y admite los mismos casos de uso y escenarios, a saber:

+ Ejecución remota, alternancia entre sesión local y sesión remota en la misma consola
+ Operacionalización con nodos web y nodos de proceso
+ Implementación de servicio web: posibilidad de empaquetar scripts de R y Python en servicios web
+ Recopilación completa de bibliotecas de funciones de R y Python

En tanto que servidor independiente desacoplado de SQL Server, la configuración, la protección y el acceso del entorno de R y Python se realizan a través del sistema operativo subyacente y las herramientas proporcionadas en el servidor independiente, y no a través de SQL Server.

Como elemento accesorio de SQL Server, un servidor independiente es útil si es necesario desarrollar soluciones de Machine Learning de alto rendimiento que pueden usar contextos de proceso remotos de toda la gama de plataformas de datos admitidas. La ejecución se puede alternar entre el servidor local y un servidor de Machine Learning Server remoto en un clúster de Spark o en otra instancia de SQL Server.

<a name="bkmk_prereqs"> </a>

## <a name="pre-install-checklist"></a>Lista de comprobación previa a la instalación

Si tiene instalada una versión anterior, como SQL Server 2016 R Server (independiente) o Microsoft R Server, desinstálela antes de continuar.

Como norma general, se recomienda tratar las instalaciones independientes de servidor y de motor de base de datos compatibles con instancias como mutuamente excluyentes, ya que así se evita la contención de recursos; pero si tiene recursos suficientes, no hay ninguna prohibición que impida tener ambos instalados en el mismo equipo físico.

Solo puede haber un servidor independiente en el equipo: o SQL Server Machine Learning Server (independiente), o SQL Server R Server (independiente). Asegúrese de desinstalar una versión antes de agregar una nueva.

::: moniker range="=sql-server-2016"
<a name="bkmk_ga_instalpatch"></a> 

 ###  <a name="install-patch-requirement"></a>Requisito de instalación de revisión 

Solo en SQL Server 2016: Microsoft ha identificado un problema con la versión concreta de los archivos binarios en tiempo de ejecución de Microsoft VC++ 2013 que instala como requisito previo SQL Server. Si esta actualización de los archivos binarios en tiempo de ejecución de VC++ no se instala, puede que SQL Server experimente problemas de estabilidad en determinados escenarios. Antes de instalar SQL Server, siga las instrucciones de [Notas de la versión de SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) para ver si el equipo necesita una revisión para los archivos binarios en tiempo de ejecución de VC.  
::: moniker-end

## <a name="get-the-installation-media"></a>Obtener los medios de instalación

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="run-setup"></a>Ejecución del programa de instalación

En instalaciones locales, debe ejecutar el programa de instalación como administrador. Si instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura y ejecución para dicho recurso.

1. Inicie el Asistente para instalación.

2. Haga clic en la pestaña **Instalación** y seleccione **Nueva instalación de Machine Learning Server (independiente)** .
    
   ::: moniker-end
   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   ![Instalación independiente de Machine Learning Server](media/2017setup-installation-page-mlsvr.png "Inicio de la instalación de Machine Learning Server (independiente)")
   ::: moniker-end
   ::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
   ![Instalación independiente de Machine Learning Server](media/2019setup-installation-page-mlsvr.png "Inicio de la instalación de Machine Learning Server (independiente)")
   ::: moniker-end
   ::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

3. Cuando finalice la comprobación de reglas, acepte los términos de licencia de SQL Server y seleccione una nueva instalación.

4. En la página **Selección de características**, las siguientes opciones ya deberían estar seleccionadas:

    - **Microsoft Machine Learning Server (independiente)**

    - **R** y **Python** están seleccionados de forma predeterminada. Puede anular la selección de cualquiera de estos lenguajes admitidos, pero se recomienda instalar al menos uno de ellos.

   ::: moniker-end
   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   ![Elección de características de R o de Python](media/2017setup-features-page-mlsvr-rpy.png "Inicio de la instalación de Machine Learning Server (independiente)")
   ::: moniker-end
   ::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
   ![Elección de características de R o de Python](media/2019setup-features-page-mlsvr-rpy.png "Inicio de la instalación de Machine Learning Server (independiente)")
   ::: moniker-end
   ::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
    
   El resto de opciones se deben omitir. 
    
   > [!NOTE]
   > No instale las **características compartidas** si el equipo ya tiene instalado Machine Learning Services para los análisis en base de datos de SQL Server, ya que ello generaría bibliotecas duplicadas.
   > 
   > Aparte de eso, los scripts de R o de Python que se ejecutan en SQL Server se administran por medio de SQL Server para que no entren en conflicto con la memoria que usan otros servicios de motor de base de datos, pero la instalación independiente de Machine Learning Server no presenta estas restricciones y podría interferir con otras operaciones de base de datos. Por último, los administradores de bases de datos suelen bloquear el acceso remoto a través de sesiones RDP, que a menudo se usa para la operacionalización.
   > 
   > Por estos motivos, generalmente se recomienda instalar Machine Learning Server (independiente) en un equipo aparte de SQL Server Machine Learning Services.

5. Acepte los términos de licencia para descargar e instalar las distribuciones de lenguaje base. Si el botón **Aceptar** no está disponible, puede hacer clic en **Siguiente**. 

6. En la página **Listo para instalar** , compruebe las opciones seleccionadas y haga clic en **Instalar**.

Una vez finalizada la instalación, vea [Informes personalizados para SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md). Para obtener ayuda sobre cualquier error o advertencia, vea [Preguntas más frecuentes de actualización e instalación de Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).
::: moniker-end

::: moniker range="=sql-server-2016"
## <a name="run-setup"></a>Ejecución del programa de instalación

En instalaciones locales, debe ejecutar el programa de instalación como administrador. Si instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura y ejecución para dicho recurso.

1. Inicie el Asistente para instalación.

2. En la pestaña **Instalación**, haga clic en **Nueva instalación de R Server (independiente)** .
    
   ![Inicio de la instalación de R Server independiente](media/2016-setup-installation-rsvr.png "Inicio de la instalación de R Server independiente")

3. Cuando finalice la comprobación de reglas, acepte los términos de licencia de SQL Server y seleccione una nueva instalación.

4. En la página **Selección de características** , la siguiente opción ya debería estar seleccionada:
    
   - **R Server (Standalone)**  
    
   ![Selecciones de características de R Server independiente](media/2016setup-rserver-features.png "Selecciones de características de R Server independiente")
    
   El resto de opciones se deben omitir. 
    
   > [!NOTE]
   > No instale las **características compartidas** si está ejecutando el programa de instalación en un equipo en el que R Services ya está instalado para los análisis en base de datos de SQL Server, ya que ello generaría bibliotecas duplicadas.
   > 
   > Los scripts de R que se ejecutan en SQL Server se administran por medio de SQL Server para que no entren en conflicto con la memoria que usan otros servicios de motor de base de datos, pero la instalación independiente de R Server no presenta estas restricciones y podría interferir con otras operaciones de base de datos.
   > 
   > Por lo general, se recomienda instalar R Server (independiente) en un equipo aparte de SQL Server R Services (en base de datos).

5. Acepte los términos de licencia para descargar e instalar las distribuciones de lenguaje base. Si el botón **Aceptar** no está disponible, puede hacer clic en **Siguiente**. 

6. En la página **Listo para instalar** , compruebe las opciones seleccionadas y haga clic en **Instalar**.

Una vez finalizada la instalación, vea [Informes personalizados para SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md). Para obtener ayuda sobre cualquier error o advertencia, vea [Preguntas más frecuentes de actualización e instalación de Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).
::: moniker-end

## <a name="set-environment-variables"></a>Establecimiento de variables de entorno

Solo de cara a la integración de características de R, conviene establecer la variable de entorno **MKL_CBWR** para [garantizar una salida coherente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) de los cálculos de la biblioteca Math Kernel Library (MKL) de Intel.

1. En el panel de control, haga clic en **Sistema y seguridad** > **Sistema** > **Configuración avanzada del sistema** > **Variables de entorno**.

2. Cree un usuario o una variable del sistema. 

  + Establezca el nombre de la variable en `MKL_CBWR`.
  + Establezca el valor de la variable en `AUTO`.

3. Reinicie el servidor.

<a name="install-path"></a>

### <a name="default-installation-folders"></a>Carpetas de instalación predeterminadas

En el desarrollo de R y Python es habitual tener varias versiones en el mismo equipo. Como la instalación se realiza a través del programa de instalación de SQL Server, la distribución base se instala en una carpeta asociada a la versión de SQL Server usada para la instalación.

En la siguiente tabla se muestran las rutas de acceso de las distribuciones de R y Python creadas por instaladores de Microsoft. La tabla muestra información completa, como las rutas de acceso generadas por el programa de instalación de SQL Server, así como el instalador independiente de Microsoft Machine Learning Server.

|Versión| Método de instalación | Carpeta predeterminada|
|----|----|----|
|SQL Server 2019 Machine Learning Server (independiente) |  Asistente para la instalación de SQL Server 2019 |`C:\Program Files\Microsoft SQL Server\150\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\150\PYTHON_SERVER`|
|SQL Server 2017 Machine Learning Server (independiente) |  Asistente para la instalación de SQL Server 2017 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Microsoft Machine Learning Server (independiente) |  Instalador independiente de Windows |`C:\Program Files\Microsoft\ML Server\R_SERVER`<br/>`C:\Program Files\Microsoft\ML Server\PYTHON_SERVER`|
|SQL Server Machine Learning Services (en base de datos) |Asistente para la instalación de SQL Server 2019, con la opción de lenguaje R|`C:\Program Files\Microsoft SQL Server\MSSQL15.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL15.<instance_name>\PYTHON_SERVICES` |
|SQL Server Machine Learning Services (en base de datos) |Asistente para la instalación de SQL Server 2017, con la opción de lenguaje R|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
|SQL Server 2016 R Server (independiente) |  Asistente para la instalación de SQL Server 2016 |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2016 R Services (en base de datos) |Asistente para la instalación de SQL Server 2016|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Aplicación de actualizaciones

Se recomienda aplicar la última actualización acumulativa tanto en el motor de base de datos como en los componentes de Machine Learning. Las actualizaciones acumulativas se instalan a través del programa de instalación. 

En los dispositivos conectados a Internet, se puede descargar un archivo ejecutable autoextraíble. Al aplicar una actualización del motor de base de datos, se incluyen automáticamente actualizaciones acumulativas de las características existentes de R y Python. 

En los servidores desconectados, se requieren pasos extra. Hay que obtener la actualización acumulativa del motor de base de datos, así como los archivos .CAB de las características de Machine Learning. Todos los archivos deben transferirse al servidor aislado y aplicarse manualmente.

1. Comience con una instancia de línea base. Solo se pueden aplicar actualizaciones acumulativas en las instalaciones existentes:

  + Machine Learning Server (independiente) de la versión inicial de SQL Server 2019
  + Machine Learning Server (independiente) de la versión inicial de SQL Server 2017
  + R Server (independiente) de la versión inicial de SQL Server 2016, SQL Server 2016 SP1 o SQL Server 2016 SP2

2. Cierre todas las sesiones de R o de Python abiertas y detenga todos los procesos que aún se estén ejecutando en el sistema.

3. Si ha habilitado la ejecución de la operacionalización como nodos web y nodos de proceso en implementaciones de servicio web, haga una copia de seguridad del archivo **AppSettings.json** como medida de precaución. Este archivo se revisa al aplicar SQL Server 2017 CU13 o posterior, por lo que probablemente quiera conservar una copia de seguridad de la versión original.

4. En una máquina conectada a Internet, descargue la actualización acumulativa más reciente para su versión desde [Actualizaciones más recientes de Microsoft SQL Server](https://docs.microsoft.com/sql/database-engine/install-windows/latest-updates-for-microsoft-sql-server).

5. Descargue la actualización acumulativa más reciente. Es un archivo ejecutable.

6. En un dispositivo conectado a Internet, haga doble clic en el archivo .exe para ejecutar el programa de instalación y realice todo el asistente para aceptar los términos de licencia, revisar las características afectadas y supervisar el progreso hasta su término.

7. En un servidor sin conectividad a Internet:

   + Obtenga los archivos .CAB correspondientes a R y Python. Para obtener los vínculos de descarga, vea [Descargas de CAB de actualizaciones acumulativas en instancias de análisis en base de datos de SQL Server](sql-ml-cab-downloads.md).

   + Transfiera todos los archivos, el archivo ejecutable principal y los archivos .CAB a una carpeta del equipo sin conexión.

   + Haga doble clic en el archivo .exe para ejecutar el programa de instalación. Cuando se instala una actualización acumulativa en un servidor sin conectividad a Internet, se le pide que seleccione la ubicación de los archivos .CAB de R y Python.

8. Después de la instalación, en un servidor donde se haya habilitado la implementación con nodos web y nodos de ejecución, edite **AppSettings.json** y agregue una entrada "MMLResourcePath" directamente en "MMLNativePath". Por ejemplo:

    ```json
    "ScorerParameters": {
        "MMLNativePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\",
        "MMLResourcePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\"
    }
    ```

9. [Ejecute la utilidad de CLI de administración](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-launch) para reiniciar los nodos web y de proceso. Para conocer los pasos y la sintaxis, vea [Supervisión, inicio y detención de nodos web y de proceso](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-stop-start).

## <a name="development-tools"></a>Herramientas de desarrollo

No se instala un IDE de desarrollo como parte de la instalación. Para más información sobre cómo configurar un entorno de desarrollo, vea [Configuración de herramientas de R](../r/set-up-a-data-science-client.md) y [Configuración de herramientas de Python](../python/setup-python-client-tools-sql.md).

## <a name="next-steps"></a>Pasos siguientes

Los desarrolladores de R pueden empezar con algunos ejemplos sencillos y conocer los aspectos básicos del funcionamiento de R con SQL Server. Para conocer el siguiente paso, vea los vínculos siguientes:

+ [Tutorial: Ejecutar R en T-SQL](../tutorials/quickstart-r-create-script.md)
+ [Tutorial: Análisis en base de datos para desarrolladores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Los desarrolladores de Python pueden aprender a usar Python con SQL Server con estos tutoriales:

+ [Tutorial: Ejecutar Python en T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análisis en base de datos para desarrolladores de Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)
::: moniker-end

Para obtener ejemplos de Machine Learning basados en escenarios del mundo real, vea los [tutoriales sobre Machine Learning](../tutorials/machine-learning-services-tutorials.md).
