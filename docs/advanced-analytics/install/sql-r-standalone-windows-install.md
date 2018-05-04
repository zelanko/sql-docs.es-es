---
title: Instalar SQL Server 2016 R Server (independiente) | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e7e5b61cb8e41d818fc13d1cc97cd4d998256efc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="install-sql-server-2016-r-server-standalone"></a>Instalar a SQL Server 2016 R Server (independiente)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe cómo usar el programa de instalación de SQL Server 2016 para instalar la versión independiente de **R 2016 de SQL Server**.

## <a name="bkmk_prereqs"> </a> Lista de comprobación previa a la instalación

Se requiere SQL Server 2016. Si tiene SQL Server 2017, instale [máquina aprendizaje Server (independiente) de SQL Server 2017](sql-machine-learning-standalone-windows-install.md) en su lugar.

Si instaló cualquier versión anterior de las herramientas de Revolution Analytics o paquetes, debe desinstalarlas primero. 

## <a name="get-the-installation-media"></a>Obtener los medios de instalación

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

 ###  <a name="bkmk_ga_instalpatch"></a> Requisito de instalación de revisión 

Microsoft ha identificado un problema con la versión concreta de los archivos binarios en tiempo de ejecución de Microsoft VC++ 2013 que instala como requisito previo SQL Server. Si esta actualización de los archivos binarios en tiempo de ejecución de VC++ no se instala, puede que SQL Server experimente problemas de estabilidad en determinados escenarios. Antes de instalar SQL Server, siga las instrucciones de [Notas de la versión de SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) para ver si el equipo necesita una revisión para los archivos binarios en tiempo de ejecución de VC.  

## <a name="run-setup"></a>Ejecute el programa de instalación

En instalaciones locales, debe ejecutar el programa de instalación como administrador. Si instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura y ejecución para dicho recurso.

1. Inicie al Asistente para la instalación de SQL Server 2016. Se recomienda que instale Service Pack 1 o posterior.

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
    > General, se recomienda instalar el servidor de R (independiente) en un equipo independiente de SQL Server R Services (In-Database).

4.  Acepte los términos de licencia para descargar e instalar Microsoft R Open. Si el botón **Aceptar** no está disponible, puede hacer clic en **Siguiente**.
    
    Instalación de estos componentes y los requisitos previos que necesiten, podría llevar algún tiempo.
    
5.  En la página **Listo para instalar** , compruebe las opciones seleccionadas y haga clic en **Instalar**.

## <a name="default-installation-folders"></a>Carpetas de instalación predeterminadas

Cuando se instala el servidor de R mediante el programa de instalación de SQL Server, se instalan las bibliotecas de R en una carpeta asociada a la versión de SQL Server que utilizó para el programa de instalación. En esta carpeta, también encontrará documentación de las herramientas de R y en tiempo de ejecución, documentación de los paquetes de base de R y datos de ejemplo.

Sin embargo, si ha instalado a Microsoft R Server mediante el instalador independiente de Windows (no el programa de instalación de SQL), o si se actualiza mediante el instalador independiente de Windows, se instalan las bibliotecas de R en una carpeta diferente.

Aunque se recomienda, si también se instala una instancia de SQL Server con R Services (In-Database) en el mismo equipo, una segunda copia de las bibliotecas de R y herramientas se instalan en una carpeta diferente.

En la tabla siguiente se enumera las rutas de acceso para cada instalación.

|Versión| Método de instalación | Carpeta predeterminada|
|----|----|----|
|R Server (Standalone) |Asistente para la instalación de SQL Server 2016|`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|R Server (Standalone) |Instalador independiente de Windows|`C:\Program Files\Microsoft\R Server\R_SERVER`|
|Machine Learning Server (independiente) |  Asistente para instalación de SQL Server 2017, con la opción de lenguaje R |`C:\Program Files\Microsoft SQL Server\140\R_SERVER`|
|Machine Learning Server (independiente) |  Asistente para instalación de SQL Server 2017, con la opción de lenguaje de Python |`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Machine Learning Server (independiente) |  Instalador independiente de Windows |`C:\Program Files\Microsoft\R Server\R_SERVER`|
|R Services (en bases de datos) |Asistente para la instalación de SQL Server 2016|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|
|Machine Learning Services (en base de datos) |Asistente para instalación de SQL Server 2017, con la opción de lenguaje R|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  |
|Machine Learning Services (en base de datos) |Asistente para instalación de SQL Server 2017, con la opción de lenguaje de Python| `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |

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

+ [Tutorial: Ejecutar R en T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md).
+ [Tutorial: Análisis de en bases de datos para los desarrolladores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Para ver ejemplos de aprendizaje automático que se basan en situaciones del mundo real, vea [máquina tutoriales de aprendizaje](../tutorials/machine-learning-services-tutorials.md).

