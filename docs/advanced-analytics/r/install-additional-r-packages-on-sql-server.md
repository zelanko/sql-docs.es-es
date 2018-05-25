---
title: Instalar nuevos paquetes de R en SQL Server Machine Learning Services | Documentos de Microsoft
description: Agregar nuevos paquetes de R para SQL Server 2016 R Services o SQL Server de 2017 Machine Learning Services (In-Database)
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/10/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 20ef7181c5ab8c0494f73b205dddcdf1ac0a620e
ms.sourcegitcommit: b5ab9f3a55800b0ccd7e16997f4cd6184b4995f9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2018
---
# <a name="install-new-r-packages-on-sql-server"></a>Instalar nuevos paquetes de R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe cómo instalar nuevos paquetes de R a una instancia de SQL Server donde está habilitado el aprendizaje automático. Existen varios métodos para instalar nuevos paquetes de R, dependiendo de qué versión de SQL Server tiene, y si el servidor tiene una conexión a internet. Los métodos siguientes para la nueva instalación de paquete son posibles.

| Método                           | Permissions  | Remota o Local |
|------------------------------------|---------------------------|-------|
| [Utilizar administradores de paquetes de R convencionales](#bkmk_rInstall)  | Administración | Local |
| [Uso de RevoScaleR](use-revoscaler-to-manage-r-packages.md) | Administración | Local |
| [Usar T-SQL (crear biblioteca externa)](install-r-packages-tsql.md) | Administrador para que el programa de instalación, después los roles de base de datos | both 
| [Use una miniCRAN para crear un repositorio local](create-a-local-package-repository-using-minicran.md) | Administrador para que el programa de instalación, después los roles de base de datos | both |

## <a name="bkmk_rInstall"></a> Instalar paquetes de R a través de una conexión a Internet

Puede usar las herramientas estándar de R para instalar nuevos paquetes en una instancia de SQL Server 2016 o SQL Server 2017, proporcionando el equipo tiene un puerto abierto 80 y tener derechos de administrador.

> [!IMPORTANT] 
> Asegúrese de instalar paquetes en la biblioteca predeterminada que está asociada a la instancia actual. Nunca instale paquetes en un directorio de usuario.

Este procedimiento utiliza RGui pero se puede utilizar RTerm o cualquier otro R herramienta línea de comandos que admite el acceso con privilegios elevados.

### <a name="install-a-package-using-rgui"></a>Instalar un paquete mediante RGui

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
> > Asegúrese de que analizar todas las dependencias y descargar **todos los** paquetes requeridos **antes de** comenzar la instalación. Se recomienda [miniCRAN](https://mran.microsoft.com/package/miniCRAN) para este proceso. Este paquete de R toma una lista de paquetes que desea instalar, analiza las dependencias y obtiene todos los archivos comprimidos. miniCRAN, a continuación, crea un repositorio único que puede copiar en el equipo del servidor.
> 
> Para obtener más información, vea [crear un repositorio de paquete local mediante miniCRAN](create-a-local-package-repository-using-minicran.md)

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

## <a name="tips-for-package-installation"></a>Sugerencias para la instalación del paquete

Esta sección proporciona sugerencias ordenadas y preguntas comunes relacionadas con la instalación del paquete de R en SQL Server.

###  <a name="packageVersion"></a> Obtener la versión de paquete correcto y formato

Hay varios orígenes de paquetes de R, como CRAN y Bioconductor. El sitio oficial del lenguaje R (<https://www.r-project.org/>) enumera muchos de estos recursos. Número de paquetes se publica en GitHub, donde puede obtener el código fuente. Por último, podría haber recibido paquetes de R desarrollados por algún miembro de su empresa, o tiene un paquete personalizado que ha escrito.

Independientemente del origen, antes de intentar instalar el paquete, asegúrese de que ha obtenido el formato binario para la plataforma Windows. 

### <a name="bkmk_zipPreparation"></a> Descargar el paquete como un archivo comprimido

Para la instalación en un servidor sin acceso a internet, debe descargar una copia del paquete en el formato de un archivo comprimido para la instalación sin conexión. **Descomprima el paquete.**

Por ejemplo, el siguiente procedimiento describe ahora para obtener la versión correcta de la [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) paquete desde Bioconductor, suponiendo que el equipo tiene acceso a internet.

1.  En la lista de **archivos de paquetes** , busque la versión **binaria de Windows** .

2.  Haga clic en el vínculo a la. Archivo ZIP y seleccione **Guardar destino como**.

3.  Vaya a la carpeta local donde se almacenan los paquetes comprimidos y haga clic en **guardar**.

    Este proceso crea una copia local del paquete. 

4. Si recibe un error de descarga, pruebe a un sitio de réplica diferente.

5. Después de que se ha descargado el archivo de paquete, puede instalar el paquete, o copiar el paquete comprimido en un servidor que no tiene acceso a internet.

> [!TIP]
> Si por error instala el paquete en lugar de descargar los archivos binarios, también se guarda una copia del archivo zip descargado en el equipo. Ver los mensajes de estado tal y como se instala el paquete para determinar la ubicación del archivo. Puede copiar dicho archivo comprimido en el servidor que no tiene acceso a internet.
> 
> Sin embargo, al obtener paquetes con este método, no se incluyen las dependencias. 

### <a name="bkmk_packageDependencies"></a> Obtención de paquetes necesarios

Paquetes de R con frecuencia dependen de varios otros paquetes, algunos de los cuales podrían no estar disponibles en la biblioteca de R predeterminada utilizada por la instancia. A veces, un paquete requiere una versión diferente de un paquete dependiente que ya está instalado.

Si necesita instalar varios paquetes o desea asegurarse de que todas las personas de su organización obtienen el tipo de paquete correcto y la versión, recomendamos que use la [miniCRAN](https://mran.microsoft.com/package/miniCRAN) paquete para analizar la cadena de dependencia completas. minicRAN crea un repositorio local que se pueden compartir entre varios usuarios o equipos. Para obtener más información, consulte [crear un repositorio de paquete local mediante miniCRAN](create-a-local-package-repository-using-minicran.md).


### <a name="know-which-library-you-are-installing-to-and-which-packages-are-already-installed"></a>Conocer la biblioteca en la que va a instalar y los paquetes que ya están instalados.

Si previamente se ha modificado el entorno de R en el equipo, antes de instalar cualquier cosa, poner en pausa un momento y asegúrese de que la variable de entorno de R `.libPath` utiliza una sola ruta de acceso.

Esta ruta de acceso debe apuntar a la carpeta R_SERVICES para la instancia. Para obtener más información, incluida la forma de determinar qué paquetes ya están instalados, consulte [paquetes de R instalados con SQL Server](installing-and-managing-r-packages.md).

### <a name="side-by-side-installation-with-standalone-r-or-python-servers"></a>Instalación en paralelo con Standalone R o servidores de Python

Si ha instalado el servidor de aprendizaje de SQL Server de 2017 Microsoft máquina (independiente) o SQL Server 2016 R Server (independiente) además de los análisis en bases de datos (SQL Server 2017 Machine Learning Services y SQL Server 2016 R Services), el equipo tiene Separe las instalaciones de R para cada una, con los duplicados de todas las bibliotecas y herramientas de R.

Paquetes que se instalan en la biblioteca R_SERVER solo son utilizados por un servidor independiente y no se pueden tener acceso a una instancia de SQL Server (In-Database). Utilice siempre el `R_SERVICES` biblioteca al instalar los paquetes que desea utilizar en bases de datos en SQL Server.
