---
title: 'Configurar un cliente de ciencia de datos para el desarrollo de Python: SQL Server Machine Learning'
description: Configurar un entorno local de Python (Jupyter Notebook o PyCharm) para las conexiones remotas a SQL Server Machine Learning Services con Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/09/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: c0ca592d98f9bb69586c537006fd14d4230b661b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642764"
---
# <a name="set-up-a-data-science-client-for-python-development-on-sql-server-machine-learning-services"></a>Configurar un cliente de ciencia de datos para el desarrollo de Python en SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Integración de Python está disponible a partir de SQL Server 2017 o posterior al incluir la opción de Python en un [instalación de Machine Learning Services (In-Database)](../install/sql-machine-learning-services-windows-install.md). 

Para desarrollar e implementar soluciones de Python para SQL Server, instale Microsoft [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) y otras bibliotecas de Python su estación de trabajo de desarrollo. La biblioteca de revoscalepy, que se encuentra también en la instancia remota de SQL Server, coordina las solicitudes de computación entre ambos sistemas. 

En este artículo, obtenga información sobre cómo configurar una estación de trabajo de desarrollo de Python para que puedan interactuar con un servidor SQL remoto habilitado para la integración de Python y aprendizaje automático. Después de completar los pasos descritos en este artículo, tendrá las mismas bibliotecas de Python como los de SQL Server. También sabe cómo insertar cálculos en una sesión de Python local a una sesión remota de Python en SQL Server.

![Componentes de cliente / servidor](media/sqlmls-python-client-revo.png "bibliotecas y las sesiones de Python Local y remotas")

