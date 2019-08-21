---
title: Obtener información de paquete de R
description: Aprenda a obtener información acerca de los paquetes de R instalados en SQL Server Machine Learning Services y SQL Server R Services.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 8c3cf3c1debc03c169c585521b8b46dd8b1365c5
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2019
ms.locfileid: "69641162"
---
# <a name="get-r-package-information"></a>Obtener información de paquete de R

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se describe cómo obtener información acerca de los paquetes de R instalados en SQL Server Machine Learning Services y SQL Server R Services. Los scripts de R de ejemplo muestran cómo Mostrar información de paquetes como la ruta de instalación y la versión.

## <a name="default-r-library-location"></a>Ubicación predeterminada de la biblioteca de R

Al instalar machine learning con SQL Server, se crea una biblioteca de paquetes única en el nivel de instancia para cada idioma que se instala. En Windows, la biblioteca de instancias es una carpeta protegida registrada con SQL Server.

Todos los scripts que se ejecutan en la base de datos en SQL Server deben cargar funciones desde la biblioteca de instancias. SQL Server no puede tener acceso a los paquetes instalados en otras bibliotecas. Esto se aplica también a los clientes remotos: cualquier script de R que se ejecute en el contexto de proceso del servidor solo puede usar paquetes instalados en la biblioteca de instancias.
Para proteger los recursos del servidor, la biblioteca de instancia predeterminada solo puede ser modificada por un administrador del equipo.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
La ruta de acceso predeterminada de los archivos binarios de R es:

`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
La ruta de acceso predeterminada de los archivos binarios de R es:

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
La ruta de acceso predeterminada de los archivos binarios de R es:

`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

Se asume la instancia predeterminada de SQL, MSSQLSERVER. Si SQL Server se instala como una instancia con nombre definida por el usuario, se utiliza en su lugar el nombre especificado.

<!-- I don't think this note is necessary. If you have these other products installed, you'd already know about them.
> [!NOTE]
> If you find other folders having similar subfolder names and files, you probably have a standalone installation of  Microsoft R Server or Machine Learning Server. These server products have different installers and paths: C:\Program Files\Microsoft\R Server\R_SERVER or C:\Program Files\Microsoft\ML SERVER\R_SERVER. For more information, see [Install R Server 9.1 for Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) or [Install Machine Learning Server for Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).
-->

Ejecute la siguiente instrucción para comprobar la biblioteca de paquetes de R predeterminada para la instancia actual:

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

La siguiente instrucción usa [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) para devolver la ruta de acceso de la biblioteca de instancia y la versión de RevoScaleR que usa SQL Server:

```sql
EXECUTE sp_execute_external_script
  @language =N'R',
  @script=N'
  sql_r_path <- rxSqlLibPaths("local")
  print(sql_r_path)
  version_info <-packageVersion("RevoScaleR")
  print(version_info)'
```

> [!NOTE]
> La función [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) solo se puede ejecutar en el equipo local. La función no puede devolver las rutas de acceso de la biblioteca para las conexiones remotas.

## <a name="default-r-packages"></a>Paquetes de R predeterminados

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

Los siguientes paquetes de R se instalan con SQL Server R Services.

|. | `Version` | Descripción |
|---------|---------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | Se usa para contextos de cálculo remotos, streaming, ejecución en paralelo de funciones RX para la importación y transformación de datos, modelado, visualización y análisis. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | Se usa para incluir scripts de R en procedimientos almacenados. |

::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"

Los siguientes paquetes de R se instalan con SQL Server Machine Learning Services al seleccionar la característica de R durante la instalación.

|. | `Version` | Descripción |
|---------|---------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 9,2 | Se usa para contextos de cálculo remotos, streaming, ejecución en paralelo de funciones RX para la importación y transformación de datos, modelado, visualización y análisis. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 9,2 | Se usa para incluir scripts de R en procedimientos almacenados. |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| 9,2 | Agrega algoritmos de aprendizaje automático en R. | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 9,2 | Se utiliza para escribir instrucciones MDX en R. |

::: moniker-end

