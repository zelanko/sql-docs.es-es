---
title: Sugerencias para el uso de paquetes de R instalados en bibliotecas de usuario
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 16f3ae10c7a05529c86bea5684182c7805f9f54b
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715675"
---
# <a name="tips-for-using-r-packages-in-sql-server"></a>Sugerencias para usar paquetes de R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artículo tiene secciones independientes para los DBA que no están familiarizados con R y los desarrolladores de R experimentados que no conocen el acceso a los paquetes en una instancia de SQL Server.

## <a name="new-to-r"></a>Novedad de R

Como administrador que instala paquetes de R por primera vez, conocer algunos aspectos básicos sobre la administración de paquetes de R puede ayudarle a empezar.

### <a name="package-dependencies"></a>Dependencias de paquetes

Los paquetes de r suelen depender de varios otros paquetes, algunos de los cuales podrían no estar disponibles en la biblioteca de R predeterminada usada por la instancia de. A veces, un paquete requiere una versión diferente de un paquete dependiente que ya está instalado. Las dependencias de paquete se indican en un archivo de Descripción insertado en el paquete, pero a veces están incompletos. Puede usar un paquete denominado [iGraph](https://igraph.org/r/) para articular completamente el gráfico de dependencias.

Si necesita instalar varios paquetes o desea asegurarse de que todos los usuarios de su organización obtienen el tipo de paquete y la versión correctos, se recomienda usar el paquete [miniCRAN](https://mran.microsoft.com/package/miniCRAN) para analizar la cadena de dependencia completa. minicRAN crea un repositorio local que se puede compartir entre varios usuarios o equipos. Para obtener más información, vea [crear un repositorio de paquetes local mediante miniCRAN](create-a-local-package-repository-using-minicran.md).

### <a name="package-sources-versions-and-formats"></a>Orígenes de paquetes, versiones y formatos

Hay varios orígenes para los paquetes de R, como [Cran](https://cran.r-project.org/) y [Bioconductor](https://www.bioconductor.org/). El sitio oficial del lenguaje R (<https://www.r-project.org/>) enumera muchos de estos recursos. Microsoft ofrece [MRAN](https://mran.microsoft.com/) para su distribución de R ([MRO](https://mran.microsoft.com/open)) de código abierto y otros paquetes. Muchos paquetes se publican en GitHub, donde los desarrolladores pueden obtener el código fuente.

Los paquetes de R se ejecutan en varias plataformas de computación. Asegúrese de que las versiones que instala son archivos binarios de Windows.

### <a name="know-which-library-you-are-installing-to-and-which-packages-are-already-installed"></a>Conozca la biblioteca en la que va a instalar y los paquetes que ya están instalados.

Si ha modificado previamente el entorno de r en el equipo, antes de instalar nada, asegúrese de que la variable `.libPath` de entorno de r usa una sola ruta de acceso.

Esta ruta de acceso debe apuntar a la carpeta R_SERVICES de la instancia. Para obtener más información, incluida la forma de determinar qué paquetes ya están instalados, vea [paquetes de R y Python predeterminados en SQL Server](../package-management/default-packages.md).

## <a name="new-to-sql-server"></a>Nuevo en SQL Server

Como desarrollador de R que trabaja en código que se ejecuta en SQL Server, las directivas de seguridad que protegen el servidor restringen su capacidad para controlar el entorno de R.

### <a name="r-user-libraries-not-supported-on-sql-server"></a>Bibliotecas de usuario de R: no se admiten en SQL Server

Los desarrolladores de r que necesiten instalar nuevos paquetes de R están acostumbrados a instalar paquetes en, mediante una biblioteca de usuario privada siempre que la biblioteca predeterminada no esté disponible o cuando el desarrollador no sea un administrador del equipo. Por ejemplo, en un entorno de desarrollo de r típico, el usuario agregaría la ubicación del paquete a la variable `libPath`de entorno de r o hacer referencia a la ruta de acceso completa del paquete, similar a la siguiente:

```R
library("c:/Users/<username>/R/win-library/packagename")
```

Esto no funciona cuando se ejecutan soluciones de R en SQL Server, ya que los paquetes de R deben instalarse en una biblioteca específica predeterminada que esté asociada a la instancia. Cuando un paquete no está disponible en la biblioteca predeterminada, se obtiene este error al intentar llamar al paquete:

*Error en la biblioteca (XXX): no hay ningún paquete denominado ' package-name '*

### <a name="avoid-package-not-found-errors"></a>Evitar errores de "paquete no encontrado"

+ Elimine las dependencias de las bibliotecas de usuario. 

    Es una práctica de desarrollo incorrecta instalar los paquetes de R necesarios en una biblioteca de usuario personalizada, ya que puede provocar errores si otro usuario que no tiene acceso a la ubicación de la biblioteca ejecuta una solución.

    Además, si un paquete está instalado en la biblioteca predeterminada, el tiempo de ejecución de R carga el paquete desde la biblioteca predeterminada, aunque especifique una versión diferente en el código de R.

+ Modifique el código para que se ejecute en un entorno compartido.

+ Evite instalar paquetes como parte de una solución. Si no tiene permisos para instalar paquetes, se producirá un error en el código. Incluso si tiene permisos para instalar paquetes, debe hacerlo por separado de otro código que desee ejecutar.

+ Comprobar el código para asegurarse de que no hay ninguna llamada a paquetes no instalados.

+ Actualice el código para quitar las referencias directas a las rutas de acceso de los paquetes de R o de las bibliotecas de R. 

+ Saber qué biblioteca de paquetes está asociada a la instancia. Para obtener más información, vea [paquetes de R y Python predeterminados en SQL Server](../package-management/default-packages.md).

## <a name="see-also"></a>Vea también

+ [Instalación de paquetes de R adicionales](install-additional-r-packages-on-sql-server.md)
+ [Instalación de paquetes de Python adicionales](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriales, muestras y soluciones](../tutorials/machine-learning-services-tutorials.md)