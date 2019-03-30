---
title: Configurar un cliente de ciencia de datos para el desarrollo de R - SQL Server Machine Learning Services
description: Instalar herramientas y bibliotecas de R locales en una estación de trabajo de desarrollo para las conexiones remotas a SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: b46ce112af08fca4c8986be51ba11a15d277fb4f
ms.sourcegitcommit: c60784d1099875a865fd37af2fb9b0414a8c9550
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2019
ms.locfileid: "58645537"
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>Configurar un cliente de ciencia de datos para el desarrollo de R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Integración de R está disponible en SQL Server 2016 o posterior al incluir la opción de lenguaje R en un [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) o [SQL Server 2017 Machine Learning Services (In-Database)](../install/sql-machine-learning-services-windows-install.md) instalación. 

Para desarrollar e implementar soluciones de R para SQL Server, instale [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) en su estación de trabajo de desarrollo para obtener [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) y otras bibliotecas de R. La biblioteca RevoScaleR, que también se requiere en la instancia remota de SQL Server, coordina las solicitudes de computación entre ambos sistemas. 

En este artículo, obtenga información sobre cómo configurar una estación de trabajo de desarrollo de cliente de R para que puedan interactuar con un servidor SQL remoto habilitado para aprendizaje automático e integración de R. Después de completar los pasos descritos en este artículo, tendrá las mismas bibliotecas de R como los de SQL Server. También sabe cómo insertar cálculos en una sesión de R local a una sesión remota de R en SQL Server.

![Componentes de cliente / servidor](media/sqlmls-r-client-revo.png "bibliotecas y las sesiones de R Local y remotas")

