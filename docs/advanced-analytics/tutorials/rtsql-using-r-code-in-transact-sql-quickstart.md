---
title: Guía de inicio rápido para una ejecución de código de R básica de "Hello World" en Transact-SQL (SQL Server Machine Learning) | Microsoft Docs
description: En este inicio rápido para script de R en SQL Server, conozca los aspectos básicos del procedimiento almacenado del sistema sp_execute_external_script con un ejercicio de hello world.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/15/2018
ms.topic: quickstart
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e738289b39f6d390bc4d6196606d242fa4803865
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086888"
---
# <a name="quickstart-hello-world-r-script-in-sql-server"></a>Inicio rápido: Script "Hola mundo" de R en SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server incluye compatibilidad de características de lenguaje R para realizar análisis en bases de datos en los datos de SQL Server residentes. Puede usar funciones de R de código abierto, paquetes de terceros y los paquetes integrados de Microsoft R para realizar análisis predictivos a escala.

En este tutorial, obtendrá información sobre los conceptos clave mediante la ejecución de un "Hello World" R script SQL de inT, una introducción a la **sp_execute_external_script** procedimiento almacenado del sistema. Ejecución de scripts de R es a través de procedimientos almacenados. Puede usar el [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) procedimiento almacenado y pase R secuencia de comandos como parámetro de entrada como se muestra en este inicio rápido o ajustar el script de R en un [procedimientos almacenados personalizados](sqldev-in-database-r-for-sql-developers.md). 

## <a name="prerequisites"></a>Requisitos previos

Este ejercicio requiere acceso a una instancia de SQL Server con uno de los siguientes ya instalados:

+ [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md), con el lenguaje R instalado
+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

  Puede ser la instancia de SQL Server en una máquina virtual de Azure o localmente. Tenga presente que la característica de scripting externa está deshabilitada de forma predeterminada, por lo que es posible que deba [habilite los scripts externos](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) y compruebe que **servicio Launchpad de SQL Server** se está ejecutando antes de empezar.

+ Una herramienta para ejecutar consultas SQL. Puede usar cualquier aplicación que pueda conectarse a una base de datos de SQL Server y ejecutar código de T-SQL. Los profesionales de SQL pueden usar SQL Server Management Studio (SSMS) o Visual Studio.

Para este tutorial, para mostrar lo fácil que es ejecutar R en SQL Server, que hemos usado el nuevo **extensión mssql para Visual Studio Code**. VS Code es un entorno de desarrollo gratuito que puede ejecutar en Windows, macOS o Linux. El **mssql** extensión es una ligera para ejecutar consultas Transact-SQL. Para obtener Visual Studio Code, vea [Download and install Visual Studio Code](https://code.visualstudio.com/Download) (Descargar e instalar Visual Studio Code). Para agregar la **mssql** extensión, consulte este artículo: [usar la extensión mssql para Visual Studio Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode).

## <a name="connect-to-a-database-and-run-a-hello-world-test-script"></a>Conectarse a una base de datos y ejecutar un script de prueba Hola a todos

1. En Visual Studio Code, cree un archivo de texto y denomínelo BasicRSQL.sql.

2. Con el archivo abierto, presione CTRL+MAYÚS+P (COMANDO + P en macOS), escriba **sql** en la lista de comandos SQL y seleccione **CONECTAR**. Visual Studio Code le pedirá que cree un perfil para usarlo al conectarse a una base de datos específica. Esto es opcional, pero resulta más fácil cambiar entre las bases de datos e inicios de sesión.
    + Elija un servidor o instancia donde se haya instalado R en SQL Server.
    + Use una cuenta que tenga permisos para crear una base de datos, ejecutar instrucciones SELECT y ver definiciones de tabla.

2. Si la conexión se establece, el usuario debe poder ver el nombre del servidor y la base de datos en la barra de estado, junto con sus credenciales actuales. Si no se establece, compruebe que los nombres del equipo y el servidor son correctos.

3. Pegue esta instrucción y ejecútela.

    ```sql
    EXEC sp_execute_external_script
      @language =N'R',
      @script=N'OutputDataSet<-InputDataSet',
      @input_data_1 =N'SELECT 1 AS hello'
      WITH RESULT SETS (([Hello World] int));
    GO
    ```

Entradas de este procedimiento almacenado se incluyen:

+ *@language* parámetro define la extensión del lenguaje para llamar, en este caso, R.
+ *@script* parámetro define los comandos que se pasan al runtime de R. El script de R debe estar todo incluido en este argumento en texto Unicode. También puede agregar texto a una variable de tipo **nvarchar** y, después, llamar a la variable.
+ *@input_data_1* se devuelven datos por la consulta, que se pasa al runtime de R, que devuelve los datos a SQL Server como una trama de datos.
+ CON conjuntos de resultados cláusula define el esquema de la tabla de datos devueltos para SQL Server, agregar "Hello World" como nombre de columna, **int** para el tipo de datos.

**Resultado**

![rsql_basictut_hello1](media/rsql-basictut-hello1.PNG)

Si recibe errores de esta consulta, descartar cualquier problema de instalación. Configuración posterior a la instalación es necesario para habilitar el uso de bibliotecas de código externo. Consulte [instalar SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) o [instalar SQL Server 2016 R Services](../install/sql-r-services-windows-install.md). Del mismo modo, asegúrese de que se está ejecutando el servicio Launchpad. 

En función del entorno, puede que tenga que habilitar las cuentas de trabajo de R para conectarse a SQL Server, instalar bibliotecas de red adicionales, habilitar la ejecución remota de código o reiniciar la instancia una vez configurado todo. Para obtener más información, consulte [R servicios de instalación y actualización, preguntas más frecuentes](../r/upgrade-and-installation-faq-sql-server-r-services.md)

> [!TIP]
> En Visual Studio Code, puede resaltar el código que quiere ejecutar y presionar CTRL+MAYÚS+E. Si le parece difícil de recordar, puede cambiarlo. Vea [Customize the shortcut key bindings](https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts) (Personalizar los enlaces de tecla de método abreviado).
> 
> ![rsql-basictut_hello1code](media/rsql-basictut-hello1code.PNG)
> 

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha confirmado la instancia está lista para trabajar con R, échele un vistazo al estructurar las entradas y salidas.

> [!div class="nextstepaction"]
> [Inicio rápido: Controlar entradas y salidas](rtsql-working-with-inputs-and-outputs.md)
