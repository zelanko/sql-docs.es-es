---
title: Requisitos del sistema para los controladores de Microsoft para PHP para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- requirements
ms.assetid: 5db4b75f-c605-4785-9560-399a533c0fc9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b601d4fbb02b489aca228acb719cfe8bad834dc0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992570"
---
# <a name="system-requirements-for-the-microsoft-drivers-for-php-for-sql-server"></a>Requisitos del sistema para los controladores de Microsoft para PHP para SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

En este documento se enumeran los componentes que se deben instalar en el sistema para tener acceso a los datos de [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]un SQL Server o Azure SQL Database mediante el.

Oficialmente se admiten las versiones 3,1 y posteriores de los controladores PHP de Microsoft para SQL Server. Para obtener información completa sobre los ciclos de vida de soporte técnico y los requisitos, incluidas las versiones anteriores de los controladores PHP, consulte la [matriz de compatibilidad](../../connect/php/microsoft-php-drivers-for-sql-server-support-matrix.md).

## <a name="php"></a>PHP

Para obtener información sobre cómo descargar e instalar los archivos binarios estables más recientes, vea [el sitio web de PHP](https://php.net).  Los controladores de Microsoft para PHP para SQL Server requieren las siguientes versiones de PHP:

|Versión del controlador de PHP para SQL Server&#8594;<br />&#8595; versión de PHP|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|:---:|---|---|---|---|---|---|---|
|7.3|7.3.0+ | | | | | | |
|7.2|7.2+<sup>1</sup>|7.2+<sup>1</sup>|7.2+<sup>1</sup>| | | | |
|7.1|7.1.0+ |7.1.0+ |7.1.0+ |7.1.0+ |       |        |        |
|7.0|       |7.0.0+ |7.0.0+ |7.0.0+ |7.0.0+ |        |        |
|5.6|       |       |       |       |       |5.6.4+  |        |
|5.5|       |       |       |       |       |5.5.16+ |5.5.16+ |
|5.4|       |       |       |       |       |5.4.32  |5.4.32  |

1. Las versiones 7.2.1 y posteriores se admiten en Windows, mientras que las versiones 7.2.0 y versiones posteriores se admiten en Linux y macOS.

-   En el directorio de extensión PHP debe haber una versión del archivo de controlador. Consulte [versiones de controladores](#driver-versions) para obtener información acerca de los diferentes archivos de controlador.  Para descargar los controladores, vea [Download the Microsoft Drivers for PHP for SQL Server](../../connect/php/download-drivers-php-sql-server.md) (Descargar los controladores de Microsoft para PHP para SQL Server). Para obtener información sobre cómo configurar el controlador para el runtime PHP, vea [Loading the Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md) (Cargar los controladores de Microsoft para PHP para SQL Server).

-   Se requiere un servidor web. El servidor web debe estar configurado para ejecutar PHP. Para obtener información sobre el hospedaje de aplicaciones PHP con IIS, vea el [tutorial sobre el sitio web de php](http://docs.php.net/manual/da/install.windows.iis7.php).

    Los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] se han probado utilizando IIS 10 con FastCGI.  

    > [!NOTE]  
    > Microsoft solo proporciona compatibilidad con IIS.  

## <a name="odbc-driver"></a>Controlador ODBC

Se requiere la versión correcta del Microsoft ODBC Driver for SQL Server en el equipo en el que se está ejecutando PHP. Puede descargar todas las versiones compatibles del controlador para las plataformas compatibles en [esta página](https://docs.microsoft.com/sql/connect/odbc/download-odbc-driver-for-sql-server?view=sql-server-2017).

Si está descargando la versión de Windows del controlador en una versión de 64 bits de Windows, el instalador de ODBC 64-bit instala los controladores ODBC de 32 bits y de 64 bits. Si usa una versión de 32 bits de Windows, use el instalador de ODBC x86. En plataformas que no son de Windows, solo están disponibles las versiones de 64 bits del controlador.

|Versión del controlador de PHP para SQL Server&#8594;<br />Versión del controlador ODBC &#8595;|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|ODBC Driver 17+ |S|S|S| | | | |
|ODBC Driver 13.1|S|S|S|S|S| | |
|ODBC Driver 13  | | | | |S| | |
|ODBC Driver 11  |S|S|S|S|S|S|S|

Si usa el controlador SQLSRV, [sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md) devuelve información sobre la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Microsoft ODBC driver for SQL Server que [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]va a usar. Si está usando el controlador PDO_SQLSRV, puede usar [PDO::getAttribute](../../connect/php/pdo-getattribute.md) para detectar la versión.  

## <a name="sql-server"></a>SQL Server

Se admiten las bases de datos SQL de Azure. Para obtener información, vea [Connecting to Windows Azure SQL Database](../../connect/php/connecting-to-microsoft-azure-sql-database.md) (Conectarse a Microsoft Azure SQL Database).

|Versión del controlador de PHP para SQL Server&#8594;<br />&#8595; versión de SQL Server|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Base de datos SQL de Azure        |S|S|S|S| | | |
|Instancia administrada de Azure SQL|S|S|S|S| | | |
|Almacenamiento de datos SQL de Azure  |S|S|S|S| | | |
|SQL Server 2017           |S|S|S|S| | | |
|SQL Server 2016           |S|S|S|S|S| | |
|SQL Server 2014           |S|S|S|S|S|S|S|
|SQL Server 2012           |S|S|S|S|S|S|S|
|SQL Server 2008 R2        |S|S|S|S|S|S|S|
|SQL Server 2008           | | | | |S|S|S|

## <a name="operating-systems"></a>Sistemas operativos
Los sistemas operativos compatibles para cada versión del controlador son los siguientes:

|Versión del controlador de PHP para SQL Server&#8594;<br />&#8595; sistema operativo|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Windows Server 2016                 |S  |S  |S  |S  |   |   |   |
|Windows Server 2012 R2              |S  |S  |S  |S  |S  |S  |S  |
|Windows Server 2012                 |S  |S  |S  |S  |S  |S  |S  |
|Windows Server 2008 R2 SP1          |   |   |   |   |S  |S  |S  |
|Windows Server 2008 SP2             |   |   |   |   |S  |S  |S  |
|Windows 10                          |S  |S  |S  |S  |S  |   |   |
|Windows 8.1                         |S  |S  |S  |S  |S  |S  |S  |
|Windows 8                           |   |   |   |S  |S  |S  |S  |
|Windows 7 SP1                       |   |   |   |   |S  |S  |S  |
|Windows Vista SP2                   |   |   |   |   |S  |S  |S  |
|Ubuntu 18,10 (64 bits)               |S  |   |   |   |   |   |   |
|Ubuntu 18,04 (64 bits)               |S  |S  |   |   |   |   |   |
|Ubuntu 17,10 (64 bits)               |   |S  |S  |   |   |   |   |
|Ubuntu 16,04 (64 bits)               |S  |S  |S  |S  |S  |   |   |
|Ubuntu 15,10 (64 bits)               |   |   |   |S  |   |   |   |
|Ubuntu 15,04 (64 bits)               |   |   |   |   |S  |   |   |
|Debian 9 (64 bits)                   |S  |S  |S  |   |   |   |   |
|Debian 8 (64 bits)                   |S  |S  |S  |S  |   |   |   |
|Red Hat Enterprise Linux 7 (64 bits) |S  |S  |S  |S  |S  |   |   |
|SuSE Enterprise Linux 15 (64 bits)   |S  |   |   |   |   |   |   |
|SuSE Enterprise Linux 12 (64 bits)   |S  |S  |S  |   |   |   |   |
|macOS Mojave (64 bits)               |S  |   |   |   |   |   |   |
|macOS High Sierra (64 bits)          |S  |S  |   |   |   |   |   |
|macOS Sierra (64 bits)               |S  |S  |S  |S  |   |   |   |
|macOS el Capitan (64 bits)           |   |S  |S  |S  |   |   |   |

## <a name="driver-versions"></a>Versiones del controlador  
En esta sección se enumeran los archivos de controladores que se incluyen con [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]cada versión de. Cada paquete de instalación contiene archivos de controlador SQLSRV y PDO_SQLSRV en variantes de subproceso y no de subproceso. En Windows, también están disponibles en variantes de 32 y 64 bits. Para configurar el controlador para su uso con el tiempo de ejecución de PHP, siga las instrucciones de instalación de [carga de los controladores de Microsoft para PHP para SQL Server](../../connect/php/loading-the-php-sql-driver.md).

En las versiones admitidas de Linux y macOS, se pueden instalar los controladores adecuados con el sistema de paquetes PECL de PHP, siguiendo las [instrucciones de instalación de Linux y MacOS](../../connect/php/installation-tutorial-linux-mac.md). Como alternativa, puede descargar los archivos binarios precompilados de la plataforma en la página de proyecto [controladores de Microsoft para PHP para SQL Server](https://github.com/Microsoft/msphpsql/releases) github. en las tablas siguientes se enumeran los archivos que se encuentran en los paquetes binarios creados previamente.

**Controladores de Microsoft 5.6 para PHP para SQL Server:**  

En Windows, se incluyen las siguientes versiones del controlador:

|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|Uso con PHP.dll|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_71_nts.dll de 32 bits<br />php_pdo_sqlsrv_71_nts.dll de 32 bits|7.1|no |php7. dll de 32 bits|  
|php_sqlsrv_71_ts.dll de 32 bits <br />php_pdo_sqlsrv_71_ts.dll de 32 bits |7.1|sí|php7ts. dll de 32 bits|  
|php_sqlsrv_71_nts.dll de 64 bits<br />php_pdo_sqlsrv_71_nts.dll de 64 bits|7.1|no |php7. dll de 64 bits|  
|php_sqlsrv_71_ts.dll de 64 bits <br />php_pdo_sqlsrv_71_ts.dll de 64 bits |7.1|sí|php7ts. dll de 64 bits|   
|php_sqlsrv_72_nts.dll de 32 bits<br />php_pdo_sqlsrv_72_nts.dll de 32 bits|7.2|no |php7. dll de 32 bits|  
|php_sqlsrv_72_ts.dll de 32 bits <br />php_pdo_sqlsrv_72_ts.dll de 32 bits |7.2|sí|php7ts. dll de 32 bits|  
|php_sqlsrv_72_nts.dll de 64 bits<br />php_pdo_sqlsrv_72_nts.dll de 64 bits|7.2|no |php7. dll de 64 bits|  
|php_sqlsrv_72_ts.dll de 64 bits <br />php_pdo_sqlsrv_72_ts.dll de 64 bits |7.2|sí|php7ts. dll de 64 bits|  
|php_sqlsrv_73_nts.dll de 32 bits<br />php_pdo_sqlsrv_73_nts.dll de 32 bits|7.3|no |php7. dll de 32 bits|  
|php_sqlsrv_73_ts.dll de 32 bits <br />php_pdo_sqlsrv_73_ts.dll de 32 bits |7.3|sí|php7ts. dll de 32 bits|  
|php_sqlsrv_73_nts.dll de 64 bits<br />php_pdo_sqlsrv_73_nts.dll de 64 bits|7.3|no |php7. dll de 64 bits|  
|php_sqlsrv_73_ts.dll de 64 bits <br />php_pdo_sqlsrv_73_ts.dll de 64 bits |7.3|sí|php7ts. dll de 64 bits|  

En Linux, se incluyen las siguientes versiones del controlador:

|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|no |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|sí|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|no |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|sí|
|php_sqlsrv_73_nts.so<br />php_pdo_sqlsrv_73_nts.so|7.3|no |
|php_sqlsrv_73_ts.so <br />php_pdo_sqlsrv_73_ts.so |7.3|sí|

**Controladores de Microsoft 5.3 para PHP para SQL Server:**  

En Windows, se incluyen las siguientes versiones del controlador:

|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|Uso con PHP.dll|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_7_nts.dll de 32 bits <br />php_pdo_sqlsrv_7_nts.dll de 32 bits |7.0|no |php7. dll de 32 bits|
|php_sqlsrv_7_ts.dll de 32 bits  <br />php_pdo_sqlsrv_7_ts.dll de 32 bits  |7.0|sí|php7ts. dll de 32 bits|
|php_sqlsrv_7_nts.dll de 64 bits <br />php_pdo_sqlsrv_7_nts.dll de 64 bits |7.0|no |php7. dll de 64 bits|  
|php_sqlsrv_7_ts.dll de 64 bits  <br />php_pdo_sqlsrv_7_ts.dll de 64 bits  |7.0|sí|php7ts. dll de 64 bits|
|php_sqlsrv_71_nts.dll de 32 bits<br />php_pdo_sqlsrv_71_nts.dll de 32 bits|7.1|no |php7. dll de 32 bits|  
|php_sqlsrv_71_ts.dll de 32 bits <br />php_pdo_sqlsrv_71_ts.dll de 32 bits |7.1|sí|php7ts. dll de 32 bits|  
|php_sqlsrv_71_nts.dll de 64 bits<br />php_pdo_sqlsrv_71_nts.dll de 64 bits|7.1|no |php7. dll de 64 bits|  
|php_sqlsrv_71_ts.dll de 64 bits <br />php_pdo_sqlsrv_71_ts.dll de 64 bits |7.1|sí|php7ts. dll de 64 bits|   
|php_sqlsrv_72_nts.dll de 32 bits<br />php_pdo_sqlsrv_72_nts.dll de 32 bits|7.2|no |php7. dll de 32 bits|  
|php_sqlsrv_72_ts.dll de 32 bits <br />php_pdo_sqlsrv_72_ts.dll de 32 bits |7.2|sí|php7ts. dll de 32 bits|  
|php_sqlsrv_72_nts.dll de 64 bits<br />php_pdo_sqlsrv_72_nts.dll de 64 bits|7.2|no |php7. dll de 64 bits|  
|php_sqlsrv_72_ts.dll de 64 bits <br />php_pdo_sqlsrv_72_ts.dll de 64 bits |7.2|sí|php7ts. dll de 64 bits|  

En Linux, se incluyen las siguientes versiones del controlador:

|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|no |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|sí|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|no |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|sí|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|no |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|sí|

**Controladores de Microsoft 5.2 para PHP para SQL Server:**  

En Windows, se incluyen las siguientes versiones del controlador:

|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|Uso con PHP.dll|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_7_nts.dll de 32 bits <br />php_pdo_sqlsrv_7_nts.dll de 32 bits |7.0|no |php7. dll de 32 bits|
|php_sqlsrv_7_ts.dll de 32 bits  <br />php_pdo_sqlsrv_7_ts.dll de 32 bits  |7.0|sí|php7ts. dll de 32 bits|
|php_sqlsrv_7_nts.dll de 64 bits <br />php_pdo_sqlsrv_7_nts.dll de 64 bits |7.0|no |php7. dll de 64 bits|  
|php_sqlsrv_7_ts.dll de 64 bits  <br />php_pdo_sqlsrv_7_ts.dll de 64 bits  |7.0|sí|php7ts. dll de 64 bits|
|php_sqlsrv_71_nts.dll de 32 bits<br />php_pdo_sqlsrv_71_nts.dll de 32 bits|7.1|no |php7. dll de 32 bits|  
|php_sqlsrv_71_ts.dll de 32 bits <br />php_pdo_sqlsrv_71_ts.dll de 32 bits |7.1|sí|php7ts. dll de 32 bits|  
|php_sqlsrv_71_nts.dll de 64 bits<br />php_pdo_sqlsrv_71_nts.dll de 64 bits|7.1|no |php7. dll de 64 bits|  
|php_sqlsrv_71_ts.dll de 64 bits <br />php_pdo_sqlsrv_71_ts.dll de 64 bits |7.1|sí|php7ts. dll de 64 bits|   
|php_sqlsrv_72_nts.dll de 32 bits<br />php_pdo_sqlsrv_72_nts.dll de 32 bits|7.2|no |php7. dll de 32 bits|  
|php_sqlsrv_72_ts.dll de 32 bits <br />php_pdo_sqlsrv_72_ts.dll de 32 bits |7.2|sí|php7ts. dll de 32 bits|  
|php_sqlsrv_72_nts.dll de 64 bits<br />php_pdo_sqlsrv_72_nts.dll de 64 bits|7.2|no |php7. dll de 64 bits|  
|php_sqlsrv_72_ts.dll de 64 bits <br />php_pdo_sqlsrv_72_ts.dll de 64 bits |7.2|sí|php7ts. dll de 64 bits|  

En Linux, se incluyen las siguientes versiones del controlador:

|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|no |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|sí|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|no |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|sí|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|no |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|sí|

**Controladores de Microsoft 4.3 para PHP para SQL Server:**  

En Windows, se incluyen las siguientes versiones del controlador:

|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|Uso con PHP.dll|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_7_nts.dll de 32 bits <br />php_pdo_sqlsrv_7_nts.dll de 32 bits |7.0|no |php7. dll de 32 bits|
|php_sqlsrv_7_ts.dll de 32 bits  <br />php_pdo_sqlsrv_7_ts.dll de 32 bits  |7.0|sí|php7ts. dll de 32 bits|
|php_sqlsrv_7_nts.dll de 64 bits <br />php_pdo_sqlsrv_7_nts.dll de 64 bits |7.0|no |php7. dll de 64 bits|  
|php_sqlsrv_7_ts.dll de 64 bits  <br />php_pdo_sqlsrv_7_ts.dll de 64 bits  |7.0|sí|php7ts. dll de 64 bits|
|php_sqlsrv_71_nts.dll de 32 bits<br />php_pdo_sqlsrv_71_nts.dll de 32 bits|7.1|no |php7. dll de 32 bits|  
|php_sqlsrv_71_ts.dll de 32 bits <br />php_pdo_sqlsrv_71_ts.dll de 32 bits |7.1|sí|php7ts. dll de 32 bits|  
|php_sqlsrv_71_nts.dll de 64 bits<br />php_pdo_sqlsrv_71_nts.dll de 64 bits|7.1|no |php7. dll de 64 bits|  
|php_sqlsrv_71_ts.dll de 64 bits <br />php_pdo_sqlsrv_71_ts.dll de 64 bits |7.1|sí|php7ts. dll de 64 bits|   

En Linux, se incluyen las siguientes versiones del controlador:

|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|no |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|sí|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|no |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|sí|  

**Controladores de Microsoft 4.0 para PHP para SQL Server:**  

En Windows, se incluyen las siguientes versiones del controlador:

|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|Uso con PHP.dll|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|no|php7. dll de 32 bits|  
|php_sqlsrv_7_ts_x86.dll<br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|sí|php7ts. dll de 32 bits|  
|php_sqlsrv_7_nts_x64.dll<br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|no|php7. dll de 64 bits|  
|php_sqlsrv_7_ts_x64.dll<br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|sí|php7ts. dll de 64 bits|   

En Linux, se incluyen las siguientes versiones del controlador:

|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|no |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|sí|

**Controladores de Microsoft 3.2 para PHP para SQL Server:**  

En Windows, se incluyen las siguientes versiones del controlador:

|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|Uso con PHP.dll|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|no|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|sí|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|no|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|sí|php5ts.dll|  
|php_sqlsrv_56_nts.dll<br />php_pdo_sqlsrv_56_nts.dll|5.6|no|php5.dll|  
|php_sqlsrv_56_ts.dll<br />php_pdo_sqlsrv_56_ts.dll|5.6|sí|php5ts.dll|  

**Controladores de Microsoft 3.1 para PHP para SQL Server**  

En Windows, se incluyen las siguientes versiones del controlador:

|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|Uso con PHP.dll|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|no|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|sí|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|no|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|sí|php5ts.dll|  

## <a name="see-also"></a>Consulte también  
[Introducción a los controladores de Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Guía de programación para los controladores de Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Referencia de la API del controlador PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
