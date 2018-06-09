---
title: Obtener información de paquete de R y Python en aprendizaje automático de SQL Server | Documentos de Microsoft
description: Determinar la versión de paquete de R y Python, comprobar la instalación y obtener una lista de paquetes instalados en SQL Server R Services o servicios de aprendizaje de máquina.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 85ea4658ca8b60fc24d7e4f7849de1655eab6082
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34707893"
---
#  <a name="get-r-and-python-package-information"></a>Obtener información de paquete de R y Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Cuando se trabaja con varios entornos o las instalaciones de R o Python, en ocasiones necesitará comprobar que el código que se está ejecutando está utilizando el entorno esperado para el área de trabajo correcto o Python para R. Por ejemplo, si ha actualizado los componentes a través de aprendizaje automático [enlace](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md), podría ser la ruta de acceso a la biblioteca de R en una carpeta diferente que el valor predeterminado. Además, si instala el cliente de R o una instancia del servidor independiente, podría tener varias bibliotecas de R en el equipo.

Ejemplos de scripts de R y Python en este artículo muestran cómo obtener la ruta de acceso y la versión de los paquetes utilizados por SQL Server.

## <a name="get-the-r-library-location"></a>Obtener la ubicación de la biblioteca de R

Para cualquier versión de SQL Server, ejecute la siguiente instrucción para comprobar la [biblioteca de paquete predeterminado R](installing-and-managing-r-packages.md) de la instancia actual:

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

Si lo desea, puede usar [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) en versiones más recientes de RevoScaleR en servicios de aprendizaje de SQL Server de 2017 máquinas o [R Services ugpraded R para al menos RevoScaleR 9.0.1](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md). Este procedimiento almacenado devuelve la ruta de acceso de la biblioteca de la instancia y la versión de RevoScaleR utilizado por SQL Server:

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

Para **Python** en SQL Server 2017, ejecute la siguiente instrucción para comprobar que la biblioteca predeterminada para la instancia actual. Este ejemplo devuelve la lista de carpetas incluidas en la versión de Python `sys.path` variable. La lista incluye el directorio actual y la ruta de acceso de la biblioteca estándar.

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

Para obtener más información acerca de la variable `sys.path` y cómo se utiliza para establecer la ruta de búsqueda del intérprete de módulos, vea el [documentación de Python](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)

## <a name="list-all-packages"></a>Enumerar todos los paquetes

Hay varias maneras en que puede obtener una lista completa de los paquetes instalados actualmente. Una de las ventajas de ejecutar comandos de la lista de paquetes de sp_execute_external_script es que se garantiza para obtener los paquetes instalados en la biblioteca de la instancia.

### <a name="r"></a>R

En el ejemplo siguiente se utiliza la función de R `installed.packages()` en un [!INCLUDE [tsql](..\..\includes\tsql-md.md)] procedimiento almacenado para obtener una matriz de los paquetes que se han instalado en la biblioteca R_SERVICES para la instancia actual. Esta secuencia de comandos devuelve los campos de nombre y la versión de paquete en el archivo de descripción, se devuelve solo el nombre.

```SQL
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

Para obtener más información sobre la parte opcional y los campos predeterminados para el campo de descripción del paquete de R, consulte [ https://cran.r-project.org ](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file).

### <a name="python"></a>Python

El `pip` módulo está instalado de forma predeterminada y es compatible con muchas operaciones para los paquetes de anuncio instalado, además de aquellos admitidos por Python estándar. Puede ejecutar `pip` desde un Python símbolo del sistema, por supuesto, pero también puede llamar a algunas funciones de pip de `sp_execute_external_script`.

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

Cuando se ejecuta `pip` desde la línea de comandos, hay muchas otras funciones útiles: `pip list` Obtiene todos los paquetes que están instalados, mientras que `pip freeze` enumera los paquetes instalados por `pip`y no se muestran los paquetes que pip propio depende. También puede usar `pip freeze` para generar un archivo de dependencia.

## <a name="find-a-single-package"></a>Buscar un único paquete

Si ha instalado un paquete y para asegurarse de que está disponible para una determinada instancia de SQL Server, puede ejecutar la siguiente llamada de procedimiento almacenado para cargar el paquete y devolver solo los mensajes.

### <a name="r"></a>R

Este ejemplo busca y carga la biblioteca RevoScaleR, si está disponible.

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("RevoScaleR")'
GO
```

