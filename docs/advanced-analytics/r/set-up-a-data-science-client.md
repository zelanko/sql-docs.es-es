---
title: Configurar un cliente de ciencia de datos para el desarrollo de R en SQL Server | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: dd0b420630846382b9d7cf456352bb606a4f0040
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
ms.locfileid: "31204567"
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>Configurar un cliente de ciencia de datos para el desarrollo de R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Después de haber configurado una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para admitir el aprendizaje automático, debe configurar un entorno de desarrollo que es capaz de conectarse al servidor para la implementación y ejecución remotas.

Este artículo describen algunos escenarios típicos del cliente, incluida la configuración de la edición de Visual Studio Community gratuita para ejecutar código R en SQL Server.

## <a name="install-r-libraries-on-the-client"></a>Instalar bibliotecas de R en el cliente

El entorno de cliente debe incluir Microsoft R Open, así como los paquetes de RevoScaleR adicionales que admiten la ejecución distribuida de R en SQL Server. Distribuciones estándar de R no tiene los paquetes que admiten contextos de proceso remoto o la ejecución en paralelo de tareas de R.

Para obtener estas bibliotecas, instalar cualquiera de las siguientes acciones:
  
+ [Cliente de Microsoft R](http://aka.ms/rclient/download)

+ Microsoft R Server (para SQL Server 2016)

    - Para instalar desde el programa de instalación de SQL Server, vea [instalar SQL Server 2016 R Server (independiente)](../install/sql-r-standalone-windows-install.md)

    - Para usar el instalador independiente basado en Windows, consulte [instalar servidor para aprendizaje máquina con Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)

+ Aprendizaje de servidor (para SQL Server de 2017) automático

    - Para instalar desde el programa de instalación de SQL Server, vea [instalar SQL Server de 2017 máquina aprendizaje Server (independiente)](../install/sql-machine-learning-standalone-windows-install.md)

    - Para usar el instalador independiente basado en Windows, consulte [instalar R Server 9.1 para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)

## <a name="r-tools"></a>Herramientas de R

Cuando se instala R con SQL Server, obtendrá las mismas herramientas de R que se instalan con cualquier **base** instalación de R, como RGui, Rterm y así sucesivamente. Por lo tanto, técnicamente, tiene todas las herramientas que necesarias para desarrollar y probar código R.

Se incluyen las siguientes herramientas estándares de R en un *base instalación* de R y por lo tanto, se instalan de forma predeterminada.

+ **RTerm**: un terminal de línea de comandos para ejecutar scripts de R

+ **RGui.exe**: sencillo editor interactivo de R. Los argumentos de la línea de comandos son los mismos en RGui.exe y en RTerm.

+ **RScript**: herramienta de línea de comandos para ejecutar scripts de R en el modo por lotes.

Para encontrar estas herramientas, determine la biblioteca de R que se instala al configurar SQL Server o la característica de aprendizaje de automático de independiente. Por ejemplo, en una instalación predeterminada, las herramientas de R se encuentran en estas carpetas:

+ SQL Server 2016 R Services: `~\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64`
+ Microsoft R Server independiente: `~\Program Files\Microsoft R\R_SERVER\bin\x64`
+ Equipo con SQL Server de 2017 servicios de aprendizaje: `~\Program Files\Microsoft SQL Server\MSSQL14.<instancename>\R_SERVICES\bin\x64`
+ Server (independiente) de aprendizaje automático: `~\Program Files\Microsoft\ML Server\R_SERVER\bin\x64`

Si necesita ayuda con las herramientas de R, simplemente abra **RGui**, haga clic en **ayuda**y seleccione una de las opciones

## <a name="microsoft-r-client"></a>Cliente de Microsoft R

Cliente de Microsoft R es una descarga gratuita que proporciona acceso a los paquetes de RevoScaleR para fines de desarrollo. Al instalar el cliente de R, puede crear soluciones de R que se pueden ejecutar en todos los contextos de proceso admitidos, incluidos el análisis de en bases de datos de SQL Server y computación distribuida R en Hadoop, Spark o Linux con el servidor de aprendizaje de máquina.

Si ya ha instalado un entorno de desarrollo de R diferente, como RStudio, asegúrese de volver a configurar el entorno para usar las bibliotecas y ejecutables proporcionados por Microsoft R cliente. Por lo que puede usar todas las características del paquete RevoScaleR, aunque el rendimiento será limitada.

Para obtener más información, vea [¿qué es Microsoft R cliente?](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

## <a name="install-a-development-environment"></a>Instale un entorno de desarrollo

Si ya no tiene un entorno de desarrollo de R preferido, se recomienda uno de los siguientes:

+ Herramientas de R para Visual Studio

    Funciona con Visual Studio 2015.

    Para obtener información de instalación, consulte [cómo instalar herramientas de R para Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation).
 
    Para configurar RTV para usar las bibliotecas de cliente de Microsoft R, consulte [sobre el cliente de R de Microsoft](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

+ Visual Studio 2017

    Incluso la edición gratuita Community incluye la carga de trabajo de ciencia de datos, que instala las plantillas de proyecto para R, Python y F #.

    Descargar Visual Studio desde [este sitio](https://www.visualstudio.com/vs/). 

+ RStudio

    Si prefiere usar RStudio, se necesitan algunos pasos más para usar las bibliotecas de RevoScaleR:

    - Instalar el cliente de R de Microsoft para obtener los paquetes necesarios y las bibliotecas.
    - Actualizar la ruta de acceso de R para usar el runtime de R de Microsoft.

    Para obtener más información, consulte [cliente R - configurar el IDE](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client#step-2-configure-your-ide).

## <a name="configure-your-ide"></a>Configurar el IDE

+ Herramientas de R para Visual Studio

    Vea [este sitio](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r) algunos ejemplos de cómo compilar y depurar R proyectos con herramientas de R para Visual Studio. 

+ Visual Studio 2017

    Si instala el cliente de Microsoft R o R Server **antes de** instalar Visual Studio, las bibliotecas de R Server automáticamente se detectan y se utiliza para la ruta de biblioteca. Si no ha instalado las bibliotecas de RevoScaleR desde el **herramientas de R** menú, seleccione **instalar el cliente de R**.

## <a name="run-r-in-sql-server"></a>Ejecutar R en SQL Server

Este ejemplo utiliza Visual Studio 2017 Community Edition, con la carga de trabajo de ciencia de datos instalado.

1. Desde el **archivo** menú, seleccione **New** y, a continuación, seleccione **proyecto**.

2. -Mano panel contiene una lista de plantillas preinstaladas. Haga clic en **R**y seleccione **proyecto R**. En el **nombre** , escriba `dbtest` y haga clic en **Aceptar**.

3. Visual Studio crea una nueva carpeta de proyecto y un archivo de script predeterminado, `Script.R`. 

4. Tipo de `.libPaths()` en la primera línea del script de archivo y, a continuación, presione CTRL + ENTRAR.

5. La ruta de biblioteca de R actual se debe mostrar en el **interactiva de R** ventana. 

6. Haga clic en el **herramientas de R** menú y seleccione **Windows** para ver una lista de otras ventanas específicas de R que se pueden mostrar en el área de trabajo.
 
    + Ver la Ayuda en los paquetes en la biblioteca actual, presione CTRL + 3.
    + Ver las variables de R en el **Explorer Variable**, presionando CTRL + 8.

7. Crear una cadena de conexión a una instancia de SQL Server y utilice la cadena de conexión en el constructor RxInSqlServer para crear un objeto de origen de datos de SQL Server. 

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
    > Para ejecutar un lote, seleccione las líneas que desea ejecutar y presione ENTRAR.

8. Establece el contexto de proceso en el servidor y, a continuación, ejecutar el código R simple en los datos.

    ```r
    rxSetComputeContext(cc)
    rxGetVarInfo(data = inDataSource)
    ```

    Resultados se devuelven en el **interactiva de R** ventana.
    
    Si desea asegurarse de que el código se está ejecutando en la instancia de SQL Server, puede utilizar el generador de perfiles para crear un seguimiento.