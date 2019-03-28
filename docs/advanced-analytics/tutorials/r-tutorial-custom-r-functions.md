---
title: Ejecutar funciones personalizadas de R en SQL Server con RevoScaleR rxExec - SQL Server Machine Learning
description: Tutorial del tutorial sobre cómo ejecutar el script personalizado de R en SQL Server con las funciones de RevoScaleR.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 5773641f442fe844657e6aabd6b9dcea24f4475b
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58509912"
---
# <a name="run-custom-r-functions-on-sql-server-using-rxexec"></a>Ejecutar funciones personalizadas de R en SQL Server con rxExec
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Puede ejecutar funciones de R personalizadas en el contexto de SQL Server, pasando la función a través [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec), suponiendo que las bibliotecas que se requiere la secuencia de comandos también están instaladas en el servidor y esas bibliotecas son compatibles con la base distribución de R. 

El **rxExec** funcionando en **RevoScaleR** proporciona un mecanismo para ejecutar los scripts de R que necesita. Además, **rxExec** puede distribuir explícitamente el trabajo entre varios núcleos en un solo servidor, agregar escala a secuencias de comandos que en caso contrario, se limitan a las restricciones de recursos del motor de R nativa.

En este tutorial, usará datos simulados para demostrar la ejecución de una función personalizada de R que se ejecuta en un servidor remoto.

## <a name="prerequisites"></a>Requisitos previos

+ [Servicios SQL Server 2017 Machine Learning (con R)](../install/sql-machine-learning-services-windows-install.md) o [SQL Server 2016 R Services (in-Database)](../install/sql-r-services-windows-install.md)
  
+ [Permisos de base de datos](../security/user-permission.md) y un inicio de sesión de usuario de base de datos de SQL Server

+ [Una estación de trabajo de desarrollo con las bibliotecas de RevoScaleR](../r/set-up-a-data-science-client.md)

La distribución de R en la estación de trabajo cliente proporciona un integrado **Rgui** herramienta que puede usar para ejecutar el script de R en este tutorial. También puede usar un IDE como RStudio o herramientas de R para Visual Studio.

## <a name="create-the-remote-compute-context"></a>Crear el contexto de cálculo remoto

Ejecute los siguientes comandos de R en una estación de trabajo cliente. Por ejemplo, usa **Rgui**, inícielo desde esta ubicación: C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64\.

1. Especifique la cadena de conexión para la instancia de SQL Server donde se realizan los cálculos. El servidor debe configurarse para la integración de R. El nombre de la base de datos no se usa en este ejercicio, pero la cadena de conexión requiere uno. Si tiene una base de datos de ejemplo o de prueba, úsela.

    **Con un inicio de sesión de SQL**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>; Database=<database-name>;Uid=<SQL-user-name>;Pwd=<password>"
    ```

    **Con la autenticación de Windows**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL-Server-instance-name>;Database=<database-name>;Trusted_Connection=True"
    ```

2. Crear un contexto de cálculo remoto a la instancia de SQL Server que se hace referencia en la cadena de conexión.

    ```R
    sqlCompute <- RxInSqlServer(connectionString = sqlConnString)
    ```

3. Activar el contexto de cálculo y, a continuación, devolver la definición del objeto como un paso de confirmación. Debería ver las propiedades del objeto de contexto de proceso.

    ```R
    rxSetComputeContext(sqlCompute)
    rxGetComputeContext()
    ```

## <a name="create-the-custom-function"></a>Cree la función personalizada

En este ejercicio, creará una función personalizada de R que simula un casino común que consta de lanzar un par de dados. Las reglas del juego determinan un resultado de pérdida o win:

+ Saca 7 u 11 en el lanzamiento inicial, gana.
+ Rollo de 2, 3 o 12, pierde.
+ Poner un 4, 5, 6, 8, 9 o 10, ese número se convierte en el punto y sigue lanzando hasta que vuelve a sacar sus puntos de nuevo (en cuyo caso gana) o saca un 7, en cuyo caso pierde.

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
  
2.  Simular un solo juego de dados mediante la ejecución de la función.
  
    ```R
    rollDice()
    ```
  
    ¿Ha ganado o perdido?
  
Ahora que tiene una secuencia de comandos operativa, veamos cómo puede usar **rxExec** para ejecutar la función varias veces para crear una simulación que ayude a determinar la probabilidad de ganar.

## <a name="pass-rolldice-in-rxexec"></a>Pasar rollDice() rxExec

Para ejecutar una función arbitraria en el contexto de un servidor SQL remoto, llame a la **rxExec** función.

1. Llame a la función personalizada como argumento a **rxExec**, junto con otros parámetros que modifican la simulación.
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    + Use el argumento *timesToRun* para indicar cuántas veces se debe ejecutar la función.  En este caso, lanza los dados 20 veces.
  
    + Los argumentos *RNGseed* y *RNGkind* pueden usarse para controlar la generación de números aleatorios. Si *RNGseed* está establecido en **auto**, se inicializa una secuencia de números aleatorios en paralelo en cada trabajo.
  
2. La función **rxExec** crea una lista con un elemento para cada ejecución, pero no verá que suceda mucho hasta que la lista esté completa. Cuando todas las iteraciones termine, la línea que empieza con **longitud** devolverá un valor.
  
    Después puede ir al paso siguiente para obtener un resumen del registro de perdidas y ganadas.
  
3. Convierta la lista devuelta en un vector con la función **unlist** de R, y resuma los resultados mediante la función **table** .
  
    ```R
    table(unlist(sqlServerExec))
    ```
  
    Los resultados deben tener el siguiente aspecto:
  
     *Perdidas ganadas* *12 8*

## <a name="conclusion"></a>Conclusión

Aunque este ejercicio es simplista, muestra un mecanismo importante para la integración de funciones arbitrarias de R en el script de R que se ejecuta en SQL Server. Para resumir los puntos clave que hacen posible esta técnica:

+ SQL Server debe configurarse para la integración de R y aprendizaje automático: [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) con la característica R, o [SQL Server 2016 R Services (en bases de datos)](../install/sql-r-services-windows-install.md).

+ Bibliotecas de terceros o de código abierto utilizadas en la función, incluidas las dependencias, deben instalarse en SQL Server. Para obtener más información, consulte [instalar nuevos paquetes de R](../r/install-additional-r-packages-on-sql-server.md).

+ Mover el script desde un entorno de desarrollo a un entorno de producción protegidos puede introducir las restricciones de firewall y red. Probar con cuidado para asegurarse de que la secuencia de comandos es llevar a cabo según lo previsto.

## <a name="next-steps"></a>Pasos siguientes

Para obtener un ejemplo más complejo de usar **rxExec**, consulte este artículo: [Paralelismo de grano grueso con foreach y rxExec](https://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)
