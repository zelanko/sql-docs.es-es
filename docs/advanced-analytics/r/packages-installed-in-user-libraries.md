---
title: Evitar errores en paquetes de R instalados en bibliotecas de usuario | Documentos de Microsoft
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 99ffd9b8-aa6d-4ac2-9840-4e66d0463978
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 0de06ebee16d903b4b00c9d8e4673bf450c485d1
ms.contentlocale: es-es
ms.lasthandoff: 10/10/2017

---
# <a name="avoiding-errors-on-r-packages-installed-in-user-libraries"></a>Evitar errores en paquetes de R instalados en bibliotecas de usuario

Los usuarios experimentados de R están acostumbrados a la instalación de paquetes de R en una biblioteca de usuario, siempre que la biblioteca predeterminada está bloqueado o no está disponible. Sin embargo, este enfoque no se admite en SQL Server y la instalación en una biblioteca de usuario finaliza normalmente un error "no se encontró el paquete".

Este tema proporciona soluciones para ayudarle a evitar este error. Explica cómo puede modificar el código de R y sugiere el proceso de instalación de paquetes de R correcto para el uso de paquetes de R desde una instancia de SQL Server.

## <a name="why-r-user-libraries-cannot-be-accessed-from-sql-server"></a>¿Por qué no se pueden tener acceso a las bibliotecas de usuario de R desde SQL Server

Los desarrolladores de R que necesitan para instalar nuevos paquetes de R están acostumbrados a la instalación de paquetes a voluntad y utilizar una biblioteca de usuario privada, siempre que la biblioteca predeterminada no está disponible, o cuando el desarrollador no es un administrador en el equipo.

Por ejemplo, en un entorno de desarrollo de R típico, el usuario podría agregar la ubicación del paquete a la variable de entorno de R `libPath`, o hacer referencia a la ruta de acceso de paquete completo, similar al siguiente:

```R
library("c:/Users/<username>/R/win-library/packagename")  
```

Sin embargo, esto nunca funcionará al ejecutar soluciones en R en SQL Server, porque los paquetes de R deben instalarse en una biblioteca de datos específica que está asociada a la instancia.

Si el paquete no está instalado en la biblioteca predeterminada, podría aparecer este error al intentar llamar al paquete:

*Error en library(xxx): no hay ningún paquete denominado 'nombre del paquete'*

También es una práctica de desarrollo incorrecta para instalar paquetes de R necesarios en una biblioteca de usuario personalizada, ya que puede provocar errores si se ejecuta una solución de otro usuario que no tiene acceso a la ubicación de la biblioteca.

## <a name="how-to-install-r-packages-to-an-accessible-library"></a>Cómo instalar paquetes de R en una biblioteca de accesible

**Para SQL Server 2016**

Utilice la biblioteca de paquete asociada a la instancia. Para obtener más información, vea [paquetes de R instalados con SQL Server](installing-and-managing-r-packages.md)

**Para SQL Server de 2017**

SQL Server proporciona características para ayudarle a administrar varias versiones de paquete y otorgar permisos de usuarios a los paquetes individuales, sin necesidad de que los usuarios tengan acceso al sistema de archivos.

Para obtener más información sobre cómo configurar una biblioteca compartida de paquete y asignar usuarios a roles, consulte [administración de paquetes de R para SQL Server](r-package-management-for-sql-server-r-services.md).

Si toma el enfoque de administración del paquete basado en roles de base de datos, no es necesario instalar varias copias del mismo paquete en los directorios de usuario diferente. Instalar una única copia del paquete que necesita y compartirlo con los usuarios autenticados. Puesto que los paquetes se administran en el nivel de base de datos, también puede copiar los grupos de los paquetes y permiso relacionada entre bases de datos.

## <a name="tips-for-avoiding-package-not-found-errors"></a>Sugerencias para evitar errores de "no se encontró el paquete"

+ Modifique el código para eliminar las dependencias de bibliotecas de usuario. Al migrar las soluciones de R se ejecuten [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)], es importante que haga lo siguiente:

    + Instalar los paquetes que necesita en la biblioteca predeterminada asociada a la instancia.

    + Modifique el código para asegurarse de que los paquetes se cargan desde la biblioteca de forma predeterminada, no desde directorios ad hoc o bibliotecas de usuario.

+ Evite la instalación del paquete ad hoc como parte de una solución. Compruebe el código para asegurarse de que no hay ninguna llamada a paquetes instalados, o el código que instala paquetes dinámicamente. Si no tiene permisos, se producirá un error en el código y, si dispone de permisos, debe instalar los paquetes de forma independiente del resto del código que desea ejecutar.

+ Modificar las rutas de acceso directos a las bibliotecas de paquete de R. Si un paquete está instalado en la biblioteca predeterminada, el tiempo de ejecución de R lo cargará desde la biblioteca predeterminada, aunque se haya especificado otra biblioteca en el código de R.

