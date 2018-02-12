---
title: Configurar un cliente de ciencia de datos para su uso con SQL Server | Documentos de Microsoft
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d15ee956-918f-40e0-b986-2bf929ef303a
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 80b4898397cd0cb6460b379d91be81eb28cd9b87
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2018
---
# <a name="set-up-a-data-science-client-for-use-with-sql-server"></a>Configurar un cliente de ciencia de datos para su uso con SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Después de haber configurado una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para admitir el aprendizaje automático, debe configurar un entorno de desarrollo que es capaz de conectarse al servidor para la implementación y ejecución remotas.

Este artículo describen algunos escenarios típicos del cliente, incluida la configuración de la edición de Visual Studio Community gratuita para ejecutar código R en SQL Server.

## <a name="install-r-libraries-on-the-client"></a>Instalar bibliotecas de R en el cliente

El entorno de cliente debe incluir Microsoft R Open, así como los paquetes de RevoScaleR adicionales que admiten la ejecución distribuida de R en SQL Server. Distribuciones estándar de R no tiene los paquetes que admiten contextos de proceso remoto o la ejecución en paralelo de tareas de R.

Para obtener estas bibliotecas, instalar cualquiera de las siguientes acciones:
  
+ [Cliente de Microsoft R](http://aka.ms/rclient/download)

+ Microsoft R Server (para SQL Server 2016)

    - Para instalar desde el programa de instalación de SQL Server, vea [crear un R Server independiente](../../advanced-analytics/r/create-a-standalone-r-server.md)

    - Para usar el instalador independiente basado en Windows, consulte [instalar servidor para aprendizaje máquina con Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)

+ Aprendizaje de servidor (para SQL Server de 2017) automático

    - Para instalar desde el programa de instalación de SQL Server, vea [crear un R Server independiente](../../advanced-analytics/r/create-a-standalone-r-server.md)

    - Para usar el instalador independiente basado en Windows, consulte [instalar R Server 9.1 para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)

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