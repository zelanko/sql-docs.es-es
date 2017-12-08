---
title: 'Actualizado: Advanced Analytics para documentos de SQL Server | Documentos de Microsoft'
description: "Mostrar fragmentos de contenido actualizado para recientemente modificadas en documentación, Advanced Analytics para Microsoft SQL Server."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.author: genemi
ms.workload: advanced-analytics
ms.openlocfilehash: 636e243f1f39f0bfa688c6caada1e03078de9a32
ms.sourcegitcommit: 29265ad41fbe3326c21c6908ec4275a3a38f1c09
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/04/2017
---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>Nuevos y actualizados recientemente: análisis avanzados para SQL Server



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; **2017-09-28** &nbsp; - a - &nbsp; **2017-12-02**
- *Área de asunto:* &nbsp; **Advanced Analytics para SQL Server**.

<!-- Repo = 'MicrosoftDocs/sql-docs'.   Branch = 'live'. -->



&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


1. [Agregar SQLRUserGroup como un usuario de base de datos](r/add-sqlrusergroup-to-database.md)
2. [Cómo utilizar las funciones de RevoScaleR para buscar o instalar paquetes de R en SQL Server](r/use-revoscaler-to-manage-r-packages.md)
3. [Uso de R en la base de datos SQL Azure](r/using-r-in-azure-sql-database.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

En esta sección se muestran extractos de actualizaciones recopiladas de artículos que han sufrido una actualización importante recientemente.

Los extractos que se muestran aquí aparecen separados de su contexto semántico correcto. Además, en ocasiones, un extracto se separa de sintaxis de Markdown importante que lo rodea en el artículo real. Por tanto, estos extractos solo sirven de guía general. Los extractos solo le permiten saber si le interesa dedicar tiempo a hacer clic en el artículo real para visitarlo.

Por estas y otras razones, no copie código de estos fragmentos y no tome como verdad exacta ningún extracto de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta de artículos que se han actualizado recientemente

En esta lista compacta se proporcionan vínculos a todos los artículos actualizados que aparecen en la sección de extractos.

1. [Problemas conocidos en servicios de aprendizaje de máquina](#TitleNum_1)
2. [Crear un repositorio de paquete local mediante miniCRAN](#TitleNum_2)
3. [Determinar qué paquetes de R están instalados en SQL Server](#TitleNum_3)
4. [Instalar paquetes de R adicionales en SQL Server](#TitleNum_4)
5. [Instalación de características en una máquina virtual de Azure de aprendizaje de automático de SQL Server](#TitleNum_5)
6. [Instalar previamente entrenado máquina aprendizaje de los modelos en SQL Server](#TitleNum_6)
7. [Evitar errores en paquetes de R instalados en bibliotecas de usuario](#TitleNum_7)
8. [Aprovisionar una máquina virtual para el aprendizaje automático de Azure](#TitleNum_8)
9. [RevoScaleR](#TitleNum_9)
10. [Habilitar o deshabilitar la administración de paquetes de R para SQL Server](#TitleNum_10)
11. [Configurar un cliente de ciencia de datos para su uso con SQL Server](#TitleNum_11)
12. [Configurar SQL Server Machine Learning Services (en base de datos)](#TitleNum_12)
13. [Instalación desatendida de servicios de aprendizaje de máquina (In-Database)](#TitleNum_13)
14. [Paso 3: Explorar y visualizar los datos](#TitleNum_14)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-known-issues-in-machine-learning-servicesknown-issues-for-sql-server-machine-learning-servicesmd"></a>1. &nbsp;[Los problemas conocidos de los servicios de aprendizaje de máquina](known-issues-for-sql-server-machine-learning-services.md)

*Actualizado: 2017-11-16* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([siguiente](#TitleNum_2))

<!-- Source markdown line 321.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 00121c648c21576d5c86494137de1d4d81e2e265 c65973f6ae9253af5ecc621916ef36d7c0398789  (PR=3980  ,  Filename=known-issues-for-sql-server-machine-learning-services.md  ,  Dirpath=docs\advanced-analytics\  ,  MergeCommitSha40=06bb91d138a4d6395c7603a2d8f99c69a20642d3) -->



**La ejecución de código Python o problemas de paquete de Python**


Esta sección contiene los problemas conocidos que son específicos a la ejecución de Python a SQL Server, así como problemas relacionados con los paquetes de Python publicados por Microsoft, incluidos los [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) y [microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).

**Se produce un error en la llamada al modelo previamente entrenado si la ruta de acceso al modelo es demasiado largo**


Si instala los modelos previamente entrenados en una instalación predeterminada, según el nombre del equipo y el nombre de instancia, la ruta de acceso completa resultante en el archivo de modelo entrenado puede ser demasiado largo para Python leer. Esta limitación se corregirá en una versión de próximos servicios.

Hay varias soluciones posibles:

+ Al instalar los modelos previamente entrenados, elija una ubicación personalizada.
+ Si es posible, instale la instancia de SQL Server en una ruta de acceso de instalación personalizada, como C:\SQL\MSSQL14. MSSQLSERVER.
+ Utilice la utilidad Windows [Fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx) para crear un vínculo físico que el archivo de modelo se asigna a una ruta más corta.

**Error al inicializar una variable varbinary provoca un error en BxlServer**


Si ejecuta el código Python en SQL Server mediante `sp_execute_external_script`y el código tiene las variables de tipo varbinary (max), varchar (max) u otros tipos similares de salida, la variable se debe inicializar o bien establecerse como parte de la secuencia de comandos. En caso contrario, el componente de intercambio de datos, BxlServer, genera un error y deja de funcionar.

Esta limitación se corregirá en una versión de próximos servicios. Como alternativa, asegúrese de que la variable se inicializa dentro del script de Python. Puede utilizarse cualquier valor válido, como en los ejemplos siguientes:

```sql
declare @b varbinary(max);
exec sp_execute_external_script
  @language = N'Python'
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-create-a-local-package-repository-using-minicranrcreate-a-local-package-repository-using-minicranmd"></a>2. &nbsp;[Crear un repositorio de paquete local mediante miniCRAN](r/create-a-local-package-repository-using-minicran.md)

*Actualizado: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_1) | [siguiente](#TitleNum_3))

<!-- Source markdown line 43.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 44b77cb127e9ffab1777216a66f0e5be9c82f3d2 65e30f10fc36acb3ce95f60f51f3501fbc98ad08  (PR=4150  ,  Filename=create-a-local-package-repository-using-minicran.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



-   **Instalación sin conexión más sencilla e**: para instalar el paquete en un servidor sin conexión requiere que también descargar todas las dependencias del paquete, mediante miniCRAN resulta más fácil obtener todas las dependencias en el formato correcto.

-   **Mejor administración de versión**: en un entorno multiusuario, hay buenos motivos para evitar la instalación sin restricciones de varias versiones de paquete en el servidor.

Después de crear el repositorio, puede modificar mediante la adición de nuevos paquetes o actualizar la versión de los paquetes existentes.

**Paso 1. Instalar el paquete miniCRAN**


Empiece por crear un repositorio de miniCRAN para usarlo como un origen. Debe crear este repositorio en un equipo que tenga acceso a internet.

1.  Instalar el paquete de miniCRAN y requerido **igraph** paquete.

```
    if(!require("miniCRAN")) install.packages("miniCRAN") if(!require("igraph"))
    install.packages("igraph") library(miniCRAN)
```

**Paso 2. Definir un origen de paquete: un espejo CRAN, o una instantánea MRAN**


1. Especifique un sitio de réplica a usar para la obtención de paquetes.

```
    CRAN_mirror \<- c(CRAN = "https://mran.microsoft.com/snapshot/2017-08-01")
```

2.  Indique una carpeta local donde se almacenarán los paquetes recopilados. No asigne un nombre a la miniCRAN carpeta; es posible que un nombre más descriptivo como "GeneticsPackages" o "ClientRPackages1.0.2".

    Asegúrese de crear la carpeta de antemano. Se produce un error si el `local_repo` carpeta no existe cuando se ejecuta el código de R más adelante.



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-determine-which-r-packages-are-installed-on-sql-serverrdetermine-which-packages-are-installed-on-sql-servermd"></a>3. &nbsp;[Determinar qué paquetes de R están instalados en SQL Server](r/determine-which-packages-are-installed-on-sql-server.md)

*Actualizado: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_2) | [siguiente](#TitleNum_4))

<!-- Source markdown line 55.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 13d93acedc6e6b4615f1a244a2a1542910feb69e 9a065066398843a4bed318fa46d4982d712915a9  (PR=4150  ,  Filename=determine-which-packages-are-installed-on-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



+ Si se encuentra el paquete, el mensaje devuelto debe ser algo parecido a "Comandos completados correctamente."

+ Si el paquete no se encuentra o cargado, obtendrá un error similar al siguiente: "se produjo un error de script externo: Error en library("RevoScaleR"): no hay ningún paquete denominado RevoScaleR"

**Obtener una lista de paquetes instalados con R**


Hay varias maneras de obtener una lista de paquetes instalados o cargados mediante herramientas y funciones de R. Muchas herramientas de desarrollo de R proporcionan un examinador de objetos o una lista de paquetes que están instalados o cargados en el área de trabajo actual de R.

+ Desde una utilidad de R local, use una función de R base, como `installed.packages()`, que se incluye en el `utils` paquete. Para obtener una lista que es precisa para una instancia, debe especificar explícitamente la ruta de biblioteca o utilizar las herramientas de R asociadas a la biblioteca de la instancia.

+ Para comprobar si un paquete en un contexto de proceso específico, puede utilizar las siguientes funciones del paquete RevoScaleR. Estas funciones ayudan a identificar los paquetes en contextos de proceso especificado:

+ [rxFindPackage](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxfindpackage)

+ [rxInstalledPackages](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxinstalledpackages)

Por ejemplo, ejecute el siguiente código de R para obtener una lista de los paquetes disponibles en el contexto de proceso de SQL Server especificado.

```r
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
sqlPackages
```
**Vea también**




&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-install-additional-r-packages-on-sql-serverrinstall-additional-r-packages-on-sql-servermd"></a>4. &nbsp;[Instalar paquetes de R adicionales en SQL Server](r/install-additional-r-packages-on-sql-server.md)

*Actualizado: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_3) | [siguiente](#TitleNum_5))

<!-- Source markdown line 266.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ba48f1838857d90d6692aafc48f393777ac602fa 37de2586a344a99969bcd9a20723c021db2604a4  (PR=4150  ,  Filename=install-additional-r-packages-on-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



Esta sección proporciona sugerencias ordenadas y código de ejemplo relacionados con la instalación del paquete de R en SQL Server.

**<a name="packageVersion"></a>Obtener la versión de paquete correcto y formato**


Puede obtener paquetes de R de varios orígenes, aunque los más conocidos son CRAN y Bioconductor. El sitio oficial del lenguaje R (<https://www.r-project.org/>) recoge muchos de estos recursos. Número de paquetes se publica en GitHub, donde puede obtener el código fuente. Sin embargo, se podrán haber recibido paquetes de R desarrollados por algún miembro de su empresa.

Independientemente del origen, debe asegurarse de que el paquete que se va a instalar tiene un formato binario para la plataforma Windows. En caso contrario, no se puede ejecutar el paquete descargado en el entorno de SQL Server.

Antes de descargar, también debe comprobar si el paquete es compatible con la versión de R que se ejecuta en SQL Server.

**<a name="bkmk_zipPreparation"></a>Descargar el paquete como archivo comprimido**


Para la instalación en un servidor sin acceso a internet, descargue una copia del paquete en el formato de un archivo comprimido para la instalación sin conexión. Descomprima el paquete.

Por ejemplo, el siguiente procedimiento describe ahora para obtener la versión correcta de la [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) paquete desde Bioconductor, suponiendo que el equipo tiene acceso a internet.

1.  En la lista de **archivos de paquetes** , busque la versión **binaria de Windows** .

2.  Haga clic en el vínculo a la. Archivo ZIP y seleccione **Guardar destino como**.

3.  Vaya a la carpeta local donde se almacenan los paquetes comprimidos y haga clic en **guardar**.

Este proceso crea una copia local del paquete. A continuación, puede instalar el paquete, o copiar el paquete comprimido en un servidor que no tiene acceso a internet.

Para obtener más información sobre el contenido del formato de archivo zip y cómo crear un paquete de R, se recomienda este tutorial, que puede descargar en formato PDF desde el sitio de proyecto de R: [crear paquetes de R](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf).



&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-installing-sql-server-machine-learning-features-on-an-azure-virtual-machinerinstalling-sql-server-r-services-on-an-azure-virtual-machinemd"></a>5. &nbsp;[Aprendizaje de las características en una máquina virtual de Azure de máquina de instalación de SQL Server](r/installing-sql-server-r-services-on-an-azure-virtual-machine.md)

*Actualizado: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_4) | [siguiente](#TitleNum_6))

<!-- Source markdown line 55.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f4d287044b8bfda2dbe77fbf65b0d9cdd8f2ff42 2a8e33de6383f5d3af52256c5dfcb60184659eb8  (PR=4150  ,  Filename=installing-sql-server-r-services-on-an-azure-virtual-machine.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



6. Si tiene previsto conectarse a la instancia desde un cliente de ciencia de datos remotos, completar [pasos adicionales: # pasos additional) según sea necesario.

**Deshabilitar las características de aprendizaje de máquina en una VM de SQL Server**


También puede habilitar o deshabilitar la característica en una máquina virtual de SQL Server existente en cualquier momento.

1. Abra la hoja de la máquina virtual.
2. Haga clic en **Configuración** y seleccione **Configuración de SQL Server**.
3. Realizar cambios en las características y aplicar.

**<a name="existing"></a>Agregar R Services a una VM existente de SQL Server 2016 Enterprise**


Si ha creado una máquina virtual de Azure que incluye SQL Server sin aprendizaje automático, puede agregar la característica siguiendo estos pasos:

1. Vuelva a ejecutar...! CLUIR-NotShown--ssNoVersion--... /.. /includes/ssNoVersion-MD.MD)] de la instalación y agregue la característica en el **configuración del servidor** página del asistente.
2. Habilitar la ejecución de scripts externos y reiniciar el..! CLUIR-NotShown--ssNoVersion--... /.. instancia de /includes/ssNoVersion-MD.MD)]. Para obtener más información, consulte [establecer seguridad de SQL Server R Services--.. /.. / advanced-analytics/r/set-up-sql-server-r-services-in-database.md).
3. (Opcional) Configure el acceso de base de datos para cuentas de trabajo de R en caso de que sea necesario para la ejecución remota de scripts.
   Para obtener más información, consulte [establecer seguridad de SQL Server R Services--.. /.. / advanced-analytics/r/set-up-sql-server-r-services-in-database.md).
3. (Opcional) Modifique una regla de firewall en la máquina virtual de Azure si tiene intención de permitir la ejecución de scripts de R desde clientes de ciencia de datos remotos. Para obtener más información, consulte [desbloqueo firewall--#firewall).
4. Instale o habilite las bibliotecas de red necesarias. Para obtener más información, consulte [Agregar red protocolos--#network).



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-install-pretrained-machine-learning-models-on-sql-serverrinstall-pretrained-models-sql-servermd"></a>6. &nbsp;[Instalar previamente entrenada modelos de aprendizaje automático en SQL Server](r/install-pretrained-models-sql-server.md)

*Actualizado: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_5) | [siguiente](#TitleNum_7))

<!-- Source markdown line 96.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 07b51584a90568cccceea382c44155e40e09c967 db083f8536fbb2ea5886fed787872867b5de5750  (PR=4150  ,  Filename=install-pretrained-models-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



    For example, to enable use of the latest version of the pretrained models for Python, in a default instance of SQL Server 2017, you would run this statement:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    On a named instance, the command would be something like this:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MyInstanceName\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    + Para usar Python previamente entrenada modelos con el servidor de aprendizaje de máquina (independiente):

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<sql_folder>\PYTHON_SERVER\site-packages\microsoftml\mxLibs"`

    Por ejemplo, suponiendo que una instalación predeterminada del servidor de aprendizaje de máquina (independiente) utilizando el programa de instalación de SQL Server 2017, ejecute esta instrucción:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER\Lib\site-packages\microsoftml\mxLibs"`

5. Se admiten los siguientes valores para el parámetro de versión:



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-avoiding-errors-on-r-packages-installed-in-user-librariesrpackages-installed-in-user-librariesmd"></a>7. &nbsp;[Evitando los errores en paquetes de R instalados en bibliotecas de usuario](r/packages-installed-in-user-libraries.md)

*Actualizado: 2017-10-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_6) | [siguiente](#TitleNum_8))

<!-- Source markdown line 33.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 52cb9a53d7d9c31ee9bc6977464ebd2a18081ff3 3537aa6755c66f12c19bb3448dc9b5c8abb9cc28  (PR=3619  ,  Filename=packages-installed-in-user-libraries.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=aecf422ca2289b2a417147eb402921bb8530d969) -->



Sin embargo, esto nunca funcionará al ejecutar soluciones en R en SQL Server, porque los paquetes de R deben instalarse en una biblioteca de datos específica que está asociada a la instancia.

Si el paquete no está instalado en la biblioteca predeterminada, podría aparecer este error al intentar llamar al paquete:

*Error en library(xxx): no hay ningún paquete denominado 'nombre del paquete'*

También es una práctica de desarrollo incorrecta para instalar paquetes de R necesarios en una biblioteca de usuario personalizada, ya que puede provocar errores si se ejecuta una solución de otro usuario que no tiene acceso a la ubicación de la biblioteca.

**Cómo instalar paquetes de R en una biblioteca de accesible**


**Para SQL Server 2016**

Utilice la biblioteca de paquete asociada a la instancia. Para obtener más información, consulte [paquetes de R instalados con SQL Server--installing-and-managing-r-packages.md)

**Para SQL Server de 2017**

SQL Server proporciona características para ayudarle a administrar varias versiones de paquete y otorgar permisos de usuarios a los paquetes individuales, sin necesidad de que los usuarios tengan acceso al sistema de archivos.

Para obtener más información sobre cómo configurar una biblioteca compartida de paquete y asignar a usuarios a roles, vea [administración de paquetes de R para SQL Server--r-package-management-for-sql-server-r-services.md.)




&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-provision-a-virtual-machine-for-machine-learning-on-azurerprovision-the-r-server-only-sql-server-2016-enterprise-vm-on-azuremd"></a>8. &nbsp;[Aprovisionar una máquina virtual para el aprendizaje automático de Azure](r/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)

*Actualizado: 2017-10-31* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_7) | [siguiente](#TitleNum_9))

<!-- Source markdown line 132.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 16439b4a8f5f4218edfcd746ed20ccbc8263dabc 1b3a8a7d1ceceaa459b3fd5640da26859df8d80b  (PR=3748  ,  Filename=provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=262e3cf5df2448bb6b532c0549c3d72daefe5a96) -->



|Nombre| Comentarios|
|----|----|----|
| **SQL Server 2016**| ***  |
|SQL Server 2016 SP1 Enterprise en Windows|Servicios de R para análisis avanzado integrado.|
|BYOL SQL Server 2016 SP1 Enterprise en Windows Server |Servicios de R para análisis avanzado integrado. |
|Licencia gratuita: Programador SQL Server 2016 SP1 en Windows Server 2016 |Servicios de R para análisis avanzado integrado. |
| Data Science Virtual Machine - 2012 de Windows|Contiene herramientas populares de ciencia de datos, incluidos Microsoft R Server Developer Edition, SQL Server 2016 Developer edition, la distribución de Anaconda Python, edición para programadores de Julia Pro y Jupyter blocs de notas para R.|
| Data Science Virtual Machine - 2016 de Windows|Incluye SQL Server 2016 Developer Edition, con compatibilidad para el análisis de R en bases de datos.|
|**SQL Server 2017**| ***   |
|SQL Server de 2017 Enterprise Windows Server 2016| Servicios de aprendizaje de máquina con el soporte de lenguaje Python y R.|
|BYOL SQL Server 2017 Enterprise Windows Server 2016|Servicios de aprendizaje de máquina con el soporte de lenguaje Python y R.|
| Licencia de gratuito de SQL Server: Programador SQL Server 2017 en Windows Server|Servicios de aprendizaje de máquina con el soporte de lenguaje Python y R.|
| **Otro**| *** |
| Servidor solo SQL Server 2017 Enterprise de aprendizaje automático|Es similar a la imagen de SQL Server 2016 Enterprise, pero que contiene la versión independiente del servidor de aprendizaje de máquina y tiene el núcleo de ScaleR y funcionalidad de puesta en marcha optimizado para Windows entornos.|
| Aprendizaje automático de servidor para Windows|Contiene la versión independiente del servidor de aprendizaje de máquina, con características de puesta en marcha optimizados para entornos de Windows.|



&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-revoscalerrrevoscaler-overviewmd"></a>9. &nbsp;[RevoScaleR](r/revoscaler-overview.md)

*Actualizado: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_8) | [siguiente](#TitleNum_10))

<!-- Source markdown line 18.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 92f2dfa2e75037a932415881c55d2fd37fc6847a c6e9f17f2df82447b18beff41769ae3ebfbed562  (PR=4150  ,  Filename=revoscaler-overview.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->




RevoScaleR es un paquete de funciones de aprendizaje de máquina, proporcionado por Microsoft, que admite la ciencia de datos a escala.

+ Las funciones admiten la importación de datos, transformación de datos, resumen, visualización y análisis.

+ _A escala_ significa que las operaciones se pueden realizar con grandes conjuntos de datos en paralelo y distribuidas en los sistemas de archivos. Algoritmos pueden operar en conjuntos de datos que no caben en la memoria, mediante fragmentación y volver a montar los resultados cuando operaciones se completan.

+ RevoScaleR proporciona muchas mejoras con respecto a las funciones de R de código abierto. Hay funciones de RevoScaleR correspondiente a muchas de las funciones de R de base más populares. Funciones de RevoScaleR se denotan con un **rx** o **Rx** prefijo para que sean fáciles de identificar.

+ RevoScaleR actúa como una plataforma para la ciencia de datos distribuidos. Por ejemplo, puede utilizar las transformaciones y los contextos de proceso de RevoScaleR con los algoritmos de última generación en [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package). También puede usar [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) para ejecutar funciones de R base en paralelo.

Para obtener ejemplos de RevoScaleR en acción, vea estos blogs:

+ [Compilar e implementar un modelo de predicción mediante R y SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [Predicciones de un millón por segundo con el servidor de aprendizaje de máquina](https://blogs.msdn.microsoft.com/mlserver/2017/10/15/1-million-predictionssec-with-machine-learning-server-web-service/)

+ [Predecir taxi las sugerencias MicrosoftML](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/01/17/predicting-nyc-taxi-tips-using-microsoftml/)

+ [Optimización del rendimiento con rxExec](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/11/14/performance-optimization-when-using-rxexec-to-parallelize-algorithms/)

**Cómo obtener RevoScaleR**




&nbsp;

&nbsp;

---

<a name="TitleNum_10"/>

### <a name="10-nbsp-enable-or-disable-r-package-management-for-sql-serverrr-package-how-to-enable-or-disablemd"></a>10. &nbsp;[Habilitar o deshabilitar la administración de paquetes de R para SQL Server](r/r-package-how-to-enable-or-disable.md)

*Actualizado: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_9) | [siguiente](#TitleNum_11))

<!-- Source markdown line 60.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5f846cd7d601459a95e694ada41e9fc5285f3de9 83a4a84adf47670c7fd4599f889f27ec3c219708  (PR=4150  ,  Filename=r-package-how-to-enable-or-disable.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



    If you do not specify a user, the current security context is used.

3. Repita el comando para cada base de datos donde deben instalarse los paquetes.

4.  Para comprobar que se han creado correctamente los nuevos roles, en SQL Server Management Studio, haga clic en la base de datos, expanda **seguridad**y expanda **Roles de base de datos**.

    También puede ejecutar una consulta en sys.database_principals como el siguiente:

```sql
    SELECT pr.principal_id, pr.name, pr.type_desc,
        pr.authentication_type_desc, pe.state_desc,
        pe.permission_name, s.name + '.' + o.name AS ObjectName
    FROM sys.database_principals AS pr
    JOIN sys.database_permissions AS pe
        ON pe.grantee_principal_id = pr.principal_id
    JOIN sys.objects AS o
        ON pe.major_id = o.object_id
    JOIN sys.schemas AS s
        ON o.schema_id = s.schema_id;
```

4.  Después de que se ha habilitado la característica, cualquier usuario con los permisos adecuados puede utilizar el [crear biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) instrucción T-SQL para agregar paquetes. Para obtener un ejemplo de cómo funciona esto, consulte [instalar paquetes adicionales en SQL Server](r/install-additional-r-packages-on-sql-server.md).

**<a name="bkmk_disable"></a>Deshabilitar la administración de paquetes**




&nbsp;

&nbsp;

---

<a name="TitleNum_11"/>

### <a name="11-nbsp-set-up-a-data-science-client-for-use-with-sql-serverrset-up-a-data-science-clientmd"></a>11. &nbsp;[Configurar un cliente de ciencia de datos para su uso con SQL Server](r/set-up-a-data-science-client.md)

*Actualizado: 2017-11-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_10) | [siguiente](#TitleNum_12))

<!-- Source markdown line 52.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f674f5d329211e4c7d8dc464bd70f1cdef633350 8c65fc96c04f32d1e4777870774a11f9fd2ee219  (PR=3765  ,  Filename=set-up-a-data-science-client.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=dc67a9c744441f9d556e98fb9a4daf4414060360) -->



    For setup information, see [How to install R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation).

    To configure RTVS to use your Microsoft R client libraries, see [About Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

+ Visual Studio de 2017

    Incluso la edición gratuita Community incluye la carga de trabajo de ciencia de datos, que instala las plantillas de proyecto para R, Python y F #.

    Descargar Visual Studio desde [este sitio](https://www.visualstudio.com/vs/).

+ RStudio

    Si prefiere usar RStudio, se necesitan algunos pasos más para usar las bibliotecas de RevoScaleR:

    - Instalar el cliente de R de Microsoft para obtener los paquetes necesarios y las bibliotecas.
    - Actualizar la ruta de acceso de R para usar el runtime de R de Microsoft.

    Para obtener más información, consulte [cliente R - configurar el IDE](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client#step-2-configure-your-ide).

**Configurar el IDE**


+ Herramientas de R para Visual Studio

    Vea [este sitio](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r) algunos ejemplos de cómo compilar y depurar R proyectos con herramientas de R para Visual Studio.

+ Visual Studio de 2017

    Si instala el cliente de Microsoft R o R Server **antes de** instalar Visual Studio, las bibliotecas de R Server automáticamente se detectan y se utiliza para la ruta de biblioteca. Si no ha instalado las bibliotecas de RevoScaleR desde el **herramientas de R** menú, seleccione **instalar el cliente de R**.

**Ejecutar R en SQL Server**


Este ejemplo utiliza Visual Studio 2017 Community Edition, con la carga de trabajo de ciencia de datos instalado.

1. Desde el **archivo** menú, seleccione **New** y, a continuación, seleccione **proyecto**.

2. -Mano panel contiene una lista de plantillas preinstaladas. Haga clic en **R**y seleccione **proyecto R**. En el **nombre** , escriba `dbtest` y haga clic en **Aceptar**.



&nbsp;

&nbsp;

---

<a name="TitleNum_12"/>

### <a name="12-nbsp-set-up-sql-server-machine-learning-services-in-databaserset-up-sql-server-r-services-in-databasemd"></a>12. &nbsp;[Configurar servicios de aprendizaje de máquina de SQL Server (In-Database)](r/set-up-sql-server-r-services-in-database.md)

*Actualizado: 2017-11-16* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_11) | [siguiente](#TitleNum_13))

<!-- Source markdown line 111.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 4d355f6494b417dd90dce3943e7176eaece7336e 20bddb8ffd4cf3774b812a7376c70b95ccc57e92  (PR=3980  ,  Filename=set-up-sql-server-r-services-in-database.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=06bb91d138a4d6395c7603a2d8f99c69a20642d3) -->



   + Servicios de Motor de base de datos
   + R Services (en bases de datos)

7. Cuando una vez completada la instalación, reinicie el equipo.


**<a name="bkmk2017top"></a>Instalar servicios de aprendizaje automático SQL Server de 2017 (en bases de datos)**


> [!div class="checklist"]
> * Instalar el motor de base de datos y características de aprendizaje automático
> * Requiere los pasos posteriores a la instalación: habilitar el aprendizaje automático y reiniciar
> * Pasos posteriores a la instalación opcionales: agregar reglas de firewall, agregar usuarios, cambiar o configurar las cuentas de servicio, configurar un cliente de ciencia de datos remotos.

**Introducción**

1. Ejecutar...! CLUIR-NotShown--ssNoVersion--... /.. programa de instalación de /includes/ssNoVersion-MD.MD)].

2. En el **instalación** ficha, seleccione **instalación independiente del nuevo servidor SQL Server o agregar características a una instalación existente**.

     ! [Instalar servicios de aprendizaje de máquina (In-Database)--media/2017setup-installation-page-mlsvcs.png "Iniciar la instalación del motor de base de datos con servicios de aprendizaje de máquina")

3. En el **selección de características** página, seleccione las opciones siguientes:

    + Seleccione **servicios del motor de base de datos**. Se requiere el motor de base de datos en cada instancia que usa el aprendizaje automático.

    + Seleccione **(en bases de datos) de servicios de aprendizaje automático**. Esta opción instala la compatibilidad para su uso en bases de datos de R. Después de seleccionar esta opción, puede seleccionar el idioma de aprendizaje automático. Puede seleccionar solo R, o puede agregar R y Python.

    ! [Características de servicios de aprendizaje de máquina selection--media/2017setup-features-page-mls-rpy.png "Seleccione estas características para R Services en bases de datos")

    Si no selecciona la R o Python la opción de idioma, el Asistente para instalación instala sólo el marco de extensibilidad, que incluye el Launchpad de confianza de SQL Server y no instala los componentes específicos del idioma.  Por lo general se recomienda que instale al menos un idioma que se inicie con. Sin embargo, puede usar esta opción si piensa utilizar inmediatamente el proceso de enlace para actualizar los componentes de aprendizaje automático. Para obtener más información, consulte [SqlBindR de uso para actualizar una instancia de R Services--use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).



&nbsp;

&nbsp;

---

<a name="TitleNum_13"/>

### <a name="13-nbsp-unattended-installation-of-machine-learning-services-in-databaserunattended-installs-of-sql-server-r-servicesmd"></a>13. &nbsp;[Instalación desatendida de servicios de aprendizaje de máquina (In-Database)](r/unattended-installs-of-sql-server-r-services.md)

*Actualizado: 2017-11-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_12) | [siguiente](#TitleNum_14))

<!-- Source markdown line 75.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ad203c90adff3f515b5f16472fad9753be7a421d 6925a9276bcd4a80babc7504de50400f1a5a2940  (PR=3765  ,  Filename=unattended-installs-of-sql-server-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=dc67a9c744441f9d556e98fb9a4daf4414060360) -->



El ejemplo siguiente muestra los argumentos necesarios para realizar un silenciosa, desatendida la instalación de servicios de máquinas de 2017 (In-Database) de SQL Server con el lenguaje de Python agregado.

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTPYTHONOPENLICENSETERMS
```

Tenga en cuenta las marcas necesarias para Python en SQL Server 2017:

+ `ADVANCEDANALYTICS`
+ `SQL_INST_MPY`
+ `IACCEPTPYTHONOPENLICENSETERMS`

**Instalar R y Python en una instancia con nombre**


El ejemplo siguiente muestra los argumentos necesarios para realizar un silenciosa, desatendida la instalación de servicios de máquinas de 2017 (In-Database) de SQL Server en una instancia con nombre. Se agregan los lenguajes R y Python.

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MR, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER.ServerName /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONOPENLICENSETERMS
```

**<a name="OldInstall"></a>Instalación de línea de comandos para SQL Server 2016**


El ejemplo siguiente muestra los argumentos necesarios para realizar un silenciosa, desatendida la instalación de SQL Server 2016 con el lenguaje R agregado.



&nbsp;

&nbsp;

---

<a name="TitleNum_14"/>

### <a name="14-nbsp-step-3-explore-and-visualize-the-datatutorialssqldev-py3-explore-and-visualize-the-datamd"></a>14. &nbsp;[Paso 3: explorar y visualizar los datos](tutorials/sqldev-py3-explore-and-visualize-the-data.md)

*Actualizado: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_13))

<!-- Source markdown line 66.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 47edcfbd8da7cf1ea1ad03a05f86d3cd26014827 674a7c7d0e8290fc91970ed2aeda3b97d5165d75  (PR=4150  ,  Filename=sqldev-py3-explore-and-visualize-the-data.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



    Class 4: `tip_amount` > $20

**Crear gráficos con Python en T-SQL**


Desarrollar una solución de ciencia de datos incluye normalmente la exploración de datos intensivos y la visualización de datos. Dado que visualización es una herramienta eficaz para comprender la distribución de los datos y los valores atípicos, Python proporciona varios paquetes para la visualización de datos. El **matplotlib** módulo es una de las bibliotecas más populares para la visualización e incluye muchas funciones para crear histogramas, los gráficos de dispersión, cuadro gráficos y otros gráficos de exploración de datos.

En esta sección, aprenderá a trabajar con gráficos de uso de procedimientos almacenados. En su lugar de abrir la imagen en el servidor, almacena el objeto de Python `plot` como **varbinary** datos y después escribir que en un archivo que puede compartir o visualizarse en otro lugar.

**Crear un gráfico como datos varbinary**


El **revoscalepy** módulo incluido con SQL Server de 2017 Machine Learning Services admite características parecidas a las de la **RevoScaleR** paquete de R.  Este ejemplo utiliza el equivalente de Python de `rxHistogram` para trazar un histograma en función de los datos de un..! CLUIR-NotShown--tsql--... /.. consulta de /includes/TSQL-MD.MD)].

El procedimiento almacenado devuelve un número de serie de Python `figure` objeto como un flujo de **varbinary** datos. No se puede ver los datos binarios directamente, pero puede utilizar código de Python en el cliente para deserializar y ver las cifras y, a continuación, guarde el archivo de imagen en un equipo cliente.

1. Crear el procedimiento almacenado _SerializePlots_, si la secuencia de comandos de PowerShell ya no lo hizo.

    - La variable `@query` define el texto de consulta `SELECT tipped FROM nyctaxi_sample`, que se pasa al bloque de código Python como argumento para la variable de entrada de secuencia de comandos, `@input_data_1`.
    - El script de Python es bastante sencillo: **matplotlib** `figure` objetos se usan para hacer el gráfico de dispersión y de histograma, y estos objetos, a continuación, se serializan con la `pickle` biblioteca.







## <a name="similar-articles"></a>Artículos similares

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

En esta sección se enumeran artículos muy similares a los artículos actualizados recientemente en otras áreas temáticas, dentro de nuestro repositorio público de GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas temáticas con artículos nuevos o actualizados recientemente

- [Nuevos y actualizados (3 + 14): **Advanced Analytics para SQL** documentos](../advanced-analytics/new-updated-advanced-analytics.md)
- [Nuevos + Actualizados (1+0): documentos de **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Nuevos y actualizados (87 + 0): **Analytics Platform System para SQL** documentos](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Nuevos y actualizados (4 de 5 +): **conectar con SQL Server** documentos](../connect/new-updated-connect.md)
- [Nuevos y actualizados (0 + 1): **motor de base de datos de SQL** documentos](../database-engine/new-updated-database-engine.md)
- [Nuevos y actualizados (2 + 2): **Integration Services para SQL** documentos](../integration-services/new-updated-integration-services.md)
- [Nuevos y actualizados (10 + 9): **Linux para SQL** documentos](../linux/new-updated-linux.md)
- [Nuevos y actualizados (2 + 4): **bases de datos relacionales de SQL** documentos](../relational-databases/new-updated-relational-databases.md)
- [Nuevos y actualizados (4 + 2): **Reporting Services para SQL** documentos](../reporting-services/new-updated-reporting-services.md)
- [Nuevos y actualizados (0 + 1): **ejemplos para SQL** documentos](../sample/new-updated-sample.md)
- [Nuevos y actualizados (21 + 0): **Studio de operaciones SQL** documentos](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Nuevos y actualizados (5 + 1): **Microsoft SQL Server** documentos](../sql-server/new-updated-sql-server.md)
- [Nuevos + Actualizados (0+1): documentos de **SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Nuevos y actualizados (1 + 0): **SQL Server Migration Assistant (SSMA)** documentos](../ssma/new-updated-ssma.md)
- [Nuevos + Actualizados (0+1): documentos de **SQL Server Management Studio (SSMS)**](../ssms/new-updated-ssms.md)
- [Nuevos y actualizados (0 + 2): **Transact-SQL** documentos](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas temáticas sin artículos nuevos ni actualizados recientemente

- [Nuevos y actualizados (0 + 0): **datos migración Ayudante (DMA) para SQL** documentos](../dma/new-updated-dma.md)
- [Nuevos + Actualizados (0+0): documentos de **Objetos de datos ActiveX (ADO) para SQL**](../ado/new-updated-ado.md)
- [Nuevos + Actualizados (0+0): documentos de **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Extensiones de minería de datos (DMX) para SQL**](../dmx/new-updated-dmx.md)
- [Nuevos + actualizados (0+0): documentos de **Master Data Services (MDS) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Expresiones multidimensionales (MDX) para SQL**](../mdx/new-updated-mdx.md)
- [Nuevos + Actualizados (0+0): documentos de **ODBC (conectividad abierta de bases de datos) para SQL**](../odbc/new-updated-odbc.md)
- [Nuevos + Actualizados (0+0): documentos de **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Nuevos + actualizados (0+0): documentos de **Herramientas para SQL**](../tools/new-updated-tools.md)
- [Nuevos + Actualizados (0+0): documentos de **XQuery para SQL**](../xquery/new-updated-xquery.md)


