---
title: Bibliotecas de paquete de R y Python en SQL Server R y aprendizaje automático de SQL Server predeterminadas | Documentos de Microsoft
description: Paquetes de R y Python instalados por SQL Server para servicios de R, R Server, Machine Learning Services (In-Database) y servidor de aprendizaje de máquina (independiente)
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/08/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 48fb451e35f58cf606c47cd64cf5f9093069c274
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="default-r-and-python-packages-in-sql-server"></a>Paquetes de R de manera predeterminada y Python en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo tratan las bibliotecas de paquete, la ubicación y las versiones de paquetes de R y Python instaladas con SQL Server. 

## <a name="using-the-default-instance-library"></a>Uso de la biblioteca de la instancia predeterminada

Cuando se instala el aprendizaje automático con SQL Server, se crea una biblioteca de paquete único en el nivel de instancia para cada idioma instalado. 

Todas las secuencias de comandos o código que se ejecuta en bases de datos en SQL Server debe cargar las funciones de la biblioteca de la instancia. SQL Server no puede tener acceso a los paquetes instalados en otras bibliotecas. Esto se aplica a los clientes remotos. Al conectarse al servidor desde un cliente remoto, cualquier código de R o Python que desea ejecutar en el contexto de proceso de servidor solo puede usar los paquetes instalados en la biblioteca de la instancia.

Para proteger los activos del servidor, la biblioteca de la instancia predeterminada se instala en una carpeta protegida que se registra con SQL Server y se puede modificar únicamente por un administrador del equipo. Si no es el propietario del equipo, debe obtener el permiso de administrador para instalar paquetes a esta biblioteca. 

Incluso si usted es el propietario del equipo, debe considerar la utilidad de cualquier paquete de R o Python determinado en un entorno de servidor antes de agregar el paquete a la biblioteca de la instancia. Tenga en cuenta factores como el tamaño de los archivos de paquete y la necesidad de varias versiones, así como si requiere el paquete de red o internet access.

### <a name="in-database-engine-instance-file-paths"></a>Las rutas de acceso del archivo de instancia de motor de base de datos

La siguiente tabla muestra la ubicación del archivo de R y Python para la base de datos y la versión de combinaciones de la instancia de motor. 

|Versión | Nombre de instancia|Ruta de acceso predeterminada|
|--------|--------------|------------|
| SQL Server 2016 |instancia predeterminada| C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\library|
| SQL Server 2016 |instancia con nombre | C:\Program Files\Microsoft SQL Server\MSSQL13. < nombre_instancia > \R_SERVICES\library|
| SQL Server de 2017 con R|instancia predeterminada | C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library |
| SQL Server de 2017 con R|instancia con nombre| C:\Program Files\Microsoft SQL Server\MSSQL14. MyNamedInstance\R_SERVICES\library |
| SQL Server de 2017 con Python |instancia predeterminada | C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\library |
| SQL Server de 2017 con Python|instancia con nombre| C:\Program Files\Microsoft SQL Server\MSSQL14. < nombre_instancia > \PYTHON_SERVICES\library |

### <a name="standalone-server-file-paths"></a>Rutas de acceso de servidor independiente 

En la tabla siguiente se enumera las rutas de acceso predeterminadas de los archivos binarios cuando se instala SQL Server 2016 R Server (independiente) o servidor de SQL Server de 2017 máquina aprendizaje Server (independiente). 

|Versión| Installation|Ruta de acceso predeterminada|
|------|------|------|
| SQL Server 2016|R Server (Standalone)| C:\Program Files\Microsoft SQL Server\130\R_SERVER|
|SQL Server 2017|Servidor, con R de aprendizaje automático |C:\Program Files\Microsoft SQL Server\140\R_SERVER|
|SQL Server 2017|Servidor, con Python de aprendizaje automático |C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER|

