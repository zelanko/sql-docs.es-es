---
title: Requisitos del sistema, instalación y archivos del controlador | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d90fa182-1dab-4d6f-bd85-a04dd1479986
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6ab9a4035e3a714e6725f28f7e4e370bf3fd0119
ms.sourcegitcommit: 82b70c39550402a2b0b327db32bf5ecf88b50d3c
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/29/2019
ms.locfileid: "73032986"
---
# <a name="system-requirements-installation-and-driver-files"></a>Requisitos del sistema, instalación y archivos del controlador

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

En este artículo se describen los controladores ODBC que se conectan a SQL Server.

## <a name="driver-versions"></a>Versiones del controlador

| Versión del controlador | Descripción del soporte técnico |
| :------------- | :--------------------- |
| ODBC driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] | Admite conexiones a SQL Server 2014, SQL Server 2012, [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)]y [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. |
| ODBC driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Windows | Se puede instalar en un equipo que también tenga una o varias versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. |
| ODBC driver 13 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] | Admite conexiones a SQL Server 2016, SQL Server 2014, SQL Server 2012, [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]y [!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)]. |
| ODBC driver 13,1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], <br/> Además de los anteriores para 13 | Admite SQL Server 2017. |
| ODBC driver 17 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] | Admite las mismas versiones de base de datos que 13,1. |
| Controlador ODBC 17 para SQL Server | Admite SQL Server 2019 a partir de la versión 17,3 del controlador. |
| &nbsp; | &nbsp; |

### <a name="connection-string-details"></a>Detalles de la cadena de conexión

El nombre del controlador que especifique en una cadena de conexión es `ODBC Driver 11 for SQL Server` o `ODBC Driver 13 for SQL Server` (para 13 y 13,1) o `ODBC Driver 17 for SQL Server`.

## <a name="supported-operating-systems"></a>Sistemas operativos admitidos

Puede ejecutar aplicaciones con el controlador en los siguientes sistemas operativos Windows:  

- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016
- Windows Vista SP2 &nbsp; _(solo el controlador ODBC 11)._
- Windows 7
- Windows 8
- Windows 8.1
- Windows 10

## <a name="installing-microsoft-odbc-driver-for-sql-server"></a>Instalación de Microsoft ODBC Driver for SQL Server

El controlador se instala al ejecutar `msodbcsql.msi` desde uno de los vínculos siguientes:

