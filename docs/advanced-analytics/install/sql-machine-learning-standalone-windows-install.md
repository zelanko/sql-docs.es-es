---
title: Instalar R Server o Machine Learning Server (independiente) mediante el programa de instalación de SQL Server | Microsoft Docs
description: Configurar un servidor independiente que reconocen instancias machine learning para el desarrollo de R y Python con RevoScaleR, revoscalepy, MicrosoftML y otros paquetes.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/28/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 70fa652e876f1011bc2d74df56104671b33775b9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48187495"
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone-using-sql-server-setup"></a>Instalar R Server (independiente) mediante el programa de instalación de SQL Server o Machine Learning Server (independiente)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

El programa de instalación de SQL Server incluye un **características compartidas** opción para instalar una instancia ajenos a, servidor independiente de aprendizaje del equipo que se ejecuta fuera de SQL Server. En SQL Server 2016, esta característica se denomina **R Server (independiente)**. En SQL Server 2017, se llama a **Machine Learning Server (independiente)** e incluye R y Python. 

Es funcionalmente equivalente a las versiones sin marca de SQL de un servidor independiente, tal y como se instala el programa de instalación de SQL Server [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), admitiendo el mismo casos de uso y escenarios, incluidos:

+ Ejecución remota, la conmutación entre sesiones locales y remotas en la misma consola
+ Puesta en marcha con nodos de web y nodos de proceso
+ Implementación del servicio Web: la capacidad para empaquetar el script de R y Python en servicios web
+ Toda la colección de bibliotecas de funciones de R y Python

Como un servidor independiente desacoplado de SQL Server, se configura el entorno de R y Python, segura y a los que accede con el sistema operativo subyacente y las herramientas proporcionadas en el servidor independiente, no de SQL Server.

Como un complemento a SQL Server, un servidor independiente es útil si necesita para desarrollar soluciones que pueden usar contextos de cálculo remoto para toda la gama de plataformas de datos admitidos de aprendizaje de automático de alto rendimiento. Puede desplazar la ejecución desde el servidor local a un servidor remoto de Machine Learning en un clúster de Spark o en otra instancia de SQL Server.

<a name="bkmk_prereqs"> </a>

## <a name="pre-install-checklist"></a>Lista de comprobación previa a la instalación

Si tiene instalada una versión anterior, como SQL Server 2016 R Server (independiente) o Microsoft R Server, desinstale la instalación existente antes de continuar.

Como norma general, se recomienda tratar servidor independiente y la base de datos motor que reconocen instancias instalaciones como mutuamente exclusivas para evitar la contención de recursos, pero si tiene recursos suficientes, no hay ninguna prohibición de la instalación de ambos en el mismo equipo físico.

Solo puede tener un servidor independiente en el equipo: SQL Server 2017 Machine Learning Server o SQL Server 2016 R Server (independiente). Debe desinstalar manualmente una versión antes de instalar una versión diferente.

::: moniker range="=sql-server-2016"
<a name="bkmk_ga_instalpatch"></a> 

 ###  <a name="install-patch-requirement"></a>Instale el requisito de revisión 

Para SQL Server 2016: Microsoft ha identificado un problema con la versión específica de los archivos binarios de Microsoft VC ++ 2013 Runtime que se instalan como requisito previo de SQL Server. Si esta actualización de los archivos binarios en tiempo de ejecución de VC++ no se instala, puede que SQL Server experimente problemas de estabilidad en determinados escenarios. Antes de instalar SQL Server, siga las instrucciones de [Notas de la versión de SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) para ver si el equipo necesita una revisión para los archivos binarios en tiempo de ejecución de VC.  
::: moniker-end

## <a name="get-the-installation-media"></a>Obtener los medios de instalación

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="run-setup"></a>Ejecute el programa de instalación

En instalaciones locales, debe ejecutar el programa de instalación como administrador. Si instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura y ejecución para dicho recurso.

1. Iniciar al Asistente para instalación.

2. Haga clic en el **instalación** pestaña y seleccione **instalación nueva Machine Learning Server (independiente)**.
    
     ![Instale Machine Learning Server (independiente)](media/2017setup-installation-page-mlsvr.png "Iniciar instalación de Machine Learning Server (independiente)")

3. Una vez completada la comprobación de reglas, acepte los términos de licencia de SQL Server y seleccione una nueva instalación.

