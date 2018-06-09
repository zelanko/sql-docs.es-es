---
title: Sugerencias para usar paquetes de R instalados en las bibliotecas de usuario en SQL Server | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/30/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e52a6f4a9a3830aab01e54819804785a7069c9d2
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34708473"
---
# <a name="tips-for-using-r-packages-in-sql-server"></a>Sugerencias para utilizar paquetes de R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo tiene secciones independientes para los DBA que no estén familiarizados con R y los desarrolladores experimentados de R que son el acceso de paquete desconocido en una instancia de SQL Server.

## <a name="new-to-r"></a>Nuevo a R

Como administrador instalar R paquetes por primera vez, conocer algunos conceptos básicos sobre la administración de paquetes de R pueden ayudar a empezar a trabajar.

### <a name="package-dependencies"></a>Dependencias de paquetes

Paquetes de R con frecuencia dependen de varios otros paquetes, algunos de los cuales podrían no estar disponibles en la biblioteca de R predeterminada utilizada por la instancia. A veces, un paquete requiere una versión diferente de un paquete dependiente que ya está instalado. Dependencias del paquete se indican en un archivo de descripción incrustado en el paquete, pero a veces están incompletas. Puede usar un paquete denominado [iGraph](http://igraph.org/r/) articular completamente el gráfico de dependencias.

Si necesita instalar varios paquetes o desea asegurarse de que todas las personas de su organización obtienen el tipo de paquete correcto y la versión, recomendamos que use la [miniCRAN](https://mran.microsoft.com/package/miniCRAN) paquete para analizar la cadena de dependencia completas. minicRAN crea un repositorio local que se pueden compartir entre varios usuarios o equipos. Para obtener más información, consulte [crear un repositorio de paquete local mediante miniCRAN](create-a-local-package-repository-using-minicran.md).

### <a name="package-sources-versions-and-formats"></a>Formatos, versiones y orígenes de paquetes

Hay varios orígenes de paquetes de R, como [CRAN](https://cran.r-project.org/) y [Bioconductor](https://www.bioconductor.org/). El sitio oficial del lenguaje R (<https://www.r-project.org/>) enumera muchos de estos recursos. Microsoft ofrece [MRAN](https://mran.microsoft.com/) para su distribución de R de código abierto ([MRO](https://mran.microsoft.com/open)) y otros paquetes. Número de paquetes se publica en GitHub, donde los desarrolladores pueden obtener el código fuente.

Paquetes de R se ejecutan en varias plataformas informáticas. Asegúrese de que las versiones que son binarios de Windows.

### <a name="know-which-library-you-are-installing-to-and-which-packages-are-already-installed"></a>Conocer la biblioteca en la que va a instalar y los paquetes que ya están instalados.

Si previamente se ha modificado el entorno de R en el equipo, antes de instalar cualquier cosa, asegúrese de que la variable de entorno de R `.libPath` utiliza una sola ruta de acceso.

Esta ruta de acceso debe apuntar a la carpeta R_SERVICES para la instancia. Para obtener más información, incluida la forma de determinar qué paquetes ya están instalados, consulte [R predeterminado y Python paquetes en SQL Server](installing-and-managing-r-packages.md).

## <a name="new-to-sql-server"></a>Experiencia en SQL Server

Como desarrollador R trabajar en código que se ejecuta en SQL Server, las directivas de seguridad que protege el servidor restringen la capacidad de controlar el entorno de R.

### <a name="r-user-libraries-not-supported-on-sql-server"></a>Bibliotecas de usuario de R: no se admite en SQL Server

Los desarrolladores de R que necesitan para instalar nuevos paquetes de R están acostumbrados a la instalación de paquetes cuando lo desee, con una privada, la biblioteca de usuario cada vez que la biblioteca predeterminada no está disponible, o cuando el desarrollador no es un administrador en el equipo. Por ejemplo, en un entorno de desarrollo de R típico, el usuario podría agregar la ubicación del paquete a la variable de entorno de R `libPath`, o hacer referencia a la ruta de acceso de paquete completo, similar al siguiente:

```R
library("c:/Users/<username>/R/win-library/packagename")
```

Esto no funciona al ejecutar soluciones en R en SQL Server, porque los paquetes de R deben instalarse en una biblioteca de datos específica que está asociada a la instancia. Cuando un paquete no está disponible en la biblioteca predeterminada, obtendrá este error al intentar llamar al paquete:

*Error en library(xxx): no hay ningún paquete denominado 'nombre del paquete'*

### <a name="avoid-package-not-found-errors"></a>Evitar errores de "no se encontró el paquete"

+ Eliminar dependencias en las bibliotecas de usuario. 

    Es una práctica de desarrollo incorrecta para instalar paquetes de R necesarios en una biblioteca de usuario personalizada, ya que puede provocar errores si se ejecuta una solución de otro usuario que no tiene acceso a la ubicación de la biblioteca.

    Además, si un paquete está instalado en la biblioteca de forma predeterminada, el runtime de R carga el paquete de la biblioteca de forma predeterminada, aunque especifique una versión distinta en el código de R.

+ Modificar el código para que se ejecute en un entorno compartido.

+ Evitar la instalación de paquetes como parte de una solución. Si no tiene permisos para instalar paquetes, se producirá un error en el código. Incluso si tiene permisos para instalar paquetes, debe hacerlo por separado desde otro código que desea ejecutar.

+ Comprobar el código para asegurarse de que no hay ninguna llamada a paquetes no instalados.

+ Actualice el código para quitar las referencias directas a las rutas de acceso de paquetes de R o bibliotecas de R. 

+ Saber qué biblioteca del paquete está asociado a la instancia. Para obtener más información, consulte [R predeterminado y Python paquetes en SQL Server](installing-and-managing-r-packages.md).

## <a name="see-also"></a>Vea también

+ [Instalación de paquetes de R adicionales](install-additional-r-packages-on-sql-server.md)
+ [Instalación de paquetes de Python adicionales](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriales, muestras y soluciones](../tutorials/machine-learning-services-tutorials.md)