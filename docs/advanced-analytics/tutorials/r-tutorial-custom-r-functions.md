---
title: Ejecutar funciones de R personalizadas en SQL Server mediante RevoScaleR rxExec
description: Tutorial tutorial sobre cómo ejecutar scripts de R personalizados en SQL Server con las funciones de RevoScaleR.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: d90e2d4887154d3545884a77d0290e632f04a569
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470596"
---
# <a name="run-custom-r-functions-on-sql-server-using-rxexec"></a>Ejecutar funciones de R personalizadas en SQL Server mediante rxExec
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Puede ejecutar funciones de R personalizadas en el contexto de SQL Server pasando la función a través de [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec), suponiendo que las bibliotecas que requiere el script también están instaladas en el servidor y esas bibliotecas son compatibles con la distribución base de R. 

La función **rxExec** de **RevoScaleR** proporciona un mecanismo para ejecutar cualquier script de R que necesite. Además, **rxExec** puede distribuir explícitamente el trabajo entre varios núcleos en un solo servidor, agregando escala a los scripts que de otro modo se limitan a las restricciones de recursos del motor de R nativo.

En este tutorial, usará datos simulados para mostrar la ejecución de una función personalizada de R que se ejecuta en un servidor remoto.

## <a name="prerequisites"></a>Requisitos previos

+ [SQL Server 2017 Machine Learning Services (con r)](../install/sql-machine-learning-services-windows-install.md) o [SQL Server 2016 R Services (en base de datos)](../install/sql-r-services-windows-install.md)
  
+ [Permisos de base de datos](../security/user-permission.md) y un inicio de sesión de usuario de SQL Server Database

+ [Una estación de trabajo de desarrollo con las bibliotecas de RevoScaleR](../r/set-up-a-data-science-client.md)

La distribución de R en la estación de trabajo cliente proporciona una herramienta de **Rgui** integrada que puede usar para ejecutar el script de r en este tutorial. También puede usar un IDE como RStudio o Herramientas de R para Visual Studio.

## <a name="create-the-remote-compute-context"></a>Crear el contexto de cálculo remoto

Ejecute los siguientes comandos de R en una estación de trabajo cliente. Por ejemplo, si usa **Rgui**, inícielo desde esta ubicación: C:\Archivos de Files\Microsoft\R Client\R_SERVER\bin\x64\.

1. Especifique la cadena de conexión para la instancia de SQL Server en la que se realizan los cálculos. El servidor debe estar configurado para la integración de R. El nombre de la base de datos no se utiliza en este ejercicio, pero la cadena de conexión requiere uno. Si tiene una base de datos de prueba o de ejemplo, puede usarla.

    **Con un inicio de sesión de SQL**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>; Database=<database-name>;Uid=<SQL-user-name>;Pwd=<password>"
    ```

    **Con la autenticación de Windows**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>;Database=<database-name>;Trusted_Connection=True"
    ```

2. Cree un contexto de cálculo remoto en la instancia de SQL Server a la que se hace referencia en la cadena de conexión.

    ```R
    sqlCompute <- RxInSqlServer(connectionString = sqlConnString)
    ```

3. Active el contexto de cálculo y, a continuación, devuelva la definición del objeto como un paso de confirmación. Debería ver las propiedades del objeto de contexto de proceso.

    ```R
    rxSetComputeContext(sqlCompute)
    rxGetComputeContext()
    ```

## <a name="create-the-custom-function"></a>Crear la función personalizada

En este ejercicio, creará una función de R personalizada que simula un casino común que se compone de un par de dados. Las reglas del juego determinan un resultado de ganancia o pérdida:

+ Revierta un 7 u 11 en el rollo inicial, gana.
+ Rollo 2, 3 o 12, pierde.
+ Haga rodar 4, 5, 6, 8, 9 o 10, ese número se convierte en el punto y continúa hasta que vuelva a poner el punto en el lugar (en cuyo caso gana) o revierta un 7, en cuyo caso se pierde.

El juego se simula con facilidad en R si crea una función personalizada y, después, la ejecuta muchas veces.

1.  Cree la función personalizada mediante el siguiente código de R:
  
    ```R
    rollDice <- function()
    {
        result <- NULL
        point <- NULL
        count <- 1
            while (is.null(result))
            {
                roll <- sum(sample(6, 2, replace=TRUE))
  
                if (is.null(point))
                { point <- roll }
                if (count == 1 && (roll == 7 || roll == 11))
                {  result <- "Win" }
                else if (count == 1 && (roll == 2 || roll == 3 || roll == 12))
                { result <- "Loss" }
                else if (count > 1 && roll == 7 )
                { result <- "Loss" }
                else if (count > 1 && point == roll)
                { result <- "Win" }
                else { count <- count + 1 }
            }
            result
    }
    ```
  
2.  Simule un único juego de dados mediante la ejecución de la función.
  
    ```R
    rollDice()
    ```
  
    ¿Ha ganado o perdido?
  
Ahora que tiene un script operativo, veamos cómo se puede usar **rxExec** para ejecutar la función varias veces para crear una simulación que ayude a determinar la probabilidad de un logro.

## <a name="pass-rolldice-in-rxexec"></a>Pase rollDice () en rxExec

Para ejecutar una función arbitraria en el contexto de un SQL Server remoto, llame a la función **rxExec** .

1. Llame a la función personalizada como argumento a **rxExec**, junto con otros parámetros que modifican la simulación.
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    + Use el argumento *timesToRun* para indicar cuántas veces se debe ejecutar la función.  En este caso, lanza los dados 20 veces.
  
    + Los argumentos *RNGseed* y *RNGkind* pueden usarse para controlar la generación de números aleatorios. Si *RNGseed* está establecido en **auto**, se inicializa una secuencia de números aleatorios en paralelo en cada trabajo.
  
2. La función **rxExec** crea una lista con un elemento para cada ejecución, pero no verá que suceda mucho hasta que la lista esté completa. Una vez completadas todas las iteraciones, la línea que empieza por la **longitud** devolverá un valor.
  
    Después puede ir al paso siguiente para obtener un resumen del registro de perdidas y ganadas.
  
3. Convierta la lista devuelta en un vector con la función **unlist** de R, y resuma los resultados mediante la función **table** .
  
    ```R
    table(unlist(sqlServerExec))
    ```
  
    Los resultados deben tener el siguiente aspecto:
  
     *Pérd gana* *12 8*

## <a name="conclusion"></a>Conclusión

Aunque este ejercicio es simplista, muestra un mecanismo importante para integrar funciones de R arbitrarias en el script de R que se ejecuta en SQL Server. Para resumir los puntos clave que hacen posible esta técnica:

+ SQL Server se debe configurar para el aprendizaje automático y la integración de R: [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) con la característica de r o [SQL Server 2016 R Services (en base de datos)](../install/sql-r-services-windows-install.md).

+ Las bibliotecas de código abierto o de terceros que se usan en la función, incluidas las dependencias, deben instalarse en SQL Server. Para obtener más información, vea [instalar nuevos paquetes de R](../r/install-additional-r-packages-on-sql-server.md).

+ Mover el script de un entorno de desarrollo a un entorno de producción protegido puede introducir restricciones de firewall y de red. Realice una prueba detenidamente para asegurarse de que el script es capaz de funcionar según lo previsto.

## <a name="next-steps"></a>Pasos siguientes

Para obtener un ejemplo más complejo del uso de **rxExec**, consulte este artículo: [Paralelismo de grano grueso con foreach y rxExec](https://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)
