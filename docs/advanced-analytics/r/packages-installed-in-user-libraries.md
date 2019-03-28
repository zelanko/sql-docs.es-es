---
title: 'Sugerencias para usar paquetes de R instalados en bibliotecas de usuario: SQL Server Machine Learning Services'
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/30/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: ee5dc9dc8b1730f26bada915d739f164a884801d
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510782"
---
# <a name="tips-for-using-r-packages-in-sql-server"></a>Sugerencias para usar paquetes de R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo tiene secciones independientes para los DBA que no estén familiarizados con R y los desarrolladores experimentados de R que son de acceso de paquete desconocido en una instancia de SQL Server.

## <a name="new-to-r"></a>Está familiarizado con R

Como un administrador de instalación de R por primera vez, los paquetes conocer algunos conceptos básicos sobre la administración de paquetes de R pueden ayudar a empezar a trabajar.

### <a name="package-dependencies"></a>Dependencias de paquetes

Paquetes de R con frecuencia dependen de varios otros paquetes, algunos de los cuales es posible que no estén disponibles en la biblioteca de R predeterminada usada por la instancia. A veces un paquete requiere una versión diferente de un paquete dependiente que ya está instalada. Las dependencias del paquete se indican en un archivo de descripción incrustado en el paquete, pero a veces están incompletas. Puede usar un paquete denominado [iGraph](https://igraph.org/r/) totalmente articular el gráfico de dependencias.

Si necesita instalar varios paquetes o quiere asegurarse de que todas las personas de su organización obtienen el tipo de paquete correcto y la versión, recomendamos que use el [miniCRAN](https://mran.microsoft.com/package/miniCRAN) paquetes para analizar la cadena de dependencias completo. minicRAN crea un repositorio local que se puede compartir entre varios usuarios o equipos. Para obtener más información, consulte [crear un repositorio de paquete local mediante miniCRAN](create-a-local-package-repository-using-minicran.md).

### <a name="package-sources-versions-and-formats"></a>Orígenes de paquetes, versiones y formatos

Hay varios orígenes de paquetes de R, como [CRAN](https://cran.r-project.org/) y [Bioconductor](https://www.bioconductor.org/). El sitio oficial para el lenguaje R (<https://www.r-project.org/>) recoge muchos de estos recursos. Microsoft ofrece [MRAN](https://mran.microsoft.com/) para su distribución de R de código abierto ([MRO](https://mran.microsoft.com/open)) y otros paquetes. Muchos paquetes se publican en GitHub, donde los desarrolladores pueden obtener el código fuente.

Paquetes de R se ejecutan en varias plataformas informáticas. Asegúrese de que las versiones que instalar los archivos binarios de Windows.

### <a name="know-which-library-you-are-installing-to-and-which-packages-are-already-installed"></a>Saber qué biblioteca que está instalando y los paquetes ya instalados.

Si previamente ha modificado el entorno de R en el equipo, antes de instalar nada, asegúrese de que la variable de entorno de R `.libPath` usa una sola ruta de acceso.

Esta ruta de acceso debe apuntar a la carpeta R_SERVICES para la instancia. Para obtener más información, incluida la forma de determinar qué paquetes ya están instalados, consulte [paquetes predeterminada de R y Python en SQL Server](installing-and-managing-r-packages.md).

## <a name="new-to-sql-server"></a>Novedad en SQL Server

Como desarrollador de R trabajando en el código se ejecuta en SQL Server, las directivas de seguridad que protege el servidor restringen la capacidad de controlar el entorno de R.

### <a name="r-user-libraries-not-supported-on-sql-server"></a>Bibliotecas de R de usuario: no se admite en SQL Server

Los desarrolladores de R que necesitan para instalar nuevos paquetes de R están acostumbrados a la instalación de paquetes a voluntad, mediante una privada, la biblioteca de usuario cada vez que la biblioteca predeterminada no está disponible o cuando el desarrollador no es un administrador en el equipo. Por ejemplo, en un entorno de desarrollo de R típico, el usuario agregaría la ubicación del paquete a la variable de entorno de R `libPath`, o hacer referencia a la ruta de acceso completa del paquete, similar al siguiente:

```R
library("c:/Users/<username>/R/win-library/packagename")
```

Esto no funciona cuando se ejecuta soluciones de R en SQL Server, porque los paquetes de R deben instalarse en una biblioteca predeterminada específica que está asociada a la instancia. Cuando un paquete no está disponible en la biblioteca predeterminada, obtendrá este error al intentar llamar al paquete:

*Error en There: no hay ningún paquete llamado 'package-name'*

### <a name="avoid-package-not-found-errors"></a>Evitar errores de "no se encontró el paquete"

+ Eliminar las dependencias en las bibliotecas de usuario. 

    Es una práctica incorrecta de desarrollo para instalar paquetes de R necesarios en una biblioteca de usuario personalizada, ya que puede provocar errores si se ejecuta una solución a otro usuario que no tiene acceso a la ubicación de la biblioteca.

    Además, si se instala un paquete en la biblioteca predeterminada, el runtime de R carga el paquete desde la biblioteca predeterminada, incluso si se especifica una versión diferente en el código de R.

+ Modifique el código para ejecutarlo en un entorno compartido.

+ Evite la instalación de paquetes como parte de una solución. Si no tiene permisos para instalar paquetes, se producirá un error en el código. Incluso si tiene permisos para instalar paquetes, debe hacer por separado del resto del código que desea ejecutar.

+ Comprobar el código para asegurarse de que no hay ninguna llamada a paquetes no instalados.

+ Actualice el código para quitar las referencias directas a las rutas de acceso de paquetes de R o bibliotecas de R. 

+ Saber qué biblioteca de paquetes está asociada a la instancia. Para obtener más información, consulte [paquetes predeterminada de R y Python en SQL Server](installing-and-managing-r-packages.md).

## <a name="see-also"></a>Vea también

+ [Instalación de paquetes de R adicionales](install-additional-r-packages-on-sql-server.md)
+ [Instalación de paquetes de Python adicionales](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriales, muestras y soluciones](../tutorials/machine-learning-services-tutorials.md)