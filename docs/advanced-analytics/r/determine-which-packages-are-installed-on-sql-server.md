---
title: Obtener información de paquete de R y Python - SQL Server Machine Learning Services
description: Determinar la versión del paquete de R y Python, comprobar la instalación y obtener una lista de paquetes instalados en SQL Server R Services o Machine Learning Services.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/08/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 3e7dd580cd7d03235be704a7c46e5171a6526ae8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62506220"
---
#  <a name="get-r-and-python-package-information"></a>Obtener información de paquete de R y Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

A veces, cuando se trabaja con varios entornos o las instalaciones de R o Python, debe comprobar que el código que se está ejecutando es usar el entorno esperado de Python o el área de trabajo correcta para R. Por ejemplo, si ha actualizado los componentes a través de aprendizaje automático [enlace](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md), podría ser la ruta de acceso a la biblioteca de R en una carpeta diferente que el valor predeterminado. Además, si instala R Client o una instancia de servidor independiente, podría tener varias bibliotecas de R en el equipo.

Ejemplos de script de R y Python en este artículo muestran cómo obtener la ruta de acceso y la versión de los paquetes utilizados por SQL Server.

## <a name="get-the-r-library-location"></a>Obtener la ubicación de la biblioteca de R

Para cualquier versión de SQL Server, ejecute la siguiente instrucción para comprobar la [biblioteca de paquetes de R predeterminada](installing-and-managing-r-packages.md) para la instancia actual:

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

Si lo desea, puede usar [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) en las versiones más recientes de RevoScaleR en Machine Learning Services de SQL Server 2017 o [R Services actualizado R para al menos RevoScaleR 9.0.1](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md). Este procedimiento almacenado devuelve la ruta de acceso de la biblioteca de la instancia y la versión de RevoScaleR utilizado por SQL Server:

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
> El [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) función se puede ejecutar solo en el equipo local. La función no puede devolver las rutas de acceso de biblioteca para las conexiones remotas.

**Resultado**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.3.0'
```

## <a name="get-the-python-library-location"></a>Obtener la ubicación de la biblioteca de Python

Para **Python** en SQL Server 2017, ejecute la siguiente instrucción para comprobar que la biblioteca predeterminada para la instancia actual. En este ejemplo devuelve la lista de carpetas incluidas en la versión de Python `sys.path` variable. La lista incluye el directorio actual y la ruta de acceso de la biblioteca estándar.

```sql
EXECUTE sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

**Resultado**

```text
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\python35.zip
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\DLLs
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\Sphinx-1.5.4-py3.5.egg
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\win32
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\win32\lib
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\Pythonwin
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\setuptools-27.2.0-py3.5.egg
```

Para obtener más información acerca de la variable `sys.path` y cómo se usa para establecer la ruta de búsqueda del intérprete de módulos, vea el [documentación de Python](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)

## <a name="list-all-packages"></a>Enumerar todos los paquetes

Hay varias formas que puede obtener una lista completa de los paquetes instalados actualmente. Una ventaja de ejecutar comandos de la lista de paquetes desde sp_execute_external_script es que se garantiza que para obtener los paquetes instalados en la biblioteca de la instancia.

### <a name="r"></a>R

En el ejemplo siguiente se usa la función de R `installed.packages()` en un [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimiento almacenado para obtener una matriz de los paquetes que se han instalado en la biblioteca R_SERVICES para la instancia actual. Este script devuelve los campos de nombre y la versión del paquete en el archivo de descripción, se devuelve solo el nombre.

```sql
EXECUTE sp_execute_external_script
  @language=N'R',
  @script = N'str(OutputDataSet);
  packagematrix <- installed.packages();
  Name <- packagematrix[,1];
  Version <- packagematrix[,3];
  OutputDataSet <- data.frame(Name, Version);',
  @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

Para obtener más información sobre el elemento opcional y los campos predeterminados para el campo de descripción del paquete de R, consulte [ https://cran.r-project.org ](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file).

### <a name="python"></a>Python

El `pip` módulo se instala de forma predeterminada y es compatible con muchas operaciones para los paquetes de anuncio instalado, además de los admitidos por el estándar de Python. Puede ejecutar `pip` desde un Python símbolo del sistema, por supuesto, pero también puede llamar a algunas funciones de pip de `sp_execute_external_script`.

```sql
EXECUTE sp_execute_external_script 
  @language = N'Python', 
  @script = N'
  import pip
  import pandas as pd
  installed_packages = pip.get_installed_distributions()
  installed_packages_list = sorted(["%s==%s" % (i.key, i.version)
     for i in installed_packages])
  df = pd.DataFrame(installed_packages_list)
  OutputDataSet = df'
WITH RESULT SETS (( PackageVersion nvarchar (150) ))
```

Cuando se ejecuta `pip` desde la línea de comandos, existen otras muchas funciones útiles: `pip list` Obtiene todos los paquetes que están instalados, mientras que `pip freeze` enumera los paquetes instalados por `pip`y no se muestran los paquetes de pip de sí mismo depende. También puede usar `pip freeze` para generar un archivo de dependencia.

## <a name="find-a-single-package"></a>Buscar un único paquete

Si ha instalado un paquete y desea asegurarse de que está disponible para una determinada instancia de SQL Server, puede ejecutar la siguiente llamada de procedimiento almacenado para cargar el paquete y devolver solo los mensajes.

### <a name="r"></a>R

En este ejemplo se busca y carga la biblioteca de RevoScaleR, si está disponible.

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("RevoScaleR")'
GO
```

+ Si se encuentra el paquete, se devuelve un mensaje: "Comandos completados correctamente."

+ Si el paquete no se encuentra o se ha cargado, se produce un error que contiene el texto: "no hay ningún paquete llamado 'MissingPackageName'"

### <a name="python"></a>Python

La comprobación equivalente para Python se puede realizar desde la versión de Python de shell, mediante `conda` o `pip` comandos. Como alternativa, puede ejecutar esta instrucción en un procedimiento almacenado:

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
  import pip
  import pkg_resources
  pckg_name = "revoscalepy"
  pckgs = pandas.DataFrame([(i.key) for i in pip.get_installed_distributions()], columns = ["key"])
  installed_pckg = pckgs.query(''key == @pckg_name'')
  print("Package", pckg_name, "is", "not" if installed_pckg.empty else "", "installed")'
```

<a name="get-package-vers"></a>

## <a name="get-package-version"></a>Obtener la versión del paquete

Puede obtener R y Python empaquetar información de versión con Management Studio.

### <a name="r-package-version"></a>Versión del paquete de R

Esta instrucción devuelve la versión del paquete RevoScaleR y la versión de R base.

```sql
EXECUTE sp_execute_external_script
  @language = N'R',
  @script = N'
print(packageDescription("RevoScaleR"))
print(packageDescription("base"))
'
```

### <a name="python-package-version"></a>Versión del paquete de Python

Esta instrucción devuelve la versión del paquete revoscalepy y la versión de Python.

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

+ [Instalación de paquetes de R adicionales](install-additional-r-packages-on-sql-server.md)
+ [Instalación de paquetes de Python adicionales](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriales, muestras y soluciones](../tutorials/machine-learning-services-tutorials.md)