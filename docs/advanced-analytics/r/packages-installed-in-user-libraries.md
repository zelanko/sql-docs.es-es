---
title: Evitar errores en paquetes de R instalados en bibliotecas de usuario | Documentos de Microsoft
titleSuffix: SQL Server
ms.custom: 
ms.date: 02/20/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 99ffd9b8-aa6d-4ac2-9840-4e66d0463978
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: b7f640cc33cb61ab8dffc57edb3b522808129880
ms.sourcegitcommit: c08d665754f274e6a85bb385adf135c9eec702eb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/28/2018
---
# <a name="avoiding-errors-on-r-packages-installed-in-user-libraries"></a>Evitar errores en paquetes de R instalados en bibliotecas de usuario
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Los usuarios experimentados de R están acostumbrados a la instalación de paquetes de R en una biblioteca de usuario, siempre que la biblioteca predeterminada está bloqueado o no está disponible. Sin embargo, este enfoque no se admite en SQL Server y la instalación en una biblioteca de usuario finaliza normalmente un error "no se encontró el paquete".

Este artículo describe soluciones alternativas para evitar este error. Explica cómo puede modificar el código de R y sugiere el proceso de instalación de paquetes de R correcto para el uso de paquetes de R desde una instancia de SQL Server.

## <a name="why-r-user-libraries-cannot-be-accessed-from-sql-server"></a>¿Por qué no se pueden tener acceso a las bibliotecas de usuario de R desde SQL Server

Los desarrolladores de R que necesitan para instalar nuevos paquetes de R están acostumbrados a la instalación de paquetes cuando lo desee, con una privada, la biblioteca de usuario cada vez que la biblioteca predeterminada no está disponible, o cuando el desarrollador no es un administrador en el equipo.

Por ejemplo, en un entorno de desarrollo de R típico, el usuario podría agregar la ubicación del paquete a la variable de entorno de R `libPath`, o hacer referencia a la ruta de acceso de paquete completo, similar al siguiente:

```R
library("c:/Users/<username>/R/win-library/packagename")
```

Esto no funciona al ejecutar soluciones en R en SQL Server, porque los paquetes de R deben instalarse en una biblioteca de datos específica que está asociada a la instancia. Cuando un paquete no está disponible en la biblioteca predeterminada, obtendrá este error al intentar llamar al paquete:

*Error en library(xxx): no hay ningún paquete denominado 'nombre del paquete'*

## <a name="how-to-avoid-package-not-found-errors"></a>Cómo evitar los errores de "no se encontró el paquete"

+ Eliminar las dependencias en las bibliotecas de usuario 

    Es una práctica de desarrollo incorrecta para instalar paquetes de R necesarios en una biblioteca de usuario personalizada, ya que puede provocar errores si se ejecuta una solución de otro usuario que no tiene acceso a la ubicación de la biblioteca.

    Además, si un paquete está instalado en la biblioteca de forma predeterminada, el runtime de R carga el paquete de la biblioteca de forma predeterminada, incluso si ha especificado una versión diferente en el código de R.

+ Modificar el código para que se ejecute en un entorno compartido.

+ Evitar la instalación de paquetes como parte de una solución. Si no tiene permisos para instalar paquetes, se producirá un error en el código. Incluso si tiene permisos para instalar paquetes, debe hacerlo por separado desde otro código que desea ejecutar.

+ Comprobar el código para asegurarse de que no hay ninguna llamada a paquetes no instalados.

+ Actualice el código para quitar las referencias directas a las rutas de acceso de paquetes de R o bibliotecas de R. 

+ Saber qué biblioteca del paquete está asociado a la instancia. Para obtener más información, vea [paquetes de R instalados con SQL Server](installing-and-managing-r-packages.md)
