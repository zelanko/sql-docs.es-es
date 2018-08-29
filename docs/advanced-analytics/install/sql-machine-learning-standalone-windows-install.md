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
ms.openlocfilehash: 7cf5cf2d78900c5bbd7607666afecc64aa98267f
ms.sourcegitcommit: e4e9f02b5c14f3bb66e19dec98f38c012275b92c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2018
ms.locfileid: "43118553"
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone-using-sql-server-setup"></a>Instalar R Server (independiente) mediante el programa de instalación de SQL Server o Machine Learning Server (independiente)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

El programa de instalación de SQL Server incluye un **características compartidas** opción para instalar una instancia ajenos a, servidor independiente de aprendizaje del equipo que se ejecuta fuera de SQL Server. En SQL Server 2016, esta característica se denomina **R Server (independiente)**. En SQL Server 2017, se llama a **Machine Learning Server (independiente)** e incluye R y Python. 

Es funcionalmente equivalente a las versiones sin marca de SQL de un servidor independiente, tal y como se instala el programa de instalación de SQL Server [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), admitiendo el mismo casos de uso y escenarios, incluidos la ejecución remota puesta en marcha y los servicios web y la colección completa de funciones de RevoScaleR y revoscalepy.

Como un servidor independiente desacoplado de SQL Server, se configura el entorno de R y Python, segura y a los que accede con el sistema operativo subyacente y las herramientas proporcionadas en el servidor independiente, no de SQL Server.

Como un complemento a SQL Server, un servidor independiente es útil si necesita desarrollar alto rendimiento aprendizaje automático contextos de cálculo de las soluciones que pueden usar remoto, cambiar indistintamente entre el servidor local y un servidor de aprendizaje de máquina remota en Spark clúster o en otro servidor SQL Server de la instancia.
  

## <a name="bkmk_prereqs"> </a> Lista de comprobación previa a la instalación

Si tiene instalada una versión anterior, como SQL Server 2016 R Server (independiente) o Microsoft R Server, desinstale la instalación existente antes de continuar.

Como norma general, se recomienda tratar servidor independiente y la base de datos motor que reconocen instancias instalaciones como mutuamente exclusivas para evitar la contención de recursos, pero si tiene recursos suficientes, no hay ninguna prohibición de la instalación de ambos en el mismo equipo físico.

Solo puede tener un servidor independiente en el equipo: SQL Server 2017 Machine Learning Server o SQL Server 2016 R Server (independiente). Debe desinstalar manualmente una versión antes de instalar una versión diferente.

::: moniker range="=sql-server-2016"
 ###  <a name="bkmk_ga_instalpatch"></a> Requisito de instalación de revisión 

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

## <a name="development-tools"></a>Herramientas de desarrollo

Un IDE de desarrollo no se instala como parte del programa de instalación. Para obtener más información sobre cómo configurar un entorno de desarrollo, consulte [configurar herramientas de R](../r/set-up-a-data-science-client.md) y [configurar herramientas de Python](../python/setup-python-client-tools-sql.md).

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
