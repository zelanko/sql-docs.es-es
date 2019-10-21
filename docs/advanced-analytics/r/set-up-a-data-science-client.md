---
title: Configuración de un cliente de ciencia de datos para el desarrollo de R
description: Instale las bibliotecas y herramientas locales de R en una estación de trabajo de desarrollo para las conexiones remotas a SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7c81a69181d1bc723e622bac9ffeb5ff67fd0280
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/17/2019
ms.locfileid: "69633638"
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>Configuración de un cliente de ciencia de datos para el desarrollo de R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La integración de R está disponible en SQL Server 2016 o posterior si incluye la opción de lenguaje R en una instalación [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) o [SQL Server Machine Learning Services (en la base de datos)](../install/sql-machine-learning-services-windows-install.md) . 

Para desarrollar e implementar soluciones de R para SQL Server, instale [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) en la estación de trabajo de desarrollo para obtener [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) y otras bibliotecas de r. La biblioteca de RevoScaleR, que también es necesaria en la instancia de SQL Server remota, coordina las solicitudes de procesamiento entre ambos sistemas. 

En este artículo, aprenderá a configurar una estación de trabajo de desarrollo de R Client para que pueda interactuar con un SQL Server remoto habilitado para el aprendizaje automático y la integración de R. Después de completar los pasos de este artículo, tendrá las mismas bibliotecas de R que las de SQL Server. También sabrá cómo enviar cálculos desde una sesión de R local a una sesión remota de R en SQL Server.

![Componentes cliente-servidor](media/sqlmls-r-client-revo.png "Sesiones y bibliotecas de R locales y remotos")

