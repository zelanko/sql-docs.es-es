---
title: Crear una simulación sencilla (análisis detallado R y SQL) | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b0db5fdfd177f1303432659f7a96b0fbf111c000
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51698243"
---
# <a name="create-a-simple-simulation-sql-and-r-deep-dive"></a>Crear una simulación sencilla (análisis detallado SQL y R)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo es el último paso del tutorial de análisis detallado de ciencia de datos, acerca de cómo usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Hasta ahora que ha estado usando funciones de R que están diseñadas específicamente para mover datos entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y contexto de cálculo de una variable local. En cambio, supongamos que escribe una función de R personalizada y quiere ejecutarla en el contexto de servidor.

Puede llamar a una función arbitraria en el contexto del equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la función [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) . También puede usar **rxExec** para distribuir explícitamente el trabajo entre núcleos en un único servidor.

En esta lección, usará el servidor remoto para crear una simulación sencilla. La simulación no requiere datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ; el ejemplo solo muestra cómo diseñar una función personalizada y llamarla mediante la función **rxExec** .

Para obtener un ejemplo más complejo de usar **rxExec**, consulte este artículo: [paralelismo de grano grueso con foreach y rxExec](https://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)

## <a name="create-the-custom-function"></a>Cree la función personalizada

Un juego de casino común consiste en lanzar un par de dados, con estas reglas:

- Si saca 7 u 11 en el lanzamiento inicial, gana.
- Si saca 2, 3 o 12, pierde.
- Si saca 4, 5, 6, 8, 9 o 10, ese número se convierte en sus puntos y sigue lanzando hasta que vuelve a sacar sus puntos de nuevo (en cuyo caso gana) o saca un 7, en cuyo caso pierde.

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
                { result \<- "Loss" }
                else if (count > 1 && roll == 7 )
                { result \<- "Loss" }
                else if (count > 1 && point == roll)
                { result <- "Win" }
                else { count <- count + 1 }
            }
            result
    }
    ```
  
2.  Para simular un solo juego de dados, ejecute la función.
  
    ```R
    rollDice()
    ```
  
    ¿Ha ganado o perdido?
  
Ahora veamos cómo puede usar **rxExec** para ejecutar la función varias veces, para crear una simulación que ayude a determinar la probabilidad de ganar.

## <a name="create-the-simulation"></a>Crear la simulación

Para ejecutar una función arbitraria en el contexto del equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , llame a la función **rxExec** . Aunque **rxExec** también admite la ejecución distribuida de una función en paralelo en todos los nodos o núcleos en un contexto de servidor, aquí lo ejecuciones de función personalizado en el equipo de SQL Server.

1. Llame a la función personalizada como argumento a **rxExec**, junto con otros parámetros que modifican la simulación.
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    - Use el argumento *timesToRun* para indicar cuántas veces se debe ejecutar la función.  En este caso, lanza los dados 20 veces.
  
    - Los argumentos *RNGseed* y *RNGkind* pueden usarse para controlar la generación de números aleatorios. Si *RNGseed* está establecido en **auto**, se inicializa una secuencia de números aleatorios en paralelo en cada trabajo.
  
2. La función **rxExec** crea una lista con un elemento para cada ejecución, pero no verá que suceda mucho hasta que la lista esté completa. Cuando estén completas todas las iteraciones, la línea que empieza con `length` devolverá un valor.
  
    Después puede ir al paso siguiente para obtener un resumen del registro de perdidas y ganadas.
  
3. Convierta la lista devuelta en un vector con la función `unlist` de R, y resuma los resultados mediante la función `table` .
  
    ```R
    table(unlist(sqlServerExec))
    ```
  
    Los resultados deben tener el siguiente aspecto:
  
     *Perdidas ganadas* *12 8*

## <a name="conclusions"></a>Conclusiones

En este tutorial, se ha convertido en experto en estas tareas:
  
-   Obtener datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para usarlos en análisis
  
-   Crear y modificar orígenes de datos en R
  
-   Pasar modelos, datos y trazados entre la estación de trabajo y el servidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
  

Si desea experimentar con estas técnicas con un conjunto de datos mayor de 10 millones de observaciones, los archivos de datos están disponibles desde el sitio de web de Revolution analytics: [índice de conjuntos de datos](https://packages.revolutionanalytics.com/datasets)

Para volver a usar este tutorial con los archivos de datos más grandes, descargar los datos y, a continuación, modifique cada uno de los orígenes de datos como sigue:

1. Modifique las variables `ccFraudCsv` y `ccScoreCsv` para que apunte a los nuevos archivos de datos
2. Cambiar el nombre de la tabla hace referenciado en *sqlFraudTable* a `ccFraud10`
3. Cambiar el nombre de la tabla hace referenciado en *sqlScoreTable* a `ccFraudScore10`

## <a name="additional-samples"></a>Encontrará más ejemplos

Ahora que ha aprendido a usar contextos de cálculo y las funciones de RevoScaler para pasar y transformar datos, consulte estos tutoriales:

[Tutoriales de R para Machine Learning Services](machine-learning-services-tutorials.md)
## <a name="previous-step"></a>Paso anterior

[Mover datos entre SQL Server y el archivo XDF](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)
