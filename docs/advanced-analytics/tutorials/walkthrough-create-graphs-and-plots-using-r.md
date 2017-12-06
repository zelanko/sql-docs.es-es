---
title: "Crear gráficos y los gráficos con SQL y R (tutorial) | Documentos de Microsoft"
ms.date: 11/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 5f70f0a6-fd4a-410f-9f44-1605503f77ec
caps.latest.revision: "16"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 8cf83243f4c2c9dd5d114799166160d53573c90f
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="create-graphs-and-plots-using-sql-and-r-walkthrough"></a>Crear gráficos y los gráficos con SQL y R (tutorial)

En esta parte del tutorial, aprenderá técnicas para generar gráficos y mapas mediante R con datos de SQL Server. Crear un histograma simple, para practicar y, a continuación, desarrolle un gráfico de mapa más complejo.

### <a name="create-a-histogram"></a>Crear un histograma

1. Ejecute estas líneas para generar el primer trazado mediante la función [rxHistogram](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource) .  La función rxHistogram proporciona funcionalidad similar a la de los paquetes de R de código abierto, pero puede ejecutar en un contexto de ejecución remoto.

    ```R
    # Plot fare amount on SQL Server and return the plot
    start.time <- proc.time()
    rxHistogram(~fare_amount, data = inDataSource, title = "Fare Amount Histogram")
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2), " seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate plot.", sep=""))
    ```

2. La imagen se devuelve en el dispositivo de gráficos de R para el entorno de desarrollo.  Por ejemplo, en RStudio, haga clic en la ventana **Trazar** .  En [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)], se abre una ventana de gráficos independiente.

    ![Uso de rxHistogram para trazar cantidades de tarifas](media/rsql-e2e-rxhistogramresult.png "Uso de rxHistogram para trazar cantidades de tarifas")

    > [!NOTE]
    > ¿Se ve diferente el gráfico?
    >  
    > Esto es así porque _inDataSource_ usa sólo las primeras 1000 filas. El orden de filas utilizando TOP es no determinista en ausencia de una cláusula ORDER BY, por lo que se espera que los datos y el gráfico resultante pueden variar.
    > Esta imagen en particular se generó con alrededor de 10 000 filas de datos. Se recomienda experimentar con distintos números de filas para obtener distintos gráficos y observar cuánto tiempo se tarda en devolver los resultados en su entorno.

### <a name="create-a-map-plot"></a>Crear un gráfico de mapa

Normalmente, los servidores de base de datos bloquean el acceso a Internet. Esto puede ser un problema al usar paquetes de R que necesitan descargar mapas u otras imágenes para generar gráficos. Sin embargo, hay una solución que le resultarán útiles al desarrollar sus propias aplicaciones. Básicamente, generar la representación de mapa en el cliente y luego superponer los puntos que se almacenan como atributos de la tabla de SQL Server en el mapa.

1. Definir la función que crea el objeto de trazado de R. La función personalizada *mapPlot* crea un gráfico de dispersión que usa las ubicaciones de recogida de taxi y se representa el número de llevar a que se inició desde cada ubicación. Usa los paquetes **ggplot2** y  **ggmap** , que ya deberían estar instalados y cargados.

    ```R
    mapPlot <- function(inDataSource, googMap){
        library(ggmap)
        library(mapproj)
        ds <- rxImport(inDataSource)
        p <- ggmap(googMap)+
        geom_point(aes(x = pickup_longitude, y =pickup_latitude ), data=ds, alpha =.5,
    color="darkred", size = 1.5)
        return(list(myplot=p))
    }
    ```

    + El *mapPlot* función toma dos argumentos: un objeto de datos existente, que se definió anteriormente con RxSqlServerData, y la representación en forma de mapa que se pasa desde el cliente.
    + En la línea que comienza con la *ds* variable, se usa para cargar en datos de memoria desde el origen de datos creado anteriormente rxImport *inDataSource*. (Dicho origen de datos contiene solo 1000 filas; si desea crear un mapa con más puntos de datos, puede sustituir un origen de datos diferente).
    + Siempre que use **de código abierto** funciones de R, los datos deben cargarse en tramas de datos en la memoria local. Sin embargo, mediante una llamada a la [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) función, puede ejecutar en la memoria del contexto de proceso remoto.

2. Cambiar el contexto de proceso local y cargar las bibliotecas necesarias para crear las asignaciones.

    ```R
    rxSetComputeContext("local")
    library(ggmap)
    library(mapproj)
    gc <- geocode("Times Square", source = "google")
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color');
    ```

    + La variable `gc` almacena un conjunto de coordenadas para Times Square, Nueva York.

    + La línea que comienza con `googmap` genera un mapa con las coordenadas especificadas en el centro.

3. Cambie al contexto de proceso de SQL Server y representar los resultados al ajustar la función de trazado en [rxExec](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexec) tal y como se muestra aquí. La función rxExec forma parte de la **RevoScaleR** paquete y admite la ejecución de funciones de R arbitrarias en un contexto de proceso remoto.

    ```R
    rxSetComputeContext(sqlcc)
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)
    plot(myplots[[1]][["myplot"]]);
    ````

    + Los datos del mapa en `googMap` se pasa como argumento a la función ejecutada de forma remota *mapPlot*. Debido a que las asignaciones se generan en su entorno local, se debe pasar a la función con el fin de crear el gráfico en el contexto de SQL Server.

    + Cuando la línea que comienza con `plot` se ejecuta, la representación de los datos se vuelve a serializar en el entorno local de R para que pueda verlo en el cliente de R.

    > [!NOTE]
    > Si está usando SQL Server en una máquina virtual de Azure, podría obtener un error en este momento. Eso es porque una regla de firewall predeterminada en Azure bloquea el acceso de red al código R. Para obtener más información sobre cómo corregir este error, consulte [instalar R Services en una VM de Azure](../r/installing-sql-server-r-services-on-an-azure-virtual-machine.md).

4. En la siguiente imagen se muestra el trazado de salida. Las ubicaciones de recogida de taxi se agregan al mapa como puntos rojos. La imagen podría ser diferente, dependiendo de cuántos ubicaciones están en el origen de datos utilizado.

    ![Trazado de transporte en taxi con una función personalizada de R](media/rsql-e2e-mapplot.png "Trazado de transporte en taxi con una función personalizada de R")

## <a name="next-lesson"></a>Lección siguiente

[Crear características de datos mediante R y SQL](/walkthrough-create-data-features.md)

## <a name="previous-lesson"></a>Lección anterior

[Resumir datos mediante R](/walkthrough-view-and-summarize-data-using-r.md)
