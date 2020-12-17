---
title: Configuración de un cliente de ciencia de datos R
description: Instale las bibliotecas y herramientas locales de R en una estación de trabajo de desarrollo para las conexiones remotas a SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 06/13/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: 7f738e20a84c82879361e999ef795825c31bf311
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470776"
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>Configuración de un cliente de ciencia de datos para el desarrollo de R en SQL Server
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

La integración de R está disponible en SQL Server 2016 o versiones posteriores cuando se incluye la opción de lenguaje R en una instalación de [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) o [SQL Server Machine Learning Services (en la base de datos)](../install/sql-machine-learning-services-windows-install.md). 

Para desarrollar e implementar soluciones de R para SQL Server, instale [Microsoft R Client](/machine-learning-server/r-client/what-is-microsoft-r-client) en la estación de trabajo de desarrollo para obtener [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) y otras bibliotecas de R. La biblioteca RevoScaleR, que también se necesita en la instancia de SQL Server remota, coordina las solicitudes de procesamiento entre ambos sistemas. 

En este artículo aprenderá a configurar una estación de trabajo de desarrollo de R que permita interactuar con una instancia de SQL Server remota habilitada para el aprendizaje automático y la integración de R. Después de seguir los pasos de este artículo, dispondrá de las mismas bibliotecas de R que en SQL Server. También aprenderá a enviar procesamientos de inserción de una sesión de R local a una sesión remota de R en SQL Server.

![Componentes de cliente y servidor](media/sqlmls-r-client-revo.png "Sesiones y bibliotecas locales y remotas de R")

