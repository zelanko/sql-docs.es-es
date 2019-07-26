---
title: Configuración de un cliente de ciencia de datos para el desarrollo de Python
description: Configure un entorno local de Python (Jupyter Notebook o PyCharm) para las conexiones remotas a SQL Server Machine Learning Services con Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: b5f406ec4b6cfbd65db7a4ecd3a1ad14dff6d8e1
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470239"
---
# <a name="set-up-a-data-science-client-for-python-development-on-sql-server-machine-learning-services"></a>Configuración de un cliente de ciencia de datos para el desarrollo de Python en SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La integración de Python está disponible a partir de SQL Server 2017 o posterior cuando se incluye la opción Python en una [instalación Machine Learning Services (en la base de datos)](../install/sql-machine-learning-services-windows-install.md). 

Para desarrollar e implementar soluciones de Python para SQL Server, instale el [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) de Microsoft y otras bibliotecas de Python en la estación de trabajo de desarrollo. La biblioteca de revoscalepy, que también está en la instancia de SQL Server remota, coordina las solicitudes de procesamiento entre ambos sistemas. 

En este artículo, aprenderá a configurar una estación de trabajo de desarrollo de Python para que pueda interactuar con un SQL Server remoto habilitado para el aprendizaje automático y la integración de Python. Después de completar los pasos de este artículo, tendrá las mismas bibliotecas de Python que en SQL Server. También sabrá cómo enviar cálculos desde una sesión de Python local a una sesión remota de Python en SQL Server.

![Componentes cliente-servidor](media/sqlmls-python-client-revo.png "Sesiones y bibliotecas de Python locales y remotas")

