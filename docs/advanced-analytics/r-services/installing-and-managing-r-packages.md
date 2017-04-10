---
title: "Instalaci&#243;n y administraci&#243;n de paquetes de R | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 4d426cf6-a658-4d9d-bfca-4cdfc8f1567f
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# Instalaci&#243;n y administraci&#243;n de paquetes de R
 Cualquier solución de R que se ejecuta en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] debe utilizar paquetes que están instalados en la biblioteca predeterminada R. Por lo general, las soluciones de R hará referencia a bibliotecas de usuario mediante la especificación de una ruta de acceso de archivo en el código de R, pero no se recomienda para entornos de producción.

Por lo tanto, es la tarea del Administrador de base de datos o de otro administrador en el servidor para asegurarse de que todos los paquetes necesarios están instalados en el [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instancia. Si no tiene privilegios administrativos en el equipo que hospeda el [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]  instancia, puede proporcionar a la información del administrador acerca de cómo instalar paquetes de R y proporcionar acceso a un repositorio de paquetes segura donde se pueden obtener los paquetes que se soliciten los usuarios. Esta sección proporciona dicha información. 

> [!TIP]
> [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] proporciona nuevas características para instalar y administrar paquetes de R que proporcionan el Administrador de base de datos y la mayor libertad de científicos de datos y control sobre el uso de paquete y el programa de instalación. Para obtener más información, vea [administración de paquetes de R para SQL Server](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md). 

## <a name="installed-packages"></a>Paquetes instalados
Al instalar  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)],  de forma predeterminada la R **base** se instalan paquetes, como `stats` y `utils`, junto con el **RevoScaleR** paquete que admite conexiones a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 
> [!NOTE]  
>  Para obtener una lista de paquetes instalados de forma predeterminada, vea [paquetes instalados con Microsoft R Open](https://mran.microsoft.com/rro/installed/).  

 Si necesita algún paquete adicional de CRAN u otro repositorio, debe descargar el paquete e instalarlo en su estación de trabajo.  
  
 Si tiene que ejecutar el nuevo paquete en el contexto del servidor, un administrador debe instalar en el servidor.   
   
## <a name="where-and-how-to-get-new-packages"></a>Ubicación y método de obtención de los nuevos paquetes  
 Puede obtener paquetes de R de varios orígenes, aunque los más conocidos son CRAN y Bioconductor. El sitio oficial del lenguaje R ([https://www.r-project.org/](https://www.r-project.org/)) enumera muchos de estos recursos. En GitHub también se publican muchos de tales paquetes, donde puede obtener el código fuente. También podría haber recibido paquetes de R desarrollados por algún miembro de su empresa.  
  
 Con independencia de su origen, los paquetes deben proporcionarse como archivos comprimidos para poder instalarse. Además, usar el paquete con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], asegúrese de obtener el archivo comprimido en el formato binario de Windows. (Algunos paquetes podrían no admitir este formato.) Para obtener más información sobre el contenido del formato de archivo zip y cómo crear un paquete de R, se recomienda este tutorial, que puede descargar en formato PDF desde el sitio de proyecto de R: [Freidrich Leisch: creación de paquetes de R](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf). 
  
 En general, los paquetes de R pueden instalarse fácilmente desde la línea de comandos sin necesidad de descargarlos de antemano, si el equipo tiene acceso a Internet.  Por lo general esto no es el caso de servidores que ejecutan [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] .  Por lo tanto, para instalar un paquete de R en un equipo que **no** tener acceso a Internet, debe descargar el paquete en el formato comprimido correcto antes de tiempo y, a continuación, copie los archivos comprimidos en una carpeta que sea accesible para el equipo. 
 
 Los temas siguientes describen dos métodos para instalar paquetes fuera de línea: 

+ [Crear un repositorio de paquetes de sin conexión mediante miniCRAN](../../advanced-analytics/r-services/create-a-local-package-repository-using-minicran.md)

  Describe cómo usar el paquete de R **miniCRAN** para crear un repositorio fuera de línea. Esto es probablemente el método más eficaz si necesita instalar paquetes en varios servidores y administrar el repositorio desde una sola ubicación. 
+ [Instalar nuevos paquetes de R desde Internet](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)

  Se incluyen instrucciones para instalar paquetes fuera de línea copiando manualmente los archivos comprimidos.   

## <a name="permissions-required-for-installing-r-packages"></a>Permisos necesarios para instalar paquetes de R  
  
Para instalar nuevos paquetes de R en un equipo que ejecute [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], debe contar con derechos administrativos en él;   

Si carece de estos derechos, póngase en contacto con el administrador y proporcione la información sobre el paquete que desea instalar.  
  

Si va a instalar un nuevo paquete de R en un equipo que está en uso como una estación de trabajo de R y el equipo no **no** tiene una instancia de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] necesitará derechos administrativos en el equipo para instalar el paquete. Después de instalar el paquete, puede ejecutarlo en el entorno local.  
 
> [!NOTE]
> En [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], se agregaron nuevos roles de base de datos para admitir el ámbito de los permisos de instalación de paquete en un nivel de base de datos y el nivel de instancia. Para obtener más información, vea [administración de paquetes de R para SQL Server](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md).
 

### <a name="location-of-default-r-library-location-for-r-services"></a>Ubicación de la ubicación de la biblioteca predeterminada R para R Services

Si instaló  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usa la instancia predeterminada, la biblioteca de paquetes de R usada por la instancia se encuentra en la [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] carpeta de la instancia. Por ejemplo: 

+ Instancia predeterminada _MSSQLSERVER_
  `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`
+ Instancia con nombre _MyNamedInstance_
  `C:\Program Files\Microsoft SQL Server\MSSQL13.MyNamedInstance\R_SERVICES\library` 


Puede ejecutar la instrucción siguiente para comprobar que la biblioteca predeterminada de la instancia actual de R. 
~~~~
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
~~~~

Para obtener más información, vea [determinar los paquetes instalados en SQL Server](../../advanced-analytics/r-services/determine-which-packages-are-installed-on-sql-server.md).

## <a name="managing-installed-packages"></a>Administración de paquetes instalados

[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] proporciona nuevas características para instalar y administrar paquetes de R que proporcionan el Administrador de base de datos y la mayor libertad de científicos de datos y control sobre el uso de paquete y el programa de instalación. Para obtener más información, vea [administración de paquetes de R para SQL Server](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md). 

Si usas SQL Server 2106 R Services, las nuevas características de administración de paquetes no están disponibles en este momento. Mientras tanto, tiene estas opciones para determinar qué paquetes están instalados en el [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] equipo, use una de estas opciones:

+ Ver la biblioteca de forma predeterminada, si tiene permisos para la carpeta.
+ Ejecutar un comando de comando de R para enumerar los paquetes en la ubicación de la biblioteca R_SERVICES
+ Usar un procedimiento almacenado como el siguiente en la instancia:
   ```SQL
   EXECUTE sp_execute_external_script  @language=N'R'  
        ,@script = N'str(OutputDataSet);  
        packagematrix <- installed.packages();  
        NameOnly <- packagematrix[,1];  
        OutputDataSet <- as.data.frame(NameOnly);'  
        ,@input_data_1 = N'SELECT 1 as col'  
        WITH RESULT SETS ((PackageName nvarchar(250) ))   
   ```


 ## <a name="see-also"></a>Vea también  
 [Administración y supervisión de soluciones en R](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  