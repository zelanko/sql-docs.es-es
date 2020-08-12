---
title: Obtención de información de paquetes de R
description: Aprenda a obtener información sobre los paquetes de R instalados en SQL Server Machine Learning Services y SQL Server R Services.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/27/2020
ms.topic: how-to
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 877728812d36a7d4db8370254c0fdccbe1011350
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723941"
---
# <a name="get-r-package-information"></a>Obtención de información de paquetes de R

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
En este artículo se describe cómo obtener información sobre los paquetes de R instalados en [Machine Learning Services en SQL Server](../sql-server-machine-learning-services.md) y en [Clústeres de macrodatos](../../big-data-cluster/machine-learning-services.md). Los scripts de R de ejemplo muestran cómo mostrar información de paquetes, como la ruta de instalación y la versión.
::: moniker-end
::: moniker range="<=sql-server-2017||=sqlallproducts-allversions"
En este artículo se describe cómo obtener información sobre los paquetes de R instalados en [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md). Los scripts de R de ejemplo muestran cómo mostrar información de paquetes, como la ruta de instalación y la versión.
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
En este artículo se describe cómo obtener información sobre los paquetes de R instalados en [Machine Learning Services en Azure SQL Managed Instance](/azure/azure-sql/managed-instance/machine-learning-services-overview). Los scripts de R de ejemplo muestran cómo mostrar información de paquetes, como la ruta de instalación y la versión.
::: moniker-end

## <a name="default-r-library-location"></a>Ubicación predeterminada de las bibliotecas de R

Al instalar Machine Learning con SQL Server, se crea una biblioteca de paquetes en el nivel de instancia para cada idioma que se instale. En Windows, la biblioteca de instancias es una carpeta protegida que está registrada en SQL Server.

Todo el script que se ejecuta en la base de datos en SQL Server debe cargar funciones desde la biblioteca de instancias. SQL Server no puede obtener acceso a los paquetes instalados en otras bibliotecas. También se aplica a los clientes remotos: cualquier script de R que se ejecute en el contexto del proceso del servidor solo puede usar paquetes instalados en la biblioteca de instancias.
Para proteger los recursos del servidor, la biblioteca de instancias predeterminadas solo la puede modificar un administrador del equipo.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
La ruta de acceso predeterminada de los archivos binarios de R es:

`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`