- [Descargar Microsoft ODBC Driver 17 for SQL Server en Windows](https://www.microsoft.com/download/details.aspx?id=56567)
- [Descargar Microsoft ODBC Driver 13.1 for SQL Server en Windows](https://www.microsoft.com/download/details.aspx?id=53339)
- [Descargar Microsoft ODBC Driver 13 for SQL Server en Windows](https://www.microsoft.com/download/details.aspx?id=50420)
- [Descargar Microsoft ODBC Driver 11 for SQL Server en Windows](https://www.microsoft.com/download/details.aspx?id=36434)

> [!NOTE]
> Para aquellos que tengan instalado el controlador 17.1.0.1 o una versión posterior, se recomienda desinstalarlo manualmente antes de instalar la versión más reciente del controlador.

### <a name="side-by-side-with-native-client"></a>En paralelo con Native Client

El controlador se puede instalar en paralelo con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.

Cuando se llama a `msodbcsql.msi`, solo se instalan los componentes de cliente de forma predeterminada. Los componentes de cliente son archivos que permiten ejecutar aplicaciones desarrolladas mediante el controlador. Para instalar los componentes de SDK, especifique `ADDLOCAL=ALL` en la línea de comandos. A continuación se muestra un ejemplo:
  
```console
msiexec /i msodbcsql.msi ADDLOCAL=ALL  
```  

### <a name="end-user-license"></a>Licencia de usuario final

Especifique `IACCEPTMSODBCSQLLICENSETERMS=YES` para aceptar los términos de la licencia para el usuario final si utiliza la opción de instalación `/passive`, `/qn`, `/qb` o `/qr`. Esta opción se debe especificar con todas las letras mayúsculas. A continuación se muestra un ejemplo:
  
```console
msiexec /quiet /passive /qn /i msodbcsql.msi IACCEPTMSODBCSQLLICENSETERMS=YES ADDLOCAL=ALL  
```  

### <a name="silent-uninstall"></a>Desinstalación silenciosa

En el ejemplo siguiente se muestra cómo realizar una desinstalación silenciosa.
  
```console
msiexec /quiet /passive /qn /uninstall msodbcsql.msi  
```  

### <a name="indicate-dependency"></a>Indicar dependencia

Cuando una aplicación utiliza el controlador, esta debe indicar que depende del controlador mediante la opción de instalación `APPGUID`. Esta indicación habilita al instalador del controlador para notificar cuáles son las aplicaciones dependientes antes de que se lleve a cabo la desinstalación. Para especificar una dependencia del controlador, establezca el parámetro de línea de comandos `APPGUID` en el código de producto cuando se instale en modo silencioso el controlador. Se debe crear un código de producto al usar Microsoft Installer para empaquetar su programa de instalación de la aplicación. A continuación se muestra un ejemplo:
  
```console
msiexec /i msodbcsql.msi APPGUID={ <Your dependent application's APPGUID> }  
```  

## <a name="command-line-tools-sqlcmdexe-and-bcpexe"></a>Herramientas de línea de comandos: sqlcmd.exe y bcp.exe

Las herramientas de `bcp.exe` y `sqlcmd.exe` para su uso con el controlador se pueden descargar en [microsoft utilidades de la línea de comandos 11 para SQL Server](https://www.microsoft.com/download/details.aspx?id=36433), [Microsoft Utilidades de la línea de comandos 13 para SQL Server](https://www.microsoft.com/download/details.aspx?id=52680)o [Microsoft utilidades de la línea de comandos 13,1 para SQL Server ](https://www.microsoft.com/download/details.aspx?id=53591). El controlador es un requisito previo para instalar `sqlcmd.exe` y `bcp.exe`.
  
`bcp.exe` y `sqlcmd.exe` se instalan en la subcarpeta `110\Tools` de `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC` para la versión 11 y `130\Tools` para 13 y 13,1.

Las aplicaciones que utilizan funciones BCP deben especificar el controlador (con la misma versión que aparece en el archivo de encabezado) y la biblioteca usada para compilar la aplicación.  

Por ejemplo, al compilar una aplicación ODBC con `msodbcsql11.lib` y `msodbcsql.h`, use "DRIVER = {ODBC driver 11 for SQL Server}" en la cadena de conexión.

## <a name="components-of-the-microsoft-odbc-driver-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Componentes de Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Windows

El controlador ODBC en Windows contiene los siguientes componentes:

| Componente | Descripción |
| :-------- | :---------- |
|msodbcsql17. dll o <br/> msodbcsql13.dll o <br/> msodbcsql11.dll|El archivo de biblioteca de vínculos dinámicos (DLL) que contiene toda la funcionalidad del controlador. Este archivo se instala en% SystemRoot%\System32.|  
|msodbcdiag17. dll o <br/> msodbcdiag13. dll o <br/> msodbcdiag11.dll|El archivo de biblioteca de vínculos dinámicos (DLL) que contiene la interfaz de diagnóstico (seguimiento) del controlador. Este archivo se instala en% SystemRoot%\System32.|
|msodbcsqlr17.rll o <br/> msodbcsqlr13.rll o <br/> msodbcsqlr11.rll|El archivo de recursos asociado de la biblioteca de controladores. Este archivo se instala en% systemroot%\system32\1033.| 
|s13ch_msodbcsql.chm o <br/> s11ch_msodbcsql.chm |El archivo de Ayuda del Asistente para orígenes de datos que documenta cómo crear un origen de datos para el controlador. Este archivo se instala en%systemroot%\system32\1033. <br /> <br /> **Nota:** No hay ningún archivo CHM para el controlador ODBC 17. |  
|msodbcsql.h|El archivo de encabezado que contiene todas las definiciones nuevas necesarias para utilizar el controlador.<br /><br /> **Nota:**  No se puede hacer referencia a msodbcsql.h y odbcss.h en el mismo programa.<br /><br /> msodbcsql.h para ODBC Driver 17 o 13 está instalado en %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK. <br /> msodbcsql.h para ODBC Driver 11 está instalado en %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK.| 
|msodbcsql17.lib o <br/> msodbcsql13.lib o <br/> msodbcsql11.lib|El archivo de biblioteca necesario para llamar a las funciones de la utilidad **bcp** que forman parte del controlador.<br /><br /> **Nota:** Si hace referencia a este archivo de biblioteca en el programa, asegúrese de que se encuentra en la ruta de acceso de su sistema y en la de los usuarios que usen la aplicación.<br /><br /> msodbcsql17.lib o msodbcsql13.lib está instalado en %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK.<br /> msodbcsql11.lib está instalado en %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK.|
| &nbsp; | &nbsp; |

## <a name="see-also"></a>Vea también

[Microsoft ODBC Driver for SQL Server en Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
