---
title: Instalación de R Server o Machine Learning Server (independiente) mediante el programa de instalación de SQL Server
description: Configure un servidor de machine learning independiente que no sea compatible con instancias para el desarrollo de R y Python con RevoScaleR, revoscalepy, MicrosoftML y otros paquetes.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/28/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f9835bae00aab15ee902dfe77dcf211eb412bc96
ms.sourcegitcommit: 2f56848ec422845ee81fb84ed321a716c677aa0e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/25/2019
ms.locfileid: "71271951"
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone-using-sql-server-setup"></a>Instalación de Machine Learning Server (independiente) o R Server (independiente) mediante el programa de instalación de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
SQL Server instalación incluye una opción de **característica compartida** para instalar un servidor de aprendizaje automático independiente que no es de instancia y que no es compatible con instancias y que se ejecuta fuera de SQL Server. Se denomina **machine learning Server (independiente)** e incluye R y Python. 
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
SQL Server instalación incluye una opción de **característica compartida** para instalar un servidor de aprendizaje automático independiente que no es de instancia y que no es compatible con instancias y que se ejecuta fuera de SQL Server. En SQL Server 2016, esta característica se denomina **R Server (independiente)** .  
::: moniker-end

Un servidor independiente tal como instalado por SQL Server el programa de instalación es funcionalmente equivalente a las versiones que no son de la marca de SQL de [Microsoft machine learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), y admite los mismos casos de uso y escenarios, entre los que se incluyen:

+ Ejecución remota, cambio entre sesiones locales y remotas en la misma consola
+ Operacionalización con nodos web y nodos de proceso
+ Implementación del servicio Web: la capacidad de empaquetar scripts de R y Python en servicios Web
+ Recopilación completa de bibliotecas de funciones de R y Python

Como un servidor independiente desacoplado de SQL Server, el entorno de R y Python está configurado, protegido y se tiene acceso a él mediante el sistema operativo subyacente y las herramientas proporcionadas en el servidor independiente, no SQL Server.

Como complemento a SQL Server, un servidor independiente es útil si necesita desarrollar soluciones de aprendizaje automático de alto rendimiento que pueden usar contextos de cálculo remotos en toda la gama de plataformas de datos compatibles. Puede cambiar la ejecución del servidor local a una Machine Learning Server remota en un clúster de Spark o en otra instancia de SQL Server.

<a name="bkmk_prereqs"> </a>

## <a name="pre-install-checklist"></a>Lista de comprobación previa a la instalación

Si instaló una versión anterior, como SQL Server 2016 R Server (independiente) o Microsoft R Server, desinstale la instalación existente antes de continuar.

Como norma general, se recomienda que se traten las instalaciones independientes del servidor y de la instancia del motor de base de datos como mutuamente excluyentes para evitar la contención de recursos, pero si tiene recursos suficientes, no hay ninguna prohibición de instalarlos ambos en el mismo equipo físico.

Solo puede tener un servidor independiente en el equipo: SQL Server Machine Learning Server (independiente) o SQL Server R Server (independiente). Asegúrese de desinstalar una versión antes de agregar una nueva.

::: moniker range="=sql-server-2016"
<a name="bkmk_ga_instalpatch"></a> 

 ###  <a name="install-patch-requirement"></a>Requisito de instalación de revisión 

Solo para SQL Server 2016: Microsoft ha identificado un problema con la versión concreta de los archivos binarios en tiempo de ejecución de Microsoft VC++ 2013 que instala como requisito previo SQL Server. Si esta actualización de los archivos binarios en tiempo de ejecución de VC++ no se instala, puede que SQL Server experimente problemas de estabilidad en determinados escenarios. Antes de instalar SQL Server, siga las instrucciones de [Notas de la versión de SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) para ver si el equipo necesita una revisión para los archivos binarios en tiempo de ejecución de VC.  
::: moniker-end

## <a name="get-the-installation-media"></a>Obtener los medios de instalación

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="run-setup"></a>Ejecutar el programa de instalación

En instalaciones locales, debe ejecutar el programa de instalación como administrador. Si instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura y ejecución para dicho recurso.

1. Inicie el Asistente para la instalación de.

2. Haga clic en la pestaña **instalación** y seleccione **nueva instalación de machine learning Server (independiente)** .
    
     ![Instalación de machine learning Server independiente](media/2017setup-installation-page-mlsvr.png "Iniciar la instalación de machine learning Server independiente")

3. Una vez completada la comprobación de reglas, acepte SQL Server términos de licencia y seleccione una nueva instalación.

