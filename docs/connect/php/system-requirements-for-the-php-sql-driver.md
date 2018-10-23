---
title: Requisitos del sistema para los controladores de Microsoft para PHP para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/23/2018
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
manager: craigg
ms.openlocfilehash: 3784a3ba9b05bde0fafea486ddfdf3a968f96914
ms.sourcegitcommit: ef78cc196329a10fc5c731556afceaac5fd4cb13
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2018
ms.locfileid: "49461130"
---
# <a name="system-requirements-for-the-microsoft-drivers-for-php-for-sql-server"></a>Requisitos del sistema para los controladores de Microsoft para PHP para SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este documento enumera los componentes que se deben instalar en el sistema para acceder a los datos en un SQL Server o Azure SQL Database usando el [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].

Se admiten oficialmente las versiones 3.1 y posteriores de Microsoft PHP Driver para SQL Server. Para obtener detalles sobre los ciclos de vida de soporte técnico y requisitos, incluidas las versiones anteriores de los controladores PHP, consulte el [matriz de compatibilidad](../../connect/php/microsoft-php-drivers-for-sql-server-support-matrix.md).

## <a name="php"></a>PHP

Para obtener información sobre cómo descargar e instalar los archivos binarios estables más recientes, vea [el sitio web de PHP](http://php.net).  Los Drivers de Microsoft para PHP para SQL Server requieren las siguientes versiones de PHP:

|PHP para la versión del controlador de SQL Server&#8594;<br />&#8595; versión de PHP|5.3 y 5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|
|7.2|7.2.1+ en Windows<br/>7.2.0+ en otras plataformas | | | | |
|7.1|7.1.0+ |7.1.0+ |       |        |        |
|7.0|7.0.0+ |7.0.0+ |7.0.0+ |        |        |
|5.6|       |       |       |5.6.4  |        |
|5.5|       |       |       |5.5.16 |5.5.16 |
|5.4|       |       |       |5.4.32  |5.4.32  |

-   En el directorio de extensión PHP debe haber una versión del archivo de controlador. Consulte [las versiones del controlador](#driver-versions) para obtener información acerca de los archivos de controlador diferente.  Para descargar los controladores, vea [Download the Microsoft Drivers for PHP for SQL Server](download-drivers-php-sql-server.md) (Descargar los controladores de Microsoft para PHP para SQL Server). Para obtener información sobre cómo configurar el controlador para el runtime PHP, vea [Loading the Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md) (Cargar los controladores de Microsoft para PHP para SQL Server).

-   Se requiere un servidor web. El servidor web debe estar configurado para ejecutar PHP. Para obtener información sobre cómo hospedar aplicaciones PHP con IIS, vea el [tutorial en el sitio web de PHP](http://php.net/manual/fa/install.windows.iis.php).  

    Los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] se han probado utilizando IIS 10 con FastCGI.  

    > [!NOTE]  
    > Microsoft solo proporciona compatibilidad con IIS.  

-   Versión 5.3 de la Microsoft Drivers para PHP para SQL Server será el último para admitir PHP 7.0.

## <a name="odbc-driver"></a>Controlador ODBC

Se requiere la versión correcta de Microsoft ODBC Driver for SQL Server en el equipo en el que se está ejecutando PHP. Puede descargar todas las versiones compatibles del controlador para las plataformas admitidas en [esta página](https://docs.microsoft.com/sql/connect/odbc/download-odbc-driver-for-sql-server?view=sql-server-2017).

Si va a descargar la versión de Windows del controlador en una versión de 64 bits de Windows, el programa de instalación ODBC 64-bit instala a controladores ODBC de 32 bits y 64 bits. Si usa una versión de 32 bits de Windows, utilice ODBC x86 instalador. En las plataformas que no sean Windows, versiones sólo de 64 bits del controlador están disponibles.

|PHP para la versión del controlador de SQL Server&#8594;<br />&#8595;Versión del controlador ODBC|5.3<br />&nbsp;|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|---|
|ODBC Driver 17+ |S|S| | | | |
|ODBC Driver 13.1|S|S|S|S| | |
|ODBC Driver 13  | | | |S| | |
|ODBC Driver 11  |S|S|S|S|S|S|

Si usa el controlador SQLSRV, [sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md) devuelve información acerca de qué versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Microsoft ODBC Driver para SQL Server está usando el [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Si está usando el controlador PDO_SQLSRV, puede usar [PDO::getAttribute](../../connect/php/pdo-getattribute.md) para detectar la versión.  

## <a name="sql-server"></a>SQL Server

Se admiten las bases de datos de SQL Azure. Para obtener información, vea [Connecting to Windows Azure SQL Database](../../connect/php/connecting-to-microsoft-azure-sql-database.md) (Conectarse a Microsoft Azure SQL Database).

|PHP para la versión del controlador de SQL Server&#8594;<br />&#8595; versión de SQL Server|5.3<br />&nbsp;|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|---|
|Base de datos SQL de Azure        |S|S|S| | | |
|Instancia administrada de Azure SQL|S|S|S| | | |
|Almacenamiento de datos SQL de Azure  |S|S|S| | | |
|SQL Server 2017           |S|S|S| | | |
|SQL Server 2016           |S|S|S|S| | |
|SQL Server 2014           |S|S|S|S|S|S|
|SQL Server 2012           |S|S|S|S|S|S|
|SQL Server 2008 R2        |S|S|S|S|S|S|
|SQL Server 2008           | | | |S|S|S|

## <a name="operating-systems"></a>Sistemas operativos
Sistemas operativos compatibles con las versiones del controlador son los siguientes:

|PHP para la versión del controlador de SQL Server&#8594;<br />&#8595; sistema operativo|5.3<br />&nbsp;|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|---|
|Windows Server 2016                      |S|S|S| | | |
|Windows Server 2012 R2                   |S|S|S|S|S|S|
|Windows Server 2012                      |S|S|S|S|S|S|
|Windows Server 2008 R2 SP1               | | | |S|S|S|
|Windows Server 2008 SP2                  | | | |S|S|S|
|Windows 10                               |S|S|S|S| | |
|Windows 8.1                              |S|S|S|S|S|S|
|Windows 8                                | | |S|S|S|S|
|Windows 7 SP1                            | | | |S|S|S|
|Windows Vista SP2                        | | | |S|S|S|
|Ubuntu 18.04 (64 bits)                    |S| | | | | |
|Con Ubuntu 17.10 (64 bits)                    |S|S| | | | |
|Ubuntu 16.04 (64 bits)                    |S|S|S|S| | |
|Ubuntu 15.10 (64 bits)                    | | |S| | | |
|Ubuntu 15.04 (64 bits)                    | | | |S| | |
|Debian 9 (64 bits)                        |S|S| | | | |
|Debian 8 (64 bits)                        |S|S|S| | | |
|Red Hat Enterprise Linux 7 (64 bits)      |S|S|S|S| | |
|SUSE Enterprise Linux 12 (64 bits)        |S|S| | | | |
|macOS High Sierra (64 bits)               |S| | | | | |
|macOS Sierra (64 bits)                    |S|S|S| | | |
|macOS El capitán (64 bits)                |S|S|S| | | |

## <a name="driver-versions"></a>Versiones del controlador  
Esta sección enumeran los archivos de controlador que se incluyen con cada versión de la [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Cada paquete de instalación contiene archivos de controlador PDO_SQLSRV SQLSRV en subprocesos y un subproceso que no son variantes. En Windows, también están disponibles en las variantes de 32 bits y 64 bits. Para configurar el controlador para su uso con el tiempo de ejecución PHP, siga las instrucciones de instalación de [Loading the Microsoft Drivers para PHP para SQL Server](../../connect/php/loading-the-php-sql-driver.md).

En las versiones compatibles de Linux y macOS, se pueden instalar los controladores adecuados mediante el sistema de PHP PECL paquete, siguiendo la [las instrucciones de instalación de Linux y macOS](../../connect/php/installation-tutorial-linux-mac.md). Como alternativa, puede descargar los archivos binarios creados previamente para su plataforma desde el [Microsoft Drivers para PHP para SQL Server](https://github.com/Microsoft/msphpsql/releases) página del proyecto de Github: las tablas siguientes muestran los archivos encontrados en los paquetes binarios precompilados.

**Controladores de Microsoft 5.3 para PHP para SQL Server:**  

En Windows, se incluyen las siguientes versiones del controlador:

|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|Uso con PHP.dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_7_nts.dll de 32 bits <br />php_pdo_sqlsrv_7_nts.dll de 32 bits |7.0|no |php7.dll de 32 bits|
|php_sqlsrv_7_ts.dll de 32 bits  <br />php_pdo_sqlsrv_7_ts.dll de 32 bits  |7.0|sí|php7ts.dll de 32 bits|
|php_sqlsrv_7_nts.dll de 64 bits <br />php_pdo_sqlsrv_7_nts.dll de 64 bits |7.0|no |php7.dll de 64 bits|  
|php_sqlsrv_7_ts.dll de 64 bits  <br />php_pdo_sqlsrv_7_ts.dll de 64 bits  |7.0|sí|php7ts.dll de 64 bits|
|php_sqlsrv_71_nts.dll de 32 bits<br />php_pdo_sqlsrv_71_nts.dll de 32 bits|7.1|no |php7.dll de 32 bits|  
|php_sqlsrv_71_ts.dll de 32 bits <br />php_pdo_sqlsrv_71_ts.dll de 32 bits |7.1|sí|php7ts.dll de 32 bits|  
|php_sqlsrv_71_nts.dll de 64 bits<br />php_pdo_sqlsrv_71_nts.dll de 64 bits|7.1|no |php7.dll de 64 bits|  
|php_sqlsrv_71_ts.dll de 64 bits <br />php_pdo_sqlsrv_71_ts.dll de 64 bits |7.1|sí|php7ts.dll de 64 bits|   
|php_sqlsrv_72_nts.dll de 32 bits<br />php_pdo_sqlsrv_72_nts.dll de 32 bits|7.2|no |php7.dll de 32 bits|  
|php_sqlsrv_72_ts.dll de 32 bits <br />php_pdo_sqlsrv_72_ts.dll de 32 bits |7.2|sí|php7ts.dll de 32 bits|  
|php_sqlsrv_72_nts.dll de 64 bits<br />php_pdo_sqlsrv_72_nts.dll de 64 bits|7.2|no |php7.dll de 64 bits|  
|php_sqlsrv_72_ts.dll de 64 bits <br />php_pdo_sqlsrv_72_ts.dll de 64 bits |7.2|sí|php7ts.dll de 64 bits|  

En Linux, se incluyen las siguientes versiones del controlador:

|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|
|---------------|---------------|----------------|
|php_sqlsrv_7_nts.SO <br />php_pdo_sqlsrv_7_nts.SO |7.0|no |
|php_sqlsrv_7_ts.SO  <br />php_pdo_sqlsrv_7_ts.SO  |7.0|sí|
|php_sqlsrv_71_nts.SO<br />php_pdo_sqlsrv_71_nts.SO|7.1|no |
|php_sqlsrv_71_ts.SO <br />php_pdo_sqlsrv_71_ts.SO |7.1|sí|  
|php_sqlsrv_72_nts.SO<br />php_pdo_sqlsrv_72_nts.SO|7.2|no |
|php_sqlsrv_72_ts.SO <br />php_pdo_sqlsrv_72_ts.SO |7.2|sí|

**Controladores de Microsoft 5.2 para PHP para SQL Server:**  

En Windows, se incluyen las siguientes versiones del controlador:

|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|Uso con PHP.dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_7_nts.dll de 32 bits <br />php_pdo_sqlsrv_7_nts.dll de 32 bits |7.0|no |php7.dll de 32 bits|
|php_sqlsrv_7_ts.dll de 32 bits  <br />php_pdo_sqlsrv_7_ts.dll de 32 bits  |7.0|sí|php7ts.dll de 32 bits|
|php_sqlsrv_7_nts.dll de 64 bits <br />php_pdo_sqlsrv_7_nts.dll de 64 bits |7.0|no |php7.dll de 64 bits|  
|php_sqlsrv_7_ts.dll de 64 bits  <br />php_pdo_sqlsrv_7_ts.dll de 64 bits  |7.0|sí|php7ts.dll de 64 bits|
|php_sqlsrv_71_nts.dll de 32 bits<br />php_pdo_sqlsrv_71_nts.dll de 32 bits|7.1|no |php7.dll de 32 bits|  
|php_sqlsrv_71_ts.dll de 32 bits <br />php_pdo_sqlsrv_71_ts.dll de 32 bits |7.1|sí|php7ts.dll de 32 bits|  
|php_sqlsrv_71_nts.dll de 64 bits<br />php_pdo_sqlsrv_71_nts.dll de 64 bits|7.1|no |php7.dll de 64 bits|  
|php_sqlsrv_71_ts.dll de 64 bits <br />php_pdo_sqlsrv_71_ts.dll de 64 bits |7.1|sí|php7ts.dll de 64 bits|   
|php_sqlsrv_72_nts.dll de 32 bits<br />php_pdo_sqlsrv_72_nts.dll de 32 bits|7.2|no |php7.dll de 32 bits|  
|php_sqlsrv_72_ts.dll de 32 bits <br />php_pdo_sqlsrv_72_ts.dll de 32 bits |7.2|sí|php7ts.dll de 32 bits|  
|php_sqlsrv_72_nts.dll de 64 bits<br />php_pdo_sqlsrv_72_nts.dll de 64 bits|7.2|no |php7.dll de 64 bits|  
|php_sqlsrv_72_ts.dll de 64 bits <br />php_pdo_sqlsrv_72_ts.dll de 64 bits |7.2|sí|php7ts.dll de 64 bits|  

En Linux, se incluyen las siguientes versiones del controlador:

|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|
|---------------|---------------|----------------|
|php_sqlsrv_7_nts.SO <br />php_pdo_sqlsrv_7_nts.SO |7.0|no |
|php_sqlsrv_7_ts.SO  <br />php_pdo_sqlsrv_7_ts.SO  |7.0|sí|
|php_sqlsrv_71_nts.SO<br />php_pdo_sqlsrv_71_nts.SO|7.1|no |
|php_sqlsrv_71_ts.SO <br />php_pdo_sqlsrv_71_ts.SO |7.1|sí|  
|php_sqlsrv_72_nts.SO<br />php_pdo_sqlsrv_72_nts.SO|7.2|no |
|php_sqlsrv_72_ts.SO <br />php_pdo_sqlsrv_72_ts.SO |7.2|sí|

**Controladores de Microsoft 4.3 para PHP para SQL Server:**  

En Windows, se incluyen las siguientes versiones del controlador:

|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|Uso con PHP.dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_7_nts.dll de 32 bits <br />php_pdo_sqlsrv_7_nts.dll de 32 bits |7.0|no |php7.dll de 32 bits|
|php_sqlsrv_7_ts.dll de 32 bits  <br />php_pdo_sqlsrv_7_ts.dll de 32 bits  |7.0|sí|php7ts.dll de 32 bits|
|php_sqlsrv_7_nts.dll de 64 bits <br />php_pdo_sqlsrv_7_nts.dll de 64 bits |7.0|no |php7.dll de 64 bits|  
|php_sqlsrv_7_ts.dll de 64 bits  <br />php_pdo_sqlsrv_7_ts.dll de 64 bits  |7.0|sí|php7ts.dll de 64 bits|
|php_sqlsrv_71_nts.dll de 32 bits<br />php_pdo_sqlsrv_71_nts.dll de 32 bits|7.1|no |php7.dll de 32 bits|  
|php_sqlsrv_71_ts.dll de 32 bits <br />php_pdo_sqlsrv_71_ts.dll de 32 bits |7.1|sí|php7ts.dll de 32 bits|  
|php_sqlsrv_71_nts.dll de 64 bits<br />php_pdo_sqlsrv_71_nts.dll de 64 bits|7.1|no |php7.dll de 64 bits|  
|php_sqlsrv_71_ts.dll de 64 bits <br />php_pdo_sqlsrv_71_ts.dll de 64 bits |7.1|sí|php7ts.dll de 64 bits|   

En Linux, se incluyen las siguientes versiones del controlador:

|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|
|---------------|---------------|----------------|
|php_sqlsrv_7_nts.SO <br />php_pdo_sqlsrv_7_nts.SO |7.0|no |
|php_sqlsrv_7_ts.SO  <br />php_pdo_sqlsrv_7_ts.SO  |7.0|sí|
|php_sqlsrv_71_nts.SO<br />php_pdo_sqlsrv_71_nts.SO|7.1|no |
|php_sqlsrv_71_ts.SO <br />php_pdo_sqlsrv_71_ts.SO |7.1|sí|  

**Controladores de Microsoft 4.0 para PHP para SQL Server:**  

En Windows, se incluyen las siguientes versiones del controlador:

|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|Uso con PHP.dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|no|php7.dll de 32 bits|  
|php_sqlsrv_7_ts_x86.dll<br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|sí|php7ts.dll de 32 bits|  
|php_sqlsrv_7_nts_x64.dll<br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|no|php7.dll de 64 bits|  
|php_sqlsrv_7_ts_x64.dll<br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|sí|php7ts.dll de 64 bits|   

En Linux, se incluyen las siguientes versiones del controlador:

|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|
|---------------|---------------|----------------|
|php_sqlsrv_7_nts.SO <br />php_pdo_sqlsrv_7_nts.SO |7.0|no |
|php_sqlsrv_7_ts.SO  <br />php_pdo_sqlsrv_7_ts.SO  |7.0|sí|

**Controladores de Microsoft 3.2 para PHP para SQL Server:**  

En Windows, se incluyen las siguientes versiones del controlador:

|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|Uso con PHP.dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|no|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|sí|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|no|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|sí|php5ts.dll|  
|php_sqlsrv_56_nts.dll<br />php_pdo_sqlsrv_56_nts.dll|5.6|no|php5.dll|  
|php_sqlsrv_56_ts.dll<br />php_pdo_sqlsrv_56_ts.dll|5.6|sí|php5ts.dll|  

**Controladores de Microsoft 3.1 para PHP para SQL Server**  

En Windows, se incluyen las siguientes versiones del controlador:

|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|Uso con PHP.dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|no|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|sí|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|no|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|sí|php5ts.dll|  

## <a name="see-also"></a>Ver también  
[Introducción a los controladores de Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Programación de guía para los controladores de Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Referencia de la API del controlador PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
