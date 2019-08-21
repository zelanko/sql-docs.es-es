---
title: Uso de administradores de paquetes de R
description: Use comandos de R estándar como install. Packages para agregar nuevos paquetes de R a SQL Server 2016 R Services o SQL Server Machine Learning Services (in-Database).
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1f6d828a7267ab2b4b1def17f9d1c6bf4a6018dc
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2019
ms.locfileid: "69633618"
---
# <a name="use-r-package-managers-to-install-r-packages-on-sql-server"></a>Usar administradores de paquetes de R para instalar paquetes de R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Puede usar las herramientas de R estándar para instalar nuevos paquetes en una instancia de SQL Server 2016 o SQL Server 2017, lo que le proporcionará un puerto abierto 80 y tendrá derechos de administrador.

> [!IMPORTANT] 
> Asegúrese de instalar paquetes en la biblioteca predeterminada que está asociada a la instancia actual. No instale nunca paquetes en un directorio de usuario.

Este procedimiento usa RGui, pero puede usar RTerm o cualquier otra herramienta de línea de comandos de R que admita el acceso con privilegios elevados.

## <a name="install-a-package-using-rgui"></a>Instalación de un paquete con RGui

1. [Determinar la ubicación de la biblioteca de instancias](../package-management/r-package-information.md). Navegue hasta la carpeta donde están instaladas las herramientas de R. Por ejemplo, la ruta de acceso predeterminada para una instancia predeterminada de SQL Server 2017 es la siguiente:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`

1. Haga clic con el botón secundario en RGui. exe y seleccione **Ejecutar como administrador**. Si no dispone de los permisos necesarios, póngase en contacto con el administrador de la base de datos y proporcione una lista de los paquetes que necesita.

1. Desde la línea de comandos, si conoce el nombre del paquete, puede escribir: `install.packages("the_package-name")`Se requieren comillas dobles para el nombre del paquete.

1. Cuando se le pida un sitio reflejado, seleccione cualquier sitio que sea adecuado para su ubicación.

Si el paquete de destino depende de paquetes adicionales, el instalador de R descarga automáticamente las dependencias y las instala.

Si tiene varias instancias de SQL Server, como instancias en paralelo de SQL Server 2016 R Services y SQL Server Machine Learning Services, ejecute la instalación por separado para cada instancia si desea utilizar el paquete en ambos contextos. Los paquetes no se pueden compartir entre instancias.

## <a name = "bkmk_offlineInstall"></a>Instalación sin conexión mediante herramientas de R

Si el servidor no tiene acceso a Internet, se requieren pasos adicionales para preparar los paquetes. Para instalar paquetes de R en un servidor que no tiene acceso a Internet, debe:

+ Analice las dependencias de antemano.
+ Descargue el paquete de destino en un equipo con acceso a Internet.
+ Descargue los paquetes necesarios en el mismo equipo y coloque todos los paquetes en un solo archivo de paquete.
+ Comprimir el archivo si aún no está en formato comprimido.
+ Copie el archivo de paquete en una ubicación en el servidor.
+ Instale el paquete de destino especificando el archivo de almacenamiento como origen.

> [!IMPORTANT] 
>  Asegúrese de analizar todas las dependencias y descargar **todos los** paquetes necesarios **antes** de comenzar la instalación. Se recomienda [miniCRAN](https://mran.microsoft.com/package/miniCRAN) para este proceso. Este paquete de R toma una lista de los paquetes que desea instalar, analiza las dependencias y obtiene todos los archivos comprimidos. a continuación, miniCRAN crea un repositorio único que se puede copiar en el equipo servidor. Para obtener más información, consulte [crear un repositorio de paquetes local mediante miniCRAN](create-a-local-package-repository-using-minicran.md)

En este procedimiento se supone que ha preparado todos los paquetes que necesita, en formato comprimido, y están listos para copiarlos en el servidor.

1. Copie el archivo comprimido del paquete, o para varios paquetes, el repositorio completo que contiene todos los paquetes en formato comprimido en una ubicación a la que el servidor pueda tener acceso.

2. Abra la carpeta en el servidor donde están instaladas las herramientas de R para la instancia de. Por ejemplo, si está usando el símbolo del sistema de Windows en un sistema con SQL Server R Services de 2016, `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`cambie a.

3. Haga clic con el botón derecho en RGui o RTerm y seleccione **Ejecutar como administrador**.

4. Ejecute el comando `install.packages` de R y especifique el nombre del paquete o del repositorio y la ubicación de los archivos comprimidos.

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    Este comando extrae el paquete `mynewpackage` de R de su archivo comprimido local, siempre que haya guardado la copia en `C:\Temp\Downloaded packages`el directorio e instale el paquete en el equipo local. Si el paquete tiene dependencias, el instalador comprueba si hay paquetes existentes en la biblioteca. Si ha creado un repositorio que incluye las dependencias, el instalador instala también los paquetes necesarios.

    Si los paquetes necesarios no están presentes en la biblioteca de instancias y no se encuentran en los archivos comprimidos, se produce un error en la instalación del paquete de destino.

## <a name="see-also"></a>Vea también

+ [Instalación de paquetes de R adicionales](install-additional-r-packages-on-sql-server.md)
+ [Instalación de paquetes de Python adicionales](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriales, muestras y soluciones](../tutorials/machine-learning-services-tutorials.md)
