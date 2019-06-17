---
title: Valor predeterminado de bibliotecas de paquetes R y Python - SQL Server Machine Learning Services
description: Paquetes de R y Python que se instala con SQL Server de servicios de R, R Server, Machine Learning Services (In-Database) y Machine Learning Server (independiente)
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 3126872e3333383d0cea53f38b3cfd06be86b704
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/14/2019
ms.locfileid: "67141404"
---
# <a name="default-r-and-python-packages-in-sql-server"></a>Paquetes de R de forma predeterminada y Python en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se enumera los paquetes de R y Python instalados con SQL Server y dónde encontrar la biblioteca de paquetes.  

## <a name="r-package-list-for-sql-server"></a>Lista de paquetes de R para SQL Server

Paquetes de R se instalan con [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) y [Machine Learning Services de SQL Server 2017](../install/sql-machine-learning-services-windows-install.md) cuando selecciona la característica R durante la instalación. 

|.         | 2016 | 2017 | Descripción |
|----------------|--------------|--------------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | 9.2 | Usar contextos de cálculo remoto, streaming, la ejecución en paralelo de las funciones rx para la importación de datos y transformación, modelado, visualización y análisis. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | 9.2 |Se utiliza para incluir el script de R en procedimientos almacenados. |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.2 | Agrega los algoritmos de aprendizaje automático en R. | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a.  | 9.2 | Utilizado para escribir instrucciones MDX en R. |

MicrosoftML y olapR están disponibles de forma predeterminada en SQL Server 2017 Machine Learning Services. En una instancia de SQL Server 2016 R Services, puede agregar estos paquetes a través de un [actualización del componente](../install/upgrade-r-and-python.md). Una actualización de componentes también obtiene las versiones más recientes de los paquetes (por ejemplo, las versiones más recientes de RevoScaleR incluyen funciones de administración de paquetes en SQL Server).

## <a name="python-package-list-for-sql-server"></a>Lista de paquetes de Python para SQL Server

Paquetes de Python solo están disponibles en SQL Server 2017 al instalar [Machine Learning Services de SQL Server 2017](../install/sql-machine-learning-services-windows-install.md) y seleccione la característica de Python.

| .         | 2017    |  Descripción |
| -----------------|-------------|------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2 | Usar contextos de cálculo remoto, streaming, la ejecución en paralelo de las funciones rx para la importación de datos y transformación, modelado, visualización y análisis. |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2 | Agrega los algoritmos de aprendizaje automático de Python. |

## <a name="open-source-r-in-your-installation"></a>R de código abierto en la instalación

Compatibilidad con R incluye abierto son por lo que puede llamar a funciones de R bases e instalar paquetes adicionales de código abierto y de terceros. Compatibilidad con el lenguaje R incluye funcionalidad básica como **base**, **estadísticas**, **utils**y otros. Una instalación básica de R también incluye numerosos conjuntos de datos de ejemplo y las herramientas de R estándares, como **RGui** (un editor ligero interactivo) y **RTerm** (una línea de comandos de R). 