> [!NOTE]
> Si encuentra otras carpetas con nombres similares de las subcarpetas y archivos, es probable que tenga una instalación independiente de Microsoft R Server o [servidor de aprendizaje automático](https://docs.microsoft.com/machine-learning-server/). Estos productos de servidor tienen instaladores diferentes y las rutas de acceso (es decir, C:\Program Files\Microsoft\R Server\R_SERVER o C:\Program Files\Microsoft\ML SERVER\R_SERVER). Para obtener más información, consulte [instalar servidor para aprendizaje máquina con Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) o [instalar R Server 9.1 para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

## <a name="what-is-included-in-a-default-installation"></a>¿Qué se incluye en una instalación predeterminada

Esta sección resumen las características de R y Python incluidas en una instalación predeterminada.

### <a name="r-components"></a>Componentes de R

Código abierto R es la distribución de Microsoft [abierto de R (MRO)](https://mran.microsoft.com/open). Paquetes de R de base incluyen funcionalidad básica como **estadísticas** y **utils**. Puede ejecutar `installed.packages(priority = "base")` para devolver una lista de paquetes. Una instalación básica de R también incluye numerosos conjuntos de datos de ejemplo y las herramientas estándar de R como RGui (un editor interactivo ligero) y RTerm (una línea de comandos de R).

Propietario R paquetes incluyen [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) para contextos de proceso remoto, transmisión por secuencias, ejecución de las funciones rx para la importación de datos y transformación en paralelo, el modelado, visualización y análisis. [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package) agrega aprendizaje automático de modelado en R. Otros paquetes de Microsoft incluyen [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) para escribir instrucciones MDX en R y [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) para incluir un script de R en los procedimientos almacenados.


|Versión             | Versión de R       | Paquetes de Microsoft    |
|--------------------|-----------------|-----------------------|
| SQL Server 2016 R Services | 3.2.2   | RevoScaleR, sqlrutil  |
| SQL Server 2017 Machine Learning Services| 3.3.3 | RevoScaleR, MicrosoftML, olapR, sqlrutil|

Puede actualizar los paquetes de componentes de R, agregar nuevos paquetes de R y modelos previamente instalados por enlace a la directiva de soporte técnico de ciclo de vida moderna. Enlace cambia el modelo de servicio. De forma predeterminada, después de la instalación inicial, paquetes de R se actualizan a través de service packs y actualizaciones acumulativas. Las actualizaciones de la versión completa de los componentes principales de investigación y paquetes adicionales sólo son posibles a través de actualizaciones de producto (a través de SQL Server 2016 a SQL Server 2017) o mediante el enlace de R admiten al servidor de aprendizaje de máquina de Microsoft. Para obtener más información, consulte [actualizar R y Python componentes de SQL Server](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

### <a name="python-components"></a>Componentes de Python

SQL Server 2017 agrega componentes de Python. Cuando se selecciona la opción de lenguaje de Python, se instala una distribución de Anaconda. Además de las bibliotecas de código de Python, la instalación estándar incluye datos de ejemplo, pruebas unitarias y scripts de ejemplo. 

Paquetes de Microsoft incluyen [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) como el equivalente de Python de RevoScaleR, con la transmisión por secuencias, ejecución de las funciones rx para la importación de datos y transformación, modelado, visualización y análisis en paralelo. Es otro paquete de Python [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) para el entrenamiento y las transformaciones, análisis de puntuación, text e image y extracción de características para derivar valores de datos existentes.

Aprendizaje automático de SQL Server de 2017 es la primera versión que R y Python admiten.

|Versión             | Versión de anaconda| Paquetes de Microsoft    |
|--------------------|-----------------|-----------------------|
| SQL Server 2017 Machine Learning Services  | 4.2 sobre 3.5 de Python | revoscalepy, microsoftml |

Después de la instalación inicial, se actualizan los paquetes de Python a través de service packs y actualizaciones acumulativas, pero las actualizaciones de versión completo sólo son posibles mediante el enlace de compatibilidad con Python para aprendizaje de máquina de Microsoft Server. Para obtener más información, consulte [actualizar R y Python componentes de SQL Server](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

## <a name="administrative-permissions-for-package-installation"></a>Permisos administrativos para la instalación del paquete

La biblioteca de paquete utilizada por una instancia de base de datos se encuentra físicamente en la carpeta archivos de programa de la instancia de SQL Server. En la escritura en esta ubicación se requiere permisos de administrador. Sin embargo, SQL Server 2017 ofrece algunas metodologías adicionales para la instalación de paquete que ofrece la posibilidad de agregar paquetes de usuarios no administradores.

+ En SQL Server 2016, es necesario para la nueva instalación de paquete acceso administrativo.
+ En SQL Server 2017, aún puede instalar paquetes como un administrador de R y Python y probablemente es el método más fácil. 

    La instrucción de DDL, crear biblioteca externa, permite al administrador de base de datos instalar paquetes sin con herramientas de R. 

    Si usa la característica de administración de paquetes en servidor de aprendizaje de máquina, puede usar RevoScaleR para instalar paquetes de R en el nivel de base de datos. El Administrador de base de datos debe habilitar la característica y, a continuación, conceder a los usuarios la capacidad para instalar sus propios paquetes por base de datos. Para obtener más información, consulte [habilitar la administración de paquetes mediante DDL](r-package-how-to-enable-or-disable.md).

### <a name="user-libraries-are-not-supported"></a>No se admiten las bibliotecas de usuario

Los usuarios que no se pueden instalar un paquete en una ubicación protegida a menudo recurren a la instalación de un paquete en una biblioteca de usuario. Sin embargo, esto no es posible en el entorno de SQL Server. Normalmente tiene restringido el acceso al sistema de archivos en el servidor e incluso si tiene derechos de administrador y el acceso a una carpeta de documentos de usuario en el servidor, el tiempo de ejecución de script externo que se ejecuta en SQL Server no puede tener acceso a los paquetes instalados fuera de la instancia predeterminada biblioteca. Sin embargo, las soluciones alternativas son posibles. Para obtener sugerencias sobre cómo resolver problemas relacionados con las bibliotecas de usuario, consulte [soluciones alternativas para las bibliotecas de usuario de R](packages-installed-in-user-libraries.md).

## <a name="next-steps"></a>Pasos siguientes

+ [Obtención de información del paquete](determine-which-packages-are-installed-on-sql-server.md)
+ [Instalación de paquetes de R adicionales](install-additional-r-packages-on-sql-server.md)
+ [Instalación de paquetes de Python adicionales](../python/install-additional-python-packages-on-sql-server.md)
+ [Habilitación de la administración de paquetes de R remota](r-package-how-to-enable-or-disable.md)
+ [Funciones de RevoScaleR para administración de paquetes de R](use-revoscaler-to-manage-r-packages.md)
+ [Sincronización de paquetes de R](package-install-uninstall-and-sync.md)
+ [miniCRAN para el repositorio local de paquetes de R](create-a-local-package-repository-using-minicran.md)
