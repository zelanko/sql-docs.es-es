---
title: Uso (SQL Server Machine Learning) de las funciones de generación de perfiles de código de R | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 64f065df5f5769e37bb1d5a8dbc2fba2d5f936ee
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51703973"
---
# <a name="using-r-code-profiling-functions"></a>Uso de funciones de generación de perfiles de código de R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Además de usar herramientas y recursos de SQL Server para supervisar la ejecución de scripts de R, puede usar herramientas de rendimiento de otros paquetes de R para obtener más información sobre las llamadas de función interna. En este tema se ofrece una lista de algunos recursos básicos para comenzar. Para obtener orientación experta, se recomienda el capítulo sobre [rendimiento](https://adv-r.had.co.nz/Performance.html) en el libro "Advanced R", de Hadley Wickham.

## <a name="using-rprof"></a>Uso de RPROF

*rprof* es una función incluida en el paquete base **utils**, que se carga de manera predeterminada. Una ventaja de *rprof* es que realiza el muestreo, lo que, por tanto, disminuye la carga de rendimiento de la supervisión.

Para usar la generación de perfiles de R en el código, llame a esta función y especifique sus parámetros, incluido el nombre de la ubicación del archivo de registro que se va a escribir. Vea la Ayuda de *rprof* para obtener más información.

Por lo general, la función *rprof* escribe la pila de llamadas en un archivo, a intervalos especificados. Después, se puede usar la función *summaryRprof* para procesar el archivo de salida. 

La generación de perfiles se puede activar y desactivar en el código. Para activar la generación de perfiles, suspenderla y reiniciarla después, se usaría una secuencia de llamadas a *rprof*:

1. Especifique un archivo de salida de la generación de perfiles.

    ```R
    varOutputFile <- "C:/TEMP/run001.log")
    Rprof(varOutputFile)
    ```
2. Desactivar la generación de perfiles
    ```R
    Rprof(NULL)
    ```
    
3. Reiniciar la generación de perfiles
    ```R
    Rprof(append=TRUE)
    ```


> [!NOTE]
> El uso de esta función requiere que Windows Perl esté instalado en el equipo donde se ejecuta el código. Por consiguiente, se recomienda generar perfiles del código durante el desarrollo en un entorno de R e implementar después el código depurado en SQL Server.  


## <a name="r-system-functions"></a>Funciones del sistema de R

El lenguaje R incluye muchas funciones del paquete base que devuelven el contenido de variables del sistema. 

Por ejemplo, como parte del código de R, podría usar `Sys.timezone` para obtener la zona horaria actual o `Sys.Time` para obtener la hora del sistema desde R. 

Para obtener información sobre funciones individuales del sistema de R, escriba el nombre de la función como argumento en la función `help()` de R desde un símbolo del sistema.

```R
help("Sys.time")
```

## <a name="debugging-and-profiling-in-r"></a>Depuración y generación de perfiles de R

La documentación de Microsoft R Open, que se instala de manera predeterminada, incluye un manual sobre el desarrollo de extensiones para el lenguaje R que analiza minuciosamente la generación de perfiles y la depuración.

El capítulo también está disponible en línea: [https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging)

### <a name="location-of-r-help-files"></a>Ubicación de los archivos de Ayuda de R

C:\Archivos de programa\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\doc\manual



