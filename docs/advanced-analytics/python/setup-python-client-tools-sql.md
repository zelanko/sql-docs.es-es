---
title: Configurar las herramientas de cliente de Python para su uso con aprendizaje automático de SQL Server | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: ace5ea536c020d2713f1aa07bd1b26c41065a587
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
ms.locfileid: "31203807"
---
# <a name="set-up-python-client-tools-for-use-with-sql-server-machine-learning"></a>Configurar Python herramientas de cliente para su uso con aprendizaje automático de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe cómo configurar un entorno de Python en un equipo de Windows para admitir la ejecución de código de Python en SQL Server. Esto incluye los siguientes escenarios:

+ Probar y desarrollar soluciones en una estación de trabajo remota de Python y enviar código a SQL Server para la ejecución en un contexto de proceso de SQL Server. 

    Por lo general, va a instalar un entorno de desarrollo de Python completa. 
    
    El entorno de Python local debe ser compatible con el entorno de Python en la instancia de SQL Server, y debe instalar las bibliotecas que admiten los contextos de proceso remoto.

+ Desarrollar y probar el código con herramientas de Python dedicados y, a continuación, migrar el código con SQL Server para ejecutar un procedimiento almacenado.

    Utilice un IDE de Python completa para el desarrollo, desactivar servidor. Sin embargo, antes de implementar el código, probarlo en un entorno que emula el entorno de SQL Server.

+ Código de Python se ejecuta principalmente en un procedimiento almacenado en SQL Server y no desarrollar código Python. Se espera que el código se ha probado y depurado antes de ajustar en un procedimiento almacenado. Sin embargo, en ocasiones tendrá que ejecutar el código fuera de SQL Server, para determinar el origen de un problema.

    No desea volver a instalar las herramientas de Python en el servidor y utiliza únicamente las herramientas de predeterminado instaladas con la distribución. Puede configurar un entorno de Python que utiliza la biblioteca de la instancia, para comprobar que el código funciona fuera de un procedimiento almacenado.

## <a name="requirements"></a>Requisitos

Independientemente de las herramientas que se utiliza para desarrollar el código Python, los siguientes requisitos se aplican siempre que se ejecute código de Python en SQL Server o utilizan datos de SQL Server:

