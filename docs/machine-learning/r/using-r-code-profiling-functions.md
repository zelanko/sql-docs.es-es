---
title: Mejora del rendimiento mediante la función de generación de perfiles de código de R
description: Recopile la información útil para mejorar el rendimiento y obtenga resultados más rápidos en los cálculos de R en SQL Server mediante el uso de funciones de generación de perfiles de R. La función *rprof* recopila y devuelve información acerca de las llamadas de función internas.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 12/12/2018
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 16a1ed8df29de58450f87118068e43646c46fd90
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/20/2020
ms.locfileid: "86484646"
---
# <a name="use-r-code-profiling-functions-to-improve-performance"></a>Uso de funciones de generación de perfiles de código de R para mejorar el rendimiento
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Además de usar herramientas y recursos de SQL Server para supervisar la ejecución de scripts de R, puede usar herramientas de rendimiento de otros paquetes de R para obtener más información sobre las llamadas de función interna. 

> [!TIP]
> En este artículo se ofrecen recursos básicos para comenzar. Para obtener orientación experta, se recomienda la sección sobre *rendimiento* del libro ["Advanced R"](http://adv-r.had.co.nz) de Hadley Wickham.

## <a name="using-rprof"></a>Uso de RPROF

[*rprof*](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/Rprof) es una función incluida en el paquete base [**utils**](https://www.rdocumentation.org/packages/utils/versions/3.5.1), que se carga de manera predeterminada. 

Por lo general, la función *rprof* escribe la pila de llamadas en un archivo, a intervalos especificados. Después, se puede usar la función [*summaryRprof*](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/summaryRprof) para procesar el archivo de salida. Una ventaja de *rprof* es que realiza el muestreo, lo que, por tanto, disminuye la carga de rendimiento de la supervisión.

Para usar la generación de perfiles de R en el código, llame a esta función y especifique sus parámetros, incluido el nombre de la ubicación del archivo de registro que se va a escribir. La generación de perfiles se puede activar y desactivar en el código. La sintaxis siguiente muestra el uso básico: 

```R
# Specify profiling output file.
varOutputFile <- "C:/TEMP/run001.log")
Rprof(varOutputFile)

# Turn off profiling
Rprof(NULL)
    
# Restart profiling
Rprof(append=TRUE)
```

> [!NOTE]
> El uso de esta función requiere que Windows Perl esté instalado en el equipo donde se ejecuta el código. Por consiguiente, se recomienda generar perfiles del código durante el desarrollo en un entorno de R e implementar después el código depurado en SQL Server.  


## <a name="r-system-functions"></a>Funciones del sistema de R

El lenguaje R incluye muchas funciones del paquete base que devuelven el contenido de variables del sistema. Por ejemplo, como parte del código de R, podría usar `Sys.timezone` para obtener la zona horaria actual o `Sys.Time` para obtener la hora del sistema desde R. 

Para obtener información sobre funciones individuales del sistema de R, escriba el nombre de la función como argumento en la función `help()` de R desde un símbolo del sistema.

```R
help("Sys.time")
```

## <a name="debugging-and-profiling-in-r"></a>Depuración y generación de perfiles de R

La documentación de Microsoft R Open, que se instala de manera predeterminada, incluye un manual sobre el desarrollo de extensiones para el lenguaje R que analiza minuciosamente la [generación de perfiles y la depuración](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging). Puede encontrar la misma documentación en su equipo en C:\Archivos de programa\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\doc\manual.

## <a name="see-also"></a>Consulte también

+ [Paquete utils de R](https://www.rdocumentation.org/packages/utils/versions/3.5.1)
+ ["Advanced R" por Hadley Wickham](http://adv-r.had.co.nz)