4. En la página **selección de características** , las siguientes opciones ya deben estar seleccionadas:

    - Microsoft Machine Learning Server (independiente)

    - R y Python están seleccionados de forma predeterminada. Puede anular la selección de cualquier idioma, pero se recomienda instalar al menos uno de los idiomas admitidos.

     ![Elección de las características de R o Python](media/2017setup-features-page-mlsvr-rpy.png "Iniciar la instalación de machine learning Server independiente")
    
    El resto de opciones se deben omitir. 
    
    > [!NOTE]
    > Evite instalar las **características** compartidas si el equipo ya tiene Machine Learning Services instalado para SQL Server análisis en base de datos. Esto crea bibliotecas duplicadas.
    > 
    > Además, mientras que los scripts de R o Python que se ejecutan en SQL Server se administran mediante SQL Server para que no entren en conflicto con la memoria que usan otros servicios de motor de base de datos, el servidor de machine learning independiente no tiene estas restricciones y puede interferir con otras operaciones de base de datos. . Por último, el acceso remoto a través de la sesión RDP, que a menudo se usa para la operacionalización, normalmente lo bloquean los administradores de bases de datos.
    > 
    > Por estos motivos, generalmente se recomienda instalar Machine Learning Server (independiente) en un equipo independiente de SQL Server Machine Learning Services.

5.  Acepte los términos de licencia para descargar e instalar las distribuciones de idioma base. Si el botón **Aceptar** no está disponible, puede hacer clic en **Siguiente**. 

     ![Contrato de licencia de Python](media/2017setup-python-license.png "Contrato de licencia de Python")

6.  En la página **Listo para instalar** , compruebe las opciones seleccionadas y haga clic en **Instalar**.

Una vez finalizada la instalación, vea [informes personalizados de SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md) para obtener ayuda con los errores o las advertencias, consulte [preguntas más frecuentes sobre actualización e instalación-Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).
::: moniker-end

::: moniker range="=sql-server-2016"
## <a name="run-setup"></a>Ejecutar el programa de instalación

En instalaciones locales, debe ejecutar el programa de instalación como administrador. Si instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura y ejecución para dicho recurso.

1. Inicie el Asistente para la instalación de.

2. En la pestaña **instalación** , haga clic en **nueva instalación de R Server (independiente)** .
    
     ![Iniciar el programa de instalación de R Server independiente](media/2016-setup-installation-rsvr.png "Iniciar el programa de instalación de R Server independiente")

3. Una vez completada la comprobación de reglas, acepte SQL Server términos de licencia y seleccione una nueva instalación.

4.  En la página **Selección de características** , la siguiente opción ya debería estar seleccionada:
    
    **R Server (Standalone)**  
    
    ![Selecciones de características para R Server independiente](media/2016setup-rserver-features.png "Selecciones de características para R Server independiente")
    
    El resto de opciones se deben omitir. 
    
    > [!NOTE]
    > Evite instalar las **características** compartidas si está ejecutando el programa de instalación en un equipo en el que ya se ha instalado R Services para SQL Server análisis de base de datos. Esto crea bibliotecas duplicadas.
    > 
    > Mientras que los scripts de R que se ejecutan en SQL Server se administran mediante SQL Server para que no entren en conflicto con la memoria que usan otros servicios de motor de base de datos, el R Server independiente no tiene ninguna restricción y puede interferir con otras operaciones de base de datos.
    > 
    > Por lo general, se recomienda instalar R Server (independiente) en un equipo independiente de SQL Server R Services (en base de datos).

5.  Acepte los términos de licencia para descargar e instalar las distribuciones de idioma base. Si el botón **Aceptar** no está disponible, puede hacer clic en **Siguiente**. 

6.  En la página **Listo para instalar** , compruebe las opciones seleccionadas y haga clic en **Instalar**.

Una vez finalizada la instalación, vea [informes personalizados de SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md) para obtener ayuda con los errores o las advertencias, consulte [preguntas más frecuentes sobre actualización e instalación-Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).
::: moniker-end

## <a name="set-environment-variables"></a>Establecer variables de entorno

Solo para la integración de características de R, debe establecer la variable de entorno **MKL_CBWR** para [garantizar una salida coherente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) de los cálculos de la biblioteca de kernels matemáticos (MKL) de Intel.

1. En el panel de control, haga clic en sistema **y seguridad** >  > **configuración** > avanzada del sistema**variables de entorno**.

2. Cree una nueva variable de usuario o del sistema. 

  + Establezca el nombre de la variable en`MKL_CBWR`
  + Establezca el valor de la variable en`AUTO`

3. Reinicie el servidor.

<a name="install-path"></a>

### <a name="default-installation-folders"></a>Carpetas de instalación predeterminadas

Para el desarrollo de R y Python, es habitual tener varias versiones en el mismo equipo. Tal como se instala mediante SQL Server el programa de instalación, la distribución base se instala en una carpeta asociada a la versión de SQL Server que se usó para el programa de instalación.

