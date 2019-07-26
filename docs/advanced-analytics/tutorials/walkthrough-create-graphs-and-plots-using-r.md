---
title: Crear gráficos y trazados con las funciones de SQL y R SQL Server Machine Learning
description: Tutorial en el que se muestra cómo crear gráficos y trazados mediante las funciones del lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: f14005b8ba9d6f05d2b69deba29d83af5695f657
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470509"
---
# <a name="create-graphs-and-plots-using-sql-and-r-walkthrough"></a>Crear gráficos y trazados mediante SQL y R (tutorial)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En esta parte del tutorial, aprenderá técnicas para generar trazados y mapas mediante R con datos de SQL Server. Cree un histograma sencillo y, a continuación, desarrolle un trazado de mapa más complejo.

## <a name="prerequisites"></a>Requisitos previos

En este paso se supone que hay una sesión de R en curso basada en los pasos anteriores de este tutorial. Utiliza las cadenas de conexión y los objetos de origen de datos creados en esos pasos. Las siguientes herramientas y paquetes se utilizan para ejecutar el script.

+ Rgui. exe para ejecutar comandos de R
+ Management Studio para ejecutar T-SQL
+ googMap
+ paquete ggmap
+ paquete mapproj

## <a name="create-a-histogram"></a>Crear un histograma

1. Ejecute estas líneas para generar el primer trazado mediante la función [rxHistogram](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource) .  La función rxHistogram proporciona una funcionalidad similar a la de los paquetes de R de código abierto, pero puede ejecutarse en un contexto de ejecución remoto.

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
    > ¿El gráfico tiene un aspecto diferente?
    >  
    > Esto se debe  a que indatasource solo usa las primeras 1000 filas. El orden de las filas utilizando TOP no es determinista en ausencia de una cláusula ORDER BY, por lo que se espera que los datos y el gráfico resultante varíen.
    > Esta imagen en particular se generó con alrededor de 10 000 filas de datos. Se recomienda experimentar con distintos números de filas para obtener distintos gráficos y observar cuánto tiempo se tarda en devolver los resultados en su entorno.

## <a name="create-a-map-plot"></a>Crear un trazado de mapa

Normalmente, los servidores de bases de datos bloquean el acceso a Internet. Esto puede ser inconveniente cuando se usan paquetes de R que necesitan descargar mapas u otras imágenes para generar trazados. Sin embargo, hay una solución alternativa que podría resultarle útil al desarrollar sus propias aplicaciones. Básicamente, se genera la representación del mapa en el cliente y, a continuación, se superpone en el mapa los puntos que se almacenan como atributos en la tabla de SQL Server.

1. Defina la función que crea el objeto de trazado de R. La función personalizada *mapPlot* crea un gráfico de dispersión que usa las ubicaciones de recogida de taxi y traza el número de acciones que se iniciaron desde cada ubicación. Usa los paquetes **ggplot2** y **ggmap** , que ya deben estar [instalados y cargados](walkthrough-data-science-end-to-end-walkthrough.md#add-packages).

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

    + La función *mapPlot* toma dos argumentos: un objeto de datos existente, que se definió anteriormente con RxSqlServerData, y la representación del mapa que se pasa desde el cliente.
    + En la línea que comienza con la variable de *DS* , se usa rxImport para cargar los datos de memoria desde el origen de datos creado anteriormente, indatasource. (Ese origen de datos solo contiene 1000 filas; si desea crear un mapa con más puntos de datos, puede sustituir a un origen de datos diferente).
    + Siempre que use funciones de R de código abierto, los datos deben cargarse en tramas de datos en la memoria local. Sin embargo, al llamar a la función [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) , puede ejecutar en la memoria del contexto de cálculo remoto.

2. Cambie el contexto de cálculo a local y cargue las bibliotecas necesarias para crear las asignaciones.

    ```R
    rxSetComputeContext("local")
    library(ggmap)
    library(mapproj)
    gc <- geocode("Times Square", source = "google")
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color');
    ```

    + La variable `gc` almacena un conjunto de coordenadas para Times Square, Nueva York.

    + La línea que comienza con `googmap` genera un mapa con las coordenadas especificadas en el centro.

3. Cambie al contexto de cálculo de SQL Server y represente los resultados, ajustando la función de trazado en [rxExec](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexec) como se muestra aquí. La función rxExec forma parte del paquete **RevoScaleR** y admite la ejecución de funciones arbitrarias de R en un contexto de cálculo remoto.

    ```R
    rxSetComputeContext(sqlcc)
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)
    plot(myplots[[1]][["myplot"]]);
    ````

    + Los datos de mapa `googMap` de se pasan como un argumento a la función ejecutada de forma remota *mapPlot*. Dado que las asignaciones se generaron en su entorno local, se deben pasar a la función para crear el trazado en el contexto de SQL Server.

    + Cuando se ejecuta la línea `plot` que comienza con, los datos representados se vuelven a serializar en el entorno local de r para que pueda verlos en el cliente de r.

    > [!NOTE]
    > Si usa SQL Server en una máquina virtual de Azure, es posible que obtenga un error en este momento. Se produce un error cuando la regla de Firewall predeterminada en Azure bloquea el acceso a la red mediante código R. Para obtener más información sobre cómo corregir este error, consulte [instalación de los servicios de machine learning (R) en una máquina virtual de Azure](../install/sql-machine-learning-azure-virtual-machine.md).

4. En la siguiente imagen se muestra el trazado de salida. Las ubicaciones de recogida de taxi se agregan al mapa como puntos rojos. La imagen podría ser diferente, en función del número de ubicaciones que haya en el origen de datos utilizado.

    ![Trazado de transporte en taxi con una función personalizada de R](media/rsql-e2e-mapplot.png "Trazado de transporte en taxi con una función personalizada de R")

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Crear características de datos mediante R y SQL](walkthrough-create-data-features.md)
