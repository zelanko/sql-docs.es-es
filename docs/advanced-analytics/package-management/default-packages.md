---
title: Obtener información de paquetes de R y Python
description: Determinar la versión del paquete de R y Python, comprobar la instalación y obtener una lista de los paquetes instalados en SQL Server R Services o Machine Learning Services.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ff4d0839cfdf24b1b43fe9d5a371092713bc63cf
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715794"
---
#  <a name="get-r-and-python-package-information"></a>Obtener información de paquetes de R y Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A veces, al trabajar con varios entornos o instalaciones de R o Python, debe comprobar que el código que está ejecutando usa el entorno esperado para Python o el área de trabajo correcta para R. Por ejemplo, si ha [actualizado R o Python](../install/upgrade-r-and-python.md), la ruta de acceso a la biblioteca de r podría estar en una carpeta distinta a la predeterminada. Además, si instala R Client o una instancia del servidor independiente, es posible que tenga varias bibliotecas de R en el equipo.

Los ejemplos de scripts de R y Python de este artículo muestran cómo obtener la ruta de acceso y la versión de los paquetes usados por SQL Server.

## <a name="get-the-r-library-location"></a>Obtener la ubicación de la biblioteca de R

Para cualquier versión de SQL Server, ejecute la siguiente instrucción para comprobar la biblioteca de paquetes de R predeterminada para la instancia actual:

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

Opcionalmente, puede usar [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) en las versiones más recientes de RevoScaleR en SQL Server Machine Learning Services o [R Services actualizado r al menos RevoScaleR 9.0.1](../install/upgrade-r-and-python.md). Este procedimiento almacenado devuelve la ruta de acceso de la biblioteca de instancias y la versión de RevoScaleR que usa SQL Server:

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

**Resultado**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.3.0'
```

## <a name="get-the-python-library-location"></a>Obtener la ubicación de la biblioteca de Python

Para **Python**, ejecute la siguiente instrucción para comprobar la biblioteca predeterminada de la instancia actual. En este ejemplo se devuelve la lista de carpetas incluida en `sys.path` la variable de Python. La lista incluye el directorio actual y la ruta de acceso de la biblioteca estándar.

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

Para obtener más información sobre la `sys.path` variable y cómo se usa para establecer la ruta de acceso de búsqueda del intérprete para los módulos, consulte la [documentación de Python](https://docs.python.org/2/tutorial/modules.html#the-module-search-path) .

## <a name="list-all-packages"></a>Enumerar todos los paquetes

Hay varias maneras de obtener una lista completa de los paquetes instalados actualmente. Una ventaja de ejecutar comandos de lista de paquetes desde sp_execute_external_script es que se garantiza que los paquetes se instalan en la biblioteca de instancias.

### <a name="r"></a>R

En el ejemplo siguiente se usa la `installed.packages()` función de [!INCLUDE[tsql](../../includes/tsql-md.md)] R en un procedimiento almacenado para obtener una matriz de paquetes que se han instalado en la biblioteca R_SERVICES para la instancia actual. Este script devuelve los campos de nombre y versión del paquete en el archivo de descripción, solo se devuelve el nombre.

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

Para obtener más información acerca de los campos opcionales y predeterminados para el campo de [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)Descripción del paquete de R, vea.

### <a name="python"></a>Python

El `pip` módulo se instala de manera predeterminada y admite muchas operaciones para enumerar los paquetes instalados, además de los admitidos por Python estándar. Puede ejecutar `pip` desde un símbolo del sistema de Python, por supuesto, pero también puede llamar a algunas funciones de `sp_execute_external_script`PIP desde.

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

Cuando se `pip` ejecuta desde la línea de comandos, hay muchas otras funciones útiles `pip list` : obtiene todos los paquetes que se instalan, mientras que `pip freeze` enumera `pip`los paquetes instalados por y no muestra los paquetes que se encuentran en el propio PIP. depende de. También puede usar `pip freeze` para generar un archivo de dependencia.

## <a name="find-a-single-package"></a>Buscar un único paquete

Si ha instalado un paquete y desea asegurarse de que está disponible para una instancia de SQL Server determinada, puede ejecutar la siguiente llamada al procedimiento almacenado para cargar el paquete y devolver solo los mensajes.

### <a name="r"></a>R

En este ejemplo se busca y se carga la biblioteca RevoScaleR, si está disponible.

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("RevoScaleR")'
GO
```

+ Si se encuentra el paquete, se devuelve un mensaje: "Comandos completados correctamente".

+ Si no se puede encontrar o cargar el paquete, obtendrá un error que contiene el texto: "no hay ningún paquete llamado ' MissingPackageName '"

### <a name="python"></a>Python

La comprobación equivalente de Python se puede realizar desde el shell de Python, `conda` mediante `pip` los comandos o. Como alternativa, ejecute esta instrucción en un procedimiento almacenado:

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

## <a name="get-package-version"></a>Obtener versión del paquete

Puede obtener información de versión del paquete de R y Python mediante Management Studio.

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

+ [Instalación de paquetes de R adicionales](../r/install-additional-r-packages-on-sql-server.md)
+ [Instalación de paquetes de Python adicionales](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriales, muestras y soluciones](../tutorials/machine-learning-services-tutorials.md)