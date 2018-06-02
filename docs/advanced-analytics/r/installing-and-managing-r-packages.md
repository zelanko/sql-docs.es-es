---
title: Bibliotecas de paquete de R y Python en SQL Server R y aprendizaje automático de SQL Server predeterminadas | Documentos de Microsoft
description: Paquetes de R y Python instalados por SQL Server para servicios de R, R Server, Machine Learning Services (In-Database) y servidor de aprendizaje de máquina (independiente)
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 9362d6e9dc98f80beabc301f43e755b205b40a10
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/01/2018
ms.locfileid: "34707293"
---
# <a name="default-r-and-python-packages-in-sql-server"></a>Paquetes de R de manera predeterminada y Python en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo enumeran los paquetes de R y Python instalados con SQL Server y dónde encontrar la biblioteca de paquete.  

## <a name="r-package-list-for-sql-server"></a>Lista de paquetes de R para SQL Server

Paquetes de R se instalan con [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) y [servicios de aprendizaje de SQL Server de 2017 máquinas](../install/sql-machine-learning-services-windows-install.md) cuando se selecciona la característica de R durante la instalación. 

.         | 2016 | 2017 | Descripción |
|----------------|--------------|--------------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | 9.2 | Usar para contextos de proceso remoto, transmisión por secuencias, la ejecución en paralelo de las funciones rx para la importación de datos y transformación, modelado, visualización y análisis. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | 9.2 |Se utiliza para incluir un script de R en los procedimientos almacenados. |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.2 | Agrega los algoritmos de aprendizaje automático en R. | 
| [OlapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a.  | 9.2 | Utilizado para escribir instrucciones MDX en R. |

MicrosoftML y olapR están disponibles de forma predeterminada en servicios de aprendizaje de máquina de SQL Server de 2017. En una instancia de SQL Server 2016 R Services, puede agregar estos paquetes a través de un [actualización del componente](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md). Una actualización del componente también obtiene las versiones más recientes de los paquetes (por ejemplo, las versiones más recientes de RevoScaleR incluyen funciones para la administración de paquetes en SQL Server).

## <a name="python-package-list-for-sql-server"></a>Lista de paquetes de Python para SQL Server

Paquetes de Python solo están disponibles en SQL Server 2017 al instalar [servicios de aprendizaje de SQL Server de 2017 máquinas](../install/sql-machine-learning-services-windows-install.md) y seleccione la característica de Python.

| .         | 2017    |  Descripción |
| -----------------|-------------|------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2 | Usar para contextos de proceso remoto, transmisión por secuencias, la ejecución en paralelo de las funciones rx para la importación de datos y transformación, modelado, visualización y análisis. |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2 | Agrega los algoritmos de aprendizaje automático de Python. |

## <a name="open-source-r-in-your-installation"></a>R de código abierto en la instalación

Compatibilidad con R incluye código abierto para que se puede llamar a funciones de R base e instalar paquetes adicionales de código abierto y de otros fabricantes. Compatibilidad con idiomas de R incluye funcionalidad básica como **base**, **estadísticas**, **utils**y otros. Una instalación básica de R también incluye varios conjuntos de datos de ejemplo y herramientas estándar de R como **RGui** (un editor interactivo ligero) y **RTerm** (una línea de comandos de R). 

La distribución de R de código abierto incluida en la instalación es [Microsoft R abrir (MRO)](https://mran.microsoft.com/open). MRO favorece a R base mediante la inclusión de paquetes adicionales de código abierto como el [Intel Math Kernel Library](https://en.wikipedia.org/wiki/Math_Kernel_Library).

En la tabla siguiente se resume las versiones de R proporcionada por MRO mediante el programa de instalación de SQL Server.

|Versión             | Versión de R       |
|--------------------|-----------------|
| [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) | 3.2.2   | 
| [Servicios de aprendizaje de máquina de 2017 de SQL Server](../install/sql-machine-learning-services-windows-install.md) | 3.3.3 |

Nunca manualmente debe sobrescribir la versión de R que se instala el programa de instalación de SQL Server con las versiones más recientes en la web. Paquetes de R de Microsoft se basan en las versiones específicas de R. modificar la instalación podría desestabilizar.

## <a name="open-source-python-in-your-installation"></a>Python de código abierto en la instalación

SQL Server 2017 agrega componentes de Python. Cuando se selecciona la opción de lenguaje de Python, distribución de Anaconda 4.2 está instalado. Además de las bibliotecas de código de Python, la instalación estándar incluye datos de ejemplo, pruebas unitarias y scripts de ejemplo. 

Aprendizaje automático de SQL Server de 2017 es la primera versión que R y Python admiten.

|Versión             | Versión de anaconda| Paquetes de Microsoft    |
|--------------------|-----------------|-----------------------|
| SQL Server 2017 Machine Learning Services  | 4.2 sobre 3.5 de Python | revoscalepy, microsoftml |

Nunca manualmente debe sobrescribir la versión de Python que instala el programa de instalación de SQL Server con las versiones más recientes en la web. Paquetes de Microsoft Python se basan en las versiones específicas de Anaconda. Modificar la instalación podría desestabilizar.

## <a name="component-upgrades"></a>Actualizaciones de componentes

Después de la instalación inicial, se actualizan los paquetes de R y Python a través de service packs y actualizaciones acumulativas, pero sólo son posibles con las actualizaciones de versión completa *enlace* a la directiva de soporte técnico de ciclo de vida moderna. Enlace cambia el modelo de servicio. De forma predeterminada, después de la instalación inicial, paquetes de R se actualizan a través de service packs y actualizaciones acumulativas. Las actualizaciones de la versión completa de los componentes principales de investigación y paquetes adicionales sólo son posibles a través de actualizaciones de producto (a través de SQL Server 2016 a SQL Server 2017) o mediante el enlace de R admiten al servidor de aprendizaje de máquina de Microsoft. Para obtener más información, consulte [actualizar R y Python componentes de SQL Server](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

## <a name="package-library-location"></a>Ubicación de la biblioteca de paquete

Cuando se instala el aprendizaje automático con SQL Server, se crea una biblioteca de paquete único en el nivel de instancia para cada idioma instalado. En Windows, la biblioteca de instancia es una carpeta protegida registrada con SQL Server.

Todas las secuencias de comandos o código que se ejecuta en bases de datos en SQL Server debe cargar las funciones de la biblioteca de la instancia. SQL Server no puede tener acceso a los paquetes instalados en otras bibliotecas. Esto se aplica a los clientes remotos. Al conectarse al servidor desde un cliente remoto, cualquier código de R o Python que desea ejecutar en el contexto de proceso de servidor solo puede usar los paquetes instalados en la biblioteca de la instancia.

Para proteger los activos del servidor, la biblioteca de la instancia predeterminada se puede modificar únicamente por un administrador del equipo. Si no es el propietario del equipo, debe obtener el permiso de administrador para instalar paquetes a esta biblioteca. 

#### <a name="file-path-for-in-database-engine-instances"></a>Ruta de acceso de archivo para instancias del motor en bases de datos

La siguiente tabla muestra la ubicación del archivo de R y Python para la base de datos y la versión de combinaciones de la instancia de motor. MSSQL13 indica que SQL Server 2016 y es solo para R. MSSQL14 indica 2017 de SQL Server y tiene carpetas R y Python. 

Las rutas de acceso de archivo también incluyen los nombres de instancia. SQL Server instala [instancias del motor de base de datos](../../database-engine/configure-windows/database-engine-instances-sql-server.md) como la instancia predeterminada (MSSQLSERVER) o como una instancia con nombre definido por el usuario. Si SQL Server está instalado como una instancia con nombre, verá dicho nombre anexado como sigue: `MSSQL13.<instance_name>`.

|Versión e idioma  | Ruta de acceso predeterminada|
|----------------------|------------|
| SQL Server 2016 |C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\library|
| SQL Server de 2017 con R|C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library |
| SQL Server de 2017 con Python |C:\Program Files\Microsoft SQL Server\MSSQL14. Paquetes de MSSQLSERVER\PYTHON_SERVICES\Lib\site |


#### <a name="file-path-for-standalone-server-installations"></a>Ruta de acceso de archivo para las instalaciones de servidor independiente

En la tabla siguiente se enumera las rutas de acceso predeterminadas de los archivos binarios cuando se instala SQL Server 2016 R Server (independiente) o servidor de SQL Server de 2017 máquina aprendizaje Server (independiente). 

|Versión| Installation|Ruta de acceso predeterminada|
|-------|-------------|------------|
| SQL Server 2016|R Server (Standalone)| C:\Program Files\Microsoft SQL Server\130\R_SERVER|
|SQL Server 2017|Servidor, con R de aprendizaje automático |C:\Program Files\Microsoft SQL Server\140\R_SERVER|
|SQL Server 2017|Servidor, con Python de aprendizaje automático |C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER|

> [!NOTE]
> Si encuentra otras carpetas con nombres similares de las subcarpetas y archivos, es probable que tenga una instalación independiente de Microsoft R Server o [servidor de aprendizaje automático](https://docs.microsoft.com/machine-learning-server/). Estos productos de servidor tienen instaladores diferentes y las rutas de acceso (es decir, C:\Program Files\Microsoft\R Server\R_SERVER o C:\Program Files\Microsoft\ML SERVER\R_SERVER). Para obtener más información, consulte [instalar servidor para aprendizaje máquina con Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) o [instalar R Server 9.1 para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

## <a name="next-steps"></a>Pasos siguientes

+ [Obtención de información del paquete](determine-which-packages-are-installed-on-sql-server.md)
+ [Instalación de paquetes de R adicionales](install-additional-r-packages-on-sql-server.md)
+ [Instalación de paquetes de Python adicionales](../python/install-additional-python-packages-on-sql-server.md)
+ [Habilitación de la administración de paquetes de R remota](r-package-how-to-enable-or-disable.md)
+ [Funciones de RevoScaleR para administración de paquetes de R](use-revoscaler-to-manage-r-packages.md)
+ [Sincronización de paquetes de R](package-install-uninstall-and-sync.md)
+ [miniCRAN para el repositorio local de paquetes de R](create-a-local-package-repository-using-minicran.md)
