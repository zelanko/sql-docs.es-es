---
title: Visualización de R o paquetes de Python instalados en SQL Server | Documentos de Microsoft
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7cea8b82337ca7d5b4cd17b1038a1eccc99370be
ms.sourcegitcommit: beaad940c348ab22d4b4a279ced3137ad30c658a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/20/2018
---
# <a name="viewing-r-or-python-packages-installed-on-sql-server"></a>Visualización de R o paquetes de Python instalados en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Si ha instalado varios entornos de Python, o usar varias herramientas de R, es fácil de instalar un paquete a la biblioteca incorrecta o el entorno y, a continuación, no pueda encontrarla más adelante. 

Este artículo proporciona algunas consultas que puede usar para determinar la versión actual y para enumerar los paquetes que están instalados en el entorno de SQL Server actual.

## <a name="verify-the-current-default-library"></a>Compruebe la biblioteca predeterminada actual

Para **R** en SQL Server, ejecute la siguiente instrucción para comprobar que la biblioteca predeterminada para la instancia actual:

```sql
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

Para **Python** en SQL Server, ejecute la siguiente instrucción para comprobar que la biblioteca predeterminada para la instancia actual:

```sql
EXEC sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

## <a name="generate-a-package-list-using-a-stored-procedure"></a>Generar una lista de paquetes mediante un procedimiento almacenado

Hay varias maneras en que puede obtener una lista completa de los paquetes instalados actualmente. Una de las ventajas de ejecutar comandos de la lista de paquetes de sp_execute_external_script es que se garantiza para obtener los paquetes instalados en la biblioteca de la instancia.

### <a name="r"></a>L

En el ejemplo siguiente se utiliza la función de R `installed.packages()` en un [!INCLUDE [tsql](..\..\includes\tsql-md.md)] procedimiento almacenado para obtener una matriz de los paquetes que se han instalado en la biblioteca R_SERVICES para la instancia actual. Para evitar el análisis de los campos del archivo de DESCRIPCIÓN, se devuelve solo el nombre.

```SQL
EXECUTE sp_execute_external_script
@language=N'R'
,@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
NameOnly <- packagematrix[,1];
OutputDataSet <- as.data.frame(NameOnly);'
, @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250) ))
```