+ Si se encuentra el paquete, se devuelve un mensaje: "Comandos completados correctamente."

+ Si el paquete no se encuentra o cargado, obtendrá un error que contiene el texto: "no hay ningún paquete denominado 'MissingPackageName'"

### <a name="python"></a>Python

Se puede realizar la comprobación equivalente de Python desde la versión de Python de shell, con `conda` o `pip` comandos. O bien, ejecute esta instrucción en un procedimiento almacenado:

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

## <a name="get-package-information-in-r-and-python-tools"></a>Obtener información de paquete en herramientas de R y Python

Todas las instrucciones anteriores se supone que está utilizando una herramienta de SQL Server como Management Studio (SSMS). Si prefiere usar herramientas de R y Python, las instrucciones siguientes explican cómo obtener información de la biblioteca y el paquete desde una línea de comandos de R o Python.

### <a name="r-commands"></a>Comandos de R

La biblioteca de instancia para R es \Program Server\MSSQL14 de SQL. MSSQLSERVER\R_SERVICES\library.

Iniciar las herramientas estándar de R desde estas ubicaciones para asegurarse de que se usan los paquetes de la biblioteca de instancia:

+ \MSSQL14. MSSQLSERVER\R_SERVICES\bin\R.exe para un símbolo del sistema de R
+ \MSSQL14. MSSQLSERVER\R_SERVICES\bin\x64\Rgui.exe para una aplicación de consola de R

Puede usar comandos de R estándar o comandos de RevoScaleR para obtener información del paquete. El paquete RevoScaleR se carga automáticamente. 

Devolver información del paquete RevoScaleR:

    > print(Revo.version)

Devolver una lista de todos los paquetes instalados:

    > installed.packages()

Devolver la versión de R:

    > packageDescription("base")

### <a name="python-commands"></a>Comandos de Python

Compatibilidad con Python solo está 2017 de SQL Server. La biblioteca de instancia para Python es \Program Server\MSSQL14 de SQL. MSSQLSERVER\PYTHON_SERVICES\.

Abra la ventana de comandos de Python desde esta ubicación para asegurarse de que se usan los paquetes de la biblioteca de instancia:

+ \MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Python.exe

Abrir la Ayuda interactiva:

    > help()

Escriba un nombre de módulo en el símbolo del sistema de ayuda para obtener el contenido del paquete, la versión y la ubicación de archivo:

    help> revoscalepy

<a name="pip-conda"></a>

### <a name="python-package-managers-pip-and-conda"></a>Administradores (Pip y Conda) del paquete de Python

Anaconda incluye herramientas de Python para administrar paquetes. En el valor predeterminado es instancia, Pip, Conda y otras herramientas pueden encontrarse en \Program Server\MSSQL14 de SQL. MSSQLSERVER\PYTHON_SERVICES\Scripts.

El programa de instalación de SQL Server no agrega Pip o Conda mantener ejecutables no sean esenciales fuera de la ruta de acceso a la ruta de acceso del sistema y en una instancia de SQL Server de producción, es una práctica recomendada. Sin embargo, para entornos de desarrollo y prueba, puede agregar la carpeta de Scripts a la variable de entorno de ruta de acceso de sistema para ejecutar Pip y Conda en el comando desde cualquier ubicación.

1. Vaya a C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Scripts

1. Haga clic en **conda.exe** > **ejecutar como administrador**y escriba `conda list` para devolver una lista de paquetes instalados en el entorno actual.

1. Del mismo modo, haga clic en **pip.exe** > **ejecutar como administrador**y escriba `pip list` para devolver la misma información. 


## <a name="next-steps"></a>Pasos siguientes

+ [Instalación de paquetes de R adicionales](install-additional-r-packages-on-sql-server.md)
+ [Instalación de paquetes de Python adicionales](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriales, muestras y soluciones](../tutorials/machine-learning-services-tutorials.md)