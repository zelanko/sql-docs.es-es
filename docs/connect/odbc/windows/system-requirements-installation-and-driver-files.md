---
title: Requisitos del sistema, instalación y archivos del controlador | Microsoft Docs
ms.custom: ''
ms.date: 03/18/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d90fa182-1dab-4d6f-bd85-a04dd1479986
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7969d9505f9f4f1896505849efe0306801838433
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920159"
---
# <a name="system-requirements-installation-and-driver-files"></a>Requisitos del sistema, instalación y archivos del controlador

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

En este artículo se describen los controladores ODBC que se conectan a SQL Server.

## <a name="sql-version-compatibility"></a>Compatibilidad con versiones de SQL

La compatibilidad indica que se ha probado la compatibilidad de un controlador con las versiones existentes de SQL en el momento de la versión del controlador. Por lo general, las versiones de SQL Server intentan mantener la compatibilidad con versiones anteriores con los controladores de cliente existentes. Pero es posible que las nuevas características de las versiones de SQL Server no estén disponibles con controladores de cliente anteriores.

|Versión del controlador|Azure SQL Database|Azure SQL DW|Instancia administrada de Azure SQL|SQL Server 2019|SQL Server 2017|SQL Server 2016|SQL Server 2014|SQL Server 2012|SQL Server 2008 R2|SQL Server 2008|SQL Server 2005|
|-|-|-|-|-|-|-|-|-|-|-|-|
|17.5|Y|Y|Y|Y|Y|Y|Y|Y| | | |
|17.4|Y|Y|Y|Y|Y|Y|Y|Y| | | |
|17.3|Y|Y|Y|Y|Y|Y|Y|Y|Y|Y| |
|17.2|Y|Y|Y| |Y|Y|Y|Y|Y|Y| |
|17.1|Y|Y|Y| |Y|Y|Y|Y|Y|Y| |
|17.0|Y|Y|Y| |Y|Y|Y|Y|Y|Y| |
|13.1| | | | |Y|Y|Y|Y|Y|Y| |
|13  | | | | | |Y|Y|Y|Y|Y| |
|11  | | | | | | |Y|Y|Y|Y|Y|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

### <a name="connection-string-details"></a>Detalles de la cadena de conexión

El nombre del controlador que especifique en una cadena de conexión es `ODBC Driver 11 for SQL Server` o `ODBC Driver 13 for SQL Server` (para 13 y 13.1) o `ODBC Driver 17 for SQL Server`.

## <a name="supported-operating-systems"></a>Sistemas operativos admitidos

En la matriz siguiente se indica la compatibilidad de la versión del controlador con las versiones del sistema operativo Windows:

|Versión del controlador|Windows Server 2019|Windows Server 2016|Windows Server 2012 R2|Windows Server 2012|Windows Server 2008 R2|Windows 10|Windows 8.1|Windows 7|Windows Vista SP2|
|-|-|-|-|-|-|-|-|-|-|
|17.5|Y|Y|Y|Y| |Y|Y| | |
|17.4|Y|Y|Y|Y|Y|Y|Y|Y| |
|17.3|Y|Y|Y|Y|Y|Y|Y|Y| |
|17.2| |Y|Y|Y|Y|Y|Y|Y| |
|17.1| |Y|Y|Y|Y|Y|Y|Y| |
|17.0| |Y|Y|Y|Y|Y|Y|Y| |
|13.1| |Y|Y|Y|Y|Y|Y|Y| |
|13  | | | |Y|Y| |Y|Y| |
|11  | | | |Y|Y| | |Y|Y|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

## <a name="installing-microsoft-odbc-driver-for-sql-server"></a>Instalación de Microsoft ODBC Driver for SQL Server

