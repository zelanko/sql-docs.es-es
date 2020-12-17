---
title: Funciones de R personalizadas mediante rxExec
description: Aprenda a usar datos simulados para mostrar la ejecución de una función de R personalizada que se ejecuta en un servidor remoto.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: 3088409167e41aa478ef831c72eee100650919a1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470586"
---
# <a name="run-custom-r-functions-on-sql-server-using-rxexec-sql-server-and-revoscaler-tutorial"></a>Ejecución de funciones de R personalizadas en SQL Server mediante rxExec (tutorial de SQL Server y RevoScaleR)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Este es el tutorial 14 de la [serie de tutoriales de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre el uso de las [funciones de RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En este tutorial, usará datos simulados para mostrar la ejecución de una función de R personalizada que se ejecuta en un servidor remoto.

Puede ejecutar funciones de R personalizadas en el contexto de SQL Server pasando la función a través de [rxExec](/machine-learning-server/r-reference/revoscaler/rxexec), siempre y cuando las bibliotecas requeridas por el script también estén instaladas en el servidor y sean compatibles con la distribución base de R. 

La función **rxExec** de **RevoScaleR** proporciona un mecanismo para ejecutar cualquier script de R que necesite. Además, **rxExec** puede distribuir explícitamente el trabajo entre varios núcleos en un solo servidor, agregando escala a los scripts que, de otro modo, se limitan a las restricciones de recursos del motor de R nativo.

## <a name="prerequisites"></a>Prerrequisitos

+ [SQL Server Machine Learning Services (con R)](../install/sql-machine-learning-services-windows-install.md) o [SQL Server 2016 R Services (en base de datos)](../install/sql-r-services-windows-install.md)
  
+ [Permisos de base de datos](../security/user-permission.md) y un inicio de sesión de usuario de base de datos de SQL Server

+ [Una estación de trabajo de desarrollo con las bibliotecas de RevoScaleR](../r/set-up-a-data-science-client.md)

La distribución de R en la estación de trabajo del cliente proporciona una herramienta integrada de **Rgui** que puede usar para ejecutar el script de R en este tutorial. También puede usar un IDE como RStudio o Herramientas de R para Visual Studio.

## <a name="create-the-remote-compute-context"></a>Creación del contexto de proceso remoto

Ejecute los siguientes comandos de R en una estación de trabajo del cliente. Por ejemplo, si usa **Rgui**, inícielo desde esta ubicación: C:\Archivos de programa\Microsoft\R Client\R_SERVER\bin\x64\..

1. Especifique la cadena de conexión para la instancia de SQL Server en la que se realizan los cálculos. El servidor debe estar configurado para la integración de R. El nombre de la base de datos no se usa en este ejercicio, pero la cadena de conexión requiere uno. Si tiene una base de datos de prueba o de ejemplo, puede usarla.

    **Con un inicio de sesión de SQL**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>; Database=<database-name>;Uid=<SQL-user-name>;Pwd=<password>"
    ```

    **Con la autenticación de Windows**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>;Database=<database-name>;Trusted_Connection=True"
    ```

2. Cree un contexto de proceso remoto en la instancia de SQL Server a la que se hace referencia en la cadena de conexión.

    ```R
    sqlCompute <- RxInSqlServer(connectionString = sqlConnString)
    ```

3. Active el contexto de proceso y, después, devuelva la definición del objeto como un paso de confirmación. Debería ver las propiedades del objeto del contexto de proceso.

    ```R
    rxSetComputeContext(sqlCompute)
    rxGetComputeContext()
    ```

## <a name="create-the-custom-function"></a>Creación de la función personalizada

En este ejercicio, creará una función de R personalizada que simula un juego de casino común que consiste en lanzar un par de dados. Las reglas del juego determinan un resultado de ganancia o pérdida:

+ Si saca 7 u 11 en el lanzamiento inicial, gana.
+ Si saca 2, 3 o 12, pierde.
+ Si saca 4, 5, 6, 8, 9 o 10, ese número se convierte en su puntuación, y sigue lanzando hasta que vuelve a sacar sus puntos de nuevo (en cuyo caso gana) o saca un 7, en cuyo caso pierde.

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
  
2.  Simule un solo juego de dados, ejecutando la función.
  
    ```R
    rollDice()
    ```
  
    ¿Ha ganado o perdido?
  
Ahora que tiene un script operacional, veamos cómo puede ejecutar la función **rxExec** varias veces para crear una simulación que ayude a determinar la probabilidad de ganar.

## <a name="pass-rolldice-in-rxexec"></a>Pasar rollDice () en rxExec

Para ejecutar una función arbitraria en el contexto de una instancia remota de SQL Server, llame a la función **rxExec**.

1. Llame a la función personalizada como un argumento de **rxExec**, junto con otros parámetros que modifican la simulación.
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    + Use el argumento *timesToRun* para indicar cuántas veces se debe ejecutar la función.  En este caso, lanza los dados 20 veces.
  
    + Los argumentos *RNGseed* y *RNGkind* pueden usarse para controlar la generación de números aleatorios. Si *RNGseed* está establecido en **auto**, se inicializa una secuencia de números aleatorios en paralelo en cada trabajo.
  
2. La función **rxExec** crea una lista con un elemento para cada ejecución, pero no verá que suceda mucho hasta que la lista esté completa. Cuando estén completas todas las iteraciones, la línea que empieza con **length** devolverá un valor.
  
    Después puede ir al paso siguiente para obtener un resumen del registro de perdidas y ganadas.
  
3. Convierta la lista devuelta en un vector con la función **unlist** de R, y resuma los resultados mediante la función **table** .
  
    ```R
    table(unlist(sqlServerExec))
    ```
  
    Los resultados deben tener el siguiente aspecto:
  
     *Perdidas Ganadas* *12 8*

## <a name="conclusion"></a>Conclusión

Aunque este ejercicio es simplista, muestra un mecanismo importante para integrar funciones de R arbitrarias en el script de R que se ejecuta en SQL Server. Como resumen de los puntos clave que hacen posible esta técnica:

+ SQL Server se debe configurar para el aprendizaje automático y la integración de R: [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) con la función R o [SQL Server 2016 R Services (en base de datos)](../install/sql-r-services-windows-install.md).

+ Debe tener instaladas en SQL Server las bibliotecas de código abierto o de terceros que se usan en la función, incluidas las dependencias. Para obtener más información, vea [Instalación de nuevos paquetes de R](../package-management/install-additional-r-packages-on-sql-server.md).

+ Si mueve el script de un entorno de desarrollo a un entorno de producción protegido se pueden presentar restricciones de firewall y de red. Realice una prueba detenidamente para asegurarse de que el script puede funcionar según lo previsto.

## <a name="next-steps"></a>Pasos siguientes

Para obtener un ejemplo más complejo del uso de **rxExec**, consulte este artículo: [Paralelismo de grano grueso con foreach y rxExec](https://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)