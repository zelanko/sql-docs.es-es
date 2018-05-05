---
title: Requisitos del sistema, instalación y archivos de controlador | Documentos de Microsoft
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d90fa182-1dab-4d6f-bd85-a04dd1479986
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10e4d020bac05317e76dabea46495d58def71cf0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="system-requirements-installation-and-driver-files"></a>Requisitos del sistema, instalación y archivos del controlador
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] admite conexiones a SQL Server 2014, SQL Server 2012 R2, [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro_md.md)], [!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)]y [!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)].  
  
ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en Windows puede instalarse en un equipo que también tenga una o varias versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client.  
  
ODBC Driver 13 y 13.1 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], además de las anteriores, es compatible con SQL Server 2016. 

El 17 del controlador ODBC para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] admite todas las anteriores y también 2017 de SQL Server.
  
El nombre del controlador que se especifica en una cadena de conexión es `ODBC Driver 11 for SQL Server` o `ODBC Driver 13 for SQL Server` (para 13 y 13.1) o `ODBC Driver 17 for SQL Server`.
  
## <a name="supported-operating-systems"></a>Sistemas operativos admitidos

Puede ejecutar aplicaciones con el controlador en los siguientes sistemas operativos de Windows:  

-   Windows Server 2008 R2 
-   Windows Server 2012
-   Windows Server 2012 R2    
-   Windows Vista SP2 *(solo en ODBC Driver 11)*  
-   Windows 7  
-   Windows 8
-   Windows 8.1
-   Windows 10
  
## <a name="installing-microsoft-odbc-driver-for-sql-server"></a>Instalar el controlador ODBC de Microsoft para SQL Server

El controlador se instala al ejecutar `msodbcsql.msi` desde uno de los siguientes vínculos:

