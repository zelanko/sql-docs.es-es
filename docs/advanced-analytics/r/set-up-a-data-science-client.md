---
title: Configurar un cliente de ciencia de datos para el desarrollo de R en SQL Server | Microsoft Docs
description: Instalar herramientas y bibliotecas de R locales en una estación de trabajo de desarrollo para las conexiones remotas a SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a88269ff6b55aa473c48cfa0937e926770bbaff1
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2018
ms.locfileid: "49462111"
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>Configurar un cliente de ciencia de datos para el desarrollo de R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Después de haber configurado una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para admitir el aprendizaje automático, debe configurar un entorno de desarrollo de R que sea capaz de conectarse al servidor para la implementación y ejecución remotas.

### <a name="evaluation-and-independent-development"></a>Evaluación y desarrollo independiente
 
Si tiene la edición de desarrollador y el plan para trabajar localmente en el script de R que se va a mover a SQL Server, puede ir directamente a [instalar un IDE](#install-ide) y elija la herramienta de bibliotecas de R locales utilizadas por SQL Server.

> [!Tip]
> Para obtener una demostración y tutorial en vídeo, consulte [ejecute R y Python de forma remota en SQL Server desde Jupyter Notebooks o cualquier IDE](https://blogs.msdn.microsoft.com/mlserver/2018/07/10/run-r-and-python-remotely-in-sql-server-from-jupyter-notebooks-or-any-ide/) o esto [vídeo de YouTube](https://youtu.be/D5erljpJDjE).

## <a name="1---install-r-packages"></a>1 - instalar paquetes de R

Funcionalidad de R en productos de Microsoft es de varias capas. Se comienza con la distribución de Microsoft código abierto de R base, pero, a continuación, se extiende con paquetes específicos de cada producto, tales como [RevoScaleR](revoscaler-overview.md), que habilitan contextos de cálculo remotos y ejecución en paralelo de tareas de R.

Operaciones coordinadas entre un cliente y el servidor remoto requieren ambos sistemas que tienen los mismos paquetes. Para obtener el complemento completo de bibliotecas en una estación de trabajo cliente, instale uno de los paquetes de software en la tabla siguiente. 

| Proveedor de bibliotecas | Uso  |
|------------------|--------------------------------|
| [Cliente de Microsoft R](http://aka.ms/rclient/download) |  Esta descarga gratuita proporciona RevoScaleR, MicrosoftML y otros paquetes de R, pero está limitada a dos subprocesos y datos en memoria. Sin embargo, puede crear soluciones de R que se inician de forma local y desplazar la ejecución (denominados *contexto de proceso*) para acceder a los datos y la potencia de cálculo de una instancia remota de SQL Server. Este es el enfoque recomendado para la integración de cliente con una instancia de SQL Server de producción. Para obtener más información sobre esta herramienta, consulte [¿qué es Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client).|
| Servidores independientes | En **características compartidas**, el programa de instalación de SQL Server incluye opciones de instalación de servidor independiente para el aprendizaje automático de SQL Server 2016 R Services y SQL Server 2017. Estos son los servidores completos, que se separa por completo de SQL Server, con la capacidad de conectarse y consumir datos desde varias plataformas de datos. Pero se podría usar el software en una capacidad de cliente para tener acceso a la instancia del motor de base de datos de SQL Server ejecuta tareas de R y Python. [SQL Server 2017 Machine Learning Server (independiente)](../install/sql-machine-learning-standalone-windows-install.md) tiene las mismas bibliotecas como una instancia de SQL Server 2017 machine learning. [SQL Server 2016 R Server (independiente)](../install/sql-r-standalone-windows-install.md) tiene las mismas bibliotecas de SQL Server 2016 R Services. |


<a name="r-tool"></a>
 
## <a name="2---open-an-r-prompt"></a>2 - abra un símbolo del sistema de R

Cuando se instala R con SQL Server, obtendrá las mismas herramientas de R que son estándar para cualquier instalación de base de R, como RGui, Rterm y así sucesivamente. Estas herramientas son ligeras y útil para comprobar la información de paquete y la biblioteca, ejecute comandos ad hoc o secuencia de comandos o ejecución paso a paso a través de tutoriales. Puede usar estas herramientas para obtener información sobre la versión de R y confirmar la conectividad.

Para usar la versión de R instalado con SQL Server o cliente de R, abra un símbolo del sistema de R desde la carpeta del programa cliente de R o SQL Server. Los pasos siguientes son para el cliente de R y RGui.exe.

1. Para R Client, vaya a `~\Program Files\Microsoft\R Client\R_SERVER\bin\x64`.
2. Haga doble clic en **RGui.exe** para iniciar una sesión de R con un símbolo del sistema de R.

Cuando se inicia una sesión de R desde una carpeta de programas de Microsoft, varios paquetes, incluidos RevoScaleR, se cargan automáticamente. Escriba **search()** en el símbolo del sistema de R para la confirmación.

   ![Información de versión al cargar R](../install/media/rclient-rgui-r-prompt.png "abra un símbolo del sistema de R")

### <a name="tool-list-and-location"></a>Ubicación y la lista de herramientas

| Herramienta | Descripción | 
|------|-------------|
| **RTerm**: | Un terminal de línea de comandos para ejecutar scripts de R | 
| **RGui.exe** | Un sencillo editor interactivo para R. Los argumentos de línea de comandos son los mismos en RGui.exe y en RTerm. |
| **RScript** | Una herramienta de línea de comandos para ejecutar scripts de R en modo por lotes. |

Las herramientas se encuentran en **bin** carpeta para R base como instalado SQL Server o cliente de R. Las rutas de acceso siguientes son las ubicaciones válidas de las herramientas, dependiendo de qué versión del producto y la característica se ha instalado:

| Producto de Microsoft | Ubicación de la herramienta de R |
|-------------------|-----------------|
| Cliente de Microsoft R | `~\Program Files\Microsoft\R Client\R_SERVER\bin\x64` |
| Microsoft Machine Learning (R) Server | `~\Program Files\Microsoft\R_SERVER\bin\x64`
| SQL Server 2016 R Services | `~\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64`|
| Servidor independiente SQL Server 2016 R | `~\Program Files\Microsoft SQL Server\130\R_SERVER\bin\x64` 
| SQL Server 2017 Machine Learning Services (R) | `~\Program Files\Microsoft SQL Server\MSSQL14.<instancename>\R_SERVICES\bin\x64`|
| Servidor independiente SQL Server 2017 Machine Learning (R) | `~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64` |

## <a name="3---permissions"></a>3 - permisos

Para conectarse a una instancia de SQL Server para ejecutar scripts y cargar los datos, debe tener un inicio de sesión válido en el servidor de base de datos. Puede usar un inicio de sesión de SQL o la autenticación integrada de Windows. Por lo general, se recomienda que utilice la autenticación integrada de Windows, pero usar el inicio de sesión SQL es más fácil para algunos escenarios.

Como mínimo, la cuenta utilizada para ejecutar el código debe tener permiso para leer desde las bases de datos que está trabajando, más el permiso especial EXECUTE ANY EXTERNAL SCRIPT. Mayoría de los desarrolladores también requiere permisos para crear nuevos objetos en forma de procedimientos almacenados que contiene el script y escribe datos en tablas que contienen datos de entrenamiento o puntuar datos. 

Pida al administrador de base de datos para configurar los siguientes permisos para la cuenta, en la base de datos donde se utilice R:

+ **EXECUTE ANY EXTERNAL SCRIPT** ejecutar R en el servidor.
+ **db_datareader** privilegios para ejecutar las consultas que utilizan para entrenar el modelo.
+ **db_datawriter** para escribir datos con puntuación o datos de entrenamiento.
+ **db_owner** para crear objetos como procedimientos almacenados, tablas, las funciones. 
  También necesita **db_owner** crear bases de datos de ejemplo y prueba. 

Si el código requiere que los paquetes que no se instalan de forma predeterminada con SQL Server, organizar con el Administrador de base de datos para que los paquetes instalados con la instancia. SQL Server es un entorno protegido y hay restricciones en donde se pueden instalar los paquetes. No se recomienda la instalación de paquetes ad hoc como parte del código, incluso si tiene derechos. Además, considere siempre detenidamente las implicaciones de seguridad antes de instalar nuevos paquetes en la biblioteca del servidor.

> [!Tip]
> Si no está familiarizado con SQL Server y trabajar en un entorno de desarrollo local, puede realizar este tutorial para obtener información sobre los inicios de sesión y establecimiento de permisos: [profundizar en RevoScaleR](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)

## <a name="4---test-connections"></a>4 - probar conexiones

SQL Server debe habilitarse para [conexiones remotas](https://docs.microsoft.com/sql/database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md) y debe tener permisos, incluido un inicio de sesión de usuario y para conectarse a una base de datos. Los siguientes pasos supone que la base de datos de demostración, [NYCTaxi_Sample](../tutorials/demo-data-nyctaxi-in-sql.md) y la autenticación de Windows.

 Como paso de verificación, utilice una herramienta integrada y RevoScaleR para confirmar la conectividad al servidor remoto.

1. Empiece por [abriendo una herramienta de R](#r-tool) en la estación de trabajo cliente. RevoScaleR carga automáticamente. Por ejemplo, vaya a `~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64` y haga doble clic en **RGui.exe** para iniciarlo.

2. Confirmar que revoscaler está operativo, ejecute este comando, que devuelve un resumen estadístico de un conjunto de datos de demostración. Asegúrese de que proporcionar un nombre de servidor válido para la instancia del motor de base de datos de SQL Server.

```r
connStr <- "Driver=SQL Server;Server=<your-server-name>;Database=NYCTaxi_Sample;Trusted_Connection=true"
testQuery <-"SELECT DISTINCT TOP(100) tip_amount FROM [dbo].nyctaxi_sample ORDER BY tip_amount DESC;"
cc <-RxInSqlServer(connectionString=connStr)
rxSummary(formula = ~ ., data = RxSqlServerData(sqlQuery=testQuery, connectionString=connStr), computeContext=cc)
```
Este script se conecta a una base de datos en el servidor remoto, proporciona una consulta, se crea un contexto de proceso `cc` instrucciones para la ejecución remota de código, a continuación, proporciona la función RevoScaleR **rxSummary** para devolver una estadística Resumen de los resultados de consulta.

<a name="install-ide"></a>

## <a name="5---install-an-ide"></a>5: instalar un IDE

Para los proyectos de desarrollo constante y graves, debe instalar un entorno de desarrollo integrado (IDE). Herramientas de SQL Server y las herramientas integradas de R no están equipadas para el desarrollo de R pesado. Una vez que el código de trabajo, puede implementarlo como un procedimiento almacenado para su ejecución en SQL Server.

Debe apuntar el IDE para las bibliotecas de R locales: base de R, RevoScaleR y así sucesivamente. Ejecutar cargas de trabajo en un servidor SQL remoto se produce durante la ejecución del script, cuando la secuencia de comandos invoca un contexto de proceso remoto en SQL Server, acceso a datos y las operaciones en ese servidor.

### <a name="rstudio"></a>RStudio

Cuando se usa [RStudio](https://www.rstudio.com/), puede configurar el entorno para usar las bibliotecas de R y los archivos ejecutables que corresponden a los que están en un servidor SQL remoto.

1. Compruebe las versiones de paquete de R instaladas en SQL Server. Para obtener más información, consulte [información del paquete de R obtener](determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location).

1. Instalar Microsoft R Client o una de las opciones de servidor independientes para agregar RevoScaleR y otros paquetes de R, incluida la distribución de R base utilizada por la instancia de SQL Server. Elegir una versión al mismo nivel o inferior (paquetes son compatibles con versiones anteriores) que proporciona las mismas versiones de paquete como los del servidor. Para obtener información de versión, consulte la versión de mapa en este artículo: [actualizar R y Python componentes](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

1. En RStudio, [actualizar su ruta de acceso de R](https://support.rstudio.com/hc/articles/200486138-Using-Different-Versions-of-R) hacia el entorno de R que proporciona RevoScaleR, Microsoft R Open y otros paquetes de Microsoft. Según cómo haya obtenido RevoScaleR y otras bibliotecas, es probablemente una de las rutas de acceso siguientes:

  + C:\Program Files\Microsoft SQL Server\130\R_SERVER\Library
  + C:\Program Files\Microsoft SQL Server\140\R_SERVER\Library
  + C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64

### <a name="r-tools-for-visual-studio-rtvs"></a>Herramientas de R para Visual Studio (RTVS)

Si no tiene ya un IDE que prefiera para R, se recomienda **R Tools para Visual Studio**.

+ [Descargar herramientas de R para Visual Studio (RTVS)](https://visualstudio.microsoft.com/vs/features/rtvs/)
+ [Instrucciones de instalación](https://docs.microsoft.com/visualstudio/rtvs/installing-r-tools-for-visual-studio) -RTVS está disponible en varias versiones de Visual Studio.
+ [Introducción a las herramientas de R para Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r)

### <a name="connect-to-sql-server-from-rtvs"></a>Conectarse a SQL Server de RTVS

Este ejemplo usa Visual Studio 2017 Community Edition, con la carga de trabajo de ciencia de datos instalado.

1. Desde el **archivo** menú, seleccione **New** y, a continuación, seleccione **proyecto**.

2. El panel izquierdo contiene una lista de plantillas preinstaladas. Haga clic en **R**y seleccione **R proyecto**. En el **nombre** , escriba `dbtest` y haga clic en **Aceptar**. 

  Visual Studio crea una nueva carpeta de proyecto y un archivo de script predeterminado, `Script.R`. 

3. Tipo `.libPaths()` en la primera línea del script de archivo y, a continuación, presione CTRL + ENTRAR.

  La ruta de acceso de biblioteca de R actual se debe mostrar en el **R interactivo** ventana. 

4. Haga clic en el **herramientas de R** menú y seleccione **Windows** para ver una lista de otras ventanas específicas de R que se pueden mostrar en el área de trabajo.
 
    + Ver la ayuda sobre los paquetes en la biblioteca actual, presione CTRL + 3.
    + Consulte las variables de R en el **Explorador de variables**, presionando CTRL + 8.

5. Crear una cadena de conexión a una instancia de SQL Server y usar la cadena de conexión en el constructor RxInSqlServer para crear un objeto de origen de datos de SQL Server. 

    ```r
    connStr <- "Driver=SQL Server;Server=MyServer;Database=MyTestDB;Uid=;Pwd="
    sqlShareDir <- paste("C:\\AllShare\\", Sys.getenv("USERNAME"), sep = "")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    cc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    sampleDataQuery <- "SELECT TOP 100 * from [dbo].[MyTestTable]"
    inDataSource <- RxSqlServerData(sqlQuery = sampleDataQuery, connectionString = connStr, rowsPerRead = 500)
    ```
    > [!TIP]
    > Para ejecutar un lote, seleccione las líneas que desea ejecutar y presionar CTRL + ENTRAR.

6. Establece el contexto de cálculo en el servidor y, a continuación, ejecutar código R sencillo en los datos.

    ```r
    rxSetComputeContext(cc)
    rxGetVarInfo(data = inDataSource)
    ```

    Los resultados se devuelven en el **R interactivo** ventana.
    
    Si desea asegurarse de que se está ejecutando el código en la instancia de SQL Server, puede usar para crear un seguimiento de Profiler.

## <a name="next-steps"></a>Pasos siguientes

Dos tutoriales diferentes incluyen ejercicios para que puede poner en práctica de cambiar el contexto de proceso desde local a una instancia remota de SQL Server.

+ [Tutorial: Funciones de uso RevoScaleR R con datos de SQL Server](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [Tutorial integral de ciencia de datos](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)