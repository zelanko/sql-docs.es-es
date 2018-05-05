---
title: Requisitos del sistema para los controladores de Microsoft para PHP para SQL Server | Documentos de Microsoft
ms.custom: ''
ms.date: 03/23/2018
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- requirements
ms.assetid: 5db4b75f-c605-4785-9560-399a533c0fc9
caps.latest.revision: 93
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1c1eae99587a1f447b809becee9509d5a04136e3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="system-requirements-for-the-microsoft-drivers-for-php-for-sql-server"></a>Requisitos del sistema para los controladores de Microsoft para PHP para SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este documento enumeran los componentes que deben instalarse en el sistema para obtener acceso a datos en un SQL Server o base de datos de SQL Azure usando el [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].

Las versiones 3.1 o posterior de los controladores de PHP de Microsoft para SQL Server son compatibles oficialmente. Para obtener detalles completos sobre los ciclos de vida de soporte técnico y requisitos, incluidas las versiones anteriores de los controladores PHP, consulte el [matriz de compatibilidad](../../connect/php/microsoft-php-drivers-for-sql-server-support-matrix.md).

## <a name="php"></a>PHP

Para obtener información acerca de cómo descargar e instalar los binarios PHP estables más recientes, consulte [el sitio web PHP](http://php.net).  Drivers de Microsoft para PHP para SQL Server requieren las siguientes versiones de PHP:

|PHP para la versión del controlador de SQL Server&#8594;<br />&#8595;Versión de PHP|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|
|7.2|7.2.1+ en Windows<br/>7.2.0+ en otras plataformas | | | | |
|7.1|7.1.0+ |7.1.0+ |       |        |        |
|7.0|7.0.0+ |7.0.0+ |7.0.0+ |        |        |
|5.6|       |       |       |5.6.4  |        |
|5.5|       |       |       |5.5.16 |5.5.16 |
|5.4|       |       |       |5.4.32  |5.4.32  |

-   En el directorio de extensión PHP debe haber una versión del archivo de controlador. Vea [versiones del controlador](#driver-versions) para obtener información acerca de los archivos de controlador diferente.  Para descargar los controladores, consulte [descargar Microsoft Drivers for PHP for SQL Server](download-drivers-php-sql-server.md). Para obtener información sobre cómo configurar el controlador para PHP, consulte [Loading the Microsoft Drivers for PHP para SQL Server](../../connect/php/loading-the-php-sql-driver.md).

-   Se requiere un servidor web. El servidor web debe estar configurado para ejecutar PHP. Para obtener información sobre el hospedaje de aplicaciones PHP con IIS, consulte la [tutorial en el sitio de web de PHP](http://php.net/manual/fa/install.windows.iis.php).  

    El [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] se han probado utilizando IIS 10 con FastCGI.  

    > [!NOTE]  
    > Microsoft solo proporciona compatibilidad con IIS.  

## <a name="odbc-driver"></a>Controlador ODBC

Se requiere la versión correcta de Microsoft ODBC Driver for SQL Server en el equipo en el que se está ejecutando PHP. Descargue uno de los siguientes vínculos:
- [Microsoft ODBC Driver 17 para SQL Server](https://www.microsoft.com/en-us/download/details.aspx?id=56567)
- [Microsoft ODBC Driver 13.1 for SQL Server](https://www.microsoft.com/en-us/download/details.aspx?id=53339)
- [Microsoft ODBC Driver 13 for SQL Server](https://www.microsoft.com/download/details.aspx?id=50420)
- [Microsoft ODBC Driver 11 for SQL Server](http://www.microsoft.com/download/details.aspx?id=36434)

Si usas un sistema operativo de 64 bits, el instalador de ODBC de 64 bits instala a controladores ODBC de 32 bits y 64 bits. Si utiliza un sistema operativo de 32 bits, utilice ODBC x86 instalador.

|PHP para la versión del controlador de SQL Server&#8594;<br />&#8595;Versión del controlador ODBC|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|
|Controlador ODBC 17  |S| | | | |
|ODBC Driver 13.1|S|S|S| | |
|ODBC Driver 13  | | |S| | |
|Controlador ODBC 11  |S|S|S|S|S|

Si está utilizando el controlador SQLSRV, [sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md) devuelve información acerca de qué versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Microsoft ODBC Driver para SQL Server está siendo utilizado por el [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Si está utilizando el controlador PDO_SQLSRV, puede usar [PDO:: GetAttribute](../../connect/php/pdo-getattribute.md) para detectar la versión.  

## <a name="sql-server"></a>SQL Server

Se admiten bases de datos de SQL Azure. Para obtener información, consulte [conectarse a la base de datos de Microsoft Azure SQL](../../connect/php/connecting-to-microsoft-azure-sql-database.md).

|PHP para la versión del controlador de SQL Server&#8594;<br />&#8595;Versión de SQL Server|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|
|Instancia administrada de SQL Azure<br/> (Vista previa privada extendido)|S|S| | | |
|Almacenamiento de datos SQL de Azure|S|S| | | |
|SQL Server 2017   |S|S| | | |
|SQL Server 2016   |S|S|S| | |
|SQL Server 2014   |S|S|S|S|S|
|SQL Server 2012   |S|S|S|S|S|
|SQL Server 2008 R2|S|S|S|S|S|
|SQL Server 2008   | | |S|S|S|

## <a name="operating-systems"></a>Sistemas operativos
Sistemas operativos compatibles con las versiones del controlador son los siguientes:

|PHP para la versión del controlador de SQL Server&#8594;<br />&#8595;Sistema operativo|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|
|Windows Server 2016                      |S|S| | | |
|Windows Server 2012 R2                   |S|S|S|S|S|
|Windows Server 2012                      |S|S|S|S|S|
|Windows Server 2008 R2 SP1               | | |S|S|S|
|Windows Server 2008 SP2                  | | |S|S|S|
|Windows 10                               |S|S|S| | |
|Windows 8.1                              |S|S|S|S|S|
|Windows 8                                | |S|S|S|S|
|Windows 7 SP1                            | | |S|S|S|
|Windows Vista SP2                        | | |S|S|S|
|Ubuntu 17.10 (64 bits)                    |S| | | | |
|Ubuntu 16.04 (64 bits)                    |S|S|S| | |
|Ubuntu 15.10 (64 bits)                    | |S| | | |
|Ubuntu 15.04 (64 bits)                    | | |S| | |
|Debian 9 (64 bits)                        |S| | | | |
|Debian 8 (64 bits)                        |S|S| | | |
|Red Hat Enterprise Linux 7 (64 bits)      |S|S|S| | |
|Linux SuSE Enterprise 12 (64 bits)        |S| | | | |
|macOS Sierra (64 bits)                    |S|S| | | |
|macOS El capitán (64 bits)                |S|S| | | |

## <a name="driver-versions"></a>Versiones del controlador  
Esta sección enumeran los archivos del controlador que se incluyen con cada versión de la [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Cada paquete de instalación contiene los archivos de controlador SQLSRV y PDO_SQLSRV en variantes uniproceso y no un subproceso. En Windows, también están disponibles en las variantes de 32 bits y 64 bits. Para configurar el controlador para su uso con el tiempo de ejecución PHP, siga las instrucciones de instalación de [Loading the Microsoft Drivers for PHP para SQL Server](../../connect/php/loading-the-php-sql-driver.md).

En versiones compatibles de Linux y Mac OS, se pueden instalar los controladores apropiados mediante el sistema de paquetes PECL de PHP, siga el [las instrucciones de instalación de Linux y Mac OS](../../connect/php/installation-tutorial-linux-mac.md). Como alternativa, puede descargar archivos binarios creada previamente para su plataforma de la [Microsoft Drivers for PHP para SQL Server](https://github.com/Microsoft/msphpsql/releases) página de proyecto de Github: las tablas siguientes muestran los archivos se encuentran en los paquetes binarios creada previamente.

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
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|no |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|sí|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|no |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|sí|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|no |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|sí|

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
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|no |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|sí|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|no |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|sí|  

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
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|no |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|sí|

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

**Controladores de Microsoft 3.1 para PHP para SQL Server:**  

En Windows, se incluyen las siguientes versiones del controlador:

|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|Uso con PHP.dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|no|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|sí|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|no|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|sí|php5ts.dll|  

## <a name="see-also"></a>Vea también  
[Introducción a los controladores de Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Programación de guía para los controladores de Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Referencia de API del controlador PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