Para validar la instalación, puede usar cuadernos de Jupyter integrados, tal como se describe en este artículo, o [vincular las bibliotecas](#install-ide) a PyCharm o a cualquier otro IDE que use normalmente.

> [!Tip]
> Para ver una demostración en vídeo de estos ejercicios, consulte [ejecución remota de R y Python en SQL Server desde cuadernos de Jupyter Notebook](https://youtu.be/D5erljpJDjE).

> [!Note]
> Una alternativa a la instalación de la biblioteca de cliente es usar un [servidor independiente](../install/sql-machine-learning-standalone-windows-install.md) como un cliente enriquecido, que algunos clientes prefieren para un trabajo de escenario más profundo. Un servidor independiente está totalmente desacoplado de SQL Server, pero como tiene las mismas bibliotecas de Python, puede utilizarlo como cliente para SQL Server análisis en base de datos. También se puede usar para trabajos no relacionados con SQL, incluida la capacidad de importar y modelar datos de otras plataformas de datos. Si instala un servidor independiente, puede encontrar el archivo ejecutable de Python en esta ubicación: `C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`. Para validar la instalación, [abra un cuaderno de Jupyter Notebook](#python-tools) para ejecutar comandos con Python. exe en esa ubicación.

## <a name="commonly-used-tools"></a>Herramientas de uso frecuente

Tanto si es un desarrollador de Python nuevo en SQL como si es un desarrollador de SQL nuevo en Python y análisis en base de datos, necesitará una herramienta de desarrollo de Python y un editor de consultas de T-SQL como [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) para ejecutar todas las capacidades de Análisis en base de datos.

Para el desarrollo de Python, puede usar cuadernos de Jupyter, que se incluyen en la distribución Anaconda instalada por SQL Server. En este artículo se explica cómo iniciar cuadernos de Jupyter Notebook para que pueda ejecutar el código de Python de forma local y remota en SQL Server.

SSMS es una descarga independiente, útil para crear y ejecutar procedimientos almacenados en SQL Server, incluidos aquellos que contienen código Python. Casi cualquier código Python que escriba en cuadernos de Jupyter Notebook se puede incrustar en un procedimiento almacenado. Puede recorrer otras guías de inicio rápido para obtener información sobre [SSMS y Embedded Python](../tutorials/quickstart-python-verify.md).

## <a name="1---install-python-packages"></a>1-instalación de paquetes de Python

Las estaciones de trabajo locales deben tener las mismas versiones de paquete de Python que las de SQL Server, incluido el 4.2.0 de base Anaconda con la distribución de Python 3.5.2 y los paquetes específicos de Microsoft.

Un script de instalación agrega tres bibliotecas específicas de Microsoft al cliente de Python. El script instala [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package), que se usa para definir los objetos de origen de datos y el contexto de cálculo. Instala [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) que proporciona algoritmos de aprendizaje automático. También se instala el paquete [azureml](https://docs.microsoft.com/machine-learning-server/python-reference/azureml-model-management-sdk/azureml-model-management-sdk) , pero se aplica a las tareas de operacionalización asociadas a un contexto de machine learning Server independiente (sin instancia) y que pueden ser de uso limitado para el análisis en bases de datos.

1. Descargue un script de instalación.

  + [https://aka.ms/mls-py](https://aka.ms/mls-py)instala la versión 9.2.1 de los paquetes de Microsoft Python. Esta versión corresponde a una instancia de SQL Server predeterminada 2017. 

  + [https://aka.ms/mls93-py](https://aka.ms/mls93-py)instala la versión 9,3 de los paquetes de Microsoft Python. Esta versión es una opción mejor si la instancia de Remote SQL Server 2017 está [enlazada a Machine Learning Server 9,3](../install/upgrade-r-and-python.md).

2. Abra una ventana de PowerShell con permisos de administrador elevados (haga clic con el botón derecho en **Ejecutar como administrador**).

3. Vaya a la carpeta en la que descargó el instalador y ejecute el script. Agregue el `-InstallFolder` argumento de línea de comandos para especificar la ubicación de una carpeta para las bibliotecas. Por ejemplo: 

   ```python
   cd {{download-directory}}
   .\Install-PyForMLS.ps1 -InstallFolder "C:\path-to-python-for-mls"
   ```

Si omite la carpeta de instalación, el valor predeterminado es C:\Archivos de Files\Microsoft\PyForMLS.

La instalación tarda algún tiempo en completarse. Puede supervisar el progreso en la ventana de PowerShell. Una vez finalizada la instalación, tiene un conjunto completo de paquetes. 

> [!Tip] 
> Se recomiendan las [preguntas más frecuentes de Python para Windows](https://docs.python.org/3/faq/windows.html) para obtener información general de purppose sobre la ejecución de programas de Python en Windows.

## <a name="2---locate-executables"></a>2-buscar ejecutables

Todavía en PowerShell, enumere el contenido de la carpeta de instalación para confirmar que se han instalado Python. exe, scripts y otros paquetes. 

1. Escriba `cd \` para ir a la unidad raíz y, a continuación, escriba la ruta de `-InstallFolder` acceso que especificó en el paso anterior. Si omite este parámetro durante la instalación, el valor predeterminado `cd C:\Program Files\Microsoft\PyForMLS`es.

2. Escriba `dir *.exe` para enumerar los ejecutables. Debería ver **Python. exe**, **pythonw.** exe y **Uninstall-Anaconda. exe**.

  ![Lista de ejecutables de Python](media/powershell-python-exe.png)
   
En los sistemas que tienen varias versiones de Python, no olvide usar este archivo Python. exe concreto si desea cargar **revoscalepy** y otros paquetes de Microsoft.

> [!Note] 
> El script de instalación no modifica la variable de entorno PATH en el equipo, lo que significa que el nuevo intérprete y los módulos de Python que acaba de instalar no están disponibles automáticamente para otras herramientas que pueda tener. Para obtener ayuda sobre cómo vincular las bibliotecas y el intérprete de Python a las herramientas de, vea [instalar un IDE](#install-ide).

<a name="python-tools"></a>

## <a name="3---open-jupyter-notebooks"></a>3-Abra notebooks de Jupyter

Anaconda incluye Jupyter notebooks. Como paso siguiente, cree un cuaderno y ejecute código Python que contenga las bibliotecas que acaba de instalar.

1. En el símbolo del sistema de PowerShell, en el directorio C:\Archivos de Files\Microsoft\PyForMLS, abra Jupyter notebooks en la carpeta scripts:

  ```powershell
  .\Scripts\jupyter-notebook
  ```

  Un cuaderno debe abrirse en el explorador predeterminado `https://localhost:8889/tree`en.

  Otra manera de empezar es hacer doble clic en **jupyter-Notebook. exe**. 

2. Haga clic en **nuevo** y, a continuación, en **Python 3**.

  ![jupyter Notebook con la nueva selección de Python 3](media/jupyter-notebook-new-p3.png)

3. Escriba `import revoscalepy` y ejecute el comando para cargar una de las bibliotecas específicas de Microsoft.

4. Escriba y ejecute `print(revoscalepy.__version__)` para devolver la información de versión. Debería ver 9.2.1 o 9.3.0. Puede usar cualquiera de estas versiones con [revoscalepy en el servidor](../package-management/installed-package-information.md). 

4. Escriba una serie más compleja de instrucciones. Este ejemplo genera estadísticas de Resumen mediante [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) en un conjunto de datos local. Otras funciones obtienen la ubicación de los datos de ejemplo y crean un objeto de origen de datos para un archivo. xdf local.

  ```python
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

En la captura de pantalla siguiente se muestra la entrada y una parte de la salida, recortada para mayor brevedad.

  ![cuaderno de jupyter Notebook que muestra entradas y salidas de revoscalepy](media/jupyter-notebook-local-revo.png)

## <a name="4---get-sql-permissions"></a>4: obtener permisos SQL

Para conectarse a una instancia de SQL Server para ejecutar scripts y cargar datos, debe tener un inicio de sesión válido en el servidor de base de datos. Puede usar un inicio de sesión de SQL o la autenticación integrada de Windows. Por lo general, se recomienda usar la autenticación integrada de Windows, pero el inicio de sesión de SQL es más sencillo en algunos escenarios, especialmente cuando el script contiene cadenas de conexión a datos externos.

Como mínimo, la cuenta utilizada para ejecutar el código debe tener permiso para leer de las bases de datos con las que está trabajando, además del permiso especial ejecutar cualquier SCRIPT externo. La mayoría de los desarrolladores también requieren permisos para crear procedimientos almacenados y para escribir datos en tablas que contienen datos de entrenamiento o datos puntuados. 

Pida al administrador de la base de datos que [Configure los siguientes permisos para su cuenta](../security/user-permission.md), en la base de datos donde usa Python:

+ **Ejecute cualquier script externo** para ejecutar Python en el servidor.
+ privilegios **db_datareader** para ejecutar las consultas que se usan para entrenar el modelo.
+ **db_datawriter** para escribir datos de entrenamiento o datos puntuados.
+ **db_owner** para crear objetos como procedimientos almacenados, tablas, funciones. 
  También necesitará **db_owner** para crear bases de datos de prueba y de ejemplo. 

Si el código requiere paquetes que no se instalan de forma predeterminada con SQL Server, organice con el administrador de la base de datos para que los paquetes se instalen con la instancia. SQL Server es un entorno protegido y hay restricciones en el lugar donde se pueden instalar los paquetes. No se recomienda la instalación ad hoc de paquetes como parte del código, aunque tenga derechos. Además, tenga siempre en cuenta las implicaciones de seguridad antes de instalar nuevos paquetes en la biblioteca de servidores.


<a name="create-iris-remotely"></a>

## <a name="5---create-test-data"></a>5-crear datos de prueba

Si tiene permisos para crear una base de datos en el servidor remoto, puede ejecutar el código siguiente para crear la base de datos de demostración de iris utilizada para el resto de los pasos de este artículo.

### <a name="1---create-the-irissql-database-remotely"></a>1: crear la base de datos de irissql de forma remota

```python
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

### <a name="2---import-iris-sample-from-sklearn"></a>2-importación de un ejemplo de iris desde SkLearn

```python
from sklearn import datasets
import pandas as pd

# SkLearn has the Iris sample dataset built in to the package
iris = datasets.load_iris()
df = pd.DataFrame(iris.data, columns=iris.feature_names)
```

### <a name="3---use-revoscalepy-apis-to-create-a-table-and-load-the-iris-data"></a>3-uso de las API de Revoscalepy para crear una tabla y cargar los datos de iris

```python
from revoscalepy import RxSqlServerData, rx_data_step

# Example of using RX APIs to load data into SQL table. You can also do this with pyodbc
table_ref = RxSqlServerData(connection_string=connection_string.format(new_db_name), table="iris_data")
rx_data_step(input_data = df, output_file = table_ref, overwrite = True)

print("New Table Created: Iris")
print("Sklearn Iris sample loaded into Iris table")
```

## <a name="6---test-remote-connection"></a>6-probar conexión remota

Antes de probar el paso siguiente, asegúrese de que tiene permisos en la instancia de SQL Server y una cadena de conexión con la [base de datos de ejemplo iris](../tutorials/demo-data-iris-in-sql.md). Si la base de datos no existe y tiene permisos suficientes, puede [crear una base de datos mediante estas instrucciones en línea](#create-iris-remotely).

Reemplace la cadena de conexión con valores válidos. En el código de `"Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"` ejemplo se usa, pero el código debe especificar un servidor remoto, posiblemente con un nombre de instancia, y una opción de credencial que se asigne al inicio de sesión de usuario de base de datos.

### <a name="define-a-function"></a>Definir una función

En el código siguiente se define una función que se enviará a SQL Server en un paso posterior. Cuando se ejecuta, utiliza los datos y las bibliotecas (revoscalepy, pandas, matplotlib) en el servidor remoto para crear los gráficos de dispersión del conjunto de datos de iris. Devuelve el bytestream del. png de nuevo a los cuadernos de Jupyter para que se representen en el explorador.

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

En este ejemplo, cree el contexto de cálculo remoto y, a continuación, envíe la ejecución de la función a SQL Server con [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec). La función **rx_exec** es útil porque acepta un contexto de cálculo como argumento. Cualquier función que desee ejecutar de forma remota debe tener un argumento de contexto de proceso. Algunas funciones, como [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) admiten este argumento directamente. En el caso de las operaciones que no, puede usar **rx_exec** para enviar el código en un contexto de cálculo remoto.

En este ejemplo, no se tenía que transferir ningún dato sin procesar de SQL Server al Jupyter Notebook. Todos los cálculos se producen en la base de datos de iris y solo el archivo de imagen se devuelve al cliente.

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

En la captura de pantalla siguiente se muestra el resultado del gráfico de entrada y dispersión.

  ![jupyter Notebook muestra la salida del gráfico de dispersión](media/jupyter-notebook-scatterplot.png)


<a name="install-ide"></a>

## <a name="7---start-python-from-tools"></a>7: Inicio de Python desde herramientas

Dado que los desarrolladores suelen trabajar con varias versiones de Python, el programa de instalación no agrega Python a la ruta de acceso. Para usar el archivo ejecutable de Python y las bibliotecas instaladas por el programa de instalación, vincule el IDE a **Python. exe** en la ruta de acceso que también proporciona **revoscalepy** y **microsoftml**. 

### <a name="command-line"></a>Línea de comandos

Al ejecutar **Python. exe** desde C:\Archivos de Files\Microsoft\PyForMLS (o cualquier ubicación que haya especificado para la instalación de la biblioteca de cliente de Python), tiene acceso a la distribución completa de Anaconda más los módulos de Microsoft Python, **revoscalepy** y **microsoftml**.

1. Vaya a C:\Archivos de Files\Microsoft\PyForMLS y haga doble clic en **Python. exe**.
2. Abra la ayuda interactiva:`help()`
3. Escriba el nombre de un módulo en el símbolo del sistema `help> revoscalepy`de ayuda:. La ayuda devuelve el nombre, el contenido del paquete, la versión y la ubicación del archivo.
4. Devuelva la información de versión y del paquete en el `revoscalepy`símbolo del sistema de **Ayuda >** :. Presione entrar varias veces para salir de la ayuda.
5. Importar un módulo:`import revoscalepy`


### <a name="jupyter-notebooks"></a>Cuadernos de Jupyter Notebook

En este artículo se usan cuadernos de Jupyter integrados para mostrar las llamadas de función a **revoscalepy**. Si no está familiarizado con esta herramienta, en la captura de pantalla siguiente se muestra cómo encajan las piezas y por qué funcionan todo ". 

La carpeta principal C:\Archivos de Files\Microsoft\PyForMLS contiene Anaconda más los paquetes de Microsoft. Los cuadernos de Jupyter Notebook se incluyen en Anaconda, en la carpeta scripts, y los ejecutables de Python se registran automáticamente con cuadernos de Jupyter Notebook. Los paquetes que se encuentran en site-Packages se pueden importar en un cuaderno, incluidos los tres paquetes de Microsoft que se usan para la ciencia de datos y el aprendizaje automático.

  ![Archivos ejecutables y bibliotecas](media/jupyter-notebook-python-registration.png)

Si usa otro IDE, tendrá que vincular los ejecutables de Python y las bibliotecas de funciones a la herramienta. En las secciones siguientes se proporcionan instrucciones para las herramientas de uso frecuente.

### <a name="visual-studio"></a>Programa para la mejora

Si tiene [Python en Visual Studio](https://code.visualstudio.com/docs/languages/python), use las siguientes opciones de configuración para crear un entorno de Python que incluya los paquetes de Microsoft Python.

| Valor de configuración | valor |
|-----------------------|-------|
| **Ruta de acceso de prefijo** | C:\Archivos de Files\Microsoft\PyForMLS |
| **Ruta de intérprete** | C:\Archivos de Files\Microsoft\PyForMLS\python.exe |
| **Intérprete con ventanas** | C:\Archivos de Files\Microsoft\PyForMLS\pythonw.exe |

Para obtener ayuda para configurar un entorno de Python, consulte [Administración de entornos de Python en Visual Studio](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio).

### <a name="pycharm"></a>PyCharm

En PyCharm, establezca el intérprete en el ejecutable de Python instalado por Machine Learning Server.

1. En un nuevo proyecto, en configuración, haga clic en **Agregar local**.

2. Escriba `C:\Program Files\Microsoft\PyForMLS\`.

Ahora puede importar los módulos **revoscalepy**, **microsoftml**o **azureml** . También puede elegir **herramientas** > **Python Console** para abrir una ventana interactiva.

## <a name="next-steps"></a>Pasos siguientes

Ahora que tiene herramientas y una conexión operativa a SQL Server, amplíe sus conocimientos mediante la ejecución de las guías de inicio rápido de Python con [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

> [!div class="nextstepaction"]
> [Inicio rápido: Compruebe que Python existe en SQL Server](../tutorials/quickstart-python-verify.md)