---
title: Configurar un cliente de Python para su uso con SQL Server Machine Learning | Microsoft Docs
description: Configurar un entorno local de Python para las conexiones remotas a SQL Server Machine Learning Services con Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/25/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 326676d1be684b90784351de316590ebdb1ff29f
ms.sourcegitcommit: 182d77997133a6e4ee71e7a64b4eed6609da0fba
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2018
ms.locfileid: "50051157"
---
# <a name="set-up-a-python-client-for-use-with-sql-server-machine-learning"></a>Configurar un cliente de Python para su uso con SQL Server Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Integración de Python está disponible a partir de SQL Server 2017 o posterior al incluir la opción de Python en una instalación de Machine Learning Services (In-Database). Para obtener más información, consulte [instalar SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md).

En este artículo, obtenga información sobre cómo configurar una estación de trabajo de desarrollo de cliente para que pueda conectarse a un servidor SQL remoto habilitado para la integración de Python y aprendizaje automático. Al final, tendrá las mismas bibliotecas de Python como los de SQL Server además de la capacidad para enviar los cálculos de una sesión local a una sesión remota de SQL Server.

> [!Tip]
> Para una demostración en vídeo, consulte [ejecute R y Python de forma remota en SQL Server en cuadernos de Jupyter](https://blogs.msdn.microsoft.com/mlserver/2018/07/10/run-r-and-python-remotely-in-sql-server-from-jupyter-notebooks-or-any-ide/).

> [!Note]
> Una alternativa para instalar solamente las bibliotecas de cliente está usando un servidor independiente. Usa un independiente server como una aplicación cliente enriquecida es una opción que algunos clientes prefieren para más trabajo del escenario de extremo a otro. Si tiene un [servidor independiente](../install/sql-machine-learning-standalone-windows-install.md) como se indica en el programa de instalación de SQL Server, tiene un servidor de Python que se separa por completo de una instancia del motor de base de datos de SQL Server. Un servidor standalon incluye la distribución de base de código abierto de Anaconda además de las bibliotecas específicas de Microsoft. Puede encontrar el archivo ejecutable de Python en esta ubicación: `C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`. Como la validación de la instalación de cliente enriquecidas, abra un [cuaderno de Jupyter notebook](#python-tools) para ejecutar comandos con el Python.exe en el servidor.

## <a name="1---install-python-packages"></a>1 - instalar paquetes de Python

Las estaciones de trabajo locales deben tener las mismas versiones de paquete de Python como los de SQL Server, incluidos los paquetes específicos de Microsoft y distribución de base [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) y [microsftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package). El [administración de modelos de azureml](https://docs.microsoft.com/machine-learning-server/python-reference/azureml-model-management-sdk/azureml-model-management-sdk) también se instala el paquete, pero se aplica a las tareas de puesta en marcha asociadas con un contexto de Machine Learning Server independiente (que no son de instancia). Para realizar análisis en bases de datos en una instancia de SQL Server, puesta en marcha es a través de procedimientos almacenados.

1. Descargue el script de instalación para instalar Anaconda 4.2.0 con Python 3.5.2 y los tres paquetes de Microsoft que mencionamos.

  + [https://aka.ms/mls-py](https://aka.ms/mls-py) Si SQL Server 2017 no está enlazado (caso común). Elija esta secuencia de comandos si no está seguro.

  + [https://aka.ms/mls93-py](https://aka.ms/mls93-py) Si la instancia remota de SQL Server está [enlazado a Machine Learning Server 9.3](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

2. Abra una ventana de PowerShell con permisos de administrador con privilegios elevados (haga clic en **ejecutar como administrador**).

3. Vaya a la carpeta donde descargó el programa de instalación y ejecute el script. Agregar el `-InstallFolder` argumento de línea de comandos para especificar una ubicación de carpeta para las bibliotecas. Por ejemplo: 

   ```python
   cd {{download-directory}}
   .\Install-PyForMLS.ps1 -InstallFolder "C:\path-to-python-for-mls"
   ```

Si se omite la carpeta de instalación, el valor predeterminado es C:\Program Files\Microsoft\PyForMLS.

Instalación tarda algún tiempo en completarse. Puede supervisar el progreso en la ventana de PowerShell. Cuando finalice la instalación, tiene un conjunto completo de paquetes. 

> [!Tip] 
> Se recomienda la [P+F de Python para Windows](https://docs.python.org/3/faq/windows.html) para obtener información general de purppose sobre la ejecución de programas de Python en Windows.

## <a name="2---locate-executables"></a>2: buscar archivos ejecutables

Todavía en PowerShell, vaya a la carpeta de instalación para confirmar la ubicación de la Python.exe, scripts y otros paquetes. 

1. Escriba `cd \` para ir a la unidad raíz y, a continuación, escriba la ruta de acceso especificada para `-InstallFolder` en el paso anterior. Si omite este parámetro durante la instalación, el valor predeterminado es `cd C:\Program Files\Microsoft\PyForMLS`.

2. Escriba `dir *.exe` para enumerar los archivos ejecutables. Debería ver **python.exe**, **pythonw.exe**, y **anaconda.exe desinstalar**.

  ![Lista de archivos ejecutables de Python](media/powershell-python-exe.png)
   
En sistemas de varias versiones de Python, recuerde que debe usar este Python.exe determinado si desea cargar **revoscalepy** y otros paquetes de Microsoft.

> [!Note] 
> El script de instalación no modifica la variable de entorno PATH en el equipo, lo que significa que el nuevo intérprete de python y que acaba de instalar los módulos no están disponibles automáticamente a otras herramientas que es posible que tenga. Para obtener ayuda sobre la vinculación de las bibliotecas y el intérprete de Python con herramientas, consulte [instalar un IDE](#install-ide).

<a name="python-tool"></a>

## <a name="3---open-jupyter-notebooks"></a>3 - abrir Jupyter Notebooks

Anaconda incluye cuadernos de Jupyter. Como siguiente paso, cree un bloc de notas y ejecutar código Python que contiene las bibliotecas que acaba de instalar.

1. En el símbolo del sistema de Powershell, vaya a la carpeta de scripts para abrir Jupyter Notebooks:

   ```powershell
   .\Scripts\jupyter-notebook
   ```

  Debe abrir un cuaderno en el explorador predeterminado en `http://localhost:8889/tree`.

2. Haga clic en **New** y, a continuación, haga clic en **Python 3**.

  ![Cuaderno de jupyter notebook con selección nueva Python 3](media/jupyter-notebook-new-p3.png)

3. Escriba `import revoscalepy` y ejecute el comando para cargar una de las bibliotecas específicas de Microsoft.

4. Escriba una serie más compleja de instrucciones. En este ejemplo genera estadísticas de resumen mediante [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) a través de un conjunto de datos local. Otras funciones de obtención la ubicación de los datos de ejemplo y creación un objeto de origen de datos para un archivo xdf local.

  ```Python
  import os
  from revoscalepy import rx_summary
  from revoscalepy import RxXdfData
  from revoscalepy import RxOptions
  sample_data_path = RxOptions.get_option("sampleDataDir")
  print(sample_data_path)
  ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
  summary = rx_summary("ArrDelay+DayOfWeek", ds)
  print(summary)
  ```

Captura de pantalla siguiente muestra la entrada y una parte de la salida, acortada para simplificar.

  ![Cuaderno de jupyter que muestra la salida y revoscalepy entradas](media/jupyter-notebook-local-revo.png)

## <a name="4---get-sql-permissions"></a>4 - obtener permisos de SQL

Para conectarse a una instancia de SQL Server para ejecutar scripts y cargar los datos, debe tener un inicio de sesión válido en el servidor de base de datos. Puede usar un inicio de sesión de SQL o la autenticación integrada de Windows. Por lo general, se recomienda que utilice la autenticación integrada de Windows, pero usar el inicio de sesión SQL es más fácil para algunos escenarios, especialmente cuando el script contiene las cadenas de conexión a datos externos.

Como mínimo, la cuenta utilizada para ejecutar el código debe tener permiso para leer desde las bases de datos que está trabajando, más el permiso especial EXECUTE ANY EXTERNAL SCRIPT. Mayoría de los desarrolladores también requiere permisos para crear procedimientos almacenados y para escribir datos en tablas que contienen datos de entrenamiento o puntuación datos. 

Pida al administrador de base de datos para configurar los siguientes permisos para la cuenta, en la base de datos que se usa Python:

+ **EXECUTE ANY EXTERNAL SCRIPT** a ejecutar Python en el servidor.
+ **db_datareader** privilegios para ejecutar las consultas que utilizan para entrenar el modelo.
+ **db_datawriter** para escribir datos con puntuación o datos de entrenamiento.
+ **db_owner** para crear objetos como procedimientos almacenados, tablas, las funciones. 
  También necesita **db_owner** crear bases de datos de ejemplo y prueba. 

Si el código requiere que los paquetes que no se instalan de forma predeterminada con SQL Server, organizar con el Administrador de base de datos para que los paquetes instalados con la instancia. SQL Server es un entorno protegido y hay restricciones en donde se pueden instalar los paquetes. No se recomienda la instalación de paquetes ad hoc como parte del código, incluso si tiene derechos. Además, considere siempre detenidamente las implicaciones de seguridad antes de instalar nuevos paquetes en la biblioteca del servidor.

## <a name="5---test-remote-connection"></a>5: probar la conexión remota

Antes de intentar este paso, asegúrese de que tiene permisos en la instancia de SQL Server y una cadena de conexión para el [base de datos de ejemplo de Iris](../tutorials/demo-data-iris-in-sql.md). Si no existe la base de datos y tiene permisos suficientes, puede [crear una base de datos mediante estas instrucciones insertadas](#create-iris-remotely).

Reemplace la cadena de conexión con los valores válidos. El código de ejemplo usa `"Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"` , pero el código debe especificar un servidor remoto, posiblemente con un nombre de instancia.

### <a name="define-a-function"></a>Definir una función

El código siguiente define una función que se enviará a SQL Server en un paso posterior. Cuando se ejecuta, usan datos y bibliotecas (revoscalepy, pandas, matplotlib) en el servidor remoto para crear gráficos de dispersión del conjunto de datos iris. Devuelve la secuencia de bytes de la .png a Jupyter Notebook para representarlo en el explorador.

```python
def send_this_func_to_sql():
    from revoscalepy import RxSqlServerData, rx_import
    from pandas.tools.plotting import scatter_matrix
    import matplotlib.pyplot as plt
    import io
    
    # remember the scope of the variables in this func are within our SQL Server Python Runtime
    connection_string = "Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"
    
    # specify a query and load into pandas dataframe df
    sql_query = RxSqlServerData(connection_string=connection_string, sql_query = "select * from iris_data")
    df = rx_import(sql_query)
    
    scatter_matrix(df)
    
    # return bytestream of image created by scatter_matrix
    buf = io.BytesIO()
    plt.savefig(buf, format="png")
    buf.seek(0)
    
    return buf.getvalue()
```

### <a name="send-the-function-to-sql-server"></a>Enviar la función a SQL Server

En este ejemplo, cree el contexto de proceso remoto y, a continuación, enviar la ejecución de la función a SQL Server con [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec). El **rx_exec** función es útil porque lo acepta como argumento en un contexto de proceso. Cualquier función que desea ejecutar de forma remota debe tener un argumento de contexto de cálculo. Algunas funciones, como [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) son compatibles directamente con este argumento. Para las operaciones que no lo hacen, puede usar **rx_exec** para entregar el código en un contexto de cálculo remoto.

En este ejemplo, no hay datos sin procesar se tenían que transferirse desde SQL Server para el cuaderno de Jupyter. Todos los cálculos se producen dentro de la base de datos de Iris y el archivo de imagen solo se devuelve al cliente.

```python
from IPython import display
import matplotlib.pyplot as plt 
from revoscalepy import RxInSqlServer, rx_exec

# create a remote compute context with connection to SQL Server
sql_compute_context = RxInSqlServer(connection_string=connection_string.format(new_db_name))

# use rx_exec to send the function execution to SQL Server
image = rx_exec(send_this_func_to_sql, compute_context=sql_compute_context)[0]

# only an image was returned to my jupyter client. All data remained secure and was manipulated in my db.
display.Image(data=image)
```

Captura de pantalla siguiente muestra el resultado de trazado de dispersión y de entrada.

  ![Cuaderno de jupyter que muestra la salida de trazado de dispersión](media/jupyter-notebook-scatterplot.png)

## <a name="6---link-ide-to-pythonexe"></a>6 - vínculo IDE a python.exe

Si simplemente va a depurar secuencias de comandos desde la línea de comandos, puede hacerlo con las herramientas de Python estándar. Sin embargo, si va a desarrollar nuevas soluciones, puede que necesite un IDE de Python completo. Opciones populares son:

+ [Visual Studio 2017 Community Edition](https://www.visualstudio.com/vs/features/python/) con Python
+ [Visual Studio tools para AI](https://docs.microsoft.com/visualstudio/ai/installation)
+ [Python en Visual Studio Code](https://code.visualstudio.com/docs/languages/python)
+ Herramientas de terceros populares como Eclipse, Spyder y PyCharm

Se recomienda Visual Studio, ya que admite proyectos de base de datos, así como proyectos de aprendizaje automático. Para obtener ayuda acerca de la configuración de un entorno de Python, consulte [entornos administrar Python en Visual Studio](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio).

Porque con frecuencia, los desarrolladores trabajar con varias versiones de Python, el programa de instalación no agrega Python a su ruta de acceso. Para utilizar el archivo ejecutable de Python y el programa de instalación instaladas las bibliotecas de, vincule su IDE para **Python.exe** en la ruta de acceso que proporciona también **revoscalepy** y **microsoftml**. 

Para un proyecto de Python en Visual Studio, el entorno personalizado especificar los valores siguientes, suponiendo que una instalación predeterminada.

| Opción de configuración | value |
|-----------------------|-------|
| **Ruta de acceso de prefijo** | C:\Program Files\Microsoft\PyForMLS |
| **Ruta de acceso del intérprete** | C:\Program Files\Microsoft\PyForMLS\python.exe |
| **Intérprete de división de particiones** | C:\Program Files\Microsoft\PyForMLS\pythonw.exe |

<a name="create-iris-remotely"></a>

## <a name="optional-create-the-iris-database-remotely"></a>Opcional: Crear la base de datos de Iris remota

Si tiene permisos para crear una base de datos en el servidor remoto, puede ejecutar el código siguiente para crear la base de datos de Iris demostración utilizado los ejemplos de este artículo.

### <a name="1---create-the-irissql-database"></a>1 - Creación de la base de datos irissql

```Python
import pyodbc

# creating a new db to load Iris sample in
new_db_name = "irissql"
connection_string = "Driver=SQL Server;Server=localhost;Database={0};Trusted_Connection=Yes;" 
                        # you can also swap Trusted_Connection for UID={your username};PWD={your password}
cnxn = pyodbc.connect(connection_string.format("master"), autocommit=True)
cnxn.cursor().execute("IF EXISTS(SELECT * FROM sys.databases WHERE [name] = '{0}') DROP DATABASE {0}".format(new_db_name))
cnxn.cursor().execute("CREATE DATABASE " + new_db_name)
cnxn.close()

print("Database created")
```

### <a name="2---import-iris-sample-from-sklearn"></a>2 - importación de ejemplo de Iris de SkLearn

```Python
from sklearn import datasets
import pandas as pd

# SkLearn has the Iris sample dataset built in to the package
iris = datasets.load_iris()
df = pd.DataFrame(iris.data, columns=iris.feature_names)
```

### <a name="3---use-recoscalepy-apis-to-create-a-table-and-load-the-iris-data"></a>3 - usar RecoscalePy APIs para crear una tabla y cargar los datos de Iris

```Python
from revoscalepy import RxSqlServerData, rx_data_step

# Example of using RX APIs to load data into SQL table. You can also do this with pyodbc
table_ref = RxSqlServerData(connection_string=connection_string.format(new_db_name), table="iris_data")
rx_data_step(input_data = df, output_file = table_ref, overwrite = True)

print("New Table Created: Iris")
print("Sklearn Iris sample loaded into Iris table")
```

<a name="install-ide"></a>

## <a name="next-steps"></a>Pasos siguientes

Ahora que tiene las herramientas y una conexión activa con SQL Server, realice un tutorial para obtener una visión más detallada de las funciones de revoscalepy y cambiar los contextos de cálculo.

> [!div class="nextstepaction"]
> [Crear un modelo usando revoscalepy y un contexto de cálculo remoto](../tutorials/use-python-revoscalepy-to-create-model.md)