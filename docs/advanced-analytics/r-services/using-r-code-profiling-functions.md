---
title: "Mediante las funciones de generaci&#243;n de perfiles de c&#243;digo de R | Microsoft Docs"
ms.custom: ""
ms.date: "11/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 132db249-b9f1-48f5-a63e-c9806cacc4af
caps.latest.revision: 6
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 5
---
# Mediante las funciones de generaci&#243;n de perfiles de c&#243;digo de R
Además de usar recursos de SQL Server y las herramientas para supervisar la ejecución del script de R, puede usar herramientas de rendimiento proporcionadas por otros paquetes de R para obtener más información acerca de las llamadas a funciones internas. En este tema se proporciona una lista de algunos recursos básicas para ayudarle a comenzar. Para obtener una guía experta, se recomienda el capítulo en [rendimiento](http://adv-r.had.co.nz/Performance.html) en la libreta de "" avanzada R"", por Hadley Wickham.

## <a name="using-rprof"></a>Usar RPROF

*rprof* es una función que se incluye en el paquete base **utils**, que se cargan de forma predeterminada. Una ventaja de *rprof* es que realiza de muestreo, por tanto, lo que reduce la carga de rendimiento de la supervisión.

Para usar R en el código de generación de perfiles, llame a esta función y especificar sus parámetros, incluidos el nombre de la ubicación del archivo de registro que se va a escribir. Consulte la Ayuda de *rprof* para obtener más información.

En general, la *rprof* función funciona mediante la escritura de la pila de llamadas a un archivo, a intervalos especificados. A continuación, puede usar el *summaryRprof* función para procesar el archivo de salida. 

Generación de perfiles puede ser activar y desactivar en el código. Para activar la generación de perfiles, suspenda la generación de perfiles y, a continuación, reiniciarlo, usaría una secuencia de llamadas a *rprof*:

1. Especifique el archivo de salida de generación de perfiles.

    ```R
    varOutputFile <- "C:/TEMP/run001.log")
    Rprof(varOutputFile)
    ```
2. Desactive la opción de generación de perfiles
    ```R
    Rprof(NULL)
    ```
    
3. Reinicie la generación de perfiles
    ```R
    Rprof(append=TRUE)
    ```


> [!NOTE] Con esta función requiere que Windows Perl esté instalado en el equipo donde se ejecuta el código. Por lo tanto, se recomienda que generar perfiles de código durante el desarrollo en un entorno de R y, a continuación, implemente el código depurado en SQL Server.  


## <a name="r-system-functions"></a>Funciones de sistema de R

El lenguaje R incluye muchas funciones de paquete básico para devolver el contenido de las variables del sistema. 

Por ejemplo, como parte del código R, podría usar `Sys.timezone` para obtener la zona horaria actual, o `Sys.Time` para obtener la hora del sistema de R. 

Para obtener información acerca de las funciones de sistema de R individuales, escriba el nombre de función como argumento para el objeto R `help()` función desde un símbolo del sistema de R.

```R
help("Sys.time")
```

## <a name="debugging-and-profiling-in-r"></a>Depurar y generar perfiles en R

La documentación de Microsoft R Open, que se instala de forma predeterminada, incluye un manual sobre el desarrollo de extensiones para el lenguaje R que se explica la generación de perfiles y depuración en detalle.

El capítulo también está disponible en línea: [https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging)

### <a name="location-of-r-help-files"></a>Ubicación de archivos de Ayuda de R

C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\doc\manual


