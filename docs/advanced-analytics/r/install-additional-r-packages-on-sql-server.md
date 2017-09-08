---
title: "Instalación de paquetes de R adicionales en SQL Server | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 16
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: adc0e5fc229547632759c5702e98d87f4b71cbb3
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="install-additional-r-packages-on-sql-server"></a>Instalación de paquetes de R adicionales en SQL Server
En este tema se describe cómo instalar nuevos paquetes de R en una instancia de [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] en un equipo que tiene acceso a Internet.

## <a name="1-locate-the-windows-binaries-in-zip-file-format"></a>1. Busque los archivos binarios de Windows en formato de archivo ZIP

Los paquetes de R se admiten en muchas plataformas. Debe asegurarse de que el paquete que va a instalar tiene un formato binario para la plataforma Windows. De lo contrario, el paquete descargado no funcionará.

Por ejemplo, para obtener el paquete [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) desde Bioconductor:  
  
1.  En la lista de **archivos de paquetes** , busque la versión **binaria de Windows** .  
  
2.  Haga clic con el botón derecho en el vínculo del archivo ZIP y seleccione  **Guardar destino como**.  
  
3.  Vaya a la carpeta local en la que se almacenan los paquetes comprimidos y haga clic en **Guardar**.  
  
 Este proceso crea una copia local del paquete. Después, se puede instalar el paquete o copiar el paquete comprimido en un servidor que no tiene acceso a Internet.  
  
  
## <a name="2-open-the-default-r-package-library-for-sql-server-r-services"></a>2. Abra la biblioteca de paquete de R predeterminada para SQL Server R Services 

Navegue hasta la carpeta en el servidor donde se han instalado los paquetes de R asociados con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Es importante instalar los paquetes en la biblioteca predeterminada que está asociada a la instancia actual. 

Para obtener instrucciones sobre cómo localizar esta biblioteca, vea [Instalación y administración de paquetes de R](../../advanced-analytics/r-services/installing-and-managing-r-packages.md).

   Para cada instancia donde se va a ejecutar un paquete, debe instalar una copia independiente de los paquetes. Actualmente los paquetes no se pueden compartir entre instancias.
     
  
## <a name="3-open-an-administrative-command-prompt"></a>3. Abra un símbolo del sistema administrativo 

Abra R como administrador.  Puede hacerlo mediante el comando p de Windows, ropt, o mediante una de las utilidades de R.
  
### <a name="using-the-windows-command-prompt"></a>Mediante el símbolo del sistema de Windows 

1. Abra un símbolo del sistema de Windows como administrador y vaya al directorio donde se encuentran los archivos RTerm.Exe o RGui.exe.  
  
    En una instalación predeterminada, los encontrará en el directorio **\bin** . Por ejemplo, en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], las herramientas de R se encuentra aquí: 

    **Instancia predeterminada**

     `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin` 
 
     **Instancia con nombre**
   
     `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`  
  
2. Ejecute **R.exe**.  
  
### <a name="using-the-r-command-line-utilities"></a>Mediante las utilidades de la línea de comandos de R 
  
1. Utilice el Explorador de Windows para ir al directorio que contiene las herramientas de R.  
  
2. Haga clic con el botón derecho en **RGui.exe** o **RTerm.exe**, y seleccione **Ejecutar como administrador**.  
## <a name="4-install-the-package"></a>4. Instalar el paquete

El comando de R para instalar el paquete depende de si el paquete se obtiene de Internet o de un archivo comprimido local.  
  
### <a name="install-package-from-internet"></a>Instalar el paquete desde Internet  
  
1.  En general, se usa el siguiente comando para instalar un nuevo paquete desde CRAN o uno de los sitios de réplica.  
  
    ```  
    install.packages("target_package_name")  
    ```
    
    Recuerde que el nombre del paquete siempre debe encerrarse entre comillas dobles.

2.  Para especificar la biblioteca donde se debe instalar el paquete, use un comando como este para establecer la ubicación de la biblioteca:
    
    ```  
    lib.SQL <- "C:\\Program Files\\Microsoft SQL Server\\MSSQL13.MSSQLSERVER\\R_SERVICES\\library"    
    ```

    Tenga en cuenta que para [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], actualmente solo se permite un paquete de biblioteca. No instale paquetes en una biblioteca de usuario, o no podrá ejecutar el paquete desde [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].   
     
3.  Después de definir la ubicación de la biblioteca, la instrucción siguiente instala el conocido paquete e1070 en la biblioteca de paquete usada por R Services.  
  
    ```  
    install.packages("e1071", lib = lib.SQL)  
    ```  
  
4.  Se le solicitará que especifique un sitio reflejado desde el que obtener el paquete. Puede seleccionar el que más le convenga.  
  
    En [este sitio](https://cran.r-project.org/mirrors.html)encontrará una lista de los sitios reflejados de CRAN actuales.  
  
    > [!TIP]  
    >  Si prefiere no tener que seleccionar un sitio reflejado cada vez que agregue un nuevo paquete, puede configurar el entorno de desarrollo de R para que use siempre el mismo repositorio.  
    >   
    >  En tal caso, tendrá que editar el archivo de configuración global de R, .Rprofile, y agregar la siguiente línea:  
    >   
    >  `options(repos=structure(c(CRAN="<mirror site URL>")))`  
    >   
    >  Para obtener información detallada sobre las preferencias y otros archivos cargados al iniciarse el runtime de R, ejecute este comando desde una consola de R:  
    >   
    >  `?Startup`  
  
5.  Si el paquete de destino depende de otros adicionales, el instalador de R descargará e instalará automáticamente las dependencias en cuestión.  
  
### <a name="manual-package-installation-or-installing-on-computer-with-no-internet-access"></a>Instalación manual del paquete o instalación en un equipo sin acceso a Internet 

1. Si el paquete que quiere instalar tiene dependencias, obtenga los paquetes necesarios antes de tiempo y agréguelos a la carpeta con otros archivos de paquete comprimidos.

    > [!TIP]
    > 
    > Se recomienda configurar un repositorio local mediante [miniCRAN](https://mran.revolutionanalytics.com/package/miniCRAN/) si se necesita admitir la instalación sin conexión frecuente de paquetes de R.  
  
2.  En el símbolo del sistema de R, escriba el comando siguiente para especificar la ruta de acceso y el nombre del paquete que se va a instalar:  
   
    ```  
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)  
    ``` 
     
    Este comando extrae el paquete de R de su archivo comprimido local, siempre que haya guardado la copia en el directorio `C:\Temp\Downloaded packages`, e instala el paquete (con sus dependencias) en la biblioteca de R del equipo local.  
  
3.  Si previamente ha modificado el entorno de R en el equipo, debería asegurarse de que la variable de entorno de R `.libPath` usa una sola ruta de acceso que señala a la carpeta R_SERVICES para la instancia.  
  
> [!NOTE]
> Si ha instalado Microsoft R Server (independiente) además de SQL Server R Services, el equipo tendrá una instalación independiente de R con todas las bibliotecas y herramientas de R. Los paquetes que se instalan en la biblioteca R_SERVER solo los usa Microsoft R Server y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede tener acceso a ellos.  
> 
>  Asegúrese de usar la biblioteca R_SERVICES al instalar los paquetes que quiere usar en SQL Server.

  
## <a name="see-also"></a>Vea también  
 [Configurar SQL Server R Services &#40;en bases de datos&#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
  
  

