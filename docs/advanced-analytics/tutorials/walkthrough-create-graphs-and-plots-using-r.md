---
title: Crear gráficos y trazados con SQL y R funciones de SQL Server Machine Learning
description: Tutorial que muestra cómo crear gráficos y trazados con las funciones del lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 0ed226a4c11c002d048572f58a75c0c04bdf936c
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58513172"
---
# <a name="create-graphs-and-plots-using-sql-and-r-walkthrough"></a>Crear gráficos y trazados con SQL y R (tutorial)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En esta parte del tutorial, aprenderá técnicas para generar trazados y mapas mediante R con datos de SQL Server. Crear un histograma simple y, a continuación, desarrolle un trazado de mapa más complejo.

## <a name="prerequisites"></a>Requisitos previos

Este paso presupone una sesión de R en curso según los pasos anteriores en este tutorial. Usa cadenas y datos de origen creados objetos de conexión en esos pasos. Las siguientes herramientas y los paquetes se utilizan para ejecutar el script.

+ Rgui.exe para ejecutar comandos de R
+ Management Studio para ejecutar T-SQL
+ googMap
+ paquete ggmap
+ paquete mapproj

## <a name="create-a-histogram"></a>Crear un histograma

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
    > ¿Parece diferente su gráfico?
    >  
    > Eso es porque _inDataSource_ usa sólo las primeras 1000 filas. El orden de las filas usando TOP es no determinista en ausencia de una cláusula ORDER BY, por lo que se espera que los datos y el gráfico resultante pueden variar.
    > Esta imagen en particular se generó con alrededor de 10 000 filas de datos. Se recomienda experimentar con distintos números de filas para obtener distintos gráficos y observar cuánto tiempo se tarda en devolver los resultados en su entorno.

## <a name="create-a-map-plot"></a>Crear un trazado de mapa

Normalmente, los servidores de base de datos bloquean el acceso a Internet. Esto puede ser un problema al usar paquetes de R que necesitan descargar asignaciones u otras imágenes para generar trazados. Sin embargo, hay una solución que puede resultarle útil al desarrollar sus propias aplicaciones. Básicamente, generar la representación del mapa en el cliente y luego superpondrá en el mapa los puntos que se almacenan como atributos en la tabla de SQL Server.

1. Definir la función que crea el objeto de trazado de R. La función personalizada *mapPlot* crea un gráfico de dispersión que usa las ubicaciones de recogida de taxi y traza el número de viajes que se inicia desde cada ubicación. Usa el **ggplot2** y **ggmap** paquetes, que ya deben estar [instala y carga](walkthrough-data-science-end-to-end-walkthrough.md#add-packages).

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

    + El *mapPlot* función toma dos argumentos: un objeto de datos existente que se definió anteriormente mediante RxSqlServerData y la representación del mapa se pasa desde el cliente.
    + En la línea que comienza con la *ds* variable, se usa para cargar datos de memoria desde el origen de datos creado anteriormente, rxImport *inDataSource*. (Ese origen de datos contiene solo 1000 filas; si desea crear un mapa con más puntos de datos, puede sustituir un origen de datos diferente).
    + Siempre que use funciones de R de código abierto, los datos deben cargarse en tramas de datos en la memoria local. Sin embargo, mediante una llamada a la [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) función, puede ejecutar en la memoria del contexto de cálculo remoto.

2. Cambiar el contexto de proceso local y cargar las bibliotecas necesarias para crear los mapas.

    ```R
    rxSetComputeContext("local")
    library(ggmap)
    library(mapproj)
    gc <- geocode("Times Square", source = "google")
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color');
    ```

    + La variable `gc` almacena un conjunto de coordenadas para Times Square, Nueva York.

    + La línea que comienza con `googmap` genera un mapa con las coordenadas especificadas en el centro.

3. Cambie al contexto de proceso de SQL Server y representar los resultados, ajustando la función de trazado en [rxExec](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexec) como se muestra aquí. La función rxExec forma parte de la **RevoScaleR** paquete y admite la ejecución de funciones arbitrarias de R en un contexto de cálculo remoto.

    ```R
    rxSetComputeContext(sqlcc)
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)
    plot(myplots[[1]][["myplot"]]);
    ````

    + Los datos del mapa en `googMap` se pasa como argumento a la función ejecutada de forma remota *mapPlot*. Dado que los mapas se generaron en su entorno local, debe pasarse a la función con el fin de crear el gráfico en el contexto de SQL Server.

    + Cuando la línea que comienza con `plot` ejecuciones, la representación de los datos se vuelven a serializar en el entorno local de R para que se puede ver en el cliente de R.

    > [!NOTE]
    > Si usa SQL Server en una máquina virtual de Azure, podría obtener un error en este momento. Se produce un error cuando la regla de firewall predeterminada en Azure bloquea el acceso de red por código de R. Para obtener más información sobre cómo solucionar este error, consulte [servicios de instalación de Machine Learning (R) en una máquina virtual de Azure](../r/installing-sql-server-r-services-on-an-azure-virtual-machine.md).

4. En la siguiente imagen se muestra el trazado de salida. Las ubicaciones de recogida de taxi se agregan al mapa como puntos rojos. La imagen podría ser diferente, dependiendo de cuántos ubicaciones están en el origen de datos utilizado.

    ![Trazado de transporte en taxi con una función personalizada de R](media/rsql-e2e-mapplot.png "Trazado de transporte en taxi con una función personalizada de R")

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Crear características de datos mediante R y SQL](walkthrough-create-data-features.md)