4. En el **selección de características** página siguiente ya deberían estar seleccionadas opciones:

    - Microsoft Machine Learning Server (independiente)

    - R y Python se selecciona de forma predeterminada. Puede anular la selección de cualquiera de estos idiomas, pero se recomienda que instale al menos uno de los idiomas admitidos.

     ![Instale Machine Learning Server (independiente)](media/2017setup-features-page-mlsvr-rpy.png "Iniciar instalación de Machine Learning Server (independiente)")
    
    El resto de opciones se deben omitir. 
    
    > [!NOTE]
    > Evite la instalación de la **características compartidas** si el equipo ya tiene instalado para el análisis en bases de datos de SQL Server Machine Learning Services. Esto crea bibliotecas duplicadas.
    > 
    > Además, mientras que SQL Server para no tener que entrar en conflicto con la memoria utilizada por otros servicios de motor de base de datos administra los scripts de R o Python que se ejecutan en SQL Server, el servidor independiente de machine learning no tiene estas restricciones y puede interferir con otras operaciones de base de datos . Por último, acceso remoto a través de la sesión RDP, que a menudo se utiliza para la operacionalización, suele estar bloqueado por los administradores de base de datos.
    > 
    > Por estos motivos, generalmente recomendamos que instale a Machine Learning Server (independiente) en un equipo independiente de SQL Server Machine Learning Services.

5.  Acepte los términos de licencia para descargar e instalar el idioma base distribuciones. Si el botón **Aceptar** no está disponible, puede hacer clic en **Siguiente**. 

     ![Contrato de licencia de Python](media/2017setup-python-license.png "contrato de licencia de Python")

6.  En la página **Listo para instalar** , compruebe las opciones seleccionadas y haga clic en **Instalar**.

Cuando finalice la instalación, consulte [informes personalizados para SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md) para obtener ayuda con los errores o advertencias, vea [actualización e instalación preguntas más frecuentes - Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).
::: moniker-end

::: moniker range="=sql-server-2016"
## <a name="run-setup"></a>Ejecute el programa de instalación

En instalaciones locales, debe ejecutar el programa de instalación como administrador. Si instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura y ejecución para dicho recurso.

1. Iniciar al Asistente para instalación.

2. En el **instalación** , haga clic **instalación de nuevo R Server (independiente)**.
    
     ![Iniciar la instalación de R Server Standalone](media/2016-setup-installation-rsvr.png "iniciar la instalación de R Server (independiente)")

3. Una vez completada la comprobación de reglas, acepte los términos de licencia de SQL Server y seleccione una nueva instalación.

4.  En la página **Selección de características** , la siguiente opción ya debería estar seleccionada:
    
    **R Server (Standalone)**  
    
    ![Las selecciones para R Server independiente de características](media/2016setup-rserver-features.png "selecciones para R Server independiente de características")
    
    El resto de opciones se deben omitir. 
    
    > [!NOTE]
    > Evite la instalación de la **características compartidas** si está ejecutando el programa de instalación en un equipo donde ya se ha instalado R Services para realizar análisis en bases de datos de SQL Server. Esto crea bibliotecas duplicadas.
    > 
    > Mientras que SQL Server para no tener que entrar en conflicto con la memoria utilizada por otros servicios de motor de base de datos administra los scripts de R que se ejecutan en SQL Server, R Server independiente no tiene estas restricciones y puede interferir con otras operaciones de base de datos.
    > 
    > General, se recomienda que instale a R Server (independiente) en un equipo independiente de SQL Server R Services (In-Database).

5.  Acepte los términos de licencia para descargar e instalar el idioma base distribuciones. Si el botón **Aceptar** no está disponible, puede hacer clic en **Siguiente**. 

6.  En la página **Listo para instalar** , compruebe las opciones seleccionadas y haga clic en **Instalar**.

Cuando finalice la instalación, consulte [informes personalizados para SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md) para obtener ayuda con los errores o advertencias, vea [actualización e instalación preguntas más frecuentes - Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).
::: moniker-end

### <a name="default-installation-folders"></a>Carpetas de instalación predeterminadas

Para el desarrollo de R y Python, es habitual tener varias versiones en el mismo equipo. Tal como se instala con el programa de instalación de SQL Server, la distribución básica se instala en una carpeta asociada a la versión de SQL Server que utilizó para el programa de instalación.

En la tabla siguiente se enumera las rutas de acceso para las distribuciones de R y Python creadas por los instaladores de Microsoft. Por integridad, la tabla incluye las rutas de acceso generados por el programa de instalación de SQL Server, así como el instalador independiente de Microsoft Machine Learning Server.

