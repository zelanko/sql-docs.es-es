---
title: "Mediante código de R en Transact-SQL (R en Inicio rápido de SQL) | Documentos de Microsoft"
ms.custom: SQL2016_New_Updated
ms.date: 08/20/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 4e6fe30d-a105-4d5b-bc05-5e5204753847
caps.latest.revision: "36"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 2513c04aaf701bcbcb83716bc6b528c5d12e28c4
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="using-r-code-in-transact-sql-r-in-sql-quickstart"></a>Mediante código de R en Transact-SQL (R en Inicio rápido de SQL)

Este tutorial le guía por los aspectos prácticos de llamar a un script de R desde un procedimiento almacenado de T-SQL.

**Lo que aprenderá**

+ Insertar código de R en una función T-SQL
+ Algunas sugerencias para trabajar con objetos de datos y tipos de datos R y SQL
+ Cómo crear un modelo sencillo y guardarlo en SQL Server
+ Cómo crear predicciones y un gráfico de R con el modelo

**Tiempo estimado**

30 minutos (instalación no incluida)

## <a name="prerequisites"></a>Requisitos previos

Debe tener acceso a una instancia de SQL Server con uno de los siguientes ya instalados:

+ SQL Server de 2017 Machine Learning Services, con el lenguaje R instalado
+ SQL Server 2016 R Services

La instancia de SQL Server puede estar en una máquina virtual de Azure o local. Solo debes tener en cuenta que la característica de scripting externa está deshabilitada de forma predeterminada, por lo que tendrá que realizar algunos pasos adicionales para que funcione.

Para ejecutar consultas SQL que incluyen el script de R, puede usar cualquier otra aplicación que pueda conectarse a una base de datos y ejecutar código de T-SQL. Los profesionales de SQL pueden usar SQL Server Management Studio (SSMS) o Visual Studio.

Para este tutorial, para mostrar lo fácil que es ejecutar R en SQL Server, hemos utilizado el nuevo **mssql extensión para Visual Studio Code**. Código de VS es un entorno de desarrollo gratuito que se puede ejecutar en Windows, Mac OS o Linux. El **mssql*** extensión es una ligera para ejecutar consultas de SQL. Para instalarlo, vea el artículo: [Use the mssql extension for Visual Studio Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode) (Usar la extensión mssql para Visual Studio Code).

## <a name="connect-to-a-database-and-run-a-hello-world-test-script"></a>Conectarse a una base de datos y ejecutar un script de prueba Hola a todos

1. En Visual Studio Code, cree un archivo de texto y denomínelo BasicRSQL.sql.
2. Con el archivo abierto, presione CTRL+MAYÚS+P (COMANDO + P en macOS), escriba **sql** en la lista de comandos SQL y seleccione **CONECTAR**. Código de Visual Studio le pedirá que cree un perfil para usarlo al conectarse a una base de datos. Esto es opcional, pero resulta más fácil cambiar entre las bases de datos e inicios de sesión.
    + Elija un servidor o instancia donde se haya instalado R en SQL Server.
    + Use una cuenta que tenga permisos para crear una base de datos, ejecutar instrucciones SELECT y ver definiciones de tabla.
2. Si la conexión se establece, el usuario debe poder ver el nombre del servidor y la base de datos en la barra de estado, junto con sus credenciales actuales. Si no se establece, compruebe que los nombres del equipo y el servidor son correctos.
3. Pegue esta instrucción y ejecútela.

    ```sql
    EXEC sp_execute_external_script
      @language =N'R',
      @script=N'OutputDataSet<-InputDataSet',
      @input_data_1 =N'SELECT 1 AS hello'
      WITH RESULT SETS (([hello] int not null));
    GO
    ```

    En Visual Studio Code, puede resaltar el código que quiere ejecutar y presionar CTRL+MAYÚS+E. Si le parece difícil de recordar, puede cambiarlo. Vea [Customize the shortcut key bindings](https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts) (Personalizar los enlaces de tecla de método abreviado).

    ![rsql-basictut_hello1code](media/rsql-basictut-hello1code.PNG)

**Resultado**

![rsql_basictut_hello1](media/rsql-basictut-hello1.PNG)

## <a name="troubleshooting"></a>Solucionar problemas

+ Si recibe errores de esta consulta, instalación podría estar incompleta. Después de agregar la característica mediante el Asistente para la instalación de SQL Server, debe realizar algunos pasos adicionales para habilitar el uso de bibliotecas de código externo.  Vea [Set up SQL Server R Services](../r/set-up-sql-server-r-services-in-database.md) (Configurar SQL Server R Services).

+ Asegúrese de que el servicio Launchpad se está ejecutando. En función del entorno, puede que tenga que habilitar las cuentas de trabajo de R para conectarse a SQL Server, instalar bibliotecas de red adicionales, habilitar la ejecución remota de código o reiniciar la instancia una vez configurado todo. Vea [Preguntas más frecuentes sobre actualización e instalación (SQL Server R Services)](../r/upgrade-and-installation-faq-sql-server-r-services.md)

+ Para obtener Visual Studio Code, vea [Download and install Visual Studio Code](https://code.visualstudio.com/Download) (Descargar e instalar Visual Studio Code).

## <a name="next-lesson"></a>Lección siguiente

Ahora que la instancia está lista para trabajar con R, vamos a empezar a trabajar.

Lección 1: [trabajar con entradas y salidas](rtsql-working-with-inputs-and-outputs.md)

Lección 2: [R y SQL objetos de datos y tipos de datos](rtsql-r-and-sql-data-types-and-data-objects.md)

Lección 3: [funciones de uso de R con datos de SQL Server](rtsql-using-r-functions-with-sql-server-data.md)

Lección 4: [crear un modelo de predicción](rtsql-create-a-predictive-model-r.md)

Lección 5: [predecir y trazado de modelo](rtsql-predict-and-plot-from-model.md)
