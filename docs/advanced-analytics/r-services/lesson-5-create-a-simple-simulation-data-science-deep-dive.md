---
title: "Lecci&#243;n 5: Crear una simulaci&#243;n sencilla (An&#225;lisis detallado de ciencia de datos) | Microsoft Docs"
ms.custom: ""
ms.date: "10/03/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: f420b816-ddab-4a1a-89b9-c8285a2d33a3
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# Lecci&#243;n 5: Crear una simulaci&#243;n sencilla (An&#225;lisis detallado de ciencia de datos)
Hasta ahora, ha estado usando funciones de R proporcionadas por SQL Server R Services que están diseñadas específicamente para mover datos entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y un contexto de proceso local. En cambio, supongamos que escribe una función de R personalizada y quiere ejecutarla en el contexto de servidor.  
  
Puede llamar a una función arbitraria en el contexto del equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la función *rxExec*. También puede usar *rxExec* para distribuir explícitamente el trabajo entre núcleos en un solo nodo de servidor.  
  
En esta lección, usará el servidor remoto para crear una simulación sencilla. La simulación no requiere datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; el ejemplo solo muestra cómo diseñar una función personalizada y llamarla mediante la función *rxExec*.  
  
Para obtener un ejemplo más complejo del uso de *rxExec*, consulte este artículo: [http://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html](http://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html).  
  
## Crear la función  
Un juego de casino común consiste en lanzar un par de dados, con estas reglas:  
  
-   Si saca 7 u 11 en el lanzamiento inicial, gana.  
  
-   Si saca 2, 3 o 12, pierde.  
  
-   Si saca 4, 5, 6, 8, 9 o 10, ese número se convierte en sus puntos y sigue lanzando hasta que vuelve a sacar sus puntos de nuevo (en cuyo caso gana) o saca un 7, en cuyo caso pierde.  
  
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
  
2.  Para simular un solo juego de dados, ejecute la función.  
  
    ```R  
    rollDice()   
    ```  
  
    ¿Ha ganado o perdido?  
  
Ahora veamos cómo puede ejecutar la función varias veces para crear una simulación que ayude a determinar la probabilidad de ganar.  
  
## Crear la simulación  
Para ejecutar una función arbitraria en el contexto del equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], llame a la función *rxExec*. Aunque *rxExec* también es compatible con la ejecución distribuida de una función en paralelo en todos los nodos o núcleos en un contexto de servidor, aquí la usará solo para ejecutar la función personalizada en el servidor.  
  
1.  Llame a la función personalizada como un argumento de *rxExec*, junto con algunos de los otros parámetros que modifican la simulación.  
  
    ```R  
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")   
    length(sqlServerExec)   
    ```  
  
    -   Use el argumento *timesToRun* para indicar cuántas veces se debe ejecutar la función.  En este caso, lanza los dados 20 veces.  
  
    -   Los argumentos *RNGseed* y *RNGkind* pueden usarse para controlar la generación de números aleatorios. Si *RNGseed* está establecido en **auto**, se inicializa una secuencia de números aleatorios en paralelo en cada trabajo.  
  
2.  La función *rxExec* crea una lista con un elemento para cada ejecución, pero no verá que suceda mucho hasta que la lista esté completa. Cuando estén completas todas las iteraciones, la línea que empieza con `length` devolverá un valor.  
  
    Después puede ir al paso siguiente para obtener un resumen del registro de perdidas y ganadas.  
  
3.  Convierta la lista devuelta en un vector con la función *unlist* de R, y resuma los resultados mediante la función *table*.  
  
    ```R  
    table(unlist(sqlServerExec))  
    ```  
  
    Los resultados deben tener el siguiente aspecto:  
  
     *Perdidas Ganadas*   
     *12 8*  
  
## Conclusiones  
En este tutorial, se ha convertido en experto en estas tareas:  
  
-   Obtener datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para usarlos en análisis  
  
-   Crear y modificar orígenes de datos en R  
  
-   Pasar modelos, datos y trazados entre la estación de trabajo y el servidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
>  [!TIP]
> 
> Si quiere probar estas técnicas con un conjunto de datos más grande de 10 millones de observaciones, los archivos de datos están disponibles en [http://packages.revolutionanalytics.com/datasets](http://packages.revolutionanalytics.com/datasets).  
>   
> Para volver a usar este tutorial con los archivos de datos más grandes, simplemente descargue los datos y, después, modifique los orígenes de datos de la manera siguiente:   
>  -   Establezca las variables *ccFraudCsv* y *ccScoreCsv* para que apunten a los nuevos archivos de datos     
>  -   Cambie el nombre de la tabla a la que se hace referencia en *sqlFraudTable* por *ccFraud10*    
>  -   Cambie el nombre de la tabla a la que se hace referencia en *sqlScoreTable* por *ccFraudScore10*   
  
## Paso anterior  
[Mover datos entre SQL Server y el archivo XDF &#40;Análisis detallado de ciencia de datos&#41;](../../advanced-analytics/r-services/move-data-between-sql-server-and-xdf-file-data-science-deep-dive.md)  
  
  
  
