---
title: Usar los administradores de paquetes de R - SQL Server Machine Learning Services
description: Use los comandos de R estándar como install.packages para agregar nuevos paquetes de R a SQL Server 2016 R Services o SQL Server 2017 Machine Learning Services (In-Database).
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 6012fb1a3376c00a64239e0fbf10115b8a4367d8
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510392"
---
# <a name="use-r-package-managers-to-install-r-packages-on-sql-server"></a>Uso de R administradores de paquetes para instalar paquetes de R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Puede usar las herramientas de R estándar para instalar nuevos paquetes en una instancia de SQL Server 2016 o SQL Server 2017, que proporciona el equipo tiene un puerto abierto 80 y tener derechos de administrador.

> [!IMPORTANT] 
> Asegúrese de instalar paquetes en la biblioteca predeterminada que está asociada con la instancia actual. Nunca instale paquetes en un directorio de usuario.

Este procedimiento utiliza RGui pero puede usar RTerm o cualquier otro R línea de comandos que admite el acceso con privilegios elevados.

## <a name="install-a-package-using-rgui"></a>Instalar un paquete mediante RGui

1. [Determinar la ubicación de la biblioteca de instancia](installing-and-managing-r-packages.md). Navegue hasta la carpeta donde se instalan las herramientas de R. Por ejemplo, la ruta de acceso predeterminada para una instancia predeterminada de SQL Server 2017 es como sigue: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`

1. Haga clic en RGui.exe y seleccione **ejecutar como administrador**. Si no tiene los permisos necesarios, póngase en contacto con el Administrador de base de datos y proporcionar una lista de los paquetes que necesita.

1. Desde la línea de comandos, si conoce el nombre del paquete, puede escribir: `install.packages("the_package-name")` Las comillas dobles son necesarias para el nombre del paquete.

1. Cuando se le pida un sitio de réplica, seleccione cualquier sitio que es conveniente para su ubicación.

Si el paquete de destino depende de los paquetes adicionales, descarga las dependencias automáticamente el instalador de R y los instala automáticamente.

Si tiene varias instancias de SQL Server, como las instancias en paralelo de SQL Server 2016 R Services y SQL Server 2017 Machine Learning Services, ejecutar la instalación por separado para cada instancia si desea usar el paquete en ambos contextos. Los paquetes no se puede compartir entre instancias.

## <a name = "bkmk_offlineInstall"></a> Instalación sin conexión mediante herramientas de R

Si el servidor no tiene acceso a internet, se requieren pasos adicionales para preparar los paquetes. Para instalar paquetes de R en un servidor que no tiene acceso a internet, debe:

+ Analizar las dependencias de antemano.
+ Descargue el paquete de destino en un equipo con acceso a Internet.
+ Descargar los paquetes necesarios en el mismo equipo y colocar todos los paquetes en un archivo de paquete único.
+ El archivo zip si aún no está en formato comprimido.
+ Copie el archivo de paquete en una ubicación en el servidor.
+ Instale el paquete de destino, especificando el archivo de almacenamiento como origen.

> [!IMPORTANT] 
>  Asegúrese de que analizar todas las dependencias y descargar **todas** los paquetes necesarios **antes** a partir de la instalación. Se recomienda [miniCRAN](https://mran.microsoft.com/package/miniCRAN) para este proceso. Este paquete de R toma una lista de los paquetes que desea instalar, analiza las dependencias y obtiene todos los archivos comprimidos para usted. miniCRAN, a continuación, crea un único repositorio que puede copiar en el equipo del servidor. Para obtener más información, consulte [crear un repositorio de paquete local mediante miniCRAN](create-a-local-package-repository-using-minicran.md)

Este procedimiento se supone que ha preparado todos los paquetes que necesita, en formato comprimido y está listo para copiarlos en el servidor.

1. Copia el paquete en archivos ZIP, o para varios paquetes, todo el repositorio que contiene todos los paquetes de comprimidos formato en una ubicación que el servidor pueda acceder.

2. Abra la carpeta en el servidor donde se instalan las herramientas de R para la instancia. Por ejemplo, si usa el símbolo del sistema de Windows en un sistema con SQL Server 2016 R Services, cambie a `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`.

3. Haga doble clic en RGui o RTerm y seleccione **ejecutar como administrador**.

4. Ejecute el comando de R `install.packages` y especifique el paquete o el nombre de repositorio y la ubicación de los archivos comprimidos.

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    Este comando extrae el paquete de R `mynewpackage` de su archivo comprimido local, siempre que haya guardado la copia en el directorio `C:\Temp\Downloaded packages`e instala el paquete en el equipo local. Si el paquete tiene dependencias, el instalador comprueba los paquetes existentes en la biblioteca. Si ha creado un repositorio que incluye las dependencias, el programa de instalación instala los paquetes necesarios también.

    Si los paquetes necesarios no están presentes en la biblioteca de la instancia y no se encuentra en los archivos comprimidos, se produce un error en la instalación del paquete de destino.

## <a name="see-also"></a>Vea también

+ [Instalación de paquetes de R adicionales](install-additional-r-packages-on-sql-server.md)
+ [Instalación de paquetes de Python adicionales](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriales, muestras y soluciones](../tutorials/machine-learning-services-tutorials.md)
