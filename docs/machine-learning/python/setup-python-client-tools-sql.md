---
title: Configuración de un cliente de ciencia de datos Python
description: Configure un entorno local de Python (Jupyter Notebook o PyCharm) para las conexiones remotas a SQL Server Machine Learning Services con Python.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/04/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5199f22e5e72e68be3b1a76769fb8bd3a9518413
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956606"
---
# <a name="set-up-a-data-science-client-for-python-development-on-sql-server-machine-learning-services"></a>Configuración de un cliente de ciencia de datos para el desarrollo de Python en SQL Server Machine Learning Services
[!INCLUDE [SQL Server 2017 and later](../../includes/applies-to-version/sqlserver2017.md)]

La integración de Python está disponible en SQL Server 2017 y posterior cuando se incluye la opción de Python en una [Instalación de Machine Learning Services (en base de datos)](../install/sql-machine-learning-services-windows-install.md). 

Para desarrollar e implementar soluciones de Python para SQL Server, instale [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) de Microsoft y otras bibliotecas de Python en la estación de trabajo de desarrollo. La biblioteca revoscalepy, que también se encuentra en la instancia de SQL Server remota, coordina las solicitudes de procesamiento entre ambos sistemas. 

En este artículo se aprende a configurar una estación de trabajo de desarrollo de Python que permite interactuar con una instancia de SQL Server remota habilitada para el aprendizaje automático y la integración de Python. Después de realizar los pasos de este artículo, dispondrá de las mismas bibliotecas de Python que en SQL Server. También se sabe cómo enviar procesamientos de inserción desde una sesión de Python local a una sesión remota de Python en SQL Server.

![Componentes de cliente y servidor](media/sqlmls-python-client-revo.png "Sesiones y bibliotecas locales y remotas de Python")