Para validar la instalación, puede usar cuadernos de Jupyter integrados tal como se describe en este artículo, o [vincular las bibliotecas](#install-ide) PyCharm o cualquier otro IDE que suela usar.

> [!Tip]
> Para una demostración en vídeo de estos ejercicios, consulte [ejecute R y Python de forma remota en SQL Server en cuadernos de Jupyter](https://youtu.be/D5erljpJDjE).

> [!Note]
> Una alternativa a la instalación de la biblioteca de cliente está usando un [servidor independiente](../install/sql-machine-learning-standalone-windows-install.md) como un cliente enriquecido, que algunos clientes prefieren para el trabajo de escenario más profundo. Un servidor independiente se separa por completo de SQL Server, pero porque tiene las mismas bibliotecas de Python, puede usar como un cliente para el análisis en bases de datos de SQL Server. También puede usar para el trabajo no relacionados con SQL, incluida la capacidad para importar y modelar datos desde otras plataformas de datos. Si instala un servidor independiente, puede encontrar el archivo ejecutable de Python en esta ubicación: `C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`. Para validar la instalación, [abrir un cuaderno de Jupyter](#python-tools) para ejecutar comandos con el Python.exe en esa ubicación.

## <a name="commonly-used-tools"></a>Herramientas utilizadas habitualmente

Tanto si es un desarrollador de Python es nuevo en SQL o un desarrollador SQL nuevo para Python y análisis en bases de datos, necesitará una herramienta de desarrollo de Python y un editor de consultas de T-SQL como [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) ejercer todos las capacidades de análisis en bases de datos.

Para el desarrollo de Python, puede usar cuadernos de Jupyter, que viene incluido en la distribución de Anaconda instalada SQL Server. En este artículo se explica cómo iniciar Jupyter Notebook para que pueda ejecutar código de Python local y remota en SQL Server.

SSMS es una descarga independiente, útil para crear y ejecutar procedimientos almacenados en SQL Server, incluidas aquéllas que contienen código de Python. Casi cualquier código de Python que se escribe en cuadernos de Jupyter se puede incrustar en un procedimiento almacenado. Puede ejecutar paso a paso a través de otras guías de inicio para obtener información sobre [SSMS y Python incrustado](../tutorials/quickstart-python-verify.md).

## <a name="1---install-python-packages"></a>1 - instalar paquetes de Python

Las estaciones de trabajo locales deben tener las mismas versiones de paquete de Python como los de SQL Server, incluido el Anaconda base 4.2.0 con la distribución de Python 3.5.2 y paquetes específicos de Microsoft.

Un script de instalación agrega tres bibliotecas específicas de Microsoft para el cliente de Python. El script instala [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package), que se usa para definir objetos de origen de datos y el contexto de cálculo. Instala [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) proporcionar algoritmos de aprendizaje automático. El [azureml](https://docs.microsoft.com/machine-learning-server/python-reference/azureml-model-management-sdk/azureml-model-management-sdk) también se instala el paquete, pero se aplica a las tareas de puesta en marcha asociadas con un contexto de Machine Learning Server independiente (que no son de instancia) y puede ser un uso limitado para realizar análisis en bases de datos.

1. Descargue un script de instalación.

  + [https://aka.ms/mls-py](https://aka.ms/mls-py) instala la versión 9.2.1 de los paquetes de Python de Microsoft. Esta versión corresponde a una instancia predeterminada de SQL Server 2017. 

  + [https://aka.ms/mls93-py](https://aka.ms/mls93-py) instala la versión 9.3 de los paquetes de Python de Microsoft. Esta versión es una opción mejor si la instancia remota de SQL Server 2017 es [enlazado a Machine Learning Server 9.3](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

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

Todavía en PowerShell, mostrar el contenido de la carpeta de instalación para confirmar que se instalan Python.exe, scripts y otros paquetes. 

1. Escriba `cd \` para ir a la unidad raíz y, a continuación, escriba la ruta de acceso especificada para `-InstallFolder` en el paso anterior. Si omite este parámetro durante la instalación, el valor predeterminado es `cd C:\Program Files\Microsoft\PyForMLS`.

2. Escriba `dir *.exe` para enumerar los archivos ejecutables. Debería ver **python.exe**, **pythonw.exe**, y **anaconda.exe desinstalar**.

  ![Lista de archivos ejecutables de Python](media/powershell-python-exe.png)
   
En sistemas de varias versiones de Python, recuerde que debe usar este Python.exe determinado si desea cargar **revoscalepy** y otros paquetes de Microsoft.

> [!Note] 
> El script de instalación no modifica la variable de entorno PATH en el equipo, lo que significa que el nuevo intérprete de python y que acaba de instalar los módulos no están disponibles automáticamente a otras herramientas que es posible que tenga. Para obtener ayuda sobre la vinculación de las bibliotecas y el intérprete de Python con herramientas, consulte [instalar un IDE](#install-ide).

<a name="python-tools"></a>

## <a name="3---open-jupyter-notebooks"></a>3 - abrir Jupyter Notebooks

Anaconda incluye cuadernos de Jupyter. Como siguiente paso, cree un bloc de notas y ejecutar código Python que contiene las bibliotecas que acaba de instalar.

1. En el símbolo del sistema de Powershell, en el directorio C:\Program Files\Microsoft\PyForMLS, abra cuadernos de Jupyter desde la carpeta de Scripts:

  ```powershell
  .\Scripts\jupyter-notebook
  ```

  Debe abrir un cuaderno en el explorador predeterminado en `https://localhost:8889/tree`.

  Otra manera de empezar es haga doble clic en **jupyter notebook.exe**. 

2. Haga clic en **New** y, a continuación, haga clic en **Python 3**.

  ![Cuaderno de jupyter notebook con selección nueva Python 3](media/jupyter-notebook-new-p3.png)

3. Escriba `import revoscalepy` y ejecute el comando para cargar una de las bibliotecas específicas de Microsoft.

4. Escriba y ejecute `print(revoscalepy.__version__)` para devolver la información de versión. Debería ver 9.2.1 o 9.3.0. Puede usar cualquiera de estas versiones con [revoscalepy en el servidor](../r/determine-which-packages-are-installed-on-sql-server.md#get-package-vers). 

4. Escriba una serie más compleja de instrucciones. En este ejemplo genera estadísticas de resumen mediante [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) a través de un conjunto de datos local. Otras funciones de obtención la ubicación de los datos de ejemplo y creación un objeto de origen de datos para un archivo xdf local.

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

Captura de pantalla siguiente muestra la entrada y una parte de la salida, acortada para simplificar.

  ![Cuaderno de jupyter que muestra la salida y revoscalepy entradas](media/jupyter-notebook-local-revo.png)

## <a name="4---get-sql-permissions"></a>4 - obtener permisos de SQL

Para conectarse a una instancia de SQL Server para ejecutar scripts y cargar los datos, debe tener un inicio de sesión válido en el servidor de base de datos. Puede usar un inicio de sesión de SQL o la autenticación integrada de Windows. Por lo general, se recomienda que utilice la autenticación integrada de Windows, pero usar el inicio de sesión SQL es más fácil para algunos escenarios, especialmente cuando el script contiene las cadenas de conexión a datos externos.

Como mínimo, la cuenta utilizada para ejecutar el código debe tener permiso para leer desde las bases de datos que está trabajando, más el permiso especial EXECUTE ANY EXTERNAL SCRIPT. Mayoría de los desarrolladores también requiere permisos para crear procedimientos almacenados y para escribir datos en tablas que contienen datos de entrenamiento o puntuación datos. 

Pida al administrador de base de datos que [configurar los siguientes permisos para la cuenta](../security/user-permission.md), en la base de datos que se usa Python:

+ **EXECUTE ANY EXTERNAL SCRIPT** a ejecutar Python en el servidor.
+ **db_datareader** privilegios para ejecutar las consultas que utilizan para entrenar el modelo.
+ **db_datawriter** para escribir datos con puntuación o datos de entrenamiento.
+ **db_owner** para crear objetos como procedimientos almacenados, tablas, las funciones. 
  También necesita **db_owner** crear bases de datos de ejemplo y prueba. 

Si el código requiere que los paquetes que no se instalan de forma predeterminada con SQL Server, organizar con el Administrador de base de datos para que los paquetes instalados con la instancia. SQL Server es un entorno protegido y hay restricciones en donde se pueden instalar los paquetes. No se recomienda la instalación de paquetes ad hoc como parte del código, incluso si tiene derechos. Además, considere siempre detenidamente las implicaciones de seguridad antes de instalar nuevos paquetes en la biblioteca del servidor.


<a name="create-iris-remotely"></a>

## <a name="5---create-test-data"></a>5 - crear datos de prueba

Si tiene permisos para crear una base de datos en el servidor remoto, puede ejecutar el código siguiente para crear la base de datos de demostración de Iris usado para los pasos restantes de este artículo.

### <a name="1---create-the-irissql-database-remotely"></a>1: crear la base de datos irissql remota

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

### <a name="2---import-iris-sample-from-sklearn"></a>2 - importación de ejemplo de Iris de SkLearn

```python
from sklearn import datasets
import pandas as pd

# SkLearn has the Iris sample dataset built in to the package
iris = datasets.load_iris()
df = pd.DataFrame(iris.data, columns=iris.feature_names)
```

### <a name="3---use-revoscalepy-apis-to-create-a-table-and-load-the-iris-data"></a>3 - usar Revoscalepy APIs para crear una tabla y cargar los datos de Iris

```python
from revoscalepy import RxSqlServerData, rx_data_step

# Example of using RX APIs to load data into SQL table. You can also do this with pyodbc
table_ref = RxSqlServerData(connection_string=connection_string.format(new_db_name), table="iris_data")
rx_data_step(input_data = df, output_file = table_ref, overwrite = True)

print("New Table Created: Iris")
print("Sklearn Iris sample loaded into Iris table")
```

## <a name="6---test-remote-connection"></a>6: probar la conexión remota

Antes de intentar este paso, asegúrese de que tiene permisos en la instancia de SQL Server y una cadena de conexión para el [base de datos de ejemplo de Iris](../tutorials/demo-data-iris-in-sql.md). Si no existe la base de datos y tiene permisos suficientes, puede [crear una base de datos mediante estas instrucciones insertadas](#create-iris-remotely).

Reemplace la cadena de conexión con los valores válidos. El código de ejemplo usa `"Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"` , pero el código debe especificar un servidor remoto, posiblemente con un nombre de instancia y una opción de credencial que se asigna al inicio de sesión de usuario de base de datos.

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


<a name="install-ide"></a>

## <a name="7---start-python-from-tools"></a>7 - iniciar Python desde herramientas

Porque con frecuencia, los desarrolladores trabajar con varias versiones de Python, el programa de instalación no agrega Python a su ruta de acceso. Para utilizar el archivo ejecutable de Python y el programa de instalación instaladas las bibliotecas de, vincule su IDE para **Python.exe** en la ruta de acceso que proporciona también **revoscalepy** y **microsoftml**. 

### <a name="command-line"></a>Línea de comandos

Al ejecutar **Python.exe** desde C:\Program Files\Microsoft\PyForMLS (o cualquier ubicación que especificó para la instalación de bibliotecas de cliente de Python), tendrá acceso a la versión de Python Microsoft además de la distribución de Anaconda completa los módulos, **revoscalepy** y **microsoftml**.

1. Vaya a C:\Program Files\Microsoft\PyForMLS y haga doble clic en **Python.exe**.
2. Abrir la Ayuda interactiva: `help()`
3. Escriba el nombre de un módulo en el símbolo del sistema de ayuda: `help> revoscalepy`. Ayuda devuelve el nombre, el contenido del paquete, versión y ubicación del archivo.
4. Devolver información de versión y el paquete en el **Ayuda >** símbolo del sistema: `revoscalepy`. Presione ENTRAR varias veces para salir de la Ayuda.
5. Importar un módulo: `import revoscalepy`


### <a name="jupyter-notebooks"></a>Cuadernos de Jupyter

Este artículo usa para demostrar las llamadas de función a integrados cuadernos de Jupyter **revoscalepy**. Si está familiarizado con esta herramienta, la captura de pantalla siguiente se muestra cómo encajan todas las piezas y por qué todo "simplemente funciona". 

La carpeta primaria C:\Program Files\Microsoft\PyForMLS contiene Anaconda además de los paquetes de Microsoft. Cuadernos de Jupyter se incluyen en Anaconda, bajo la carpeta de Scripts, y los ejecutables de Python son registrarse automáticamente con cuadernos de Jupyter. Paquetes que se encuentran en los paquetes del sitio pueden importarse en un bloc de notas, incluidos los tres paquetes de Microsoft utilizados para ciencia de datos y el aprendizaje automático.

  ![Archivos ejecutables y bibliotecas](media/jupyter-notebook-python-registration.png)

Si utiliza otro IDE, deberá vincular las bibliotecas de Python de los archivos ejecutables y la función a la herramienta. Las secciones siguientes proporcionan instrucciones para las herramientas utilizadas habitualmente.

### <a name="visual-studio"></a>Programa para la mejora

Si tiene [Python en Visual Studio](https://code.visualstudio.com/docs/languages/python), utilice las siguientes opciones de configuración para crear un entorno de Python que incluya los paquetes de Python de Microsoft.

| Opción de configuración | value |
|-----------------------|-------|
| **Ruta de acceso de prefijo** | C:\Program Files\Microsoft\PyForMLS |
| **Ruta de acceso del intérprete** | C:\Program Files\Microsoft\PyForMLS\python.exe |
| **Intérprete de división de particiones** | C:\Program Files\Microsoft\PyForMLS\pythonw.exe |

Para obtener ayuda acerca de la configuración de un entorno de Python, consulte [entornos administrar Python en Visual Studio](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio).

### <a name="pycharm"></a>PyCharm

En PyCharm, establezca el intérprete Python ejecutables instalado por Machine Learning Server.

1. En un proyecto nuevo, en configuración, haga clic en **agregar Local**.

2. Escriba `C:\Program Files\Microsoft\PyForMLS\`.

Ahora puede importar **revoscalepy**, **microsoftml**, o **azureml** módulos. También puede elegir **herramientas** > **consola Python** para abrir una ventana interactiva.

## <a name="next-steps"></a>Pasos siguientes

Ahora que tiene las herramientas y una conexión activa con SQL Server, expanda sus conocimientos mediante la ejecución a través de las guías de inicio rápido de Python con [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

> [!div class="nextstepaction"]
> [Inicio rápido: Compruebe que existe de Python en SQL Server](../tutorials/quickstart-python-verify.md)