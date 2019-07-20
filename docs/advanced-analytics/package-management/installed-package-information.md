---
title: Bibliotecas de paquetes de R y Python predeterminadas
description: Paquetes de r y Python instalados por SQL Server para R Services, R Server, Machine Learning Services (in-Database) y Machine Learning Server (independiente)
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: f6cf66725ae15b2b738c020258142576ede734ec
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345084"
---
# <a name="default-r-and-python-packages-in-sql-server"></a>Paquetes de R y Python predeterminados en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se enumeran los paquetes de R y Python instalados con SQL Server y dónde encontrar la biblioteca de paquetes.  

## <a name="r-package-list-for-sql-server"></a>Lista de paquetes de R para SQL Server

Los paquetes de r se instalan con [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) y [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) cuando se selecciona la característica de r durante la instalación. 

|.         | 2016 | 2017 | Descripción |
|----------------|--------------|--------------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | 9,2 | Se usa para contextos de cálculo remotos, streaming, ejecución en paralelo de funciones RX para la importación y transformación de datos, modelado, visualización y análisis. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | 9,2 |Se usa para incluir scripts de R en procedimientos almacenados. |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9,2 | Agrega algoritmos de aprendizaje automático en R. | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a.  | 9,2 | Se utiliza para escribir instrucciones MDX en R. |

MicrosoftML y olapr están disponibles de forma predeterminada en SQL Server 2017 Machine Learning Services. En una instancia de SQL Server 2016 R Services, puede agregar estos paquetes a través de una [actualización de componente](../install/upgrade-r-and-python.md). Una actualización de componente también obtiene las versiones más recientes de los paquetes (por ejemplo, las versiones más recientes de RevoScaleR incluyen funciones para la administración de paquetes en SQL Server).

## <a name="python-package-list-for-sql-server"></a>Lista de paquetes de Python para SQL Server

Los paquetes de Python solo están disponibles en SQL Server 2017 al instalar [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) y seleccionar la característica de Python.

| .         | 2017    |  Descripción |
| -----------------|-------------|------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9,2 | Se usa para contextos de cálculo remotos, streaming, ejecución en paralelo de funciones RX para la importación y transformación de datos, modelado, visualización y análisis. |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9,2 | Agrega algoritmos de aprendizaje automático en Python. |

## <a name="open-source-r-in-your-installation"></a>R de código abierto en su instalación

La compatibilidad con r incluye código abierto para que pueda llamar a las funciones base de R e instalar paquetes de código abierto y de terceros adicionales. La compatibilidad con el lenguaje R incluye funcionalidades básicas como **base**, **estadísticas**, **utilidades**y otras. Una instalación base de R también incluye numerosos conjuntos de datos de ejemplo y herramientas de R estándar como **RGui** (un editor interactivo ligero) y **RTerm** (un símbolo del sistema de r). 