La distribución de R de código abierto, incluido en la instalación es [Microsoft R abrir (MRO)](https://mran.microsoft.com/open). MRO agrega valor a R base al incluir paquetes adicionales de código abierto, como el [Intel Math Kernel Library](https://en.wikipedia.org/wiki/Math_Kernel_Library).

En la tabla siguiente se resume las versiones de R proporcionados por MRO mediante el programa de instalación de SQL Server.

|Versión             | Versión de R       |
|--------------------|-----------------|
| [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) | 3.2.2   | 
| [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) | 3.3.3 |

Nunca debe sobrescribir la versión de R que se instala el programa de instalación de SQL Server con las versiones más recientes en la web. Paquetes de R de Microsoft se basan en versiones específicas de R. modificar la instalación podría desestabilizar.

## <a name="open-source-python-in-your-installation"></a>Python de código abierto en la instalación

SQL Server 2017 agrega los componentes de Python. Cuando se selecciona la opción de lenguaje de Python, se instala la distribución de Anaconda 4.2. Además de las bibliotecas de código de Python, la instalación estándar incluye datos de ejemplo, las pruebas unitarias y scripts de muestra. 

Aprendizaje automático de SQL Server 2017 es la primera versión que R y Python admite.

|Versión             | Versión de anaconda| Paquetes de Microsoft    |
|--------------------|-----------------|-----------------------|
| SQL Server 2017 Machine Learning Services  | 4.2 sobre Python 3.5 | revoscalepy, microsoftml |

Nunca debe sobrescribir la versión de Python que se instala el programa de instalación de SQL Server con las versiones más recientes en la web. Paquetes de Python de Microsoft se basan en versiones específicas de Anaconda. Modificar la instalación podría desestabilizar.

## <a name="component-upgrades"></a>Actualizaciones de componentes

Después de la instalación inicial, se actualizan los paquetes R y Python a través de los service packs y actualizaciones acumulativas, pero solo son posibles por las actualizaciones de versión completa *enlace* a la directiva de soporte técnico de ciclo de vida moderno. Enlace cambia el modelo de mantenimiento. De forma predeterminada, tras la instalación inicial, los paquetes de R se actualizan a través de los service packs y actualizaciones acumulativas. Paquetes adicionales y las actualizaciones de versión completa de los componentes principales de R solo son posibles a través de las actualizaciones de producto (desde SQL Server 2016 a SQL Server 2017) o mediante el enlace de R admiten Microsoft Machine Learning Server. Para obtener más información, consulte [componentes actualizar R y Python en SQL Server](../install/upgrade-r-and-python.md).

## <a name="package-library-location"></a>Ubicación de la biblioteca de paquete

Cuando se instala el aprendizaje automático con SQL Server, se crea una biblioteca de paquetes solo en el nivel de instancia para cada idioma instalado. En Windows, la biblioteca de la instancia es una carpeta protegida registrada con SQL Server.

Todas las secuencias de comandos o código que se ejecuta en bases de datos en SQL Server debe cargar las funciones de la biblioteca de la instancia. SQL Server no puede tener acceso a los paquetes instalados en otras bibliotecas. Esto se aplica a los clientes remotos. Al conectarse al servidor desde un cliente remoto, cualquier código R o Python que se desea ejecutar en el contexto de proceso de servidor solo puede usar los paquetes instalados en la biblioteca de la instancia.

Para proteger los activos del servidor, la biblioteca de la instancia predeterminada se puede modificar únicamente por un administrador del equipo. Si no es el propietario del equipo, es posible que deba obtener permiso de administrador para instalar paquetes en esta biblioteca. 

#### <a name="file-path-for-in-database-engine-instances"></a>Ruta de acceso de las instancias del motor de base de datos

La siguiente tabla muestra las combinaciones de instancia del motor de la ubicación del archivo de R y Python para la versión y la base de datos. MSSQL13 indica que SQL Server 2016 y es solo para R. MSSQL14 indica que SQL Server 2017 y tiene carpetas de R y Python. 

Las rutas de acceso de archivo también incluyen los nombres de instancia. SQL Server instala [instancias del motor de base de datos](../../database-engine/configure-windows/database-engine-instances-sql-server.md) como la instancia predeterminada (MSSQLSERVER) o como una instancia con nombre definido por el usuario. Si SQL Server está instalado como una instancia con nombre, podrá ver ese nombre anexado como sigue: `MSSQL13.<instance_name>`.

|Versión e idioma  | Ruta de acceso predeterminada|
|----------------------|------------|
| SQL Server 2016 |C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\library|
| SQL Server 2017 con R|C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library |
| SQL Server 2017 con Python |C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Lib\site paquetes |


#### <a name="file-path-for-standalone-server-installations"></a>Ruta de acceso de archivo para instalaciones de servidor independiente

En la tabla siguiente se enumera las rutas de acceso predeterminada de los archivos binarios cuando se instala SQL Server 2016 R Server (independiente) o el servidor de SQL Server 2017 Machine Learning Server (independiente). 

|Versión| Instalación|Ruta de acceso predeterminada|
|-------|-------------|------------|
| SQL Server 2016|R Server (Standalone)| C:\Program Files\Microsoft SQL Server\130\R_SERVER|
|SQL Server 2017|Machine Learning Server con R |C:\Program Files\Microsoft SQL Server\140\R_SERVER|
|SQL Server 2017|Machine Learning Server, con Python |C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER|

> [!NOTE]
> Si encuentra otras carpetas que tienen nombres similares de subcarpeta y archivos, probablemente tenga una instalación independiente de Microsoft R Server o [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/). Estos productos de servidor tienen instaladores diferentes y las rutas de acceso (es decir, C:\Program Files\Microsoft\R Server\R_SERVER o C:\Program programa\microsoft\ml SERVER\R_SERVER). Para obtener más información, consulte [instale Machine Learning Server para Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) o [instalar R Server 9.1 para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

## <a name="next-steps"></a>Pasos siguientes

+ [Obtención de información del paquete](installed-package-information.md)
+ [Instalación de paquetes de R adicionales](../r/install-additional-r-packages-on-sql-server.md)
+ [Instalación de paquetes de Python adicionales](../python/install-additional-python-packages-on-sql-server.md)
+ [Habilitación de la administración de paquetes de R remota](../r/r-package-how-to-enable-or-disable.md)
+ [Funciones de RevoScaleR para administración de paquetes de R](../r/use-revoscaler-to-manage-r-packages.md)
+ [Sincronización de paquetes de R](../r/package-install-uninstall-and-sync.md)
+ [miniCRAN para el repositorio local de paquetes de R](../r/create-a-local-package-repository-using-minicran.md)
