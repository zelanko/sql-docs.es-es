---
title: Instalar o configurar herramientas de R | Microsoft Docs
ms.custom: 
ms.date: 01/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7c04ae30-d391-4369-9742-d2b275e14c0d
caps.latest.revision: 9
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a3baf97a960d7e8f950bb6e9cd251550f4c4b942
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="setup-or-configure-r-tools"></a>Instalar o configurar herramientas de R
  Microsoft R Server proporciona todas las bibliotecas de R básicas, un conjunto de paquetes de ScaleR y las herramientas de R estándar que se necesitan para desarrollar y probar el código R. Aun así, si quiere usar un entorno de desarrollo de R dedicado, hay varias herramientas disponibles, muchas de ellas gratuitas.  
  
## <a name="basic-r-tools"></a>Herramientas de R básicas  
 En una instalación de Microsoft R Server no se precisan más herramientas, ya que todas las herramientas de R estándar que se incluyen en una *instalación base* de R se instalan de forma predeterminada.

-   **RTerm**: herramienta de línea de comandos para ejecutar scripts de R. 
  
-   **RGui.exe**: sencillo editor interactivo de R. Los argumentos de la línea de comandos son los mismos en RGui.exe y en RTerm. 
  
-   **RScript**: herramienta de línea de comandos para ejecutar scripts de R en el modo por lotes.  

Para encontrar estas herramientas, busque la ubicación de la biblioteca de R. Esta dependerá de si ha instalado solo SQL Server R Services o si también ha instalado R Server (independiente). Para más información, vea [Qué está instalado y dónde encontrar paquetes de R](https://msdn.microsoft.com/library/mt695941(sql.130).aspx#Anchor_1).

Luego, busque en la carpeta `..\R_SERVER\bin\x64`.  

> [!TIP]  
>  ¿Necesita ayuda con las herramientas de R? Encontrará documentación en la carpeta de instalación: `C:\Program Files\Microsoft SQL Server\R_SERVER\doc` y en `C:\Program Files\Microsoft SQL Server\R_SERVER\doc\manual`.  
>   
>  También puede abrir **RGui**, hacer clic en **Help** y seleccionar una de las opciones.  

## <a name="microsoft-r-client"></a>Cliente de Microsoft R

Microsoft R Client es una descarga gratuita que permite desarrollar soluciones de R que se pueden ejecutar fácilmente en Microsoft R Server o en SQL Server R Services. Esta opción se proporciona para que los científicos de datos que no tienen acceso a R Server (disponible en Enterprise Edition) puedan desarrollar soluciones que usen ScaleR. 

Si usa un entorno de desarrollo de R diferente, como Herramientas de R para Visual Studio o RStudio, y va a usar ScaleR, deberá especificar que Microsoft R Client se usará como el ejecutable de R. Esto proporciona acceso total al paquete de RevoScaleR y a otras características de Microsoft R Server, aunque el rendimiento se verá limitado.

También puede usar las herramientas proporcionadas en R Client (como RGui y RTerm) para ejecutar scripts o escribir y ejecutar código de R ad hoc.

[Instalar Microsoft R Client](https://msdn.microsoft.com/microsoft-r/r-client-install)
  
##  <a name="bkmk_RTools"></a> Herramientas de R para Visual Studio  

 Para trabajar más cómodamente con bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], sopese la posibilidad de usar [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] como entorno de desarrollo. [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] es un complemento gratuito de Visual Studio que funciona en todas las ediciones de Visual Studio. Visual Studio también admite la integración de Python y F#.  

 Para obtener instrucciones de instalación, consulte [cómo instalar herramientas de R para Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation).

> [!TIP]
> Antes de instalar nuevos paquetes, compruebe qué tiempo de ejecución de R se está usando de forma predeterminada. Si no lo hace, puede ocurrir con mucha facilidad que se instalen nuevos paquetes de R en una ubicación de biblioteca predeterminada que, luego, no se pueden encontrar en R Server.


## <a name="rstudio"></a>RStudio

Si prefiere usar RStudio, se necesitan algunos pasos más para usar las bibliotecas de RevoScaleR:
- Instalar Microsoft R Server o Microsoft R Client para obtener los paquetes y las bibliotecas necesarios.
- Actualizar la ruta de acceso de R de forma que use el tiempo de ejecución de R Server.

Para más información, vea [Configure Your IDE](https://msdn.microsoft.com/microsoft-r/r-client-get-started#step-2-configure-your-ide) (Configurar el IDE).


## <a name="see-also"></a>Vea también  
 [Crear un R Server independiente](../../advanced-analytics/r-services/create-a-standalone-r-server.md)   
 [Introducción a Microsoft R Server &#40;independiente&#41;](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
  
  