+ Para usar Python, se requiere SQL Server 2017 o una versión posterior. Debe instalar la característica que admite servicios de aprendizaje de máquina (en bases de datos) y habilitar explícitamente la característica. Para obtener más información, consulte [configurar SQL Server 2017](../r/set-up-sql-server-r-services-in-database.md).

    Si ha instalado una versión preliminar de SQL Server 2017, podría obtener errores si intenta ejecutar comandos de Python desde esta utilidad de línea de comandos. Se recomienda [actualizar a la versión más reciente](#bkmk_update) si es posible. 

+ Debe asegurarse de que la cuenta que utilice para ejecutar el código tiene permiso para conectarse a la base de datos y ejecutar código Python. El permiso especial `EXECUTE ANY EXTERNAL SCRIPT` es necesario para todas las cuentas que usan el script de R o Python. 

+ Debe asegurarse de que la cuenta tiene los permisos de base de datos que podrían ser necesarios para leer los datos o crear objetos nuevos. 

+ Si el código requiere que los paquetes que no se instalan de forma predeterminada con SQL Server, organizar con el Administrador de base de datos para que los paquetes instalados en el entorno de Python que se usa por la instancia. SQL Server es un entorno protegido y hay restricciones en donde se pueden instalar paquetes. 

    No se recomienda la instalación de ad hoc de paquetes como parte del código, incluso si dispone de derechos. Además, siempre tenga en cuenta las implicaciones de seguridad antes de instalar nuevos paquetes de la biblioteca del servidor.

> [!NOTE]
> Si va a usar Python con el servidor de aprendizaje de máquina, que es compatible con contextos de proceso adicionales, como los clústeres de Linux o Spark, vea estos artículos:
> 
> + [Cómo instalar el intérprete y paquetes Python personalizados localmente en Windows](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)
> + [Herramientas de Python de vínculo e IDE al intérprete de Python instalado con el servidor de aprendizaje de máquina](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)

## <a name="default-tools-included-with-standard-install"></a>Herramientas predeterminadas incluidas con la instalación estándar

Una instalación predeterminada de SQL Server 2017 con servicios de aprendizaje de máquina (en bases de datos) y Python agrega las siguientes herramientas estándares de Python y recursos:

+ Datos de ejemplo de Python
+ Distribución de anaconda 4.2 
+ Pythonw.exe y Python ejecutables python.exe

De forma predeterminada, la instalación consiste en esta carpeta: `~\Program Files\Microsoft SQL Server\<instance_name>\PYTHON_SERVICES`. 

## <a name="open-python-from-the-command-line"></a>Abrir Python desde la línea de comandos 

Para utilizar el tiempo de ejecución de Python que se instala con la instancia, puede iniciar la versión de Python ejecutable desde la ruta de instalación. Instrucciones básicas están disponibles en la [Python para Windows preguntas más frecuentes sobre](https://docs.python.org/3/faq/windows.html).

> [!IMPORTANT]
> Por lo general, para evitar la contención de recursos, se recomienda **no** ejecutar Python desde la biblioteca de la instancia en el servidor, si cree que es posible que la instancia de SQL Server ejecuta código Python. Sin embargo, con las herramientas de la biblioteca de la instancia puede ser útil si está intentando depurar un problema que se produce solo cuando se ejecuta en SQL Server y desea ver los mensajes de error más detallados, o asegúrese de que todos los paquetes necesarios están instalados.

1. Navegue hasta la carpeta donde está instalada la biblioteca de la instancia. Por ejemplo, en una instalación predeterminada, la carpeta es `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`.

2. Busque Python.exe. 

3. Haga clic en y seleccione **ejecutar como administrador** para abrir una ventana de línea de comandos interactiva.

## <a name="bkmk_update"></a> Actualizar componentes de Python

Puede actualizar los componentes de Python, descargue e instale una versión más reciente, con la secuencia de comandos se describe aquí: [cliente instalar Python en Windows](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter#install-on-windows)
> 
> El instalador descargado por la secuencia de comandos está [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054&clcid=1033). Si tiene una versión diferente, consulte [instalación de componentes de aprendizaje de máquina sin acceso a internet](http://bing.com)

## <a name="set-up-a-python-development-environment"></a>Configurar un entorno de desarrollo de Python

Si simplemente está depurando los scripts desde la línea de comandos, puede obtener con las herramientas estándares de Python instaladas con los servicios de aprendizaje de máquina, o utilice un editor de texto. Sin embargo, si está desarrollando nuevas soluciones o trabajar desde un cliente remoto, te recomendamos que uses un IDE de Python con todas las características de. Opciones conocidas son:

+ [Visual Studio 2017 Community Edition](https://www.visualstudio.com/vs/features/python/) con Python
+ [Herramientas de AI para Visual Studio](https://docs.microsoft.com/visualstudio/ai/installation)
+ [Python en el código de Visual Studio](https://code.visualstudio.com/docs/languages/python)
+ Herramientas de terceros populares, como PyCharm y Spyder, Eclipse

Se recomienda Visual Studio, ya que admite proyectos de base de datos, así como proyectos de aprendizaje de máquina. Para obtener ayuda acerca de la configuración de un entorno de Python, consulte [entornos de Python de administrar en Visual Studio](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio)

## <a name="install-revoscalepy"></a>Instalar revoscalepy

Incluso si se han instalado correctamente Servicios de aprendizaje de máquina, puede obtener un error al intentar cargar **revoscalepy** funciones desde una línea de comandos de Python. Estos pasos describe cómo puede instalar una actualización para habilitar el uso de **revoscalepy**.

1. Descargar el script de shell de instalación de https://aka.ms/mls93-py (o use https://aka.ms/mls-py para el 9.2. versión). La secuencia de comandos instala Anaconda 4.2.0, que incluye Python 3.5.2, junto con todos los paquetes enumerados anteriormente.

2. Abra una nueva ventana de PowerShell con permisos elevados (como administrador).

3. Abra la carpeta en la que descargó el programa de instalación y ejecute la secuencia de comandos:

```ps1
cd {{download-directory}}
.\Install-PyForMLS.ps1
```

También puede ejecutar el `-InstallFolder` argumento de línea de comandos y especificar la nueva ruta de acceso como parte del comando. Por ejemplo: 

```ps1
.\Install-PyForMLS.ps1 -InstallFolder "<installation_path>")
```

Si se produce un error, debe suspender las directivas de ejecución para un archivo específico, la duración de la sesión, como se indica a continuación: 

```ps1
powershell -ExecutionPolicy Bypass -File "C:\<installation_path>\Install-PyForMLS.ps1"
```

También puede suspender las directivas de ejecución para la duración de la sesión. Con esta declaración, la directiva de ejecución se establece en `Unrestricted` para la duración de la sesión y no cambia la configuración ni escribir el cambio en el disco.

```ps1
Set-ExecutionPolicy Bypass -Scope Process
```

## <a name="verify-that-python-and-revoscalepy-are-working"></a>Compruebe que están trabajando Python y revoscalepy

Después de instalar todas las herramientas y bibliotecas, debe conectarse al servidor y compruebe que puede crear un contexto de proceso, o que Python puede comunicar con SQL Server.

### <a name="verify-that-revoscalepy-works-from-the-python-command-line"></a>Compruebe que revoscalepy funciona desde la línea de comandos de Python

Para comprobar que la **revoscalepy** módulo se puede cargar, ejecute el siguiente código de ejemplo desde un símbolo del sistema interactivo de Python. El código genera un resumen de datos utilizando los datos de ejemplo de Python y [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary). 

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

Se imprime la ruta de acceso de datos de ejemplo para que pueda determinar qué instancia de Python se llama.

### <a name="verify-that-python-can-be-called-from-sql-server"></a>Compruebe que se puede llamar Python desde SQL Server

Para comprobar que Python se comunica con SQL Server, abra SQL Server Management Studio. (Puede usar otra herramienta similar, como [SQL operaciones Studio](https://docs.microsoft.com/sql/sql-operations-studio/what-is).) Abra una nueva **consulta** ventana y ejecutar cualquier Python simple de comandos en el contexto de un procedimiento almacenado:

```SQL
EXEC sp_execute_external_script @language = N'Python', 
@script = N'print(3+4)'
```

Puede tardar un tiempo para iniciar el tiempo de ejecución de Python por primera vez, pero si no hay ningún error, sabe que funciona el Launchpad de SQL Server y Python se puede iniciar desde SQL Server.

Para comprobar que **revoscalepy** está disponible en la biblioteca de instancia de SQL Server, ejecute el script basado en [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary), con algunas pequeñas modificaciones para generar resultados compatibles con SQL Server. 

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

### <a name="verify-python-execution-in-sql-server-as-remote-compute-context"></a>Comprobar la ejecución de Python en SQL Server como contexto de proceso remoto.

Si ha instalado **revoscalepy** en su entorno de desarrollo local de Python, debe poder conectarse a una instancia de SQL Server 2017 donde se ha habilitado Python y ejecutar un ejemplo de código similar que utiliza el servidor como el proceso contexto. 


```Python
import os
from revoscalepy import rx_summary, RxOptions, RxXdfData, RxSqlServerData, RxInSqlServer

# define connection string and compute context
sql_conn_string="Driver=SQL Server;Server=;Database=TestDB;Trusted_Connection=True"
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

En este ejemplo, se devuelve el objeto de resumen para la consola, en lugar de devolver datos tabulares correctos a SQL Server. 

Además, dado que [rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) ha sido invoca, se cargan los datos de ejemplo desde la carpeta de ejemplos en el equipo de SQL Server y no desde la carpeta de ejemplos local.