### <a name="component-upgrades"></a>Actualizaciones de componentes

De forma predeterminada, los paquetes de R se actualizan a través de los Service Pack y las actualizaciones acumulativas. Los paquetes adicionales y las actualizaciones de versión completa de los componentes principales de R solo son posibles a través de las actualizaciones de productos o mediante el enlace de la compatibilidad de R con Microsoft Machine Learning Server.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Además, puede agregar paquetes MicrosoftML y olapr a una instancia de SQL Server a través de una actualización de componente.
::: moniker-end

Para obtener más información, consulte [actualización de los componentes de R y Python en SQL Server](../install/upgrade-r-and-python.md).

## <a name="default-open-source-r-packages"></a>Paquetes de R de código abierto predeterminados

La compatibilidad con r incluye código abierto para que pueda llamar a las funciones base de R e instalar paquetes de código abierto y de terceros adicionales. La compatibilidad con el lenguaje R incluye funcionalidades básicas como **base**, **estadísticas**, **utilidades**y otras. Una instalación base de R también incluye numerosos conjuntos de datos de ejemplo y herramientas de R estándar como **RGui** (un editor interactivo ligero) y **RTerm** (un símbolo del sistema de r).

La distribución de R de código abierto incluida en la instalación es [Microsoft R Open (MRO)](https://mran.microsoft.com/open). MRO agrega valor a base R mediante la inclusión de paquetes de código abierto adicionales, como la [biblioteca de kernel de matemáticas de Intel](https://en.wikipedia.org/wiki/Math_Kernel_Library).

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
La versión de R que proporciona MRO mediante SQL Server R Services el programa de instalación es 3.2.2.
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
La versión de R proporcionada por MRO mediante SQL Server Machine Learning Services configuración es 3.3.3.
::: moniker-end

> [!IMPORTANT]
> Nunca debe sobrescribir manualmente la versión de R instalada SQL Server el programa de instalación con las versiones más recientes en la Web. Los paquetes de Microsoft R se basan en versiones específicas de R. la modificación de la instalación podría desestabilizarla.

## <a name="list-all-installed-r-packages"></a>Enumerar todos los paquetes de R instalados

En el ejemplo siguiente se usa la `installed.packages()` función de [!INCLUDE[tsql](../../includes/tsql-md.md)] r en un procedimiento almacenado para mostrar una lista de los paquetes de r que se han instalado en la biblioteca R_SERVICES para la instancia actual de SQL. Este script devuelve los campos de nombre y versión del paquete en el archivo de descripción.

```sql
EXECUTE sp_execute_external_script
  @language=N'R',
@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
Name <- packagematrix[,1];
Version <- packagematrix[,3];
OutputDataSet <- data.frame(Name, Version);',
@input_data_1 = N'
  '
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

Para obtener más información acerca de los campos opcionales y predeterminados para el campo de [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)Descripción del paquete de R, vea.

## <a name="find-a-single-r-package"></a>Buscar un único paquete de R

Si ha instalado un paquete de R y desea asegurarse de que está disponible para una instancia de SQL Server determinada, puede ejecutar un procedimiento almacenado para cargar el paquete y devolver los mensajes.

Por ejemplo, la siguiente instrucción busca y carga el paquete de [adherencia](https://cran.r-project.org/web/packages/glue/) , si está disponible.
Si no se puede encontrar o cargar el paquete, se obtiene un error que contiene el texto "no hay ningún paquete llamado ' glue '".

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("glue")'
GO
```

Para obtener más información acerca del paquete, vea `packageDescription`.
La siguiente instrucción devuelve información del paquete **glue** .

```sql
EXECUTE sp_execute_external_script
  @language = N'R',
  @script = N'
print(packageDescription("glue"))
  '
```

## <a name="next-steps"></a>Pasos siguientes

+ [Instalación de paquetes de R adicionales](../r/install-additional-r-packages-on-sql-server.md)
+ [Obtener información de paquete de Python](python-package-information.md)
+ [Instalación de paquetes de Python adicionales](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriales de R y Python](../tutorials/machine-learning-services-tutorials.md)