Para validar la instalación, puede usar cuadernos integrados de Jupyter Notebook, como se explica en este artículo, o [vincular las bibliotecas](#install-ide) a PyCharm o a cualquier otro IDE que use normalmente.

> [!Tip]
> Para ver una demostración en vídeo de estos ejercicios, vea [Ejecución remota de R y Python en SQL Server desde cuadernos de Jupyter Notebook](https://youtu.be/D5erljpJDjE).

> [!Note]
> Una alternativa a la instalación de la biblioteca cliente es el uso de un [servidor independiente](../install/sql-machine-learning-standalone-windows-install.md) como cliente enriquecido, lo que algunos clientes prefieren para un trabajo más especializado. Un servidor independiente está totalmente desasociado de SQL Server, pero como tiene las mismas bibliotecas de Python, se puede usar como cliente para el análisis en base de datos de SQL Server. También se puede usar para trabajos no relacionados con SQL, lo que incluye la capacidad de importar y modelar datos de otras plataformas de datos. Si instala un servidor independiente, puede encontrar el archivo ejecutable de Python en esta ubicación: `C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`. Para validar la instalación, [abra un cuaderno de Jupyter](#python-tools) para ejecutar comandos con el archivo Python.exe en esa ubicación.

## <a name="commonly-used-tools"></a>Herramientas de uso común

Tanto si es un desarrollador de Python nuevo en SQL como si es un desarrollador de SQL nuevo en Python y el análisis en base de datos, necesita una herramienta de desarrollo de Python y un editor de consultas de T-SQL como [SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md) para usar todas las capacidades de análisis en base de datos.

Para el desarrollo de Python puede usar cuadernos de Jupyter Notebook, que se incluyen en la distribución de Anaconda instalada por SQL Server. En este artículo se explica cómo iniciar cuadernos de Jupyter Notebook para poder ejecutar el código de Python de forma local y remota en SQL Server.

SSMS es una descarga independiente que resulta útil para crear y ejecutar procedimientos almacenados en SQL Server, incluidos aquellos que contienen código de Python. Prácticamente cualquier código de Python que escriba en cuadernos de Jupyter Notebook se puede insertar en un procedimiento almacenado. Puede ejecutar paso a paso otros inicios rápidos para obtener información sobre [SSMS y Python insertado](../tutorials/quickstart-python-create-script.md).

## <a name="1---install-python-packages"></a>1 - Instalar paquetes de Python

Las estaciones de trabajo locales deben tener las mismas versiones de paquete de Python que las de SQL Server, incluida la distribución base de Anaconda 4.2.0 con Python 3.5.2, y los paquetes específicos de Microsoft.

Un script de instalación agrega tres bibliotecas específicas de Microsoft al cliente de Python. El script instala [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package), que se usa para definir los objetos de origen de datos y el contexto de proceso. Instala [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package), que proporciona algoritmos de aprendizaje automático. También se instala el paquete [azureml](/machine-learning-server/python-reference/azureml-model-management-sdk/azureml-model-management-sdk), pero se aplica a tareas de operatividad asociadas a un contexto de Machine Learning Server independiente (sin instancia) y puede tener un uso limitado en el análisis en base de datos.

1. Descargue un script de instalación.

   + [https://aka.ms/mls-py](https://aka.ms/mls-py) instala la versión 9.2.1 de los paquetes de Python de Microsoft. Esta versión corresponde a una instancia de SQL Server predeterminada. 

   + [https://aka.ms/mls93-py](https://aka.ms/mls93-py) instala la versión 9.3 de los paquetes de Python de Microsoft. Esta versión es una opción mejor si la instancia de SQL Server remota está [enlazada a Machine Learning Server 9.3](../install/upgrade-r-and-python.md).

2. Abra una ventana de PowerShell con permisos de administrador elevados (haga clic con el botón derecho en **Ejecutar como administrador**).

3. Vaya a la carpeta en la que ha descargado el instalador y ejecute el script. Agregue el argumento de línea de comandos `-InstallFolder` para especificar una ubicación de carpeta para las bibliotecas. Por ejemplo: 

   ```python
   cd {{download-directory}}
   .\Install-PyForMLS.ps1 -InstallFolder "C:\path-to-python-for-mls"
   ```

Si omite la carpeta de instalación, el valor predeterminado es C:\Archivos de programa\Microsoft\PyForMLS.

La instalación tarda algún tiempo en completarse. Puede supervisar el progreso en la ventana de PowerShell. Una vez finalizada la instalación, tiene un conjunto completo de paquetes. 

> [!Tip] 
> Se recomienda leer las [Preguntas más frecuentes sobre Python para Windows](https://docs.python.org/3/faq/windows.html) para obtener información general sobre la ejecución de programas de Python en Windows.

## <a name="2---locate-executables"></a>2 - Buscar los archivos ejecutables

Todavía en PowerShell, vea el contenido de la carpeta de instalación para confirmar que se han instalado Python.exe, los scripts y otros paquetes. 

1. Escriba `cd \` para ir a la unidad raíz y luego escriba la ruta de acceso especificada para `-InstallFolder` en el paso anterior. Si ha omitido este parámetro durante la instalación, el valor predeterminado es `cd C:\Program Files\Microsoft\PyForMLS`.

2. Escriba `dir *.exe` para ver los archivos ejecutables. Debería ver **python.exe**, **pythonw.exe** y **uninstall-anaconda.exe**.

   ![Lista de archivos ejecutables de Python](media/powershell-python-exe.png)
   
En los sistemas que tienen varias versiones de Python, no olvide usar este archivo Python.exe concreto si quiere cargar **revoscalepy** y otros paquetes de Microsoft.

> [!Note] 
> El script de instalación no modifica la variable de entorno PATH en el equipo, lo que significa que el nuevo intérprete y los módulos de Python que acaba de instalar no están disponibles automáticamente para otras herramientas que pueda tener. Para obtener ayuda para vincular las bibliotecas y el intérprete de Python a las herramientas, vea [Instalar un IDE](#install-ide).

<a name="python-tools"></a>

## <a name="3---open-jupyter-notebooks"></a>3 - Abrir cuadernos de Jupyter Notebook

Anaconda incluye cuadernos de Jupyter Notebook. Como paso siguiente, cree un cuaderno y ejecute el código de Python que contenga las bibliotecas que acaba de instalar.

1. En el símbolo del sistema de PowerShell, en el directorio C:\Archivos de programa\Microsoft\PyForMLS, abra cuadernos de Jupyter Notebook desde la carpeta Scripts:

   ```powershell
   .\Scripts\jupyter-notebook
   ```

   Debe abrirse un cuaderno en el explorador predeterminado en `https://localhost:8889/tree`.

   Otra manera de empezar es hacer doble clic en **jupyter-notebook.exe**. 

2. Haga clic en **Nuevo** y luego en **Python 3**.

   ![Jupyter Notebook con la selección Nuevo - Python 3](media/jupyter-notebook-new-p3.png)

3. Escriba `import revoscalepy` y ejecute el comando para cargar una de las bibliotecas específicas de Microsoft.

4. Escriba y ejecute `print(revoscalepy.__version__)` para devolver la información de versión. Debería ver 9.2.1 o 9.3.0. Puede usar cualquiera de estas versiones con [revoscalepy en el servidor](../package-management/r-package-information.md).

4. Escriba una serie más compleja de instrucciones. Este ejemplo genera estadísticas de resumen mediante [rx_summary](/machine-learning-server/python-reference/revoscalepy/rx-summary) sobre un conjunto de datos local. Otras funciones obtienen la ubicación de los datos de ejemplo y crean un objeto de origen de datos para un archivo .xdf local.

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

En la captura de pantalla siguiente se muestra la entrada y una parte de la salida, recortada por motivos de brevedad.

  ![Jupyter Notebook con las entradas y la salida de revoscalepy](media/jupyter-notebook-local-revo.png)

## <a name="4---get-sql-permissions"></a>4 - Obtener permisos SQL

Para conectarse a una instancia de SQL Server a fin de ejecutar scripts y cargar datos, debe tener un inicio de sesión válido en el servidor de base de datos. Puede usar un inicio de sesión de SQL o la autenticación integrada de Windows. Por lo general, se recomienda usar la autenticación integrada de Windows, pero el inicio de sesión de SQL es más sencillo en algunos escenarios, especialmente si el script contiene cadenas de conexión a datos externos.

Como mínimo, la cuenta usada para ejecutar código debe tener permiso para leer en las bases de datos con las que se está trabajando, además del permiso especial EXECUTE ANY EXTERNAL SCRIPT. La mayoría de los desarrolladores también necesitan permisos para crear procedimientos almacenados y para escribir datos en tablas que contienen datos de entrenamiento o datos puntuados. 

Pida al administrador de bases de datos que [configure los siguientes permisos para la cuenta](../security/user-permission.md) en la base de datos donde usa Python:

+ **EXECUTE ANY EXTERNAL SCRIPT** para ejecutar Python en el servidor.
+ Privilegios **db_datareader** para ejecutar las consultas usadas para entrenar el modelo.
+ **db_datawriter** para escribir datos de entrenamiento o datos puntuados.
+ **db_owner** para crear objetos como procedimientos almacenados, tablas y funciones. 
  También necesita **db_owner** para crear bases de datos de prueba y ejemplo. 

Si el código requiere paquetes que no se instalan de forma predeterminada con SQL Server, hable con el administrador de bases de datos para que los paquetes se instalen con la instancia. SQL Server es un entorno protegido y hay restricciones sobre la ubicación donde se pueden instalar los paquetes. No se recomienda la instalación ad hoc de paquetes como parte del código, aunque tenga derechos. Además, considere siempre cuidadosamente las implicaciones de seguridad antes de instalar nuevos paquetes en la biblioteca de servidores.


<a name="create-iris-remotely"></a>

## <a name="5---create-test-data"></a>5 - Crear datos de prueba

Si tiene permisos para crear una base de datos en el servidor remoto, puede ejecutar el código siguiente para crear la base de datos de demostración Iris que se usa en los pasos restantes de este artículo.

### <a name="1---create-the-irissql-database-remotely"></a>1 - Crear la base de datos irissql de forma remota

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

### <a name="2---import-iris-sample-from-sklearn"></a>2 - Importar el ejemplo Iris desde SkLearn

```python
from sklearn import datasets
import pandas as pd

# SkLearn has the Iris sample dataset built in to the package
iris = datasets.load_iris()
df = pd.DataFrame(iris.data, columns=iris.feature_names)
```

### <a name="3---use-revoscalepy-apis-to-create-a-table-and-load-the-iris-data"></a>3 - Usar las API de Revoscalepy para crear una tabla y cargar los datos de Iris

```python
from revoscalepy import RxSqlServerData, rx_data_step

# Example of using RX APIs to load data into SQL table. You can also do this with pyodbc
table_ref = RxSqlServerData(connection_string=connection_string.format(new_db_name), table="iris_data")
rx_data_step(input_data = df, output_file = table_ref, overwrite = True)

print("New Table Created: Iris")
print("Sklearn Iris sample loaded into Iris table")
```

## <a name="6---test-remote-connection"></a>6 - Probar la conexión remota

Antes de probar el paso siguiente, asegúrese de que tiene permisos en la instancia de SQL Server y una cadena de conexión a la [base de datos de ejemplo Iris](../tutorials/demo-data-iris-in-sql.md). Si la base de datos no existe y tiene permisos suficientes, puede [crear una base de datos con estas instrucciones en línea](#create-iris-remotely).

Reemplace la cadena de conexión por valores válidos. En el código de ejemplo se usa `"Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"`, pero el código debe especificar un servidor remoto, posiblemente con un nombre de instancia, y una opción de credencial que se asigne al inicio de sesión de usuario de base de datos.

### <a name="define-a-function"></a>Definir una función

En el código siguiente se define una función que se envía a SQL Server en un paso posterior. Cuando se ejecuta, usa los datos y las bibliotecas (revoscalepy, pandas, matplotlib) en el servidor remoto para crear gráficos de dispersión del conjunto de datos Iris. Devuelve la secuencia de bytes del archivo .png a los cuadernos de Jupyter Notebook para que se represente en el explorador.

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

### <a name="send-the-function-to-sql-server"></a>Enviar la función a SQL Server

En este ejemplo, cree el contexto de proceso remoto y luego envíe la ejecución de la función a SQL Server con [rx_exec](/machine-learning-server/python-reference/revoscalepy/rx-exec). La función **rx_exec** es útil porque acepta un contexto de proceso como argumento. Cualquier función que quiera ejecutar de forma remota debe tener un argumento de contexto de proceso. Algunas funciones, como [rx_lin_mod](/machine-learning-server/python-reference/revoscalepy/rx-lin-mod), admiten este argumento directamente. En el caso de las operaciones que no lo hacen, puede usar **rx_exec** para entregar el código en un contexto de proceso remoto.

En este ejemplo no es necesario transferir ningún dato sin procesar desde SQL Server a Jupyter Notebook. Todo el procesamiento se produce en la base de datos Iris y solo el archivo de imagen se devuelve al cliente.

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

En la captura de pantalla siguiente se muestra la entrada y la salida del gráfico de dispersión.

  ![Jupyter Notebook con la salida del gráfico de dispersión](media/jupyter-notebook-scatterplot.png)


<a name="install-ide"></a>

## <a name="7---start-python-from-tools"></a>7 - Iniciar Python desde herramientas

Dado que los desarrolladores suelen trabajar con varias versiones de Python, el programa de instalación no agrega Python a PATH. Para usar el archivo ejecutable y las bibliotecas de Python instalados por el programa de instalación, vincule el IDE a **Python.exe** en la ruta de acceso que también proporciona **revoscalepy** y **microsoftml**. 

### <a name="command-line"></a>Línea de comandos

Al ejecutar **Python.exe** desde C:\Archivos de programa\Microsoft\PyForMLS (o cualquier ubicación especificada para la instalación de la biblioteca cliente de Python), tiene acceso a la distribución completa de Anaconda más los módulos de Python de Microsoft, **revoscalepy** y **microsoftml**.

1. Vaya a C:\Archivos de programa\Microsoft\PyForMLS y haga doble clic en **Python.exe**.
2. Abra la ayuda interactiva: `help()`
3. Escriba el nombre de un módulo en el cuadro de la ayuda: `help> revoscalepy`. La ayuda devuelve el nombre, el contenido del paquete, la versión y la ubicación del archivo.
4. Versión e información del paquete devuelta en el cuadro **ayuda>** : `revoscalepy`. Presione Entrar varias veces para salir de la ayuda.
5. Importe un módulo: `import revoscalepy`


### <a name="jupyter-notebooks"></a>Cuadernos de Jupyter Notebook

En este artículo se usan cuadernos integrados de Jupyter Notebook para mostrar las llamadas de función a **revoscalepy**. Si no está familiarizado con esta herramienta, en la captura de pantalla siguiente se muestra cómo encajan las piezas y por qué todo "simplemente funciona". 

La carpeta principal C:\Archivos de programa\Microsoft\PyForMLS contiene Anaconda más los paquetes de Microsoft. Los cuadernos de Jupyter Notebook se incluyen en Anaconda, en la carpeta Scripts, y los ejecutables de Python se registran automáticamente en Jupyter Notebook. Los paquetes que se encuentran en paquetes del sitio se pueden importar en un cuaderno, incluidos los tres paquetes de Microsoft que se usan para la ciencia de datos y el aprendizaje automático.

  ![Archivos ejecutables y bibliotecas](media/jupyter-notebook-python-registration.png)

Si usa otro IDE, tiene que vincular los ejecutables de Python y las bibliotecas de funciones a la herramienta. En las secciones siguientes se proporcionan instrucciones para herramientas de uso común.

### <a name="visual-studio"></a>Visual Studio

Si tiene [Python en Visual Studio](https://code.visualstudio.com/docs/languages/python), use las siguientes opciones de configuración para crear un entorno de Python que incluya los paquetes de Python de Microsoft.

| Opción de configuración | value |
|-----------------------|-------|
| **Ruta de acceso del prefijo** | C:\Archivos de programa\Microsoft\PyForMLS |
| **Ruta de acceso del intérprete** | C:\Archivos de programa\Microsoft\PyForMLS\python.exe |
| **Intérprete con ventanas** | C:\Archivos de programa\Microsoft\PyForMLS\pythonw.exe |

Para obtener ayuda para configurar un entorno de Python, vea [Administración de entornos de Python en Visual Studio](/visualstudio/python/managing-python-environments-in-visual-studio).

### <a name="pycharm"></a>PyCharm

En PyCharm, establezca el intérprete en el ejecutable de Python instalado por Machine Learning Server.

1. En un nuevo proyecto, en Configuración, haga clic en **Add Local** (Agregar local).

2. Escriba `C:\Program Files\Microsoft\PyForMLS\`.

Ahora puede importar los módulos **revoscalepy**, **microsoftml** o **azureml**. También puede seleccionar **Herramientas** > **Consola de Python** para abrir una ventana interactiva.

## <a name="next-steps"></a>Pasos siguientes

Ahora que tiene herramientas y una conexión operativa a SQL Server, amplíe sus conocimientos mediante la ejecución de los inicios rápidos de Python con [SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md).

> [!div class="nextstepaction"]
> [Inicio rápido: Crear y ejecutar scripts de Python simples con SQL Server Machine Learning Services](../tutorials/quickstart-python-create-script.md)