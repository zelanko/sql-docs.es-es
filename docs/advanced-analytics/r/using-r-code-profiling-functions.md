---
title: 'Usar R código de generación de perfiles de funciones: SQL Server Machine Learning Services'
description: Mejorar el rendimiento y obtener resultados más rápidos en los cálculos de R en SQL Server mediante las funciones de generación de perfiles de R para devolver información sobre las llamadas de función interna.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7bd54130ecb17241f0a5cddf4d80e186d7a8a427
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645035"
---
# <a name="use-r-code-profiling-functions-to-improve-performance"></a>Usar funciones de generación de perfiles de código de R para mejorar el rendimiento
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Además de usar herramientas y recursos de SQL Server para supervisar la ejecución de scripts de R, puede usar herramientas de rendimiento de otros paquetes de R para obtener más información sobre las llamadas de función interna. 

> [!TIP]
> Este artículo proporciona recursos básicos para ayudarle a comenzar. Para obtener orientación experta, se recomienda la *rendimiento* sección ["Advanced R" de Hadley Wickham](http://adv-r.had.co.nz).

## <a name="using-rprof"></a>Uso de RPROF

[*rprof* ](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/Rprof) es una función incluida en el paquete base [ **utils**](https://www.rdocumentation.org/packages/utils/versions/3.5.1), que se cargan de forma predeterminada. 

Por lo general, la función *rprof* escribe la pila de llamadas en un archivo, a intervalos especificados. A continuación, puede usar el [ *summaryRprof* ](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/summaryRprof) función para procesar el archivo de salida. Una ventaja de *rprof* es que realiza el muestreo, lo que, por tanto, disminuye la carga de rendimiento de la supervisión.

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

La documentación de Microsoft R Open, que se instala de forma predeterminada, incluye un manual sobre el desarrollo de extensiones para el lenguaje R que analiza [de generación de perfiles y depuración](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging) en detalle. Puede encontrar la documentación del misma en el equipo en C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\doc\manual.

## <a name="see-also"></a>Vea también

+ [paquete de R utils](https://www.rdocumentation.org/packages/utils/versions/3.5.1)
+ ["Advanced R" de Hadley Wickham](http://adv-r.had.co.nz)
