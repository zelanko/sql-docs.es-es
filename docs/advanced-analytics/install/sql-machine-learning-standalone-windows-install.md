---
title: Instalar servidor de aprendizaje de máquina (independiente) de SQL Server de 2017 | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1c56d3cb9420d8d0e48ec936008d0351d5d32eb4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="install-sql-server-2017-machine-learning-server-standalone-on-windows"></a>Instalar Server (independiente) en Windows de aprendizaje de máquina SQL Server de 2017
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

El programa de instalación de SQL Server incluye la opción para instalar un servidor que se ejecuta fuera de SQL Server de aprendizaje automático. Esta opción puede ser útil si tiene que desarrollar alto rendimiento aprendizaje automático contextos de proceso de soluciones que pueden usar remoto, cambiar indistintamente entre el servidor local y un servidor de aprendizaje remoto de máquina en un clúster de Spark o en otro servidor SQL Server instancia.
  
En este artículo se describe cómo usar el programa de instalación de SQL Server para instalar la versión independiente de **servidor de aprendizaje de SQL Server de 2017 máquina**. 

## <a name="bkmk_prereqs"> </a> Lista de comprobación previa a la instalación

Se requiere SQL Server 2017. Si tiene SQL Server 2016, instale [R Server (independiente) de SQL Server 2016](sql-r-standalone-windows-install.md) en su lugar.

Si tiene instalada una versión anterior, como SQL Server 2016 R Server (independiente) o Microsoft R Server, desinstalar la instalación existente antes de continuar.

## <a name="get-the-installation-media"></a>Obtener los medios de instalación

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>Ejecute el programa de instalación

En instalaciones locales, debe ejecutar el programa de instalación como administrador. Si instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura y ejecución para dicho recurso.

1. Inicie al Asistente para la instalación de SQL Server 2017.

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

### <a name="default-installation-folders"></a>Carpetas de instalación predeterminadas

Al instalar el servidor de R o servidor de aprendizaje de máquina mediante el programa de instalación de SQL Server, se instalan las bibliotecas de R en una carpeta asociada a la versión de SQL Server que utilizó para el programa de instalación. En esta carpeta, también encontrará documentación de las herramientas de R y en tiempo de ejecución, documentación de los paquetes de base de R y datos de ejemplo.

Sin embargo, si se instalan mediante el instalador independiente de Windows, o si se actualiza mediante el instalador independiente de Windows, se instalan las bibliotecas de R en una carpeta diferente.

Solo sirven de referencia, si ha instalado una instancia de SQL Server con R Services (In-Database) o servicios de aprendizaje de máquina (In-Database), y esa instancia está en el mismo equipo, las bibliotecas de R y herramientas se instalan de forma predeterminada en una carpeta diferente.

En la tabla siguiente se enumera las rutas de acceso para cada instalación.

|Versión| Método de instalación | Carpeta predeterminada|
|----|----|----|
|Servidor de aprendizaje de SQL Server de 2017 máquina (independiente) |  Asistente para la instalación de SQL Server 2017 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Microsoft Machine Learning Server (independiente) |  Instalador independiente de Windows |`C:\Program Files\Microsoft\ML Server\R_SERVER`<br/>`C:\Program Files\Microsoft\ML Server\PYTHON_SERVER`|
|Servicios de aprendizaje de máquina (en bases de datos) de SQL Server de 2017 |Asistente para instalación de SQL Server 2017, con la opción de lenguaje R|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
|SQL Server 2016 R Server (independiente) |  Asistente para la instalación de SQL Server 2016 |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2016 R Services (In-Database) |Asistente para la instalación de SQL Server 2016|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|

## <a name="development-tools"></a>Herramientas de desarrollo

IDE de desarrollo no se instala como parte del programa de instalación. No se requieren herramientas adicionales, tal y como se incluyen todas las herramientas estándares que se proporcionan con una distribución de R o Python.

Se recomienda que pruebe la nueva versión de [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] o [Python para Visual Studio](https://docs.microsoft.com/en-us/visualstudio/python/installing-python-support-in-visual-studio). Visual Studio admite tanto R y Python, así como herramientas de desarrollo de base de datos, conectividad con SQL Server y herramientas de BI. Sin embargo, puede usar cualquier entorno de desarrollo preferido, incluido RStudio.

## <a name="get-help"></a>Obtener ayuda

¿Necesita ayuda con la instalación o actualización? Para obtener respuestas a preguntas comunes y los problemas conocidos, vea el artículo siguiente:

* [Actualización e instalación preguntas más frecuentes: servicios de aprendizaje de máquina](../r/upgrade-and-installation-faq-sql-server-r-services.md)

Para comprobar el estado de instalación de la instancia y solucionar problemas comunes, pruebe estos informes personalizados.

* [Informes personalizados para SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>Pasos siguientes

Los desarrolladores de R pueden empezar a trabajar con algunos ejemplos sencillos y conozca los aspectos básicos del funcionamiento de R con SQL Server. Para el siguiente paso, vea los siguientes vínculos:

+ [Tutorial: Ejecutar R en T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análisis de en bases de datos para los desarrolladores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Los desarrolladores de Python pueden aprender a usar Python con SQL Server, siga estos tutoriales:

+ [Tutorial: Ejecutar Python en T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análisis de en bases de datos para los desarrolladores de Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Para ver ejemplos de aprendizaje automático que se basan en situaciones del mundo real, vea [máquina tutoriales de aprendizaje](../tutorials/machine-learning-services-tutorials.md).