En la tabla siguiente se enumeran las rutas de acceso de las distribuciones de R y Python creadas por los instaladores de Microsoft. Por integridad, la tabla incluye las rutas de acceso generadas por el programa de instalación de SQL Server, así como el instalador independiente de Microsoft Machine Learning Server.

|`Version`| Método de instalación | Carpeta predeterminada|
|----|----|----|
|SQL Server 2017 Machine Learning Server (independiente) |  Asistente para la instalación de SQL Server 2017 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Microsoft Machine Learning Server (independiente) |  Instalador independiente de Windows |`C:\Program Files\Microsoft\ML Server\R_SERVER`<br/>`C:\Program Files\Microsoft\ML Server\PYTHON_SERVER`|
|SQL Server Machine Learning Services (in-Database) |SQL Server el Asistente para la instalación de 2017, con la opción de lenguaje R|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
|SQL Server 2016 R Server (independiente) |  Asistente para la instalación de SQL Server 2016 |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2016 R Services (in-Database) |Asistente para la instalación de SQL Server 2016|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Aplicar actualizaciones

Se recomienda aplicar la última actualización acumulativa al motor de base de datos y a los componentes de aprendizaje automático. Las actualizaciones acumulativas se instalan a través del programa de instalación. 

En los dispositivos conectados a Internet, puede descargar un archivo ejecutable autoextraíble. Al aplicar una actualización para el motor de base de datos, se incorporan automáticamente las actualizaciones acumulativas para las características existentes de R y Python. 

En los servidores desconectados, se requieren pasos adicionales. Debe obtener la actualización acumulativa para el motor de base de datos, así como los archivos. CAB para las características de aprendizaje automático. Todos los archivos se deben transferir al servidor aislado y aplicarlos manualmente.

1. Comience con una instancia de línea de base. Solo puede aplicar las actualizaciones acumulativas a las instalaciones existentes:

  + Machine Learning Server (independiente) de SQL Server versión inicial 2017
  + R Server (independiente) de SQL Server versión 2016 inicial, SQL Server 2016 SP 1 o SQL Server 2016 SP 2

2. Cierre todas las sesiones de R o Python abiertas y detenga todos los procesos que todavía se estén ejecutando en el sistema.

3. Si ha habilitado la operacionalización para que se ejecute como nodos web y nodos de proceso para implementaciones de servicios Web, realice una copia de seguridad del archivo **appSettings. JSON** como precaución. Al aplicar SQL Server 2017 CU13 o posterior, se revisa este archivo, por lo que es posible que desee una copia de seguridad para conservar la versión original.

4. En un dispositivo conectado a Internet, haga clic en el vínculo de actualización acumulativa correspondiente a su versión de SQL Server.

  + [SQL Server 2017 actualizaciones](https://sqlserverupdates.com/sql-server-2017-updates/)
  + [SQL Server 2016 actualizaciones](https://sqlserverupdates.com/sql-server-2016-updates/)

5. Descargue la actualización acumulativa más reciente. Es un archivo ejecutable.

6. En un dispositivo conectado a Internet, haga doble clic en el archivo. exe para ejecutar el programa de instalación y recorra el Asistente para aceptar los términos de licencia, revisar las características afectadas y supervisar el progreso hasta la finalización.

7. En un servidor sin conectividad a Internet:

   + Obtiene los archivos. CAB correspondientes para R y Python. Para obtener vínculos de descarga, consulte [descargas de CAB para actualizaciones acumulativas en SQL Server instancias de análisis en base de datos](sql-ml-cab-downloads.md).

   + Transfiera todos los archivos, el archivo ejecutable principal y los archivos. CAB, a una carpeta del equipo sin conexión.

   + Haga doble clic en el archivo. exe para ejecutar el programa de instalación. Al instalar una actualización de acumulación en un servidor sin conectividad a Internet, se le pedirá que seleccione la ubicación de los archivos. cab para R y Python.

8. Después de la instalación, en un servidor para el que haya habilitado la operacionalización con nodos web y nodos de proceso, edite **appSettings. JSON**y agregue una entrada "MMLResourcePath", directamente en "MMLNativePath":

    ```json
    "ScorerParameters": {
        "MMLNativePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\",
        "MMLResourcePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\"
    }
    ```

9. [Ejecute la utilidad de administración](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-launch) de la CLI para reiniciar los nodos web y de proceso. Para conocer los pasos y la sintaxis, consulte [supervisión, Inicio y detención de nodos web y de proceso](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-stop-start).

## <a name="development-tools"></a>Herramientas de desarrollo

No se instala un IDE de desarrollo como parte del programa de instalación de. Para obtener más información sobre cómo configurar un entorno de desarrollo, vea [configurar herramientas de R](../r/set-up-a-data-science-client.md) y [configurar herramientas de Python](../python/setup-python-client-tools-sql.md).

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
