---
title: "Instalaci&#243;n de paquetes de R adicionales en SQL Server | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 16
---
# Instalaci&#243;n de paquetes de R adicionales en SQL Server
Este tema describe cómo instalar nuevos paquetes de R a una instancia de [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] en un equipo que tiene acceso a Internet.

## <a name="1-locate-the-windows-binaries-in-zip-file-format"></a>1. Busque los archivos binarios de Windows en formato de archivo ZIP

Paquetes de R se admiten en varias plataformas. Debe asegurarse de que el paquete que se va a instalar tiene un formato binario para la plataforma Windows. En caso contrario, el paquete descargado no funcionará.

Por ejemplo, para obtener el paquete [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) desde Bioconductor:  
  
1.  En la lista de **archivos de paquetes** , busque la versión **binaria de Windows** .  
  
2.  Haga clic con el botón derecho en el vínculo del archivo ZIP y seleccione  **Guardar destino como**.  
  
3.  Vaya a la carpeta local en la que se almacenan los paquetes comprimidos y haga clic en **Guardar**.  
  
 Este proceso crea una copia local del paquete. A continuación, puede instalar el paquete, o copiar el paquete comprimido en un servidor que no tiene acceso a Internet.  
  
  
## <a name="2-open-the-default-r-package-library-for-sql-server-r-services"></a>2. Abra la biblioteca de paquete predeterminado R para SQL Server R Services 

Navegue hasta la carpeta en el servidor de los paquetes de R asociados con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] se han instalado. Es importante instalar paquetes en la biblioteca predeterminada que está asociada a la instancia actual. 

Para obtener instrucciones sobre cómo localizar esta biblioteca, consulte [instalar y administrar paquetes de R](../../advanced-analytics/r-services/installing-and-managing-r-packages.md).

   Para cada instancia donde se ejecutará un paquete, debe instalar una copia independiente de los paquetes. Actualmente los paquetes no se pueden compartir entre instancias.
     
  
## <a name="3-open-an-administrative-command-prompt"></a>3. Abra un símbolo del sistema administrativo 

Abra R como administrador.  Puede hacerlo mediante el comando de Windows p, ropt, o mediante una de las utilidades de R.
  
### <a name="using-the-windows-command-prompt"></a>Mediante el símbolo del sistema de Windows 

1. Abra un símbolo del sistema de Windows como administrador y navegue al directorio donde se encuentran los archivos RTerm.Exe o RGui.exe.  
  
    En una instalación predeterminada, los encontrará en el directorio **\bin** . Por ejemplo, en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], las herramientas de R se encuentran aquí: 

    **Instancia predeterminada**

     `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin` 
 
     **Instancia con nombre**
   
     `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`  
  
2. Ejecute **R.exe**.  
  
### <a name="using-the-r-commandline-utilities"></a>Mediante las utilidades de la línea de comandos de R 
  
1. Utilice el Explorador de Windows para ir al directorio que contiene las herramientas de R.  
  
2. Haga clic en **RGui.exe** o **RTerm.exe**, y seleccione **Ejecutar como administrador**.  
## <a name="4-install-the-package"></a>4. Instalar el paquete

El comando de R para instalar el paquete depende de si se obtiene el paquete desde Internet o desde un archivo comprimido local.  
  
### <a name="install-package-from-internet"></a>Instalar el paquete de Internet  
  
1.  En general, utilice el siguiente comando para instalar nuevos paquetes de CRAN o uno de los sitios de reflejo.  
  
    ```  
    install.packages("target_package_name")  
    ```
    
    Recuerde que el nombre del paquete siempre debe encerrarse entre comillas dobles.

2.  Para especificar la biblioteca que debe estar instalado el paquete, use un comando como este para establecer la ubicación de la biblioteca:
    
    ```  
    lib.SQL <- "C:\\Program Files\\Microsoft SQL Server\\MSSQL13.MSSQLSERVER\\R_SERVICES\\library"    
    ```

    Tenga en cuenta que para [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], actualmente se permite la biblioteca de un único paquete. No instale paquetes a una biblioteca de usuario, o no podrá ejecutar el paquete de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].   
     
3.  Definir la ubicación de la biblioteca, la instrucción siguiente instala el paquete de e1070 populares en la biblioteca de paquete que se usa en R Services.  
  
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
  
### <a name="manual-package-installation-or-installing-on-computer-with-no-internet-access"></a>Instalación manual del paquete o instalar en el equipo sin acceso a Internet 

1. Si el paquete que se va a instalar tiene dependencias, obtener los paquetes necesarios antes de tiempo y agréguelos a la carpeta con otro paquete de archivos comprimido.

    > [!TIP]
    > 
    > Se recomienda que configure un repositorio local utilizando [miniCRAN](https://mran.revolutionanalytics.com/package/miniCRAN/) Si necesita admitir frecuente instalación sin conexión de paquetes de R.  
  
2.  En el símbolo del sistema de R, escriba el comando siguiente para especificar la ruta de acceso y el nombre del paquete que se va a instalar:  
   
    ```  
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)  
    ``` 
     
    Este comando extrae el paquete de R de su archivo comprimido local, siempre que haya guardado la copia en el directorio `C:\Temp\Downloaded packages`, e instala el paquete (con sus dependencias) en la biblioteca de R en el equipo local.  
  
3.  Si previamente se ha modificado el entorno de R en el equipo, debe asegurarse de que la variable de entorno de R `.libPath` usa solo una ruta de acceso que señala a la carpeta R_SERVICES para la instancia.  
  
> [!NOTE]
> Si ha instalado a Microsoft R Server (independiente) además de SQL Server R Services, el equipo tendrá una instalación independiente de R con todas las bibliotecas y herramientas de R. Paquetes que se instalan en la biblioteca R_SERVER solo son utilizados por Microsoft R Server y no se puede tener acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
> 
>  Asegúrese de usar la biblioteca R_SERVICES al instalar los paquetes que desea usar en SQL Server.

  
## <a name="see-also"></a>Vea también  
 [Configuración de SQL Server R Services &#40; en bases de datos &#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
  
  