Para validar la instalación, puede usar integrada **RGUI** herramienta tal como se describe en este artículo, o [vincular las bibliotecas](#install-ide) a RStudio o cualquier otro IDE que suela usar.

> [!Note]
> Una alternativa a la instalación de la biblioteca de cliente está usando un [servidor independiente](../install/sql-machine-learning-standalone-windows-install.md) como un cliente enriquecido, que algunos clientes prefieren para el trabajo de escenario más profundo. Un servidor independiente se separa por completo de SQL Server, pero porque tiene las mismas bibliotecas de R, puede usar como un cliente para el análisis en bases de datos de SQL Server. También puede usar para el trabajo no relacionados con SQL, incluida la capacidad para importar y modelar datos desde otras plataformas de datos. Si instala un servidor independiente, puede encontrar el archivo ejecutable de R en esta ubicación: `C:\Program Files\Microsoft SQL Server\140\R_SERVER`. Para validar la instalación, [abrir una aplicación de consola de R](#R-tools) para ejecutar comandos con el R.exe en esa ubicación.

## <a name="commonly-used-tools"></a>Herramientas utilizadas habitualmente

Tanto si es un desarrollador de R es nuevo en SQL o un desarrollador SQL nuevo para R y análisis en bases de datos, necesitará una herramienta de desarrollo de R y un editor de consultas de T-SQL como [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) para ejecutar todos los capacidades de análisis en bases de datos.

Para escenarios de desarrollo de R sencillos, puede usar el ejecutable, RGUI agrupados en la distribución básica de R en MRO y SQL Server. Este artículo explica cómo usar RGUI para las sesiones de R locales y remotas. Para mejorar la productividad, debe usar un IDE completo, como [RStudio o Visual Studio](#install-ide).

SSMS es una descarga independiente, útil para crear y ejecutar procedimientos almacenados en SQL Server, incluidas aquéllas que contienen código de R. Casi cualquier código de R que se escribe en un entorno de desarrollo se puede incrustar en un procedimiento almacenado. Puede ejecutar paso a paso a través de otros tutoriales para obtener información sobre [SSMS y R incrustado](../tutorials/sqldev-in-database-r-for-sql-developers.md).

## <a name="1---install-r-packages"></a>1 - instalar paquetes de R

Paquetes de R de Microsoft están disponibles en varios productos y servicios. En una estación de trabajo local, se recomienda instalar Microsoft R Client. R Client proporciona [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler), [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package), [SQLRUtils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)y otros paquetes de R.

1. [Descargar Microsoft R Client](https://aka.ms/rclient/download).

2. En el Asistente para la instalación, acepte o cambie la ruta de instalación predeterminada, acepte o cambie la lista de componentes y acepte los términos de licencia de Microsoft R Client.

  Cuando finalice la instalación, una pantalla de bienvenida presenta el producto y la documentación.

3. Cree una variable de entorno del sistema MKL_CBWR para garantizar resultados coherentes en los cálculos de Intel Math Kernel Library (MKL).

  + En el Panel de Control, haga clic en **sistema y seguridad** > **sistema** > **configuración avanzada del sistema**  >   **Las Variables de entorno**.
  + Crear una nueva variable del sistema denominada **MKL_CBWR**, con un valor establecido en **automática**.

## <a name="2---locate-executables"></a>2: buscar archivos ejecutables

Buscar y mostrar el contenido de la carpeta de instalación para confirmar que están instalados R.exe, RGUI y otros paquetes. 

1. En el Explorador de archivos, abra la carpeta C:\Program Files\Microsoft\R Client\R_SERVER\bin para confirmar la ubicación de R.exe.

2. Abrir el x64 subcarpeta para confirmar **RGUI**. Usará esta herramienta en el paso siguiente.

3. Abra C:\Program Files\Microsoft\R Client\R_SERVER\library para revisar la lista de paquetes instalados con R Client, incluidos RevoScaleR, MicrosoftML y otros.


<a name="R-tools"></a>
 
## <a name="3---start-rgui"></a>3 - inicio RGUI

Cuando se instala R con SQL Server, obtendrá las mismas herramientas de R que son estándar para cualquier instalación de base de R, como RGui, Rterm y así sucesivamente. Estas herramientas son ligeras y útil para comprobar la información de paquete y la biblioteca, ejecute comandos ad hoc o secuencia de comandos o ejecución paso a paso a través de tutoriales. Puede usar estas herramientas para obtener información sobre la versión de R y confirmar la conectividad.

1. Abra C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64 y haga doble clic en **RGui** para iniciar una sesión de R con un símbolo del sistema de R.

  Cuando se inicia una sesión de R desde una carpeta de programas de Microsoft, varios paquetes, incluidos RevoScaleR, se cargan automáticamente. 

2. Escriba `print(Revo.version)` en el símbolo del sistema para devolver RevoScaleR información de versión del paquete. Debe tener la versión 9.2.1 o 9.3.0 para RevoScaleR.

3. Escriba **search()** en el símbolo del sistema de R para obtener una lista de los paquetes instalados.

   ![Información de versión al cargar R](../install/media/rclient-rgui-r-prompt.png "abra un símbolo del sistema de R")


## <a name="4---get-sql-permissions"></a>4 - obtener permisos de SQL

En el cliente de R, procesamiento de R está limitado a dos subprocesos y datos en memoria. Para el procesamiento escalable con varios núcleos y grandes conjuntos de datos, puede desplazar la ejecución (denominados *contexto de proceso*) para los conjuntos de datos y la potencia de cálculo de una instancia remota de SQL Server. Este es el enfoque recomendado para la integración de cliente con una instancia de SQL Server de producción, y tendrá permisos y la información de conexión para que funcione.

Para conectarse a una instancia de SQL Server para ejecutar scripts y cargar los datos, debe tener un inicio de sesión válido en el servidor de base de datos. Puede usar un inicio de sesión de SQL o la autenticación integrada de Windows. Por lo general, se recomienda que utilice la autenticación integrada de Windows, pero usar el inicio de sesión SQL es más fácil para algunos escenarios, especialmente cuando el script contiene las cadenas de conexión a datos externos.

Como mínimo, la cuenta utilizada para ejecutar el código debe tener permiso para leer desde las bases de datos que está trabajando, más el permiso especial EXECUTE ANY EXTERNAL SCRIPT. Mayoría de los desarrolladores también requiere permisos para crear procedimientos almacenados y para escribir datos en tablas que contienen datos de entrenamiento o puntuación datos. 

Pida al administrador de base de datos que [configurar los siguientes permisos para la cuenta](../security/user-permission.md), en la base de datos donde se utilice R:

+ **EXECUTE ANY EXTERNAL SCRIPT** para ejecutar el script de R en el servidor.
+ **db_datareader** privilegios para ejecutar las consultas que utilizan para entrenar el modelo.
+ **db_datawriter** para escribir datos con puntuación o datos de entrenamiento.
+ **db_owner** para crear objetos como procedimientos almacenados, tablas, las funciones. 
  También necesita **db_owner** crear bases de datos de ejemplo y prueba. 

Si el código requiere que los paquetes que no se instalan de forma predeterminada con SQL Server, organizar con el Administrador de base de datos para que los paquetes instalados con la instancia. SQL Server es un entorno protegido y hay restricciones en donde se pueden instalar los paquetes. Para obtener más información, consulte [instalar nuevos paquetes de R en SQL Server](install-additional-r-packages-on-sql-server.md).

## <a name="5---test-connections"></a>5 - probar conexiones

 Como paso de verificación, utilice **RGUI** y RevoScaleR para confirmar la conectividad al servidor remoto. SQL Server debe habilitarse para [conexiones remotas](https://docs.microsoft.com/sql/database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server) y debe tener permisos, incluido un inicio de sesión de usuario y para conectarse a una base de datos. 

Los siguientes pasos supone que la base de datos de demostración, [NYCTaxi_Sample](../tutorials/demo-data-nyctaxi-in-sql.md)y la autenticación de Windows.

1. Abra **RGUI** en la estación de trabajo cliente. Por ejemplo, vaya a `~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64` y haga doble clic en **RGui.exe** para iniciarlo.

2. RevoScaleR carga automáticamente. Confirme que está operativa RevoScaleR, ejecute este comando: `print(Revo.version)`

3. Escriba el script de demostración que se ejecuta en el servidor remoto. Debe modificar el siguiente script de ejemplo para incluir un nombre válido para una instancia remota de SQL Server. Esta sesión se inicia como una sesión local, pero la **rxSummary** función se ejecuta en la instancia remota de SQL Server.

  ```R
  # Define a connection. Replace server with a valid server name.
  connStr <- "Driver=SQL Server;Server=<your-server-name>;Database=NYCTaxi_Sample;Trusted_Connection=true"
  
  # Specify the input data in a SQL query.
  sampleQuery <-"SELECT DISTINCT TOP(100) tip_amount FROM [dbo].nyctaxi_sample ORDER BY tip_amount DESC;"
  
  # Define a remote compute context based on the remote server.
  cc <-RxInSqlServer(connectionString=connStr)

  # Execute the function using the remote compute context.
  rxSummary(formula = ~ ., data = RxSqlServerData(sqlQuery=sampleQuery, connectionString=connStr), computeContext=cc)
  ```

  **Resultados:**

  Este script se conecta a una base de datos en el servidor remoto, proporciona una consulta, se crea un contexto de proceso `cc` instrucciones para la ejecución remota de código, a continuación, proporciona la función RevoScaleR **rxSummary** para devolver una estadística Resumen de los resultados de consulta.

  ```R
    Call:
  rxSummary(formula = ~., data = RxSqlServerData(sqlQuery = sampleQuery, 
      connectionString = connStr), computeContext = cc)

  Summary Statistics Results for: ~.
  Data: RxSqlServerData(sqlQuery = sampleQuery, connectionString = connStr) (RxSqlServerData Data Source)
  Number of valid observations: 100 
  
  Name       Mean   StdDev   Min Max ValidObs MissingObs
  tip_amount 63.245 31.61087 36  180 100      0     
  ```

4. Obtener y establecer el contexto de cálculo. Una vez establecido un contexto de cálculo, permanece en vigor para la duración de la sesión. Si no está seguro de si el cálculo es local o remoto, ejecute el comando siguiente para averiguar. Los resultados que se especifican una cadena de conexión indican un contexto de cálculo remoto.

  ```R
  # Return the current compute context.
  rxGetComputeContext()

  # Revert to a local compute context.
  rxSetComputeContext("local")
  rxGetComputeContext()

  # Switch back to remote.
  connStr <- "Driver=SQL Server;Server=<your-server-name>;Database=NYCTaxi_Sample;Trusted_Connection=true"
  cc <-RxInSqlServer(connectionString=connStr)
  rxSetComputeContext(cc)
  rxGetComputeContext()
  ```  

5. Devuelven información acerca de las variables en el origen de datos, incluidos el nombre y tipo.

  ```R
  rxGetVarInfo(data = inDataSource)
  ```
  Los resultados incluyen 23 variables.


6. Generar un gráfico de dispersión para explorar si hay dependencias entre dos variables. 

  ```R
  # Set the connection string. Substitute a valid server name for the placeholder.
  connStr <- "Driver=SQL Server;Server=<your database name>;Database=NYCTaxi_Sample;Trusted_Connection=true"

  # Specify a query on the nyctaxi_sample table.
  # For variables on each axis, remove nulls. Use a WHERE clause and <> to do this.
  sampleQuery <-"SELECT DISTINCT TOP 100 * from [dbo].[nyctaxi_sample] WHERE fare_amount <> '' AND  tip_amount <> ''"
  cc <-RxInSqlServer(connectionString=connStr)

  # Generate a scatter plot.
  rxLinePlot(fare_amount ~ tip_amount, data = RxSqlServerData(sqlQuery=sampleQuery, connectionString=connStr, computeContext=cc), type="p")
  ```

  Captura de pantalla siguiente muestra el resultado de trazado de dispersión y de entrada.

   ![Gráfico de dispersión en RGUI](media/rclient-setup-scatterplot.png "gráfico de dispersión en los datos de demostración de taxis de Nueva York")

<a name="install-ide"></a>

## <a name="6---link-tools-to-rexe"></a>6 - herramientas de vínculo para R.exe

Para los proyectos de desarrollo constante y graves, debe instalar un entorno de desarrollo integrado (IDE). Herramientas de SQL Server y las herramientas integradas de R no están equipadas para el desarrollo de R pesado. Una vez que el código de trabajo, puede implementarlo como un procedimiento almacenado para su ejecución en SQL Server.

Seleccione las bibliotecas de R locales el IDE: base de R, RevoScaleR y así sucesivamente. Ejecutar cargas de trabajo en un servidor SQL remoto se produce durante la ejecución del script, cuando la secuencia de comandos invoca un contexto de proceso remoto en SQL Server, acceso a datos y las operaciones en ese servidor.

### <a name="rstudio"></a>RStudio

Cuando se usa [RStudio](https://www.rstudio.com/), puede configurar el entorno para usar las bibliotecas de R y los archivos ejecutables que corresponden a los que están en un servidor SQL remoto.

1. Compruebe las versiones de paquete de R instaladas en SQL Server. Para obtener más información, consulte [información del paquete de R obtener](determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location).

1. Instalar Microsoft R Client o una de las opciones de servidor independientes para agregar RevoScaleR y otros paquetes de R, incluida la distribución de R base utilizada por la instancia de SQL Server. Elegir una versión al mismo nivel o inferior (paquetes son compatibles con versiones anteriores) que proporciona las mismas versiones de paquete como en el servidor. Para obtener información de versión, consulte la versión de mapa en este artículo: [Actualizar componentes de R y Python](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

1. En RStudio, [actualizar su ruta de acceso de R](https://support.rstudio.com/hc/articles/200486138-Using-Different-Versions-of-R) hacia el entorno de R que proporciona RevoScaleR, Microsoft R Open y otros paquetes de Microsoft. 

  + Para una instalación de cliente de R, busque C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64
  + Para un servidor independiente, busque C:\Program Files\Microsoft SQL Server\140\R_SERVER\Library o C:\Program Files\Microsoft SQL Server\130\R_SERVER\Library

2. Cierre y, a continuación, abra RStudio.

Cuando vuelva a RStudio, el ejecutable de cliente de R (o servidor independiente) de R es el motor de R predeterminada.


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

## <a name="next-steps"></a>Pasos siguientes

Dos tutoriales diferentes incluyen ejercicios para que puede poner en práctica de cambiar el contexto de proceso desde local a una instancia remota de SQL Server.

+ [Tutorial: Usar funciones de RevoScaleR R con datos de SQL Server](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [Tutorial integral de ciencia de datos](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)