Se da por sentado que la instancia predeterminada de SQL es MSSQLSERVER. Si se instala SQL Server como instancia con nombre definida por el usuario, se usará el nombre especificado.
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
La ruta de acceso predeterminada de los archivos binarios de R es:

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library`

Se da por sentado que la instancia predeterminada de SQL es MSSQLSERVER. Si se instala SQL Server como instancia con nombre definida por el usuario, se usará el nombre especificado.
::: moniker-end

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
La ruta de acceso predeterminada de los archivos binarios de R es:

`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES\library`

Se da por sentado que la instancia predeterminada de SQL es MSSQLSERVER. Si se instala SQL Server como instancia con nombre definida por el usuario, se usará el nombre especificado.
::: moniker-end

Ejecute la siguiente instrucción para comprobar la biblioteca de paquetes de R predeterminada de la instancia actual:

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

## <a name="default-microsoft-r-packages"></a>Paquetes predeterminados de R en Microsoft

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

Los siguientes paquetes de R de Microsoft se instalan con SQL Server R Services.

|Paquetes | Versión | Descripción |
|---------|---------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | Se usa para los contextos de procesos remotos, streaming, ejecución en paralelo de funciones rx para la importación y transformación de datos, modelado, visualización y análisis. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 1.0.0 | Se usa para incluir scripts de R en procedimientos almacenados. |

::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"

Los siguientes paquetes de R de Microsoft se instalan con SQL Server Machine Learning Services al seleccionar la característica de R durante la instalación.

|Paquetes | Versión | Descripción |
|---------|---------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 9.2 | Se usa para los contextos de procesos remotos, streaming, ejecución en paralelo de funciones rx para la importación y transformación de datos, modelado, visualización y análisis. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 1.0.0 | Se usa para incluir scripts de R en procedimientos almacenados. |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| 1.4.0 | Agrega algoritmos de aprendizaje automático en R. | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1.0.0 | Se utiliza para escribir instrucciones MDX en R. |

::: moniker-end

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions"

Los siguientes paquetes de R de Microsoft se instalan con SQL Server Machine Learning Services al seleccionar la característica de R durante la instalación.

|Paquetes | Versión | Descripción |
|---------|---------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 9.4.7 | Se usa para los contextos de procesos remotos, streaming, ejecución en paralelo de funciones rx para la importación y transformación de datos, modelado, visualización y análisis. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 1.0.0 | Se usa para incluir scripts de R en procedimientos almacenados. |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| 9.4.7 | Agrega algoritmos de aprendizaje automático en R. |
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1.0.0 | Se utiliza para escribir instrucciones MDX en R. |

::: moniker-end

### <a name="component-upgrades"></a>Actualizaciones de componentes

De forma predeterminada, los paquetes de R se actualizan mediante Service Packs y actualizaciones acumulativas. Los paquetes adicionales y las actualizaciones de versión completa de los componentes básicos de R solo son posibles mediante las actualizaciones de producto o enlazando la compatibilidad de R con Microsoft Machine Learning Server.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Además, puede agregar paquetes de MicrosoftML y olapR a una instancia de SQL Server a través de una actualización de componente.
::: moniker-end

Para obtener más información, consulte [Actualización de componentes de R y Python en SQL Server](../install/upgrade-r-and-python.md).

## <a name="default-open-source-r-packages"></a>Paquetes de código abierto predeterminados de R

La compatibilidad con R incluye R de código abierto para que pueda llamar a las funciones base de R e instalar paquetes de código abierto y de terceros adicionales. La compatibilidad con el lenguaje de R incluye funcionalidades básicas, como **base**, **stats**, **utils**, entre otras. Una instalación base de R también incluye numerosos conjuntos de datos de ejemplo y herramientas de R estándar, como **RGui** (un editor interactivo ligero) y **RTerm** (un símbolo del sistema de R).

La distribución de R de código abierto incluida en la instalación es [Microsoft R Open (MRO)](https://mran.microsoft.com/open). MRO agrega valor a R base mediante la inclusión de paquetes de código abierto adicionales, como la [biblioteca de kernels matemáticos de Intel](https://en.wikipedia.org/wiki/Math_Kernel_Library).

Para obtener información sobre la versión de R que se incluye con cada versión de SQL Server, consulte [Versiones de Python y R](../sql-server-machine-learning-services.md#versions).

> [!IMPORTANT]
> Nunca debe sobrescribir manualmente la versión de R instalada por el programa de instalación de SQL Server por versiones más recientes en la web. Los paquetes de Microsoft R se basan en versiones específicas de R. La modificación de la instalación podría desestabilizarla.

## <a name="list-all-installed-r-packages"></a>Visualización de todos los paquetes de R instalados

En el ejemplo siguiente se usa la función de R `installed.packages()` en un procedimiento almacenado [!INCLUDE[tsql](../../includes/tsql-md.md)] para mostrar una lista de paquetes de R que se han instalado en la biblioteca R_SERVICES para la instancia actual de SQL. Este script devuelve los campos de nombre y versión del paquete en el archivo DESCRIPTION.

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

Para obtener más información sobre los campos opcionales y predeterminados del archivo DESCRIPTION del paquete de R, consulte [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file).

## <a name="find-a-single-r-package"></a>Búsqueda de un paquete de R

Si ha instalado un paquete de R y quiere asegurarse de que está disponible para una instancia de SQL Server determinada, puede ejecutar un procedimiento almacenado para cargar el paquete y devolver los mensajes.

Por ejemplo, la siguiente instrucción busca y carga el paquete [glue](https://cran.r-project.org/web/packages/glue/), si está disponible.
Si no se puede encontrar o cargar el paquete, obtendrá un error.

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'
require("glue")
'
```

Para ver más información sobre el paquete, consulte `packageDescription`.
La siguiente instrucción devuelve información del paquete **MicrosoftML**.

```sql
EXECUTE sp_execute_external_script
  @language = N'R',
  @script = N'
print(packageDescription("MicrosoftML"))
'
```

## <a name="next-steps"></a>Pasos siguientes

::: moniker range="<=sql-server-2017||=sqlallproducts-allversions"
+ [Instalación de paquetes con herramientas de R](install-r-packages-standard-tools.md)
::: moniker-end
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions"
+ [Instalación de nuevos paquetes de R con sqlmlutils](install-additional-r-packages-on-sql-server.md)
::: moniker-end