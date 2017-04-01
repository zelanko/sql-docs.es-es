---
title: "Crear gr&#225;ficos y trazados con R (Tutorial integral de ciencia de datos) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
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
ms.assetid: 5f70f0a6-fd4a-410f-9f44-1605503f77ec
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Crear gr&#225;ficos y trazados con R (Tutorial integral de ciencia de datos)
En esta lección, aprenderá técnicas para generar trazados y mapas mediante R con datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  Verá lo fácil que es ver trazados que se crean en el servidor y cómo se pueden pasar objetos gráficos al servidor.  
  
## <a name="creating-graphics"></a>Creación de gráficos
En [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], los objetos gráficos, así como los modelos y los resultados se serializan entre el equipo y el contexto de cálculo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

Cuando usa un contexto de cálculo de SQL Server, es posible que no pueda descargar la representación del mapa porque la mayoría de los servidores de base de datos de producción bloquean completamente el acceso a Internet.  Por lo tanto, para crear el segundo conjunto de trazados, generará la representación del mapa en el cliente y luego superpondrá en el mapa los puntos que se almacenan como atributos en la tabla *nyctaxi_sample* .   

Para ello, cree primero la representación del mapa mediante una llamada a Google Maps y, después, pase la representación del mapa al contexto SQL.  
  
Se trata de un patrón que puede resultarle útil al desarrollar sus propias aplicaciones.   
  
### <a name="create-a-histogram"></a>Crear un histograma  
Para crear un histograma, usará el origen de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que creó anteriormente, junto con la función `rxHistogram` proporcionada en R Services.  
  
1.  Ejecute estas líneas para generar el primer trazado mediante la función *rxHistogram*.  La función *rxHistogram* proporciona una funcionalidad similar a la de los paquetes de R de código abierto, pero se puede ejecutar en un contexto de ejecución remota. 
  
    ```R  
    #Plot fare amount on SQL Server and return the plot  
    start.time <- proc.time()  
    rxHistogram(~fare_amount, data = inDataSource, title = "Fare Amount Histogram")  
    used.time <- proc.time() - start.time  
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2), " seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))    
    ```         
  
2.  La imagen se devuelve en el dispositivo de gráficos de R para el entorno de desarrollo.  Por ejemplo, en RStudio, haga clic en la ventana **Trazar** .  En [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)], se abre una ventana de gráficos independiente.  
  
    ![using rxHistogram to plot fare amounts](../../advanced-analytics/r-services/media/rsql-e2e-rxhistogramresult.png "using rxHistogram to plot fare amounts")  
  
    > [!NOTE]  Como la ordenación de las filas usando TOP es no determinista sin una cláusula ORDER BY, podría ver resultados muy diferentes. Se recomienda experimentar con distintos números de filas para obtener distintos gráficos y observar cuánto tiempo se tarda en devolver los resultados en su entorno.  Esta imagen en particular se generó con alrededor de 10 000 filas de datos.
  
### <a name="create-a-map-plot"></a>Crear un trazado de mapa  
En este ejemplo, generará un objeto de trazado usando la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como el contexto de cálculo y después devolverá el objeto de trazado al contexto de cálculo local para su representación.  
   
1.  En primer lugar, defina la función que crea el objeto de trazado.  

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
    + La función personalizada de R *mapPlot* crea un gráfico de dispersión que usa las ubicaciones de recogida de taxi para trazar el número de viajes que se inicia desde cada ubicación. Usa los paquetes **ggplot2** y  **ggmap** , que ya deberían estar instalados y cargados.  
    + La función *mapPlot* toma dos argumentos: un objeto de datos existente que se definió anteriormente mediante *RxSqlServerData*, y la representación del mapa que se pasa desde el cliente.    
    + Observe el uso de la variable *ds* para cargar datos del origen de datos creado anteriormente, *inDataSource*.  Siempre que use funciones de R de código abierto, los datos deben cargarse en tramas de datos en memoria. Puede hacerlo mediante la función *rxImport* del paquete **RevoScaleR**.  Pero esta función se ejecuta en memoria en el contexto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definido anteriormente. Es decir, la función no usa la memoria de la estación de trabajo local.  
  
2.  Luego cargará las bibliotecas necesarias para crear los mapas en su entorno local de R.  
  
    ```R  
    library(ggmap)  
    library(mapproj)  
    gc <- geocode("Times Square", source = "google")  
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color';    
    ```  
    + Este código se ejecuta en el cliente de R. Observe la llamada repetida a las bibliotecas **ggmap** y **mapproj**. La razón es que la definición de la función anterior se ejecutó en el contexto del servidor y las bibliotecas nunca se cargaron localmente. Ahora va a incluir la operación de trazado en su estación de trabajo.  
  
    -   La variable *gc* almacena un conjunto de coordenadas para Times Square, Nueva York.  
  
    -   La línea que comienza con *googmap* genera un mapa con las coordenadas especificadas en el centro.  
          
  
3.  Ejecute la función de trazado y represente los resultados en su entorno local de R. Para ello, ajuste la función de trazado en *rxExec* como se muestra aquí.  La función *rxExec* se incluye en el paquete **RevoScaleR** y admite la ejecución de funciones arbitrarias de R en un contexto de cálculo remoto. 
  
    ```R  
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)  
    plot(myplots[[1]][["myplot"]]);  
  
    ```  
    + En la primera línea, puede ver que los datos del mapa se pasan como un argumento (*googMap*) a la función ejecutada de forma remota *mapPlot*. Se debe a que los mapas se generaron en su entorno local y se deben pasar a la función con el fin de crear el gráfico en el contexto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].   
  
        Después, los datos representados se vuelven a serializar en el entorno local de R para que los pueda ver, con la ventana **Trazar** de RStudio u otro dispositivo de gráficos de R.  
  
  
4.  Aquí está el trazado de salida, que muestra las ubicaciones de recogida en el mapa como puntos rojos.  
  
    ![plotting taxi rides using a custom R function](../../advanced-analytics/r-services/media/rsql-e2e-mapplot.png "plotting taxi rides using a custom R function")  
  
## <a name="next-lesson"></a>Lección siguiente  
[Lección 3: Crear características de datos &#40;Tutorial integral de ciencia de datos&#41;](../../advanced-analytics/r-services/lesson-3-create-data-features-data-science-end-to-end-walkthrough.md)  
  
  
  