Para validar la instalación, puede usar la herramienta integrada **RGUI**, como se explica en este artículo, o [vincular las bibliotecas](#install-ide) a RStudio o cualquier otro IDE que use normalmente.

> [!Note]
> Una alternativa a la instalación de la biblioteca cliente es el uso de un [servidor independiente](../install/sql-machine-learning-standalone-windows-install.md) como cliente enriquecido, lo que algunos clientes prefieren para un trabajo más especializado. Un servidor independiente está totalmente desasociado de SQL Server, pero como tiene las mismas bibliotecas de R, se puede usar como cliente para el análisis en base de datos de SQL Server. También se puede usar para trabajos no relacionados con SQL, lo que incluye la capacidad de importar y modelar datos de otras plataformas de datos. Si instala un servidor independiente, puede encontrar el archivo ejecutable de R en `C:\Program Files\Microsoft SQL Server\140\R_SERVER`. Para validar la instalación, [abra una aplicación de consola de R](#R-tools) con el fin de ejecutar comandos mediante R.exe en esa ubicación.

## <a name="commonly-used-tools"></a>Herramientas de uso común

Tanto si es un desarrollador de R que no está familiarizado con SQL como si es un desarrollador de SQL que no está familiarizado con R y el análisis en base de datos, necesitará una herramienta de desarrollo de R y un editor de consultas de T-SQL como [SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md) para usar todas las capacidades de análisis en la base de datos.

En el caso de escenarios sencillos de desarrollo de R, puede usar el ejecutable RGUI, incluido en la distribución base de R en MRO y SQL Server. En este artículo se explica cómo usar RGUI para sesiones de R locales y remotas. Para mejorar la productividad, debe usar un IDE con todas las características, como [RStudio o Visual Studio](#install-ide).

SSMS es una descarga independiente que resulta útil para crear y ejecutar procedimientos almacenados en SQL Server, incluidos aquellos que contienen código de R. Casi cualquier código R que escriba en un entorno de desarrollo se puede insertar en un procedimiento almacenado. Puede seguir los pasos que se indican en otros tutoriales para obtener información sobre [SSMS y R insertado](../tutorials/r-taxi-classification-introduction.md).

## <a name="1---install-r-packages"></a>1\. Instalación de paquetes de R

Los paquetes de Microsoft R están disponibles en varios productos y servicios. En una estación de trabajo local, se recomienda instalar Microsoft R Client. R Client proporciona [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler), [MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package), [SQLRUtils](/machine-learning-server/r-reference/sqlrutils/sqlrutils) y otros paquetes de R.

1. [Descargue Microsoft R Client](https://aka.ms/rclient/download).

2. En el asistente para instalación, acepte o cambie la ruta predeterminada, acepte o cambie la lista de componentes y acepte los términos de licencia de Microsoft R Client.

   Una vez finalizada la instalación, una pantalla de bienvenida le presentará el producto y la documentación.

3. Cree una variable de entorno del sistema MKL_CBWR para garantizar una salida coherente en los cálculos de la Math Kernel Library (MKL) de Intel.

   + En el panel de control, haga clic en **Sistema y seguridad** > **Sistema** > **Configuración avanzada del sistema** > **Variables de entorno**.
   + Cree una nueva variable del sistema denominada **MKL_CBWR**, con un valor establecido en **Automático**.

## <a name="2---locate-executables"></a>2 - Buscar los archivos ejecutables

Busque y enumere el contenido de la carpeta de instalación para confirmar que se ha instalado R.exe, RGUI y otros paquetes. 

1. En el explorador de archivos, abra la carpeta C:\Archivos de programa\Microsoft\R Client\R_SERVER\bin para confirmar la ubicación de R.exe.

2. Abra la subcarpeta x64 para confirmar **RGUI**. Esta herramienta se usarán en el paso siguiente.

3. Abra C:\Archivos de programa\Microsoft\R Client\R_SERVER\library para revisar la lista de paquetes instalados con el cliente de R, incluidos RevoScaleR, MicrosoftML y otros.


<a name="R-tools"></a>
 
## <a name="3---start-rgui"></a>3\. Inicio de RGUI

Al instalar R con SQL Server, obtendrá las mismas herramientas de R habituales de cualquier instalación base de R, como RGui, Rterm, etc. Estas herramientas son ligeras, útiles para comprobar la información de la biblioteca y el paquete, ejecutar scripts o comandos ad hoc o recorrer los tutoriales. Puede usar estas herramientas para obtener información de versión de R y confirmar la conectividad.

1. Abra C:\Archivos de programa\Microsoft\R Client\R_SERVER\bin\x64 y haga doble clic en **RGui** para iniciar una sesión de R con un símbolo del sistema de R.

   Al iniciar una sesión de R desde una carpeta de programas de Microsoft, se cargan automáticamente varios paquetes, incluido RevoScaleR. 

2. Escriba `print(Revo.version)` en el símbolo del sistema para obtener la información de versión del paquete RevoScaleR. Debe tener la versión 9.2.1 o 9.3.0 para RevoScaleR.

3. Escriba **search()** en el símbolo del sistema de R para obtener una lista de los paquetes instalados.

   ![Información de versión al cargar R](../install/media/rclient-rgui-r-prompt.png "Abrir un símbolo del sistema de R")


## <a name="4---get-sql-permissions"></a>4 - Obtener permisos SQL

En R Client, el procesamiento de R se limita a dos subprocesos y datos en memoria. Para el procesamiento escalable con varios núcleos y conjuntos de datos grandes, puede desplazar la ejecución (denominada *contexto de proceso*) a los conjuntos de datos y la potencia de proceso de una instancia de SQL Server remota. Este es el enfoque recomendado para la integración de clientes con una instancia de SQL Server de producción y necesitará permisos e información de conexión para que funcione.

Para conectarse a una instancia de SQL Server a fin de ejecutar scripts y cargar datos, debe tener un inicio de sesión válido en el servidor de base de datos. Puede usar un inicio de sesión de SQL o la autenticación integrada de Windows. Por lo general, se recomienda usar la autenticación integrada de Windows, pero el inicio de sesión de SQL es más sencillo en algunos escenarios, especialmente si el script contiene cadenas de conexión a datos externos.

Como mínimo, la cuenta usada para ejecutar código debe tener permiso para leer en las bases de datos con las que se está trabajando, además del permiso especial EXECUTE ANY EXTERNAL SCRIPT. La mayoría de los desarrolladores también necesitan permisos para crear procedimientos almacenados y para escribir datos en tablas que contienen datos de entrenamiento o datos puntuados. 

Pida al administrador de bases de datos que [configure los siguientes permisos para la cuenta](../security/user-permission.md) en la base de datos donde usa R:

+ **EXECUTE ANY EXTERNAL SCRIPT** para ejecutar el script de R en el servidor.
+ Privilegios **db_datareader** para ejecutar las consultas usadas para entrenar el modelo.
+ **db_datawriter** para escribir datos de entrenamiento o datos puntuados.
+ **db_owner** para crear objetos como procedimientos almacenados, tablas y funciones. 
  También necesita **db_owner** para crear bases de datos de prueba y ejemplo. 

Si el código requiere paquetes que no se instalan de forma predeterminada con SQL Server, hable con el administrador de bases de datos para que los paquetes se instalen con la instancia. SQL Server es un entorno protegido y hay restricciones sobre la ubicación donde se pueden instalar los paquetes. Para más información, vea [Instalación de nuevos paquetes en SQL Server](../package-management/install-additional-r-packages-on-sql-server.md).

## <a name="5---test-connections"></a>5\. Prueba de las conexiones

Como paso de comprobación, use **RGUI** y RevoScaleR para confirmar la conectividad con el servidor remoto. SQL Server debe estar habilitado para [conexiones remotas](../../database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md) y debe tener permisos, incluido un inicio de sesión de usuario y una base de datos a la que conectarse. 

En los pasos siguientes se presupone que se usa la base de datos de demo [NYCTaxi_Sample](../tutorials/demo-data-nyctaxi-in-sql.md) y la autenticación de Windows.

1. Abra **RGUI** en la estación de trabajo del cliente. Por ejemplo, vaya a `~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64` y haga doble clic en **RGui. exe** para iniciarlo.

2. RevoScaleR se carga automáticamente. Confirme que RevoScaleR está operativo mediante la ejecución de este comando: `print(Revo.version)`

3. Escriba el script de demo que se ejecuta en el servidor remoto. Debe modificar el siguiente script de ejemplo para que incluya un nombre válido para una instancia de SQL Server remota. Esta sesión se inicia como una sesión local, pero la función **rxSummary** se ejecuta en la instancia de SQL Server remota.

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

   Este script se conecta a una base de datos del servidor remoto, proporciona una consulta, crea una instrucción `cc` de contexto de proceso para la ejecución remota de código y, después, proporciona la función **rxSummary** de RevoScaleR para devolver un resumen estadístico de los resultados de la consulta.

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

4. Obtenga y establezca el contexto de proceso. Una vez que establece un contexto de proceso, este permanece activo mientras dure la sesión. Si no está seguro de si el proceso es local o remoto, ejecute el siguiente comando para averiguarlo. Los resultados que especifican una cadena de conexión indican un contexto de proceso remoto.

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

5. Devuelva información sobre las variables en el origen de datos, incluidos el nombre y el tipo.

   ```R
   rxGetVarInfo(data = inDataSource)
   ```
   Los resultados incluyen 23 variables.


6. Genere un gráfico de dispersión para explorar si hay dependencias entre dos variables. 

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

   En la captura de pantalla siguiente se muestra la entrada y la salida del gráfico de dispersión.

   ![Gráfico de dispersión en RGUI](media/rclient-setup-scatterplot.png "Gráfico de dispersión de los datos de demo Taxis de Nueva York")

<a name="install-ide"></a>

## <a name="6---link-tools-to-rexe"></a>6\. Vinculación de las herramientas a R.exe

En el caso de los proyectos de desarrollo continuos y graves, debe instalar un entorno de desarrollo integrado (IDE). Las herramientas de SQL Server y las herramientas de R integradas no están equipadas para un desarrollo intensivo de R. Una vez que tenga código de trabajo, puede implementarlo como un procedimiento almacenado para su ejecución en SQL Server.

Haga que el IDE apunte a las bibliotecas locales de R: R base, RevoScaleR, etc. La ejecución de cargas de trabajo en un servidor SQL Server remoto se produce durante la ejecución del script, cuando el script invoca un contexto de proceso remoto en SQL Server y accede a los datos y las operaciones de ese servidor.

### <a name="rstudio"></a>RStudio

Al usar [RStudio](https://www.rstudio.com/), puede configurar el entorno para que use las bibliotecas de R y los archivos ejecutables que se corresponden con los de un servidor SQL Server remoto.

1. Compruebe las versiones del paquete de R instaladas en SQL Server. Para más información, vea [Obtener información sobre paquetes de R](../package-management/r-package-information.md).

1. Instale Microsoft R Client o una de las opciones de servidor independiente para agregar RevoScaleR y otros paquetes de R, incluida la distribución de R base usada por la instancia de SQL Server. Elija una versión en el mismo nivel o inferior (los paquetes son compatibles con versiones anteriores) que proporcione las mismas versiones de paquete que las del servidor. Para obtener información sobre la versión, vea el mapa de versiones de este artículo: [Actualización de componentes de R y Python](../install/upgrade-r-and-python.md).

1. En RStudio, [actualice la ruta de acceso de R](https://support.rstudio.com/hc/articles/200486138-Using-Different-Versions-of-R) para que apunte al entorno de R que proporciona RevoScaleR, Microsoft R Open y otros paquetes de Microsoft. 

   + Para una instalación de cliente de R, busque C:\Archivos de programa\Microsoft\R Client\R_SERVER\bin\x64
   + Para un servidor independiente, busque C:\Archivos de programa\Microsoft SQL Server\140\R_SERVER\Library o C:\Archivos de programa\Microsoft SQL Server\130\R_SERVER\Library.

1. Cierre RStudio y vuelva a abrirlo.

Al volver a abrir RStudio, el motor de R predeterminado es el archivo ejecutable de R desde el cliente de R (o el servidor independiente).


### <a name="r-tools-for-visual-studio-rtvs"></a>Herramientas de R para Visual Studio (RTVS)

Si aún no tiene un IDE preferido para R, se recomienda **Herramientas de R para Visual Studio**.

+ [Descarga de Herramientas de R para Visual Studio (RTVS)](https://marketplace.visualstudio.com/items?itemName=MikhailArkhipov007.RTVS2019)
+ [Instrucciones de instalación](/visualstudio/rtvs/installing-r-tools-for-visual-studio): RTVS está disponible en varias versiones de Visual Studio.
+ [Introducción a Herramientas de R para Visual Studio](/visualstudio/rtvs/getting-started-with-r)

### <a name="connect-to-sql-server-from-rtvs"></a>Conexión a SQL Server desde RTVS

En este ejemplo se usa Visual Studio 2017 Community Edition, con la carga de trabajo de ciencia de datos instalada.

1. En el menú **Archivo**, seleccione **Nuevo** y haga clic en **Proyecto**.

2. El panel izquierdo contiene una lista de plantillas preinstaladas. Haga clic en **R** y seleccione **Proyecto de R**. En el cuadro **Nombre**, escriba `dbtest` y haga clic en **Aceptar**. 

   Visual Studio crea una nueva carpeta de proyecto y un archivo de script predeterminado, `Script.R`. 

3. Escriba `.libPaths()` en la primera línea del archivo de script y, después, presione CTRL + Entrar.

   La ruta de acceso de la biblioteca de R actual debe aparecer en la ventana **R interactivo**. 

4. Haga clic en el menú **Herramientas de R** y seleccione **Ventanas** para ver una lista de otras ventanas específicas de R que se pueden mostrar en el área de trabajo.
 
   + Para ver la ayuda sobre los paquetes de la biblioteca actual, presione CTRL + 3.
   + Para ver las variables de R en el **Explorador de variables**, presione CTRL + 8.

## <a name="next-steps"></a>Pasos siguientes

Dos tutoriales diferentes con ejercicios para que pueda practicar el cambio del contexto de proceso de una instancia SQL Server local a una remota.

+ [Tutorial: Uso de funciones de RevoScaleR de R con datos de SQL Server](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [Tutorial integral de ciencia de datos](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)