---
title: "Lección 5: Crear una simulación sencilla (Análisis detallado de ciencia de datos) | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: f420b816-ddab-4a1a-89b9-c8285a2d33a3
caps.latest.revision: "16"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e5dfca8ecef324b510b614ae93b7aefe9a4efe07
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="create-a-simple-simulation"></a>Cree una simulación Simple

Hasta ahora ha estado utilizando las funciones de R que se han diseñado específicamente para mover datos entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y contexto de proceso de una variable local. En cambio, supongamos que escribe una función de R personalizada y quiere ejecutarla en el contexto de servidor.

Puede llamar a una función arbitraria en el contexto del equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la función **rxExec** . También puede utilizar rxExec para distribuir de forma explícita el trabajo a través de núcleos en un solo nodo de servidor.

En esta lección, usará el servidor remoto para crear una simulación sencilla. La simulación no requiere una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos; el ejemplo solo muestra cómo diseñar una función personalizada y, a continuación, llamarlo con la función rxExec.

Para obtener un ejemplo más complejo de usar rxExec, vea este artículo: [paralelismo de grano grueso propia con foreach y rxExec](http://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)

## <a name="create-the-function"></a>Crear la función

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
  
Ahora veamos cómo puede ejecutar la función varias veces para crear una simulación que ayude a determinar la probabilidad de ganar.

## <a name="create-the-simulation"></a>Crear la simulación

Para ejecutar una función arbitraria en el contexto de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo, se llama a la función rxExec. Aunque rxExec también admite la ejecución distribuida de una función en paralelo a través de nodos o núcleos en un contexto de servidor, aquí podrá usarlo solo para ejecutar la función personalizada en el servidor.

1. Llame a la función personalizada como argumento a rxExec, junto con algunos otros parámetros que modifican la simulación.
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    - Use el argumento *timesToRun* para indicar cuántas veces se debe ejecutar la función.  En este caso, lanza los dados 20 veces.
  
    - Los argumentos *RNGseed* y *RNGkind* pueden usarse para controlar la generación de números aleatorios. Si *RNGseed* está establecido en **auto**, se inicializa una secuencia de números aleatorios en paralelo en cada trabajo.
  
2. La función rxExec crea una lista con un elemento para cada ejecución; Sin embargo, no verá mucho ocurre hasta que la lista esté completa. Cuando estén completas todas las iteraciones, la línea que empieza con `length` devolverá un valor.
  
    Después puede ir al paso siguiente para obtener un resumen del registro de perdidas y ganadas.
  
3. Convierta la lista devuelta en un vector con la función `unlist` de R, y resuma los resultados mediante la función `table` .
  
    ```R
    table(unlist(sqlServerExec))
    ```
  
    Los resultados deben tener el siguiente aspecto:
  
     *Pérdida Win* *8 de 12*

## <a name="conclusions"></a>Conclusiones

En este tutorial, se ha convertido en experto en estas tareas:
  
-   Obtener datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para usarlos en análisis
  
-   Crear y modificar orígenes de datos en R
  
-   Pasar modelos, datos y trazados entre la estación de trabajo y el servidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
  
>  [!TIP]
> 
> Si desea experimentar con estas técnicas con un conjunto de datos mayor de 10 millones de observaciones, los archivos de datos están disponibles en el sitio web de análisis de Revolution: [índice de conjuntos de datos](http://packages.revolutionanalytics.com/datasets)
>   
> Para volver a utilizar este tutorial con los archivos de datos más grandes, descargar los datos y, a continuación, modifique cada uno de los orígenes de datos como sigue:
>  - Establezca las variables *ccFraudCsv* y *ccScoreCsv* para que apunten a los nuevos archivos de datos
>  - Cambie el nombre de la tabla a la que se hace referencia en *sqlFraudTable* por *ccFraud10*
>  - Cambie el nombre de la tabla a la que se hace referencia en *sqlScoreTable* por *ccFraudScore10*

## <a name="previous-step"></a>Paso anterior

[Mover datos entre SQL Server y el archivo xdf.](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)