Para obtener más información sobre la parte opcional y los campos predeterminados para el campo de descripción del paquete de R, consulte [ https://cran.r-project.org ](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file).

### <a name="python"></a>Python

El `pip` módulo está instalado de forma predeterminada y es compatible con muchas operaciones para los paquetes de anuncio instalado, además de aquellos admitidos por Python estándar. Puede ejecutar `pip` desde un Python símbolo del sistema, por supuesto, pero también puede llamar a algunas funciones de pip de `sp_execute_external_script`.

```sql
execute sp_execute_external_script 
@language = N'Python', 
@script = N'
import pip
import pandas as pd
installed_packages = pip.get_installed_distributions()
installed_packages_list = sorted(["%s==%s" % (i.key, i.version)
     for i in installed_packages])
df = pd.DataFrame(installed_packages_list)
OutputDataSet = df
'
WITH RESULT SETS (( PackageVersion nvarchar (150) ))
```

Cuando se ejecuta `pip` desde la línea de comandos, hay muchas otras funciones útiles: `pip list` Obtiene todos los paquetes que están instalados, mientras que `pip freeze` enumera los paquetes instalados por `pip`y no se muestran los paquetes que pip propio depende. También puede usar `pip freeze` para generar un archivo de dependencia.

## <a name="verify-whether-a-package-is-installed-with-an-instance"></a>Compruebe si se instala un paquete con una instancia

Si ha instalado un paquete y para asegurarse de que está disponible para una determinada instancia de SQL Server, puede ejecutar la siguiente llamada de procedimiento almacenado para cargar el paquete y devolver solo los mensajes.

### <a name="r"></a>L

Este ejemplo busca y carga la biblioteca RevoScaleR, si está disponible.

```sql
EXEC sp_execute_external_script  @language =N'R',
@script=N'require("RevoScaleR")'
GO
```

+ Si se encuentra el paquete, se devuelve un mensaje: "Comandos completados correctamente."

+ Si el paquete no se encuentra o cargado, obtendrá un error que contiene el texto: "no hay ningún paquete denominado 'MissingPackageName'"

### <a name="python"></a>Python

Se puede realizar la comprobación equivalente de Python desde la versión de Python de shell, con `conda` o `pip` comandos. O bien, ejecute esta instrucción en un procedimiento almacenado:

```sql
exec sp_execute_external_script
       @language = N'Python'
       , @script = N'
import pip
import pkg_resources
pckg_name = "revoscalepy"
pckgs = pandas.DataFrame([(i.key) for i in pip.get_installed_distributions()], columns = ["key"])
installed_pckg = pckgs.query(''key == @pckg_name'')
print("Package", pckg_name, "is", "not" if installed_pckg.empty else "", "installed")'
```

## <a name="view-installed-packages-using-a-utility-or-ide"></a>Ver los paquetes instalados con una utilidad o IDE

Herramientas de desarrollo mayoría proporcionan un Examinador de objetos o una lista de paquetes que están instalados o cargados en el área de trabajo actual o el entorno. En esta sección se proporciona algunas sugerencias cortos para usar las herramientas de R o Python populares.

### <a name="r-tools"></a>Herramientas de R

Hay varias maneras de obtener una lista de paquetes instalados o cargados con utilidades de R. 

+ Desde una utilidad de R local, use una función de R base, como `installed.packages()`, que se incluye en el `utils` paquete. Para obtener una lista que es precisa para una instancia, debe especificar explícitamente la ruta de biblioteca o utilizar las herramientas de R asociadas a la biblioteca de la instancia.

### <a name="python-tools"></a>Herramientas de Python

Extensiones de Python para Visual Studio facilitan muy ver los paquetes instalados en el entorno actual, o en otros entornos virtuales que se muestran en el IDE. Puede configurar varios entornos, elija un entorno de una lista y ver los paquetes o instalar nuevos paquetes en ese entorno.

+ [Entornos de Python](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio)

Código de Visual Studio es un editor disponible que admita Python, con varios linters Python disponibles. Aunque frente a código no proporciona un explorador del paquete como el de Visual Studio, admite configurar y cambiar entre varios entornos.

+ [Python en el código de Visual Studio](https://code.visualstudio.com/docs/languages/python)

Podría ser necesario alguna configuración adicional para ejecutar **revoscalepy** comandos desde un cliente remoto:

+ [Instalar el intérprete y paquetes Python personalizados localmente en Windows](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)

Este blog proporciona algunas sugerencias útiles acerca de cómo configurar otros entornos de Python, incluidos PyCharm, para trabajar con **revoscalepy**.

+ [Empezar a trabajar con servicios Web de Python con el servidor de aprendizaje de máquina](https://blogs.msdn.microsoft.com/mlserver/2017/12/13/getting-started-with-python-web-services-using-machine-learning-server/)

## <a name="use-functions-from-machine-learning-server"></a>Usar funciones de servidor de aprendizaje de máquina

Dado que las bibliotecas que se utilizan con la ejecución de soporte técnico de SQL Server de código desde un cliente remoto, puede utilizar estas funciones para averiguar qué paquetes se instalan en un entorno remoto.

### <a name="revoscaler"></a>RevoScaleR

Si está trabajando en un cliente remoto y no tiene acceso al servidor, todavía puede obtener una lista de paquetes que están instalados en SQL Server, mediante el uso de funciones de RevoScaleR. Especifique el servidor SQL Server como un contexto de proceso, que requiere que tenga permiso para conectarse al servidor. 

+ [rxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage) busca la ruta de acceso para un paquete en el contexto de proceso remoto.

+ [rxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages) obtiene información sobre paquetes instalados en un contexto de proceso.

Por ejemplo, ejecute el siguiente código de R para obtener una lista de los paquetes disponibles en el contexto de proceso de SQL Server especificado.

```R
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
sqlPackages
```

En el ejemplo siguiente se obtiene la ubicación de la biblioteca de RevoScaleR en el contexto de proceso local y la versión del paquete.

```R
rxFindPackage(RevoScaleR, "local")
packageVersion("RevoScaleR")
```

### <a name="revoscalepy"></a>revoscalepy

Funciones similares a las de RevoScaleR no están disponibles en este momento. Busque en una versión posterior de **revoscalepy**.

## <a name="get-library-location-and-version"></a>Obtener la versión y la ubicación de biblioteca

Cuando se trabaja con varios entornos o las instalaciones de R o Python, en ocasiones necesitará comprobar que el código que se está ejecutando está utilizando el entorno correcto para Python o el área de trabajo correcta para R.

Por ejemplo, si ha actualizado los componentes mediante el enlace de aprendizaje automático, la ruta de acceso a la biblioteca de R podría estar en una carpeta diferente a la predeterminada. Además, si instala el cliente de R o una instancia del servidor independiente, podría tener varias bibliotecas de R en el equipo.

Estos ejemplos muestran cómo obtener la ruta de acceso y la versión de la biblioteca que se está usando SQL Server.

### <a name="r"></a>L

Este procedimiento almacenado devuelve la ruta de acceso de la biblioteca de la instancia y la versión del paquete RevoScaleR utilizado por SQL Server:

```sql
EXEC sp_execute_external_script
  @language =N'R',
  @script=N'
  sql_r_path <- rxSqlLibPaths("local")
  print(sql_r_path)
  version_info <-packageVersion("RevoScaleR")
  print(version_info)'
```

> [!NOTE]
> El [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) función se puede ejecutar solo en el equipo de destino. La función no puede devolver las rutas de acceso de biblioteca para las conexiones remotas.

**Resultado**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.2.1'
```

### <a name="python"></a>Python

Este ejemplo devuelve la lista de carpetas incluidas en la versión de Python `sys.path` variable. La lista incluye el directorio actual y la ruta de acceso de la biblioteca estándar.

```sql
EXEC sp_execute_external_script
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