- [Descargar Microsoft ODBC Driver 17 para SQL Server en Windows](https://www.microsoft.com/download/details.aspx?id=56567)
- [Descargar Microsoft ODBC Driver 13.1 for SQL Server en Windows](https://www.microsoft.com/download/details.aspx?id=53339)
- [Descargar Microsoft ODBC Driver 13 for SQL Server en Windows](https://www.microsoft.com/download/details.aspx?id=50420)
- [Descargar Microsoft ODBC Driver 11 for SQL Server en Windows](https://www.microsoft.com/download/details.aspx?id=36434). 

Se puede instalar en paralelo con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client.  

Cuando se invoca `msodbcsql.msi`, solo los componentes de cliente se instalan de forma predeterminada. Los componentes de cliente son archivos que permiten ejecutar aplicaciones desarrolladas mediante el controlador. Para instalar los componentes del SDK, especifique `ADDLOCAL=ALL` en la línea de comandos. Por ejemplo:  
  
```  
msiexec /i msodbcsql.msi ADDLOCAL=ALL  
```  
  
 Especifique `IACCEPTMSODBCSQLLICENSETERMS=YES` para aceptar los términos de licencia de usuario final si usa el `/passive`, `/qn`, `/qb`, o `/qr` opción para instalar. Esta opción se debe especificar con todas las letras mayúsculas. Por ejemplo:  
  
```  
msiexec /quiet /passive /qn /i msodbcsql.msi IACCEPTMSODBCSQLLICENSETERMS=YES ADDLOCAL=ALL  
```  
  
 Para realizar una desinstalación silenciosa, haga lo siguiente:  
  
```  
msiexec /quiet /passive /qn /uninstall msodbcsql.msi  
```  
  
Cuando una aplicación utiliza el controlador, la aplicación debe indicar que depende del controlador mediante la opción de instalación `APPGUID`. Si lo hace, el instalador del controlador para las aplicaciones dependientes de informes antes de desinstalar. Para especificar una dependencia en el controlador, establezca la `APPGUID` parámetro de línea de comandos para el código de producto cuando se instale en modo silencioso el controlador. (se debe crear un código de producto al usar Microsoft Installer para empaquetar el programa de instalación de la aplicación). Por ejemplo:  
  
```  
msiexec /i msodbcsql.msi APPGUID={ <Your dependent application's APPGUID> }  
```  

## <a name="command-line-tools-sqlcmdexe-and-bcpexe"></a>Herramientas de línea de comandos: sqlcmd.exe y bcp.exe

El `bcp.exe` y `sqlcmd.exe` de las herramientas para usarlo con el controlador se puede descargar en [11 de utilidades de línea de comandos de Microsoft para SQL Server](http://www.microsoft.com/download/details.aspx?id=36433), [13 de utilidades de línea de comandos de Microsoft para SQL Server](https://www.microsoft.com/download/details.aspx?id=52680), o [13.1 de utilidades de línea de comandos de Microsoft para SQL Server](https://www.microsoft.com/download/details.aspx?id=53591). El controlador es un requisito previo para instalar `sqlcmd.exe` y `bcp.exe`.
  
`bcp.exe` y `sqlcmd.exe` se instalan en el `110\Tools` subcarpeta de `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC` para la versión 11, y `130\Tools` para 13.1 y 13.

Una aplicación que utiliza funciones BCP debe especificar el controlador de la misma versión que se incluye con el archivo de encabezado y biblioteca usada para compilar la aplicación.  

Por ejemplo, cuando se compila una aplicación ODBC con `msodbcsql11.lib` y `msodbcsql.h`, use "DRIVER = {ODBC Driver 11 for SQL Server}" en la cadena de conexión.

## <a name="components-of-the-microsoft-odbc-driver-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>Componentes de Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en Windows 
 El controlador ODBC en Windows contiene los siguientes componentes:
 
|Componente|Description|  
|---------------|-----------------|  
|msodbcsql17.dll o <br> msodbcsql13.dll o <br> msodbcsql11.dll|El archivo de biblioteca de vínculos dinámicos (DLL) que contiene toda la funcionalidad del controlador. Este archivo está instalado en % SYSTEMROOT%\System32.|  
|msodbcdiag17.dll o <br> msodbcdiag13.dll o <br> msodbcdiag11.dll|El archivo de biblioteca de vínculos dinámicos (DLL) que contiene la interfaz de diagnósticos (seguimiento) del controlador. Este archivo está instalado en % SYSTEMROOT%\System32.|
|msodbcsqlr17.rll o <br> msodbcsqlr13.rll o <br> msodbcsqlr11.rll|El archivo de recursos asociado de la biblioteca de controladores. Este archivo está instalado en % SYSTEMROOT%\System32\1033.| 
|s13ch_msodbcsql.chm o <br> s11ch_msodbcsql.chm |El archivo de Ayuda del Asistente para orígenes de datos que documenta cómo crear un origen de datos para el controlador. Este archivo se instala en %SYSTEMROOT%\System32\1033 <br /> <br /> **Nota:** no hay ningún archivo chm para 17 del controlador ODBC. |  
|msodbcsql.h|El archivo de encabezado que contiene todas las definiciones nuevas necesarias para usar el controlador.<br /><br /> **Nota:**  No se puede hacer referencia a msodbcsql.h y odbcss.h en el mismo programa.<br /><br /> msodbcsql.h de 17 del controlador de ODBC o 13 está instalado en %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK. <br /> msodbcsql.h para ODBC Driver 11 se instala en %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK.| 
|msodbcsql17.lib o <br> msodbcsql13.lib o <br> msodbcsql11.lib|El archivo de biblioteca necesario para llamar a la **bcp** funciones de utilidad que forman parte del controlador.<br /><br /> **Nota:** si hace referencia a este archivo de biblioteca en el programa, asegúrese de que está en la ruta del sistema y en la ruta de acceso de sistema de los usuarios que usen la aplicación.<br /><br /> msodbcsql17.lib o msodbcsql13.lib está instalado en %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK.<br /> msodbcsql11.lib está instalado en %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK.|

  
## <a name="see-also"></a>Vea también  
 [Microsoft ODBC Driver for SQL Server en Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
