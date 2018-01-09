---
title: "Cree una simulación simple (SQL y R profundización) | Documentos de Microsoft"
ms.custom: 
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs: R
ms.assetid: f420b816-ddab-4a1a-89b9-c8285a2d33a3
caps.latest.revision: "16"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: c6aa0cd9afcb3b125c73106272979d008c2062bd
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="create-a-simple-simulation-sql-and-r-deep-dive"></a>Cree una simulación simple (SQL y R profundización)

En este artículo es el último paso del tutorial exhaustiva de ciencia de datos, acerca de cómo usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Hasta ahora ha estado utilizando las funciones de R que se han diseñado específicamente para mover datos entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y contexto de proceso de una variable local. En cambio, supongamos que escribe una función de R personalizada y quiere ejecutarla en el contexto de servidor.

Puede llamar a una función arbitraria en el contexto del equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la función [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) . También puede usar **rxExec** para distribuir de forma explícita el trabajo a través de núcleos en un único servidor.

En esta lección, se utiliza el servidor remoto para crear una simulación sencilla. La simulación no requiere datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ; el ejemplo solo muestra cómo diseñar una función personalizada y llamarla mediante la función **rxExec** .

Para obtener un ejemplo más complejo de usar **rxExec**, consulte este artículo: [paralelismo de grano grueso propia con foreach y rxExec](http://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)

## <a name="create-the-custom-function"></a>Crear la función personalizada

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
  
2.  Para simular un único juego de dados, ejecute la función.
  
    ```R
    rollDice()
    ```
  
    ¿Ha ganado o perdido?
  
Ahora veamos cómo puede usar **rxExec** para ejecutar la función varias veces, para crear una simulación que ayuda a determinar la probabilidad de que un win.

## <a name="create-the-simulation"></a>Crear la simulación

Para ejecutar una función arbitraria en el contexto del equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , llame a la función **rxExec** . Aunque **rxExec** también admite la ejecución distribuida de una función en paralelo en todos los nodos o núcleos en un contexto de servidor, a continuación, se ejecuta personalizado funcione en el equipo de SQL Server.

1. Llamar a la función personalizada como argumento pasado a **rxExec**, junto con otros parámetros que modifican la simulación.
  
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
  
     *Pérdida Win* *8 de 12*

## <a name="conclusions"></a>Conclusiones

En este tutorial, se ha convertido en experto en estas tareas:
  
-   Obtener datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para usarlos en análisis
  
-   Crear y modificar orígenes de datos en R
  
-   Pasar modelos, datos y trazados entre la estación de trabajo y el servidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
  

Si desea experimentar con estas técnicas con un conjunto de datos mayor de 10 millones de observaciones, los archivos de datos están disponibles en el sitio web de análisis de Revolution: [índice de conjuntos de datos](http://packages.revolutionanalytics.com/datasets)

Para volver a utilizar este tutorial con los archivos de datos más grandes, descargar los datos y, a continuación, modifique cada uno de los orígenes de datos como sigue:

1. Modifique las variables de `ccFraudCsv` y `ccScoreCsv` para que apunte a los nuevos archivos de datos
2. Cambiar el nombre de la tabla que se hace referencia en *sqlFraudTable* a`ccFraud10`
3. Cambiar el nombre de la tabla que se hace referencia en *sqlScoreTable* a`ccFraudScore10`

## <a name="additional-samples"></a>Ejemplos adicionales

Ahora que ha aprendido al uso de funciones de RevoScaler para pasar y transformar datos y contextos de proceso, consulte estos tutoriales:

[Tutoriales de R para servicios de aprendizaje de máquina](machine-learning-services-tutorials.md)
## <a name="previous-step"></a>Paso anterior

[Mover datos entre SQL Server y el archivo XDF](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)