|Versión| Método de instalación | Carpeta predeterminada|
|----|----|----|
|Machine Learning Server (independiente) de SQL Server 2017 |  Asistente para la instalación de SQL Server 2017 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Microsoft Machine Learning Server (independiente) |  Instalador independiente de Windows |`C:\Program Files\Microsoft\ML Server\R_SERVER`<br/>`C:\Program Files\Microsoft\ML Server\PYTHON_SERVER`|
|SQL Server 2017 Machine Learning Services (en bases de datos) |Asistente para instalación de SQL Server 2017, con la opción de lenguaje R|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
|SQL Server 2016 R Server (independiente) |  Asistente para la instalación de SQL Server 2016 |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2016 R Services (In-Database) |Asistente para la instalación de SQL Server 2016|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Aplicar actualizaciones

Se recomienda que aplique la actualización acumulativa más reciente para el motor de base de datos y los componentes de aprendizaje automático. Las actualizaciones acumulativas se instalan a través del programa de instalación. 

En los dispositivos conectados a internet, normalmente se aplican las actualizaciones acumulativas a través de Windows Update, pero también puede usar los pasos siguientes para las actualizaciones controladas. Al aplicar la actualización para el motor de base de datos, el programa de instalación extrae las actualizaciones acumulativas para las características de R o Python instalado en el servidor independiente. 

En los servidores sin conexión, se necesitan pasos adicionales. Debe obtener la actualización acumulativa para el motor de base de datos, así como los archivos CAB para características de aprendizaje automático. Todos los archivos se deben transferir al servidor aislado y aplica manualmente.

1. Comience con una instancia de la línea base. Solo se pueden aplicar las actualizaciones acumulativas para las instalaciones existentes:

  + Machine Learning Server (independiente) desde la versión inicial de SQL Server 2017
  + R Server (independiente) desde la versión inicial de SQL Server 2016, SQL Server 2016 Service Pack 1 o SQL Server 2016 Service Pack 2

2. En un dispositivo conectado a internet, vaya a la lista de actualizaciones acumulativas para su versión de SQL Server.

  + [Actualizaciones de SQL Server 2017](https://sqlserverupdates.com/sql-server-2017-updates/)
  + [Actualizaciones de SQL Server 2016](https://sqlserverupdates.com/sql-server-2016-updates/)

3. Descargue la actualización acumulativa más reciente. Es un archivo ejecutable.

4. En un dispositivo conectado a internet, haga doble clic en el archivo .exe para ejecutar el programa de instalación y recorrer el Asistente para aceptar los términos de licencia, revise las características afectadas y supervisar el progreso hasta la finalización.

5. En un servidor sin conectividad a internet:

   + Obtener archivos CAB correspondientes para R y Python. Para obtener vínculos de descarga, vea [CAB descargas para las actualizaciones acumulativas en el análisis en bases de datos de SQL Server en instancias](sql-ml-cab-downloads.md).

   + Transferir todos los archivos, el archivo ejecutable principal y los archivos CAB, en una carpeta en el equipo sin conexión.

   + Haga doble clic en el archivo .exe para ejecutar el programa de instalación. Al instalar una actualización de acumular en un servidor sin conectividad a internet, deberá seleccionar la ubicación de los archivos .cab de R y Python.

6. Tras la instalación, en un servidor que se haya habilitado puesta en marcha con nodos de web y nodos de proceso, editar **appsettings.json**, agregue una entrada "MMLResourcePath", directamente debajo de "MMLNativePath":

    ```json
    "ScorerParameters": {
        "MMLNativePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\",
        "MMLResourcePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\"
    }
    ```

7. [Ejecute la utilidad de la CLI de administración](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-launch) para reiniciar la web y nodos de proceso. Para pasos y la sintaxis, vea [Monitor, inicio y detención web y nodos de proceso](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-stop-start).

## <a name="development-tools"></a>Herramientas de desarrollo

Un IDE de desarrollo no se instala como parte del programa de instalación. Para obtener más información acerca de cómo configurar un entorno de desarrollo, consulte [configurar herramientas de R](../r/set-up-a-data-science-client.md) y [configurar herramientas de Python](../python/setup-python-client-tools-sql.md).

## <a name="next-steps"></a>Pasos siguientes

Los desarrolladores de R pueden empezar a trabajar con algunos ejemplos sencillos y conozca los aspectos básicos del funcionamiento de R con SQL Server. Para el siguiente paso, vea los siguientes vínculos:

+ [Tutorial: Ejecución de R en T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análisis de en bases de datos para los desarrolladores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Los desarrolladores de Python pueden aprender a usar Python con SQL Server, siga estos tutoriales:

+ [Tutorial: Ejecución de Python en T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análisis de en bases de datos para desarrolladores de Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)
::: moniker-end

Para ver ejemplos de aprendizaje automático que se basan en escenarios del mundo real, consulte [tutoriales de aprendizaje automático](../tutorials/machine-learning-services-tutorials.md).
