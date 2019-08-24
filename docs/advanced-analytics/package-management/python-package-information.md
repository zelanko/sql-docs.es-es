---
title: Obtención de información de paquetes de Python
description: Aprenda a obtener información acerca de los paquetes de Python instalados, incluidas las versiones y las ubicaciones de instalación, en SQL Server Machine Learning Services.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/22/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1aa12da4a138ea8f292fa8b64db00456d3c35fe3
ms.sourcegitcommit: 01c8df19cdf0670c02c645ac7d8cc9720c5db084
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000448"
---
# <a name="get-python-package-information"></a>Obtención de información de paquetes de Python

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se describe cómo obtener información acerca de los paquetes de Python instalados, incluidas las versiones y las ubicaciones de instalación, en SQL Server Machine Learning Services. Ejemplos de scripts de Python muestran cómo Mostrar información de paquetes como la ruta de instalación y la versión.

## <a name="default-python-library-location"></a>Ubicación predeterminada de la biblioteca de Python

Al instalar machine learning con SQL Server, se crea una biblioteca de paquetes única en el nivel de instancia para cada idioma que se instala. En Windows, la biblioteca de instancias es una carpeta protegida registrada con SQL Server.

Todo el script o el código que se ejecuta en la base de datos en SQL Server deben cargar funciones desde la biblioteca de instancias. SQL Server no puede tener acceso a los paquetes instalados en otras bibliotecas. Esto se aplica también a los clientes remotos: cualquier código de Python que se ejecute en el contexto de proceso del servidor solo puede usar paquetes instalados en la biblioteca de instancias.
Para proteger los recursos del servidor, la biblioteca de instancia predeterminada solo puede ser modificada por un administrador del equipo.

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
La ruta de acceso predeterminada de los archivos binarios de Python es:

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`
::: moniker-end

::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
La ruta de acceso predeterminada de los archivos binarios de Python es:

`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\PYTHON_SERVICES`
::: moniker-end

Se asume la instancia predeterminada de SQL, MSSQLSERVER. Si SQL Server se instala como una instancia con nombre definida por el usuario, se utiliza en su lugar el nombre especificado.

Ejecute la siguiente instrucción para comprobar la biblioteca predeterminada de la instancia actual. En este ejemplo se devuelve la lista de carpetas incluida en `sys.path` la variable de Python. La lista incluye el directorio actual y la ruta de acceso de la biblioteca estándar.

```sql
EXECUTE sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

Para obtener más información sobre la `sys.path` variable y cómo se usa para establecer la ruta de acceso de búsqueda del intérprete para los módulos, vea [la ruta de búsqueda del módulo](https://docs.python.org/2/tutorial/modules.html#the-module-search-path).

## <a name="default-python-packages"></a>Paquetes de Python predeterminados

Los siguientes paquetes de Python se instalan con SQL Server Machine Learning Services al seleccionar la característica de Python durante la instalación.

| . | `Version` |  Descripción |
| ---------|---------|--------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9,2 | Se usa para contextos de cálculo remotos, streaming, ejecución en paralelo de funciones RX para la importación y transformación de datos, modelado, visualización y análisis. |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9,2 | Agrega algoritmos de aprendizaje automático en Python. |

### <a name="component-upgrades"></a>Actualizaciones de componentes

De forma predeterminada, los paquetes de Python se actualizan a través de los Service Pack y las actualizaciones acumulativas. Los paquetes adicionales y las actualizaciones de versión completa de los componentes básicos de Python solo son posibles a través de las actualizaciones del producto o mediante el enlace de la compatibilidad de Python con Microsoft Machine Learning Server.

Para obtener más información, consulte [actualización de los componentes de R y Python en SQL Server](../install/upgrade-r-and-python.md).

## <a name="default-open-source-python-packages"></a>Paquetes de Python de código abierto predeterminados

Al seleccionar la opción de idioma de Python durante la instalación, se instala Anaconda 4,2 Distribution (en Python 3,5). Además de las bibliotecas de código de Python, la instalación estándar incluye datos de ejemplo, pruebas unitarias y scripts de ejemplo.

> [!IMPORTANT]
> Nunca debe sobrescribir manualmente la versión de Python instalada por SQL Server el programa de instalación con las versiones más recientes en la Web. Los paquetes de Microsoft Python se basan en versiones específicas de anaconda. La modificación de la instalación podría desestabilizarla.

## <a name="list-all-installed-python-packages"></a>Enumerar todos los paquetes de Python instalados

En el siguiente script de ejemplo se muestra una lista de los paquetes instalados y sus versiones.

```sql
EXECUTE sp_execute_external_script 
  @language = N'Python', 
  @script = N'
import pkg_resources
import pandas as pd
installed_packages = pkg_resources.working_set
installed_packages_list = sorted(["%s==%s" % (i.key, i.version) for i in installed_packages])
df = pd.DataFrame(installed_packages_list)
OutputDataSet = df
  '
WITH RESULT SETS (( PackageVersion nvarchar (150) ))
```

## <a name="find-a-single-python-package"></a>Buscar un solo paquete de Python

Si ha instalado un paquete de Python y desea asegurarse de que está disponible para una instancia de SQL Server determinada, puede ejecutar un procedimiento almacenado para cargar el paquete y devolver los mensajes.

Por ejemplo, el código siguiente busca el `scikit-learn` paquete.
Si se encuentra el paquete, el código devuelve el mensaje "el paquete scikit-Learn está instalado".

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import pkg_resources
pckg_name = "scikit-learn"
pckgs = pandas.DataFrame([(i.key) for i in pkg_resources.working_set], columns = ["key"])
installed_pckg = pckgs.query(''key == @pckg_name'')
print("Package", pckg_name, "is", "not" if installed_pckg.empty else "", "installed")
  '
```

<a name="get-package-vers"></a>

En el ejemplo siguiente se devuelven las versiones del paquete revoscalepy y de Python.

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import revoscalepy
import sys
print(revoscalepy.__version__)
print(sys.version)
  '
```

## <a name="next-steps"></a>Pasos siguientes

+ [Instalación de paquetes de Python adicionales](../python/install-additional-python-packages-on-sql-server.md)
+ [Obtener información de paquete de R](r-package-information.md)
+ [Instalación de paquetes de R adicionales](../r/install-additional-r-packages-on-sql-server.md)
+ [Tutoriales de R y Python](../tutorials/machine-learning-services-tutorials.md)