La distribución de R de código abierto incluida en la instalación es [Microsoft R Open (MRO)](https://mran.microsoft.com/open). MRO agrega valor a base R mediante la inclusión de paquetes de código abierto adicionales, como la [biblioteca de kernel de matemáticas de Intel](https://en.wikipedia.org/wiki/Math_Kernel_Library).

En la tabla siguiente se resumen las versiones de R proporcionadas por MRO mediante el programa de instalación de SQL Server.

|Release             | Versión de R       |
|--------------------|-----------------|
| [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) | 3.2.2   | 
| [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) | 3.3.3 |

Nunca debe sobrescribir manualmente la versión de R instalada SQL Server el programa de instalación con las versiones más recientes en la Web. Los paquetes de Microsoft R se basan en versiones específicas de R. la modificación de la instalación podría desestabilizarla.

## <a name="open-source-python-in-your-installation"></a>Python de código abierto en su instalación

SQL Server 2017 agrega componentes de Python. Al seleccionar la opción de idioma de Python, se instala la distribución de Anaconda 4,2. Además de las bibliotecas de código de Python, la instalación estándar incluye datos de ejemplo, pruebas unitarias y scripts de ejemplo. 

SQL Server 2017 Machine Learning es la primera versión que tiene compatibilidad con R y Python.

|Release             | Versión de Anaconda| Paquetes de Microsoft    |
|--------------------|-----------------|-----------------------|
| SQL Server 2017 Machine Learning Services  | 4,2 en Python 3,5 | revoscalepy, microsoftml |

Nunca debe sobrescribir manualmente la versión de Python instalada por SQL Server el programa de instalación con las versiones más recientes en la Web. Los paquetes de Microsoft Python se basan en versiones específicas de anaconda. La modificación de la instalación podría desestabilizarla.

## <a name="component-upgrades"></a>Actualizaciones de componentes

Después de una instalación inicial, los paquetes de R y Python se actualizan a través de los Service Pack y las actualizaciones acumulativas, pero las actualizaciones de versión completas solo son posibles si se *enlaza* a la Directiva de soporte técnico moderno del ciclo de vida. El enlace cambia el modelo de servicio. De forma predeterminada, después de una instalación inicial, los paquetes de R se actualizan a través de los Service Pack y las actualizaciones acumulativas. Los paquetes adicionales y las actualizaciones de versión completa de los componentes principales de R solo son posibles a través de las actualizaciones de productos (de SQL Server 2016 a SQL Server 2017) o mediante el enlace de soporte de R a Microsoft Machine Learning Server. Para obtener más información, consulte [actualización de los componentes de R y Python en SQL Server](../install/upgrade-r-and-python.md).

## <a name="package-library-location"></a>Ubicación de la biblioteca de paquetes

Al instalar machine learning con SQL Server, se crea una biblioteca de paquetes única en el nivel de instancia para cada idioma que se instala. En Windows, la biblioteca de instancias es una carpeta protegida registrada con SQL Server.

Todo el script o el código que se ejecuta en la base de datos en SQL Server deben cargar funciones desde la biblioteca de instancias. SQL Server no puede tener acceso a los paquetes instalados en otras bibliotecas. Esto también se aplica a los clientes remotos. Al conectarse al servidor desde un cliente remoto, cualquier código de R o Python que desee ejecutar en el contexto de proceso del servidor solo puede usar los paquetes instalados en la biblioteca de instancias.

Para proteger los recursos del servidor, la biblioteca de instancia predeterminada solo puede ser modificada por un administrador del equipo. Si no es el propietario del equipo, es posible que tenga que obtener el permiso de un administrador para instalar paquetes en esta biblioteca. 

#### <a name="file-path-for-in-database-engine-instances"></a>Ruta de acceso de archivo para instancias del motor de base de datos

En la tabla siguiente se muestra la ubicación del archivo de R y Python para las combinaciones de versión y de instancia del motor de base de datos. MSSQL13 indica SQL Server 2016 y es de solo lectura. MSSQL14 indica SQL Server 2017 y tiene carpetas R y Python. 

Las rutas de acceso de archivo también incluyen nombres de instancia. SQL Server instala [las instancias del motor de base de datos](../../database-engine/configure-windows/database-engine-instances-sql-server.md) como instancia predeterminada (MSSQLSERVER) o como una instancia con nombre definida por el usuario. Si SQL Server se instala como una instancia con nombre, verá que el nombre se anexa como se indica `MSSQL13.<instance_name>`a continuación:.

|Versión e idioma  | Ruta de acceso predeterminada|
|----------------------|------------|
| SQL Server 2016 |C:\Archivos de Programa\microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\library|
| SQL Server 2017 con R|C:\Archivos de Programa\microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library |
| SQL Server 2017 con Python |C:\Archivos de Programa\microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages |


#### <a name="file-path-for-standalone-server-installations"></a>Ruta de acceso de archivo para instalaciones de servidor independientes

En la tabla siguiente se enumeran las rutas de acceso predeterminadas de los archivos binarios cuando se instala SQL Server 2016 R Server (independiente) o SQL Server 2017 Machine Learning Server (independiente). 

|`Version`| Instalación|Ruta de acceso predeterminada|
|-------|-------------|------------|
| SQL Server 2016|R Server (Standalone)| C:\Archivos de Programa\microsoft SQL Server\130\R_SERVER|
|SQL Server 2017|Machine Learning Server, con R |C:\Archivos de Programa\microsoft SQL Server\140\R_SERVER|
|SQL Server 2017|Machine Learning Server, con Python |C:\Archivos de Programa\microsoft SQL Server\140\PYTHON_SERVER|

> [!NOTE]
> Si encuentra otras carpetas con nombres y archivos de subcarpetas similares, es probable que tenga una instalación independiente de Microsoft R Server o [machine learning Server](https://docs.microsoft.com/machine-learning-server/). Estos productos de servidor tienen distintos instaladores y rutas de acceso (es decir, C:\Archivos de Files\Microsoft\R Server\R_SERVER o C:\Archivos de Programa\microsoft\ml SERVER\R_SERVER). Para obtener más información, consulte [instalación de machine learning Server para Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) o [instalación de R Server 9,1 para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

## <a name="next-steps"></a>Pasos siguientes

+ [Obtención de información del paquete](installed-package-information.md)
+ [Instalación de paquetes de R adicionales](../r/install-additional-r-packages-on-sql-server.md)
+ [Instalación de paquetes de Python adicionales](../python/install-additional-python-packages-on-sql-server.md)
+ [Habilitación de la administración de paquetes de R remota](../r/r-package-how-to-enable-or-disable.md)
+ [Funciones de RevoScaleR para administración de paquetes de R](../r/use-revoscaler-to-manage-r-packages.md)
+ [Sincronización de paquetes de R](../r/package-install-uninstall-and-sync.md)
+ [miniCRAN para el repositorio local de paquetes de R](../r/create-a-local-package-repository-using-minicran.md)
