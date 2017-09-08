---
title: Instalar y administrar paquetes de R | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 4d426cf6-a658-4d9d-bfca-4cdfc8f1567f
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ae30bfc42e42b69158dbba5a38b0bccbe93523b4
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="installing-and-managing-r-packages"></a>Instalar y administrar paquetes de R
 Cualquier solución de R que se ejecuta en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] debe usar los paquetes que hay instalados en la biblioteca de R predeterminada. Por lo general, las soluciones de R harán referencia a las bibliotecas de usuario especificando una ruta de acceso en el código de R, aunque esto no es recomendable en entornos de producción.

Por lo tanto, es tarea del administrador de la base de datos (o de cualquier otro administrador en el servidor) asegurarse de que todos los paquetes necesarios están instalados en la instancia de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Si no tiene privilegios administrativos en el equipo donde se hospeda la instancia de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], puede informar al administrador de cómo instalar paquetes de R y proporcionar acceso a un repositorio seguro de paquetes donde obtener los paquetes solicitados por los usuarios. En esta sección se proporciona ese tipo de información. 

> [!TIP]
> [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] proporciona nuevas características para instalar y administrar paquetes de R con las que tanto el administrador de base de datos como el científico de datos disfrutarán de una mayor libertad y un mayor control a la hora de instalar y usar los paquetes. Para más información, vea [Administración de paquetes de R para SQL Server](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md). 

## <a name="installed-packages"></a>Paquetes instalados
Al instalar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], se instalan de forma predeterminada los paquetes **básicos** de R, como `stats` y `utils`, junto con el paquete **RevoScaleR**, que permite establecer conexiones con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 
> [!NOTE]  
>  Para obtener una lista de los paquetes que se instalan de forma predeterminada, vea [Paquetes instalados con Microsoft R Open](https://mran.microsoft.com/rro/installed/).  

 Si necesita algún paquete más de CRAN o de cualquier otro repositorio, tendrá que descargarlo e instalarlo en su estación de trabajo.  
  
 Si necesita ejecutar el nuevo paquete en el contexto del servidor, un administrador deberá instalarlo también en el servidor.   
   
## <a name="where-and-how-to-get-new-packages"></a>Ubicación y método de obtención de los nuevos paquetes  
 Puede obtener paquetes de R de varios orígenes, aunque los más conocidos son CRAN y Bioconductor. El sitio oficial del lenguaje R ([https://www.r-project.org/](https://www.r-project.org/)) recoge muchos de estos recursos. En GitHub también se publican muchos de tales paquetes, donde puede obtener el código fuente. También podría haber recibido paquetes de R desarrollados por algún miembro de su empresa.  
  
 Con independencia de su origen, los paquetes deben proporcionarse como archivos comprimidos para poder instalarse. Además, para usar el paquete con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], asegúrese de obtener el archivo comprimido en formato binario de Windows. (Puede que algunos de los paquetes no admitan este formato). Para más información sobre el contenido del formato de archivo ZIP y cómo crear un paquete de R, recomendamos este tutorial, que puede descargar en formato PDF del sitio del proyecto de R: [Freidrich Leisch: Creating R Packages](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf) (Freidrich Leisch: creación de paquetes de R). 
  
 En general, los paquetes de R pueden instalarse fácilmente desde la línea de comandos sin necesidad de descargarlos de antemano, siempre que el equipo tenga acceso a Internet.  Este no suele ser el caso de los servidores que ejecutan [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].  Por lo tanto, para instalar un paquete de R en un equipo que **no** disponga de acceso a Internet, debe descargar con antelación el paquete correspondiente en un formato comprimido y, tras ello, copiar los archivos comprimidos en una carpeta a la que el equipo tenga acceso. 
 
 En los siguientes temas se explican dos métodos para instalar paquetes sin conexión: 

+ [Create an Offline Package Repository using miniCRAN](../../advanced-analytics/r-services/create-a-local-package-repository-using-minicran.md) (Crear un repositorio de paquetes sin conexión con miniCRAN)

  Aquí se explica cómo usar el paquete de R **miniCRAN** para crear un repositorio sin conexión. Probablemente sea el método más eficaz si necesita instalar paquetes en varios servidores y administrar el repositorio desde una sola ubicación. 
+ [Install New R Packages from the Internet](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md) (Instalar nuevos paquetes de R desde Internet)

  Incluye instrucciones para instalar paquetes sin conexión copiando manualmente los archivos comprimidos.   

## <a name="permissions-required-for-installing-r-packages"></a>Permisos necesarios para instalar paquetes de R  
  
Para instalar un nuevo paquete de R en un equipo donde se ejecuta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], debe tener derechos administrativos en dicho equipo.   

Si carece de estos derechos, póngase en contacto con el administrador y proporcione la información sobre el paquete que desea instalar.  
  

Si quiere instalar un nuevo paquete de R en un equipo que se usa como estación de trabajo de R y dicho equipo **no** dispone de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], también necesitará derechos administrativos en él. Después de instalar el paquete, puede ejecutarlo en el entorno local.  
 
> [!NOTE]
> En [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], se han incorporado nuevos roles de base de datos para dar cabida a los permisos de instalación de paquetes en el nivel de base de datos y en el nivel de instancia. Para más información, vea [Administración de paquetes de R para SQL Server](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md).
 

### <a name="location-of-default-r-library-location-for-r-services"></a>Localización de la ubicación de la biblioteca de R predeterminada para R Services

Si ha instalado [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usando la instancia predeterminada, la biblioteca de paquetes de R que la instancia ha usado estará en la carpeta de instancia [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Por ejemplo: 

+ Instancia predeterminada _MSSQLSERVER_
  `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`
+ Instancia con nombre _MyNamedInstance_
  `C:\Program Files\Microsoft SQL Server\MSSQL13.MyNamedInstance\R_SERVICES\library` 


Puede ejecutar la siguiente instrucción para comprobar la biblioteca predeterminada de la instancia actual de R. 
~~~~
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
~~~~

Para más información, vea [Determinación de los paquetes instalados en SQL Server](../../advanced-analytics/r-services/determine-which-packages-are-installed-on-sql-server.md).

## <a name="managing-installed-packages"></a>Administrar paquetes instalados

[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] proporciona nuevas características para instalar y administrar paquetes de R con las que tanto el administrador de base de datos como el científico de datos disfrutarán de una mayor libertad y un mayor control a la hora de instalar y usar los paquetes. Para más información, vea [Administración de paquetes de R para SQL Server](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md). 

Si usa SQL Server 2106 R Services, las nuevas características de administración de paquetes no están disponibles en este momento. Mientras tanto, puede recurrir a cualquiera de los siguientes métodos para saber qué paquetes están instalados en el equipo con [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]:

+ Ver la biblioteca predeterminada, si tiene permisos en la carpeta en cuestión.
+ Ejecutar un comando de R para obtener una lista de los paquetes en la ubicación de la biblioteca R_SERVICES
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

