---
title: Instalar nuevos paquetes de R en SQL Server Machine Learning Services | Documentos de Microsoft
description: Agregar nuevos paquetes de R para SQL Server 2016 R Services o SQL Server de 2017 Machine Learning Services (In-Database)
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8f7b0ee2b623f6a208a92823948bf0295bae33f6
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/01/2018
ms.locfileid: "34707503"
---
# <a name="use-r-package-managers-to-install-r-packages-on-sql-server"></a>Utilizar administradores de paquetes de R para instalar paquetes de R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Puede usar las herramientas estándar de R para instalar nuevos paquetes en una instancia de SQL Server 2016 o SQL Server 2017, proporcionando el equipo tiene un puerto abierto 80 y tener derechos de administrador.

> [!IMPORTANT] 
> Asegúrese de instalar paquetes en la biblioteca predeterminada que está asociada a la instancia actual. Nunca instale paquetes en un directorio de usuario.

Este procedimiento utiliza RGui pero se puede utilizar RTerm o cualquier otro R herramienta línea de comandos que admite el acceso con privilegios elevados.

## <a name="install-a-package-using-rgui"></a>Instalar un paquete mediante RGui

1. [Determinar la ubicación de la biblioteca de instancia](installing-and-managing-r-packages.md). Navegue hasta la carpeta donde se instalan las herramientas de R. Por ejemplo, la ruta de acceso predeterminada para una instancia predeterminada de SQL Server 2017 es como sigue: `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`

1. Haga clic en RGui.exe y seleccione **ejecutar como administrador**. Si no tiene los permisos necesarios, póngase en contacto con el Administrador de base de datos y proporcionar una lista de los paquetes que necesita.

1. Desde la línea de comandos, si conoce el nombre del paquete, puede escribir: `install.packages("the_package-name")` comillas dobles son necesarias para el nombre del paquete.

1. Cuando se le pida un sitio de réplica, seleccione cualquier sitio que es conveniente para su ubicación.

Si el paquete de destino depende de otros paquetes, descarga las dependencias automáticamente el instalador de R y los instala automáticamente.

Si tiene varias instancias de SQL Server, como side-by-side las instancias de SQL Server 2016 R Services y servicios de aprendizaje de máquina de 2017 de SQL Server, ejecute la instalación por separado para cada instancia si desea utilizar el paquete en ambos contextos. Los paquetes no se pueden compartir entre instancias.

## <a name = "bkmk_offlineInstall"></a> Instalación sin conexión con herramientas de R

Si el servidor no tiene acceso a internet, se requieren pasos adicionales para preparar los paquetes. Para instalar paquetes de R en un servidor que no tiene acceso a internet, debe:

+ Analizar las dependencias de antemano.
+ Descargue el paquete de destino en un equipo con acceso a Internet.
+ Descargar los paquetes necesarios en el mismo equipo y colocar todos los paquetes en un archivo de paquete único.
+ El archivo zip si aún no está en formato comprimido.
+ Copie el archivo de paquete en una ubicación en el servidor.
+ Instale el paquete de destino Especifica el archivo de almacenamiento como origen.

> [!IMPORTANT] 
>  Asegúrese de que analizar todas las dependencias y descargar **todos los** paquetes requeridos **antes de** comenzar la instalación. Se recomienda [miniCRAN](https://mran.microsoft.com/package/miniCRAN) para este proceso. Este paquete de R toma una lista de paquetes que desea instalar, analiza las dependencias y obtiene todos los archivos comprimidos. miniCRAN, a continuación, crea un repositorio único que puede copiar en el equipo del servidor. Para obtener más información, vea [crear un repositorio de paquete local mediante miniCRAN](create-a-local-package-repository-using-minicran.md)

Este procedimiento se supone que ha preparado todos los paquetes que necesita, en formato comprimido y está listo para copiarlos en el servidor.

1. Copia el paquete en archivo ZIP o para varios paquetes en el repositorio completando que contiene todos los paquetes en zip formato en una ubicación que el servidor tiene acceso.

2. Abra la carpeta en el servidor donde se instalan las herramientas de R para la instancia. Por ejemplo, si se usa el símbolo del sistema de Windows en un sistema con SQL Server 2016 R Services, cambia a `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`.

3. Haga doble clic en RGui o RTerm y seleccione **ejecutar como administrador**.

4. Ejecute el comando R `install.packages` y especifique el paquete o el nombre del repositorio y la ubicación de los archivos comprimidos.

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    Este comando extrae el paquete de R `mynewpackage` de su archivo comprimido local, siempre que haya guardado la copia en el directorio `C:\Temp\Downloaded packages`e instala el paquete en el equipo local. Si el paquete tiene dependencias, el instalador comprueba si los paquetes existentes en la biblioteca. Si ha creado un repositorio que incluye las dependencias, el programa de instalación instala también los paquetes necesarios.

    Si los paquetes necesarios no están presentes en la biblioteca de la instancia y no se encuentra en los archivos comprimidos, se produce un error en la instalación del paquete de destino.

## <a name="see-also"></a>Vea también

+ [Instalación de paquetes de R adicionales](install-additional-r-packages-on-sql-server.md)
+ [Instalación de paquetes de Python adicionales](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriales, muestras y soluciones](../tutorials/machine-learning-services-tutorials.md)