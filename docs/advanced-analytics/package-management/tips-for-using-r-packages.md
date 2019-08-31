---
title: Sugerencias para usar paquetes de R
description: Obtenga sugerencias útiles sobre el uso de paquetes de R en SQL Server para quienes no están familiarizados con R o con SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/06/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5e283ab478a6d65243e9962fd5c26f5f91d87c15
ms.sourcegitcommit: 00350f6ffb73c2c0d99beeded61c5b9baa63d171
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2019
ms.locfileid: "70196348"
---
# <a name="tips-for-using-r-packages"></a>Sugerencias para usar paquetes de R

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se proporcionan sugerencias útiles sobre el uso de paquetes de R en SQL Server. Estas sugerencias están destinadas a DBA que no están familiarizados con R y desarrolladores de R experimentados que no están familiarizados con el acceso a paquetes en una instancia de SQL Server.

## <a name="if-youre-new-to-r"></a>Si no está familiarizado con R

Como administrador que instala paquetes de R por primera vez, conocer algunos aspectos básicos sobre la administración de paquetes de R puede ayudarle a empezar.

### <a name="package-dependencies"></a>Dependencias de paquetes

Los paquetes de r suelen depender de varios otros paquetes, algunos de los cuales podrían no estar disponibles en la biblioteca de R predeterminada usada por la instancia de. A veces, un paquete requiere una versión diferente de un paquete dependiente de lo que ya está instalado. Las dependencias de paquete se indican en un archivo de Descripción insertado en el paquete, pero a veces están incompletos. Puede usar un paquete denominado [iGraph](https://igraph.org/r/) para articular completamente el gráfico de dependencias.

Si necesita instalar varios paquetes o desea asegurarse de que todos los usuarios de su organización obtienen el tipo de paquete y la versión correctos, se recomienda usar el paquete [miniCRAN](https://mran.microsoft.com/package/miniCRAN) para analizar la cadena de dependencia completa. minicRAN crea un repositorio local que se puede compartir entre varios usuarios o equipos. Para obtener más información, vea [crear un repositorio de paquetes local mediante miniCRAN](create-a-local-package-repository-using-minicran.md).

### <a name="package-sources-versions-and-formats"></a>Orígenes de paquetes, versiones y formatos

Hay varios orígenes para los paquetes de R, como [Cran](https://cran.r-project.org/) y [Bioconductor](https://www.bioconductor.org/). El sitio oficial del lenguaje R (<https://www.r-project.org/>) enumera muchos de estos recursos. Microsoft ofrece [MRAN](https://mran.microsoft.com/) para su distribución de R ([MRO](https://mran.microsoft.com/open)) de código abierto y otros paquetes. Muchos paquetes se publican en GitHub, donde los desarrolladores pueden obtener el código fuente.

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
Los paquetes de R se ejecutan en varias plataformas de computación. Asegúrese de que las versiones que instala son archivos binarios de Windows.
::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"
Los paquetes de R se ejecutan en varias plataformas de computación. Asegúrese de que las versiones que instala son archivos binarios de Linux.
::: moniker-end

### <a name="know-which-library-youre-installing-to-and-which-packages-are-already-installed"></a>Saber en qué biblioteca se está instalando y qué paquetes ya están instalados

Si ha modificado previamente el entorno de r en el equipo, antes de instalar nada, asegúrese de que la `.libPath` variable de entorno de r usa una sola ruta de acceso.

Esta ruta de acceso debe apuntar a la carpeta R_SERVICES de la instancia. Para obtener más información, incluida la forma de determinar qué paquetes ya están instalados, vea [obtener información de paquetes de R](../package-management/r-package-information.md).

## <a name="if-youre-new-to-sql-server"></a>Si no está familiarizado con SQL Server

Como desarrollador de R que trabaja en código que se ejecuta en SQL Server, las directivas de seguridad que protegen el servidor restringen su capacidad para controlar el entorno de R. En las sugerencias siguientes se describen las situaciones típicas y se proporcionan sugerencias para trabajar en este entorno.

### <a name="r-user-libraries-not-supported-on-sql-server"></a>Bibliotecas de usuario de R: no se admiten en SQL Server

Los desarrolladores de r que necesiten instalar nuevos paquetes de R están acostumbrados a instalar paquetes en, mediante una biblioteca de usuario privada siempre que la biblioteca predeterminada no esté disponible o cuando el desarrollador no sea un administrador del equipo. Por ejemplo, en un entorno de desarrollo de r típico, el usuario agregaría la ubicación del paquete a la variable `libPath`de entorno de r o hacer referencia a la ruta de acceso completa del paquete, similar a la siguiente:

```R
library("c:/Users/<username>/R/win-library/packagename")
```

Esto no funciona cuando se ejecutan soluciones de R en SQL Server, ya que los paquetes de R deben instalarse en una biblioteca específica predeterminada que esté asociada a la instancia. Cuando un paquete no está disponible en la biblioteca predeterminada, se obtiene este error al intentar llamar al paquete:

*Error en la biblioteca (XXX): no hay ningún paquete denominado ' package-name '*

Para obtener información sobre cómo instalar paquetes de R en SQL Server, consulte [instalar nuevos paquetes de r en SQL Server Machine Learning Services o SQL Server R Services](install-additional-r-packages-on-sql-server.md).

### <a name="how-to-avoid-package-not-found-errors"></a>Cómo evitar errores de "paquete no encontrado"

El uso de las siguientes instrucciones le ayudará a evitar los errores de "paquete no encontrado".

+ Elimine las dependencias de las bibliotecas de usuario.

    Es una práctica de desarrollo incorrecta instalar los paquetes de R necesarios en una biblioteca de usuario personalizada. Esto puede dar lugar a errores si otro usuario que no tiene acceso a la ubicación de la biblioteca ejecuta una solución.

    Además, si un paquete está instalado en la biblioteca predeterminada, el tiempo de ejecución de R carga el paquete desde la biblioteca predeterminada, aunque especifique una versión diferente en el código de R.

+ Asegúrese de que el código pueda ejecutarse en un entorno compartido.

+ Evite instalar paquetes como parte de una solución. Si no tiene permisos para instalar paquetes, se producirá un error en el código. Incluso si tiene permisos para instalar paquetes, debe hacerlo por separado de otro código que desee ejecutar.

+ Comprobar el código para asegurarse de que no hay ninguna llamada a paquetes no instalados.

+ Actualice el código para quitar las referencias directas a las rutas de acceso de los paquetes de R o de las bibliotecas de R.

+ Saber qué biblioteca de paquetes está asociada a la instancia. Para obtener más información, vea [obtener información de paquetes de R](../package-management/r-package-information.md).

## <a name="see-also"></a>Vea también

+ [Instalación de paquetes de R adicionales](install-additional-r-packages-on-sql-server.md)
+ [Instalación de paquetes de Python adicionales](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriales, muestras y soluciones](../tutorials/machine-learning-services-tutorials.md)