Para validar la instalación, puede usar la herramienta integrada **RGUI** tal como se describe en este artículo, o [vincular las bibliotecas](#install-ide) a RSTUDIO o cualquier otro IDE que use normalmente.

> [!Note]
> Una alternativa a la instalación de la biblioteca de cliente es usar un [servidor independiente](../install/sql-machine-learning-standalone-windows-install.md) como un cliente enriquecido, que algunos clientes prefieren para un trabajo de escenario más profundo. Un servidor independiente está totalmente desacoplado de SQL Server, pero como tiene las mismas bibliotecas de R, puede utilizarlo como cliente para SQL Server análisis en base de datos. También se puede usar para trabajos no relacionados con SQL, incluida la capacidad de importar y modelar datos de otras plataformas de datos. Si instala un servidor independiente, puede encontrar el ejecutable de R en esta ubicación: `C:\Program Files\Microsoft SQL Server\140\R_SERVER`. Para validar la instalación, [abra una aplicación de consola de r](#R-tools) para ejecutar comandos con el archivo R. exe en esa ubicación.

## <a name="commonly-used-tools"></a>Herramientas de uso frecuente

Tanto si es un desarrollador de R nuevo en SQL como si es un desarrollador de SQL nuevo en R y análisis en base de datos, necesitará una herramienta de desarrollo de R y un editor de consultas de T-SQL como [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) para ejecutar todas las capacidades de en la base de datos. Analytics.

En el caso de escenarios sencillos de desarrollo de R, puede usar el ejecutable RGUI, incluido en la distribución base de R en MRO y SQL Server. En este artículo se explica cómo usar RGUI para sesiones de R locales y remotas. Para mejorar la productividad, debe usar un IDE con todas las características, como [RStudio o Visual Studio](#install-ide).

SSMS es una descarga independiente, útil para crear y ejecutar procedimientos almacenados en SQL Server, incluidos aquellos que contienen código de R. Casi cualquier código R que escriba en un entorno de desarrollo se puede incrustar en un procedimiento almacenado. Puede recorrer otros tutoriales para obtener información sobre [SSMS y Embedded R](../tutorials/sqldev-in-database-r-for-sql-developers.md).

## <a name="1---install-r-packages"></a>1-instalación de paquetes de R

Los paquetes de R de Microsoft están disponibles en varios productos y servicios. En una estación de trabajo local, se recomienda instalar Microsoft R Client. R Client proporciona [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler), [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package), [SQLRUtils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)y otros paquetes de R.

1. [Descargue Microsoft R Client](https://aka.ms/rclient/download).

2. En el Asistente para la instalación, acepte o cambie la ruta de instalación predeterminada, acepte o cambie la lista de componentes y acepte los términos de licencia de Microsoft R Client.

  Una vez finalizada la instalación, una pantalla de bienvenida le presenta el producto y la documentación.

3. Cree una variable de entorno del sistema MKL_CBWR para garantizar una salida coherente en los cálculos de la biblioteca de kernels matemáticos (MKL) de Intel.

  + En el panel de control, haga clic en **sistema y seguridad**  > **sistema**  > **Configuración avanzada del sistema**  > **variables de entorno**.
  + Cree una nueva variable del sistema denominada **MKL_CBWR**con un valor establecido en **auto**.

## <a name="2---locate-executables"></a>2-buscar ejecutables

Busque y enumere el contenido de la carpeta de instalación para confirmar que se han instalado R. exe, RGUI y otros paquetes. 

1. En el explorador de archivos, abra la carpeta C:\Archivos de Files\Microsoft\R Client\R_SERVER\bin para confirmar la ubicación de R. exe.

2. Abra la subcarpeta x64 para confirmar **RGUI**. Usará esta herramienta en el paso siguiente.

3. Abra C:\Archivos de Files\Microsoft\R Client\R_SERVER\library para revisar la lista de paquetes instalados con el cliente de R, incluidos RevoScaleR, MicrosoftML y otros.


<a name="R-tools"></a>
 
## <a name="3---start-rgui"></a>3-iniciar RGUI

Al instalar R con SQL Server, obtendrá las mismas herramientas de R que son estándar para cualquier instalación base de R, como RGui, Rterm, etc. Estas herramientas son ligeras, útiles para comprobar la información de la biblioteca y el paquete, ejecutar scripts o comandos ad hoc o recorrer los tutoriales. Puede usar estas herramientas para obtener información de versión de R y confirmar la conectividad.

1. Abra C:\Archivos de Files\Microsoft\R Client\R_SERVER\bin\x64 y haga doble clic en **RGui** para iniciar una sesión de r con un símbolo del sistema de r.

  Al iniciar una sesión de R desde una carpeta de programas de Microsoft, varios paquetes, incluido RevoScaleR, se cargan automáticamente. 

2. Escriba `print(Revo.version)` en el símbolo del sistema para devolver la información de versión del paquete RevoScaleR. Debe tener la versión 9.2.1 o 9.3.0 para RevoScaleR.

3. Escriba **Search ()** en el símbolo del sistema de R para obtener una lista de los paquetes instalados.

   ![Información de versión al cargar R](../install/media/rclient-rgui-r-prompt.png "Abra un símbolo del sistema de R")


## <a name="4---get-sql-permissions"></a>4: obtener permisos SQL

En R Client, el procesamiento de R se limita a dos subprocesos y datos en memoria. Para el procesamiento escalable con varios núcleos y conjuntos de datos grandes, puede desplazar la ejecución (denominada *contexto de cálculo*) a los conjuntos de datos y la potencia de cálculo de una instancia de SQL Server remota. Este es el enfoque recomendado para la integración de clientes con una instancia de SQL Server de producción y necesitará permisos e información de conexión para que funcione.

Para conectarse a una instancia de SQL Server para ejecutar scripts y cargar datos, debe tener un inicio de sesión válido en el servidor de base de datos. Puede usar un inicio de sesión de SQL o la autenticación integrada de Windows. Por lo general, se recomienda usar la autenticación integrada de Windows, pero el inicio de sesión de SQL es más sencillo en algunos escenarios, especialmente cuando el script contiene cadenas de conexión a datos externos.

Como mínimo, la cuenta utilizada para ejecutar el código debe tener permiso para leer de las bases de datos con las que está trabajando, además del permiso especial ejecutar cualquier SCRIPT externo. La mayoría de los desarrolladores también requieren permisos para crear procedimientos almacenados y para escribir datos en tablas que contienen datos de entrenamiento o datos puntuados. 

Pida al administrador de la base de datos que [Configure los siguientes permisos para su cuenta](../security/user-permission.md), en la base de datos donde se usa R:

+ **Ejecute cualquier script externo** para ejecutar el script de R en el servidor.
+ privilegios **db_datareader** para ejecutar las consultas que se usan para entrenar el modelo.
+ **db_datawriter** para escribir datos de entrenamiento o datos puntuados.
+ **db_owner** para crear objetos como procedimientos almacenados, tablas, funciones. 
  También necesitará **db_owner** para crear bases de datos de prueba y de ejemplo. 

Si el código requiere paquetes que no se instalan de forma predeterminada con SQL Server, organice con el administrador de la base de datos para que los paquetes se instalen con la instancia. SQL Server es un entorno protegido y hay restricciones en el lugar donde se pueden instalar los paquetes. Para obtener más información, vea [instalar nuevos paquetes de R en SQL Server](install-additional-r-packages-on-sql-server.md).

## <a name="5---test-connections"></a>5-probar conexiones

 Como paso de comprobación, use **RGUI** y RevoScaleR para confirmar la conectividad con el servidor remoto. SQL Server debe estar habilitado para [las conexiones remotas](https://docs.microsoft.com/sql/database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server) y debe tener permisos, incluido un inicio de sesión de usuario y una base de datos a la que conectarse. 

En los pasos siguientes se da por supuesto la base de datos de demostración, [NYCTaxi_Sample](../tutorials/demo-data-nyctaxi-in-sql.md)y la autenticación de Windows.

1. Abra **RGUI** en la estación de trabajo del cliente. Por ejemplo, vaya a `~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64` y haga doble clic en **RGui. exe** para iniciarlo.

2. RevoScaleR se carga automáticamente. Confirme que RevoScaleR está operativo ejecutando este comando: `print(Revo.version)`

3. Escriba el script de demostración que se ejecuta en el servidor remoto. Debe modificar el siguiente script de ejemplo para incluir un nombre válido para una instancia de SQL Server remota. Esta sesión se inicia como una sesión local, pero la función **rxSummary** se ejecuta en la instancia de SQL Server remota.

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

  Este script se conecta a una base de datos del servidor remoto, proporciona una consulta, crea un contexto de cálculo `cc` instrucción para la ejecución remota de código y, a continuación, proporciona la función RevoScaleR **rxSummary** para devolver un resumen estadístico de los resultados de la consulta.

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

4. Obtiene y establece el contexto de cálculo. Una vez que se establece un contexto de cálculo, permanece activo mientras dure la sesión. Si no está seguro de si el cálculo es local o remoto, ejecute el siguiente comando para averiguarlo. Los resultados que especifican una cadena de conexión indican un contexto de cálculo remoto.

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

5. Devuelven información acerca de las variables en el origen de datos, incluidos el nombre y el tipo.

  ```R
  rxGetVarInfo(data = inDataSource)
  ```
  Los resultados incluyen 23 variables.


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

  En la captura de pantalla siguiente se muestra el resultado del gráfico de entrada y dispersión.

   ![Gráfico de dispersión en RGUI](media/rclient-setup-scatterplot.png "Datos de demostración del gráfico de dispersión en Nueva York taxi")

<a name="install-ide"></a>

## <a name="6---link-tools-to-rexe"></a>6-Link Tools para R. exe

En el caso de los proyectos de desarrollo continuos y graves, debe instalar un entorno de desarrollo integrado (IDE). SQL Server herramientas y las herramientas de R integradas no están equipadas para un desarrollo intensivo de R. Una vez que tenga código de trabajo, puede implementarlo como un procedimiento almacenado para su ejecución en SQL Server.

Apunte el IDE a las bibliotecas locales de R: R, RevoScaleR, etc. Las cargas de trabajo en ejecución en un SQL Server remoto se producen durante la ejecución del script, cuando el script invoca un contexto de cálculo remoto en SQL Server, teniendo acceso a los datos y a las operaciones en ese servidor.

### <a name="rstudio"></a>RStudio

Al usar [RStudio](https://www.rstudio.com/), puede configurar el entorno para usar las bibliotecas de R y los ejecutables que se corresponden con los de un SQL Server remoto.

1. Compruebe las versiones del paquete de R instaladas en SQL Server. Para obtener más información, vea [obtener información de paquetes de R](../package-management/r-package-information.md).

1. Instale Microsoft R Client o una de las opciones de servidor independiente para agregar RevoScaleR y otros paquetes de R, incluida la distribución de R base usada por la instancia de SQL Server. Elija una versión en el mismo nivel o inferior (los paquetes son compatibles con versiones anteriores) que proporciona las mismas versiones de paquete que en el servidor. Para obtener información sobre la versión, consulte el mapa de versión de este artículo: [actualización de los componentes de R y Python](../install/upgrade-r-and-python.md).

1. En RStudio, [actualice la ruta de acceso de r](https://support.rstudio.com/hc/articles/200486138-Using-Different-Versions-of-R) para que apunte al entorno de r que proporciona RevoScaleR, Microsoft R Open y otros paquetes de Microsoft. 

  + Para una instalación de cliente de R, busque C:\Archivos de Files\Microsoft\R Client\R_SERVER\bin\x64
  + Para un servidor independiente, busque C:\Archivos de Programa\microsoft SQL Server\140\R_SERVER\Library o C:\Archivos de Programa\microsoft SQL Server\130\R_SERVER\Library

2. Cierre y, a continuación, abra RStudio.

Al volver a abrir RStudio, el archivo ejecutable de R desde el cliente de R (o el servidor independiente) es el motor de R predeterminado.


### <a name="r-tools-for-visual-studio-rtvs"></a>Herramientas de R para Visual Studio (RTVS)

Si aún no tiene un IDE preferido para R, se recomienda **herramientas de R para Visual Studio**.

+ [Descargar Herramientas de R para Visual Studio (RTVS)](https://visualstudio.microsoft.com/vs/features/rtvs/)
+ [Instrucciones de instalación](https://docs.microsoft.com/visualstudio/rtvs/installing-r-tools-for-visual-studio) : RTVS está disponible en varias versiones de Visual Studio.
+ [Introducción a Herramientas de R para Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r)

### <a name="connect-to-sql-server-from-rtvs"></a>Conexión a SQL Server desde RTVS

En este ejemplo se usa Visual Studio 2017 Community Edition, con la carga de trabajo de ciencia de datos instalada.

1. En el menú **archivo** , seleccione **nuevo** y seleccione **proyecto**.

2. El panel izquierdo contiene una lista de plantillas preinstaladas. Haga clic en **r**y seleccione **proyecto de r**. En el cuadro **nombre** , escriba `dbtest` y haga clic en **Aceptar**. 

  Visual Studio crea una nueva carpeta de proyecto y un archivo de script predeterminado, `Script.R`. 

3. Escriba `.libPaths()` en la primera línea del archivo de script y, a continuación, presione CTRL + entrar.

  La ruta de acceso de la biblioteca de R actual debe aparecer en la ventana **R interactivo** . 

4. Haga clic en el menú **herramientas de r** y seleccione **Windows** para ver una lista de otras ventanas específicas de r que puede mostrar en el área de trabajo.
 
  + Para ver la ayuda sobre los paquetes de la biblioteca actual, presione CTRL + 3.
  + Para ver las variables de R en el **Explorador de variables**, presione Ctrl + 8.

## <a name="next-steps"></a>Pasos siguientes

Dos tutoriales diferentes incluyen ejercicios para que pueda practicar el cambio del contexto de proceso de local a una instancia de SQL Server remota.

+ [Tutorial: uso de las funciones de RevoScaleR R con datos de SQL Server](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [Tutorial integral de ciencia de datos](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)