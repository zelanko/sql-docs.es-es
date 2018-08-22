---
title: Configurar las herramientas de cliente de Python para su uso con SQL Server Machine Learning | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/21/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6f6823870060992586756dffa93aac6937d27d65
ms.sourcegitcommit: 9528843359cc43b9c66afac363f542ae343266e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2018
ms.locfileid: "40401305"
---
# <a name="set-up-python-client-tools-for-use-with-sql-server-machine-learning"></a>Configurar Python en las herramientas de cliente para su uso con SQL Server Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Integración de Python está disponible a partir de SQL Server 2017 o versiones posteriores, cuando se agrega compatibilidad con Python en Machine Learning Services (In-Database). Para obtener más información, consulte [instalar SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md).

En este artículo, obtenga información sobre cómo configurar estaciones de trabajo de desarrollo para que pueda conectarse a un servidor SQL remoto habilitado para Python.

### <a name="evaluation-and-independent-development"></a>Evaluación y desarrollo independiente
 
Si tiene la edición de desarrollador y el plan para trabajar localmente en el script de Python que se va a mover a SQL Server, puede ir directamente a [instalar un IDE](#install-ide) y elija la herramienta de bibliotecas de Python locales utilizadas por SQL Server.

> [!Tip]
> Para obtener una demostración y tutorial en vídeo, consulte [ejecute R y Python de forma remota en SQL Server desde Jupyter Notebooks o cualquier IDE](https://blogs.msdn.microsoft.com/mlserver/2018/07/10/run-r-and-python-remotely-in-sql-server-from-jupyter-notebooks-or-any-ide/) o esto [vídeo de YouTube](https://youtu.be/D5erljpJDjE).

## <a name="1---install-python-packages"></a>1 - instalar paquetes de Python

Las estaciones de trabajo locales deben tener las mismas versiones de paquete de Python como los de SQL Server: revoscalepy y microsftml. Paquetes de Python adicionales están disponibles, pero se usan más habitualmente con otros escenarios en un contexto de Machine Learning Server independiente (que no son de instancia). 

1. Descargar el script de shell de instalación desde [ https://aka.ms/mls93-py ](https://aka.ms/mls93-py) (o use [ https://aka.ms/mls-py ](https://aka.ms/mls-py) para el 9.2. versión). El script instala Anaconda 4.2.0, que incluye Python 3.5.2, junto con todos los paquetes enumerados anteriormente.

  Se proporcionan los componentes de Python a través [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054&clcid=1033). Si necesita una versión diferente, consulte [CAB descargas](../install/sql-ml-cab-downloads.md)

2. Ventana de PowerShell abierta con permisos de administrador con privilegios elevados (haga clic en **ejecutar como administrador**).

3. Vaya a la carpeta donde descargó el programa de instalación y ejecute el script. Agregar el `-InstallFolder` argumento de línea de comandos para especificar una ubicación de carpeta para las bibliotecas. Por ejemplo: 

   ```python
   cd {{download-directory}}
   .\Install-PyForMLS.ps1 -InstallFolder "C:\path-to-python-for-mls")
   ```

   Instalación tarda algún tiempo en completarse. Puede supervisar el progreso en la ventana de PowerShell. Cuando finalice la instalación, tiene un conjunto completo de paquetes. Por ejemplo, si especificó `C:\mspythonlibs` como el nombre de carpeta, encontrará los paquetes en `C:\mspythonlibs\Lib\site-packages`. En caso contrario, la carpeta predeterminada es `C:\Program Files\Microsoft\PyForMLS1`.

El script de instalación no modifica la variable de entorno PATH en el equipo para que el nuevo intérprete de python y que acaba de instalar los módulos no estén disponibles automáticamente a sus herramientas. Para obtener ayuda sobre la vinculación de las bibliotecas y el intérprete de Python con herramientas, consulte [5: instalar un IDE](#install-ide).

<a name="python-tool"></a>
 
## <a name="2---open-a-python-prompt"></a>2 - abra un símbolo del sistema de Python

Integración de Python en Microsoft incluye herramientas integradas y los datos además de las bibliotecas específicas de cada producto, como microsoftml y de revoscalepy. Los siguientes elementos están disponibles en las instancias de cliente y servidor cuando se completa el programa de instalación:

+ Datos de ejemplo de Python
+ Distribución de anaconda 4.2 
+ Pythonw.exe y Python ejecutables python.exe

> [!Tip] 
> Se recomienda la [P+F de Python para Windows](https://docs.python.org/3/faq/windows.html) para obtener información general de purppose sobre la ejecución de programas de Python en Windows.

### <a name="on-client-workstations"></a>En las estaciones de trabajo cliente

Para usar el archivo ejecutable de Python instalado por el script de configuración:

1. Vaya a `C:\Program Files\Microsoft\PyForMLS\python.exe` o cualquier ubicación que eligió para la ruta de instalación.

2. Haga clic en **Python.exe** y seleccione **ejecutar como administrador** para abrir una ventana de línea de comandos interactiva.

### <a name="on-sql-server"></a>En SQL Server

El programa de instalación de SQL Server agrega recursos y herramientas de Python estándares a una instancia del servidor. Si está usando la edición para desarrolladores y desea comprobar la versión de Python o ejecute comandos ad hoc:

1. Vaya al `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`.

2. Haga clic en **Python.exe** y seleccione **ejecutar como administrador** para abrir una ventana de línea de comandos interactiva.

> [!Note]
> Por lo general, para evitar la contención de recursos, se recomienda **no** ejecutar Python desde la biblioteca de instancia en el servidor, si piensa que es posible que la instancia de SQL Server ejecuta código de Python. Sin embargo, podría ser útil si está intentando depurar un problema que se produce sólo cuando se ejecuta en SQL Server y desea ver los mensajes de error más detallados, o asegúrese de que todos los paquetes necesarios están instalados con las herramientas de la biblioteca de la instancia.

## <a name="3---permissions"></a>3 - permisos

Para conectarse a una instancia de SQL Server para ejecutar scripts y cargar los datos, debe tener un inicio de sesión válido en el servidor de base de datos. Puede usar un inicio de sesión de SQL o la autenticación integrada de Windows. Por lo general, se recomienda que utilice la autenticación integrada de Windows, pero usar el inicio de sesión SQL es más fácil para algunos escenarios.

Como mínimo, la cuenta utilizada para ejecutar el código debe tener permiso para leer desde las bases de datos que está trabajando, más el permiso especial EXECUTE ANY EXTERNAL SCRIPT. Mayoría de los desarrolladores también requiere permisos para crear nuevos objetos en forma de procedimientos almacenados que contiene el script y escribe datos en tablas que contienen datos de entrenamiento o puntuar datos. 

Pida al administrador de base de datos para configurar los siguientes permisos para la cuenta, en la base de datos que se usa Python:

+ **EXECUTE ANY EXTERNAL SCRIPT** a ejecutar Python en el servidor.
+ **db_datareader** privilegios para ejecutar las consultas que utilizan para entrenar el modelo.
+ **db_datawriter** para escribir datos con puntuación o datos de entrenamiento.
+ **db_owner** para crear objetos como procedimientos almacenados, tablas, las funciones. 
  También necesita **db_owner** crear bases de datos de ejemplo y prueba. 

Si el código requiere que los paquetes que no se instalan de forma predeterminada con SQL Server, organizar con el Administrador de base de datos para que los paquetes instalados con la instancia. SQL Server es un entorno protegido y hay restricciones en donde se pueden instalar los paquetes. No se recomienda la instalación de paquetes ad hoc como parte del código, incluso si tiene derechos. Además, considere siempre detenidamente las implicaciones de seguridad antes de instalar nuevos paquetes en la biblioteca del servidor.

## <a name="4---test-connections"></a>4 - probar conexiones

Después de instalar todas las herramientas y bibliotecas, debe conectarse al servidor y compruebe que puede crear un contexto de cálculo o que Python puede comunicarse con SQL Server.

### <a name="verify-that-revoscalepy-works-from-the-python-command-line"></a>Compruebe que revoscalepy funciona desde la línea de comandos de Python

Para comprobar que la **revoscalepy** módulo se puede cargar, ejecute el siguiente código de ejemplo desde un símbolo del sistema interactivo de Python. El código genera un resumen de datos con los datos de ejemplo de Python y [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary). 

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

Se imprime la ruta de acceso de datos de ejemplo para que pueda determinar qué instancia de Python se está llamando.

### <a name="verify-that-python-can-be-called-from-a-local-sql-server"></a>Comprobar que Python puede llamarse desde un servidor SQL local

En un entorno de desarrollo local, compruebe que Python se comunica con local [instancia de SQL Server configurada para scripting externo](../install/sql-machine-learning-services-windows-install.md). Usar SQL Server Management Studio para abrir una nueva **consulta** ventana y ejecute cualquier Python simple de comandos en el contexto de un procedimiento almacenado:

```SQL
EXEC sp_execute_external_script @language = N'Python', 
@script = N'print(3+4)'
```

Puede tardar un tiempo para iniciar el tiempo de ejecución de Python por primera vez, pero si no hay ningún error, sabe que funciona el Launchpad de SQL Server, y Python se puede iniciar desde SQL Server.

Para comprobar que **revoscalepy** está disponible en la biblioteca de instancia de SQL Server, ejecute el script según [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary), con algunas pequeñas modificaciones para generar resultados compatibles con SQL Server. 

```SQL
EXEC sp_execute_external_script @language = N'Python', 
@script = N'
import os
from pandas import DataFrame
from revoscalepy import rx_summary
from revoscalepy import RxXdfData
from revoscalepy import RxOptions

sample_data_path = RxOptions.get_option("sampleDataDir")
print(sample_data_path)

ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
summary = rx_summary("ArrDelay + DayOfWeek", ds)
print(summary)
dfsummary = summary.summary_data_frame
OutputDataSet = dfsummary
'
WITH RESULT SETS  ((ColName nvarchar(25) , ColMean float, ColStdDev  float, ColMin  float,   ColMax  float, Col_ValidObs  float, Col_MissingObs int))
```

Dado que rx_summary devuelve un objeto de tipo `class revoscalepy.functions.RxSummary.RxSummaryResults`, que contiene varios elementos, para controlar los resultados en SQL Server, puede extraer la trama de datos en formato tabular.

### <a name="verify-python-execution-in-sql-server-as-remote-compute-context"></a>Comprobar la ejecución de Python en SQL Server como contexto de cálculo remoto

Si ha instalado **revoscalepy** en su entorno de desarrollo de Python local, debe ser capaz de conectarse a una instancia remota de SQL Server 2017 donde se ha habilitado Python y ejecutar un ejemplo de código similar con el servidor como el contexto de proceso. 

Para que ejecutar este script, especifique un nombre de servidor válido y una base de datos existente. Este script no usa la base de datos, pero lo requiere la cadena de conexión.

```Python
import os
from revoscalepy import rx_summary, RxOptions, RxXdfData, RxSqlServerData, RxInSqlServer

# define connection string and compute context
sql_conn_string="Driver=SQL Server;Server=<server-name>;Database=TestDB;Trusted_Connection=True"
sqlcc = RxInSqlServer(
    connection_string = sql_conn_string,
    num_tasks = 1,
    auto_cleanup = False,
    console_output = True,
    execution_timeout_seconds = 0,
    wait = True
    )
rx_set_compute_context(sqlcc)

# get sample data and path
sample_data_path = RxOptions.get_option("sampleDataDir")
print(sample_data_path)

# generate summary
ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
summary = rx_summary("ArrDelay+DayOfWeek", ds)
print(summary)
```

En este ejemplo, se devuelve el objeto de resumen en la consola, en lugar de devolver datos tabulares con formato correcto a SQL Server. 

Además, dado que [rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) ha sido invoca, se cargan los datos de ejemplo desde la carpeta de ejemplos en el equipo de SQL Server y no desde la carpeta de ejemplos local.


<a name="install-ide"></a>

## <a name="5---install-an-ide"></a>5: instalar un IDE

Si simplemente va a depurar secuencias de comandos desde la línea de comandos, puede hacerlo con las herramientas de Python estándar. Sin embargo, si son desarrollar nuevas soluciones o trabajar desde un cliente remoto, se recomienda el uso de un IDE de Python completo. Opciones populares son:

+ [Visual Studio 2017 Community Edition](https://www.visualstudio.com/vs/features/python/) con Python
+ [Visual Studio tools para AI](https://docs.microsoft.com/visualstudio/ai/installation)
+ [Python en Visual Studio Code](https://code.visualstudio.com/docs/languages/python)
+ Herramientas de terceros populares como Eclipse, Spyder y PyCharm

Se recomienda Visual Studio, ya que admite proyectos de base de datos, así como proyectos de aprendizaje automático. Para obtener ayuda acerca de la configuración de un entorno de Python, consulte [entornos administrar Python en Visual Studio](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio).

Porque con frecuencia, los desarrolladores trabajar con varias versiones de Python, el programa de instalación no agrega Python a su ruta de acceso. Para utilizar el archivo ejecutable de Python y el programa de instalación instaladas las bibliotecas de, vincule su IDE para **Python.exe** en la ruta de acceso que proporciona también microsoftml y revoscalepy. Por ejemplo, para un proyecto de Python en Visual Studio, el entorno personalizado especificaría `C:\Program Files\Microsoft\PyForMLS`, `C:\Program Files\Microsoft\PyForMLS\python.exe` y `C:\Program Files\Microsoft\PyForMLS\pythonw.exe` para **ruta del prefijo**, **interpretu**y  **División de particiones intérprete**, respectivamente.

Para obtener más información, consulte [herramientas de Python de vínculo e IDE](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools). El artículo está escrito para Microsoft Machine Learning Server para las rutas de acceso de Python son diferentes, pero le muestra cómo vincular a bibliotecas de Python desde distintas herramientas.

## <a name="next-steps"></a>Pasos siguientes

Ahora que tiene las herramientas y una conexión activa con SQL Server, realice un tutorial para obtener una visión más detallada de las funciones de revoscalepy y cambiar los contextos de cálculo.

> [!div class="nextstepaction"]
> [Crear un modelo usando revoscalepy y un contexto de cálculo remoto](../tutorials/use-python-revoscalepy-to-create-model.md)