El controlador se instala al ejecutar `msodbcsql.msi` desde una de las [Descargas para Windows](../download-odbc-driver-for-sql-server.md#download-for-windows).

> [!NOTE]
> Para aquellos que tengan instalado Driver en la versión 17.1.0.1 o una posterior, se recomienda desinstalarlo manualmente antes de instalar la versión más reciente del controlador.

### <a name="side-by-side-with-native-client"></a>En paralelo con Native Client

El controlador se puede instalar en paralelo con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. También se pueden instalar las versiones principales del controlador (11, 13, 17) en paralelo con las demás.

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

En el ejemplo siguiente se muestra cómo se realiza una desinstalación silenciosa.
  
```console
msiexec /quiet /passive /qn /uninstall msodbcsql.msi  
```  

### <a name="indicate-dependency"></a>Indicación de dependencia

Cuando una aplicación utiliza el controlador, esta debe indicar que depende del controlador mediante la opción de instalación `APPGUID`. Esta indicación habilita al instalador del controlador para notificar cuáles son las aplicaciones dependientes antes de que se lleve a cabo la desinstalación. Para especificar una dependencia del controlador, establezca el parámetro de línea de comandos `APPGUID` en el código de producto cuando se instale en modo silencioso el controlador. Se debe crear un código de producto al usar Microsoft Installer para empaquetar su programa de instalación de la aplicación. A continuación se muestra un ejemplo:
  
```console
msiexec /i msodbcsql.msi APPGUID={ <Your dependent application's APPGUID> }  
```  

## <a name="command-line-tools-sqlcmdexe-and-bcpexe"></a>Herramientas de línea de comandos: sqlcmd.exe y bcp.exe

Las herramientas de `bcp.exe` y `sqlcmd.exe` para su uso con el controlador se pueden descargar en [Utilidades de la línea de comandos 11 de Microsoft para SQL Server](https://www.microsoft.com/download/details.aspx?id=36433), [Utilidades de la línea de comandos 13 de Microsoft para SQL Server](https://www.microsoft.com/download/details.aspx?id=52680) o [Utilidades de línea de la comandos 13.1 de Microsoft para SQL Server](https://www.microsoft.com/download/details.aspx?id=53591). El controlador es un requisito previo para instalar `sqlcmd.exe` y `bcp.exe`.
  
`bcp.exe` y `sqlcmd.exe` se instalan en la subcarpeta `110\Tools` de `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC` para la versión 11 y `130\Tools` para 13 y 13.1.

Las aplicaciones que utilizan funciones BCP deben especificar el controlador (con la misma versión que aparece en el archivo de encabezado) y la biblioteca usada para compilar la aplicación.  

Por ejemplo, cuando compile una aplicación de ODBC con `msodbcsql11.lib` y `msodbcsql.h`, use "DRIVER={ODBC Driver 11 for SQL Server}" en la cadena de conexión.

## <a name="components-of-the-microsoft-odbc-driver-for-ssnoversion-on-windows"></a>Componentes de Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Windows

El controlador ODBC en Windows contiene los siguientes componentes:

| Componente | Descripción |
| :-------- | :---------- |
|msodbcsql17.dll o <br/> msodbcsql13.dll o <br/> msodbcsql11.dll|El archivo de biblioteca de vínculos dinámicos (DLL) que contiene toda la funcionalidad del controlador. Este archivo está instalado en %SYSTEMROOT%\System32.|  
|msodbcdiag17.dll o <br/> msodbcdiag13.dll o <br/> msodbcdiag11.dll|El archivo de biblioteca de vínculos dinámicos (DLL) que contiene toda la interfaz de diagnóstico del controlador (seguimiento). Este archivo está instalado en %SYSTEMROOT%\System32.|
|msodbcsqlr17.rll o <br/> msodbcsqlr13.rll o <br/> msodbcsqlr11.rll|El archivo de recursos asociado de la biblioteca de controladores. Este archivo está instalado en %SYSTEMROOT%\System32\1033.| 
|s13ch_msodbcsql.chm o <br/> s11ch_msodbcsql.chm |El archivo de Ayuda del Asistente para orígenes de datos que documenta cómo crear un origen de datos para el controlador. Este archivo está instalado en %SYSTEMROOT%\System32\1033. <br /> <br /> **NOTA:** No hay ningún archivo chm para ODBC Driver 17. |  
|msodbcsql.h|El archivo de encabezado que contiene todas las definiciones nuevas necesarias para utilizar el controlador.<br /><br /> **Nota:**  No se puede hacer referencia a msodbcsql.h y odbcss.h en el mismo programa.<br /><br /> msodbcsql.h para ODBC Driver 17 o 13 está instalado en %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK. <br /> msodbcsql.h para ODBC Driver 11 está instalado en %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK.| 
|msodbcsql17.lib o <br/> msodbcsql13.lib o <br/> msodbcsql11.lib|El archivo de biblioteca necesario para llamar a las funciones de la utilidad **bcp** que forman parte del controlador.<br /><br /> **Nota:**  Si hace referencia a este archivo de biblioteca en el programa, asegúrese de que se encuentra en la ruta de acceso de su sistema y en la de los usuarios que usen la aplicación.<br /><br /> msodbcsql17.lib o msodbcsql13.lib está instalado en %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK.<br /> msodbcsql11.lib está instalado en %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK.|
| &nbsp; | &nbsp; |

## <a name="see-also"></a>Consulte también

[Microsoft ODBC Driver for SQL Server en Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
