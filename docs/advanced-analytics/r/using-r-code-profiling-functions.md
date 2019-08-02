---
title: Usar las funciones de generación de perfiles de código de R
description: Mejorar el rendimiento y obtener resultados más rápidos en los cálculos de R en SQL Server mediante el uso de funciones de generación de perfiles de R para devolver información acerca de las llamadas de función internas.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e03ae1a8c4cdab87f46f63da6271886b4518b5e3
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715013"
---
# <a name="use-r-code-profiling-functions-to-improve-performance"></a>Uso de funciones de generación de perfiles de código de R para mejorar el rendimiento
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Además de usar herramientas y recursos de SQL Server para supervisar la ejecución de scripts de R, puede usar herramientas de rendimiento de otros paquetes de R para obtener más información sobre las llamadas de función interna. 

> [!TIP]
> En este artículo se proporcionan recursos básicos para comenzar. Para obtener instrucciones de expertos, se recomienda la sección de *rendimiento* en ["Advanced R" de Hadley Wickham](http://adv-r.had.co.nz).

## <a name="using-rprof"></a>Uso de RPROF

[*rprof*](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/Rprof) es una función incluida en el paquete base [**utils**](https://www.rdocumentation.org/packages/utils/versions/3.5.1), que se carga de forma predeterminada. 

Por lo general, la función *rprof* escribe la pila de llamadas en un archivo, a intervalos especificados. Después, puede usar la función [*summaryRprof*](https://www.rdocumentation.org/packages/utils/versions/3.5.1/topics/summaryRprof) para procesar el archivo de salida. Una ventaja de *rprof* es que realiza el muestreo, lo que, por tanto, disminuye la carga de rendimiento de la supervisión.

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

La documentación de Microsoft R Open, que se instala de forma predeterminada, incluye un manual sobre el desarrollo de extensiones para el lenguaje R que describe detalladamente la [generación de perfiles y](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging) la depuración. Puede encontrar la misma documentación en el equipo en C:\Archivos de Programa\microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\doc\manual.

## <a name="see-also"></a>Vea también

+ [paquete de utils R](https://www.rdocumentation.org/packages/utils/versions/3.5.1)
+ ["Advanced R" por Hadley Wickham](http://adv-r.had.co.nz)
