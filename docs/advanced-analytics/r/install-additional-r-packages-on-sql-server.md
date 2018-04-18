---
title: Instalar paquetes de R adicionales en SQL Server | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 0ac316f4870482b15700395eb44b3adef934f2ad
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="install-additional-r-packages-on-sql-server"></a>Instalar paquetes de R adicionales en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe cómo instalar nuevos paquetes de R a una instancia de SQL Server donde está habilitado el aprendizaje automático.

Existen varios métodos para instalar nuevos paquetes de R, dependiendo de qué versión de SQL Server tiene, y si el servidor tiene acceso a internet.

+ [Instalar nuevos paquetes con herramientas de R, con acceso a internet](#bkmk_rInstall)

    Usar comandos de R convencionales para instalar paquetes de Internet. Este es el método más sencillo, pero requiere acceso administrativo.

    **Se aplica a:**[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)][!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]. También se requiere para instancias de [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] donde no se ha habilitado la administración de paquetes a través de DDL.

+ [Instalar nuevos paquetes de R en un servidor con **sin** acceso a internet](#bkmk_offlineInstall)

    Si el servidor no tiene acceso a internet, son necesarios algunos pasos adicionales para preparar los paquetes. En esta sección se describe cómo preparar los archivos necesarios para la instalación del paquete y sus dependencias.

+ [Instalar paquetes mediante la instrucción crear biblioteca externa](#bkmk_createlibrary) 

    El [crear biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) instrucción se proporciona en SQL Server 2017, y le permite crear una biblioteca de paquete sin ejecutar código R o directamente el código Python. Sin embargo, este método requiere que preparar todos los paquetes necesarios de antemano y requiere permisos adicionales de la base de datos.

    **Se aplica a:** [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]; aplican otras restricciones

## <a name="bkmk_rInstall"></a> Instalar nuevos paquetes de R con Internet

Puede utilizar las herramientas estándar de R para instalar nuevos paquetes en una instancia de SQL Server 2016 o 2017 de SQL Server. Este proceso requiere que usted es un administrador en el equipo.

> [!IMPORTANT] 
> Asegúrese de instalar paquetes en la biblioteca predeterminada que está asociada a la instancia actual. Nunca instale paquetes en un directorio de usuario.

Este procedimiento describe cómo puede instalar paquetes con RGui; Sin embargo, puede usar RTerm o cualquier otro R herramienta línea de comandos que admite el acceso con privilegios elevados.

### <a name="install-a-package-using-rgui-or-rterm"></a>Instalar un paquete mediante RGui o RTerm

1. Navegue hasta la carpeta en el servidor donde se instalan las bibliotecas de R para la instancia.

  **Instancia predeterminada**

    2017 de SQL Server: `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

  **Instancia con nombre**

    2017 de SQL Server: `C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

  Si ha utilizado el enlace para actualizar los componentes de aprendizaje automático, podría haber cambiado la ruta de acceso. Compruebe siempre la ruta de acceso de instancia antes de instalar nuevos paquetes. 

2. Haga clic en RGui.exe y seleccione **ejecutar como administrador**.

    Si no tiene los permisos necesarios, póngase en contacto con el Administrador de base de datos y proporcionar una lista de los paquetes que necesita.

3. Desde la línea de comandos, si conoce el nombre del paquete, puede escribir: `install.packages("the_package-name")` comillas dobles son necesarias para el nombre del paquete.

4. Cuando se le pida un sitio de réplica, seleccione cualquier sitio que es conveniente para su ubicación.

5. Si el paquete de destino depende de otros paquetes, descarga las dependencias automáticamente el instalador de R y los instala automáticamente.

6. Para cada instancia que necesite usar el paquete, ejecutar la instalación por separado. Los paquetes no se pueden compartir entre instancias.

## <a name = "bkmk_offlineInstall"></a> Instalación sin conexión con herramientas de R

Para instalar paquetes de R en un servidor que no tiene acceso a internet, debe:

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

2. Abra la carpeta en el servidor donde se instalan las bibliotecas de R para la instancia. Por ejemplo, si usa el símbolo del sistema de Windows, navegue al directorio donde se encuentran RTerm.Exe o RGui.exe.

  **Instancia predeterminada**

    2017 de SQL Server: `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

  **Instancia con nombre**

    2017 de SQL Server: `C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

3. Haga doble clic en el RGui o el símbolo del sistema y seleccione **ejecutar como administrador**.

4. Ejecute el comando R `install.packages` y especifique el paquete o el nombre del repositorio y la ubicación de los archivos comprimidos.

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    Este comando extrae el paquete de R `mynewpackage` de su archivo comprimido local, siempre que haya guardado la copia en el directorio `C:\Temp\Downloaded packages`e instala el paquete en el equipo local. Si el paquete tiene dependencias, el instalador comprueba si los paquetes existentes en la biblioteca. Si ha creado un repositorio que incluye las dependencias, el programa de instalación instala también los paquetes necesarios.

    Si los paquetes necesarios no están presentes en la biblioteca de la instancia y no se encuentra en los archivos comprimidos, se produce un error en la instalación del paquete de destino.

## <a name="bkmk_createlibrary"></a> Usar una instrucción DDL para instalar un paquete 

En SQL Server 2017, puede usar el [crear biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) instrucción para agregar un paquete o un conjunto de paquetes a una instancia o una base de datos. Esta instrucción de DDL y los roles de base de datos auxiliares están diseñados para facilitar la instalación y administración de paquetes de un propietario de base de datos sin tener que utilizar herramientas de R o Python.

Este proceso requiere cierta preparación, en comparación con la instalación de paquetes usando métodos convencionales de R o Python.

+ Todos los paquetes se deben estar disponible como una variable local zip archivo, en lugar de descarga de internet.

    Si no tiene acceso al sistema de archivos en el servidor, también puede pasar un paquete completo como una variable, usando un formato binario. Para obtener más información, consulte [crear biblioteca externa](../../t-sql/statements/create-external-library-transact-sql.md).

+ La instrucción produce un error si los paquetes necesarios no están disponibles. Debe analizar las dependencias del paquete que desea instalar y asegúrese de que los paquetes se cargan en el servidor y la base de datos. Se recomienda usar **miniCRAN** o **igraph** para analizar las dependencias de paquetes.

+ Debe tener los permisos necesarios en la base de datos. Para obtener más información, consulte [crear biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql).

### <a name="prepare-the-packages-in-archive-format"></a>Preparar los paquetes en formato de archivo

1. Si va a instalar un único paquete, descargue el paquete en formato comprimido. 

2. Si el paquete requiere otros paquetes, debe comprobar que los paquetes necesarios están disponibles. Puede usar miniCRAN para analizar el paquete de destino e identificar todas sus dependencias. 

3. Copie los archivos comprimidos o en el repositorio de miniCRAN que contiene todos los paquetes en una carpeta local en el servidor.

4. Abra un **consulta** ventana, con una cuenta con privilegios administrativos.

5. Ejecute la instrucción de T-SQL `CREATE EXTERNAL LIBRARY` para cargar la recopilación del paquete comprimido en la base de datos.

    Por ejemplo, la siguiente instrucción nombres como el origen del paquete un repositorio de miniCRAN que contiene el **randomForest** paquete, junto con sus dependencias. 

    ```R
    CREATE EXTERNAL LIBRARY randomForest
    FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
    WITH (LANGUAGE = 'R');
    ```

    No se puede usar un nombre arbitrario; el nombre de biblioteca externa debe tener el mismo nombre que se espera que se utilizará al cargar o el paquete de la llamada.

6. Si la biblioteca se haya creado correctamente, puede ejecutar el paquete en SQL Server, si lo llaman dentro de un procedimiento almacenado.
    
    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    library(randomForest)'
    ```

### <a name="known-issues-with-create-external-library"></a>Problemas conocidos relacionados con crear una biblioteca externa

CREAR una biblioteca externa se admite en las siguientes condiciones:

+ Va a instalar un único paquete no tiene dependencias.
+ Va a instalar paquetes con dependencias y haber preparado todos los paquetes de antemano. 

Se produce un error en la instrucción DDL si faltan las dependencias de paquetes. Por ejemplo, se sabe que el proceso de instalación producirá un error en estos casos:

+ Ha instalado un paquete que tiene dependencias de segundo nivel y el análisis no se ampliaron a los paquetes de segundo nivel. Por ejemplo, va a instalar **gglot2**e identifica todos los paquetes que figuran en el manifiesto; sin embargo, dichos paquetes tenían otras dependencias que no se instalaron.
+ Instala un conjunto de paquetes que requieren versiones diferentes de un paquete de soporte, y el servidor tenía una versión incorrecta.

## <a name="package-installation-tips"></a>Sugerencias de instalación de paquete

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


### <a name="know-which-library-you-are-using-for-installation"></a>Saber qué biblioteca se usar para la instalación

Si previamente se ha modificado el entorno de R en el equipo, antes de instalar cualquier cosa, poner en pausa un momento y asegúrese de que la variable de entorno de R `.libPath` utiliza una sola ruta de acceso.

Esta ruta de acceso debe apuntar a la carpeta R_SERVICES para la instancia. Para obtener más información, consulte [paquetes de R instalados con SQL Server](installing-and-managing-r-packages.md).

### <a name="side-by-side-installation-with-r-server"></a>Instalación en paralelo con R Server

Si ha instalado al servidor de aprendizaje de máquina de Microsoft (independiente) además de los servicios de aprendizaje de máquina de SQL Server, el equipo debe tener instalaciones independientes de R para cada una, con los duplicados de todas las bibliotecas y herramientas de R.

Paquetes que se instalan en la biblioteca R_SERVER solo son utilizados por Microsoft R Server y no se pueden tener acceso a SQL Server. Asegúrese de utilizar el `R_SERVICES` biblioteca al instalar los paquetes que desea usar en SQL Server.

### <a name="how-to-determine-which-packages-are-already-installed"></a>¿Cómo determinar qué paquetes ya están instalados?

 Vea [paquetes de R instalados con SQL Server](installing-and-managing-r-packages.md)