---
title: Requisitos del sistema para el controlador SQL para PHP | Documentos de Microsoft
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: requirements
ms.assetid: 5db4b75f-c605-4785-9560-399a533c0fc9
caps.latest.revision: "93"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: abff6843dbf1b8f1362f10dbf2fe52fa5f686515
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="system-requirements-for-the-php-sql-driver"></a>Requisitos del sistema para el controlador SQL para PHP
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Para obtener acceso a datos en un SQL Server o base de datos de SQL Azure usando el [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], debe tener los siguientes componentes instalados en el equipo:  
  
-   PHP es necesario. Para obtener información acerca de cómo descargar e instalar los archivos binarios estables más recientes, consulte [http://php.net](http://go.microsoft.com/fwlink/?LinkId=101876).  Drivers de Microsoft para PHP para SQL Server requieren las siguientes versiones:
  
|Controladores de Microsoft para PHP para SQL Server|Versiones compatibles de PHP|  
|----------------------------------------------------|--------------------------|  
|4.3|PHP 7.0 y 7.1 de PHP| 
|4.0|PHP 7.0|  
|3.2|PHP 5.6.4 (o superior) o<br /><br />PHP 5.5.16 (o superior) o<br /><br />PHP 5.4.32|  
|3.1|PHP 5.5.16 (o superior) o<br /><br />PHP 5.4.32|  
|3.0|PHP 5.4.32 o<br /><br />PHP 5.3.0|  
|2,0|PHP 5.3.0 o<br /><br />PHP 5.2.4 o<br /><br />PHP 5.2.13|  
  
-   En el directorio de extensión PHP debe haber una versión del archivo de controlador. Consulte la sección Versiones del controlador, que encontrará más adelante en este tema, para obtener información sobre los diferentes archivos de controlador. Vea [Carga del controlador SQL para PHP](../../connect/php/loading-the-php-sql-driver.md)  para obtener información sobre cómo configurar el controlador para el tiempo de ejecución de PHP. Para descargar los controladores, consulte [Controladores de Microsoft para PHP para SQL Server](http://www.microsoft.com/download/details.aspx?id=20098).  
  
-   Se requiere un servidor web. El servidor web debe estar configurado para ejecutar PHP. Para obtener información sobre el hospedaje de aplicaciones PHP con Internet Information Services (IIS) 6.0, vea [Using FastCGI to Host PHP Applications on IIS 6.0](http://go.microsoft.com/fwlink/?LinkId=117131). Para obtener información sobre el hospedaje de aplicaciones PHP con IIS 7.0, consulte [Using FastCGI to Host PHP Applications on IIS 7.0](http://go.microsoft.com/fwlink/?LinkId=117132)(Uso de FastCGI para hospedar aplicaciones PHP en IIS 7.0).  
  
    Los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] se han probado utilizando IIS 6 e IIS 7 con FastCGI.  
  
    > [!NOTE]  
    > Microsoft solo proporciona compatibilidad con IIS.  
  
-   Se requiere la versión correcta de Microsoft ODBC Driver for SQL Server o SQL Server Native Client en el equipo donde se está ejecutando PHP.  Si usas un sistema operativo de 64 bits, el instalador de ODBC de 64 bits instala a controladores ODBC de 32 bits y 64 bits. Si utiliza un sistema operativo de 32 bits, utilice ODBC x86 instalador.

|Controladores de Microsoft para PHP para SQL Server|Versión del controlador ODBC de Microsoft para SQL Server o SQL Server Native Client|  
|----------------------------------------------------|--------------------------|
|4.3|Microsoft ODBC Driver 11 for SQL Server o Microsoft ODBC Driver 13.1 for SQL Server. Para descargar el controlador ODBC de Microsoft, consulte el [Microsoft ODBC Driver 11 para la página de SQL Server](http://www.microsoft.com/download/details.aspx?id=36434) o [Microsoft ODBC Driver 13.1 para página de SQL Server](https://www.microsoft.com/en-us/download/details.aspx?id=53339)|    
|4.0|Microsoft ODBC Driver 11 for SQL Server o Microsoft ODBC Driver 13 for SQL Server. Para descargar el controlador ODBC de Microsoft, consulte el [Microsoft ODBC Driver 11 para la página de SQL Server](http://www.microsoft.com/download/details.aspx?id=36434) o [Microsoft ODBC Driver 13 para la página de SQL Server](https://www.microsoft.com/download/details.aspx?id=50420)|  
|3.2 o <br><br> 3.1|Microsoft ODBC Driver 11 for SQL Server. Para descargar el controlador ODBC de Microsoft, consulte el [Microsoft ODBC Driver 11 para la página de SQL Server](http://www.microsoft.com/download/details.aspx?id=36434)|   
|3.0|Microsoft [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Native Client. Puede descargar Microsoft [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Native Client en la [página del paquete de características de SQL Server 2012](http://go.microsoft.com/fwlink/?LinkID=236805)| 
|2,0|Microsoft [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro_md.md)] Native Client:<br /><br />[Paquete de descarga el X86](http://go.microsoft.com/fwlink/?LinkID=188400&clcid=0x409) para los sistemas operativos de 32 bits <br /><br />[Paquete de descarga el X64](http://go.microsoft.com/fwlink/?LinkID=188401&clcid=0x409) para los sistemas operativos de 64 bits|  

  
Si está utilizando el controlador SQLSRV, [sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md) devuelve información acerca de qué versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Native Client o Microsoft ODBC Driver para SQL Server se está usando por la [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Si está utilizando el controlador PDO_SQLSRV, puede usar [PDO:: GetAttribute](../../connect/php/pdo-getattribute.md) para detectar la versión.  



## <a name="database-versions"></a>Versiones de la base de datos
-   Se admiten bases de datos de SQL Azure. Para obtener información, consulte [conectarse a la base de datos de Microsoft Azure SQL](../../connect/php/connecting-to-microsoft-azure-sql-database.md). 

- [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]versión 4.3 admite SQL Server 2008 R2 y versiones posteriores
- [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]compatibilidad con la versión 4.0 SQL Server 2008 y versiones posterior
- [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]compatibilidad con la versión 3.1 SQL Server 2008 y versiones posterior
- [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]compatibilidad con la versión 2.0 y 3.0 SQL Server 2005 y versiones posterior


## <a name="driver-versions"></a>Versiones del controlador  
En esta sección se enumera los controladores que se incluyen con cada versión de la [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
Para configurar el controlador para su uso con el tiempo de ejecución PHP, siga las instrucciones de instalación de [carga del controlador de SQL de PHP](../../connect/php/loading-the-php-sql-driver.md).  
  
**Controladores de Microsoft 4.3 para PHP para SQL Server:**  

En Windows, para 4.3 están instaladas las siguientes versiones del controlador:
  
|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|Uso con PHP.dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br /><br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|no|php7.dll de 32 bits| 
|php_sqlsrv_7_ts_x86.dll<br /><br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|sí|php7ts.dll de 32 bits| 
|php_sqlsrv_7_nts_x64.dll<br /><br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|no|php7.dll de 64 bits|  
|php_sqlsrv_7_ts_x64.dll<br /><br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|sí|php7ts.dll de 64 bits| 
|php_sqlsrv_71_nts_x86.dll<br /><br />php_pdo_sqlsrv_71_nts_x86.dll|7.1|no|php7.dll de 32 bits|  
|php_sqlsrv_71_ts_x86.dll<br /><br />php_pdo_sqlsrv_71_ts_x86.dll|7.1|sí|php7ts.dll de 32 bits|  
|php_sqlsrv_71_nts_x64.dll<br /><br />php_pdo_sqlsrv_71_nts_x64.dll|7.1|no|php7.dll de 64 bits|  
|php_sqlsrv_71_ts_x64.dll<br /><br />php_pdo_sqlsrv_71_ts_x64.dll|7.1|sí|php7ts.dll de 64 bits|   
  
**Controladores de Microsoft 4.0 para PHP para SQL Server:**  

En Windows, para la versión 4.0 se instalan las siguientes versiones del controlador:
  
|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|Uso con PHP.dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br /><br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|no|php7.dll de 32 bits|  
|php_sqlsrv_7_ts_x86.dll<br /><br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|sí|php7ts.dll de 32 bits|  
|php_sqlsrv_7_nts_x64.dll<br /><br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|no|php7.dll de 64 bits|  
|php_sqlsrv_7_ts_x64.dll<br /><br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|sí|php7ts.dll de 64 bits|   
  
En las versiones admitidas de Linux, se puede instalar la versión adecuada de sqlsrv o pdo_sqlsrv con el sistema de paquetes PECL de PHP. 
  
**La versión 3.2 de los controladores de Microsoft para PHP para SQL Server instala las siguientes versiones del controlador:**  
  
|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|Uso con PHP.dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br /><br />php_pdo_sqlsrv_54_nts.dll|5.4|no|php5.dll|  
|php_sqlsrv_54_ts.dll<br /><br />php_pdo_sqlsrv_54_ts.dll|5.4|sí|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br /><br />php_pdo_sqlsrv_55_nts.dll|5.5|no|php5.dll|  
|php_sqlsrv_55_ts.dll<br /><br />php_pdo_sqlsrv_55_ts.dll|5.5|sí|php5ts.dll|  
|php_sqlsrv_56_nts.dll<br /><br />php_pdo_sqlsrv_56_nts.dll|5.6|no|php5.dll|  
|php_sqlsrv_56_ts.dll<br /><br />php_pdo_sqlsrv_56_ts.dll|5.6|sí|php5ts.dll|  
  
**La versión 3.1 de los controladores de Microsoft para PHP para SQL Server instala las siguientes versiones del controlador:**  
  
|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|Uso con PHP.dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br /><br />php_pdo_sqlsrv_54_nts.dll|5.4|no|php5.dll|  
|php_sqlsrv_54_ts.dll<br /><br />php_pdo_sqlsrv_54_ts.dll|5.4|sí|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br /><br />php_pdo_sqlsrv_55_nts.dll|5.5|no|php5.dll|  
|php_sqlsrv_55_ts.dll<br /><br />php_pdo_sqlsrv_55_ts.dll|5.5|sí|php5ts.dll|  
  
**La versión 3.0 de los controladores de Microsoft para PHP para SQL Server instala las siguientes versiones del controlador:**  
  
|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|Uso con PHP.dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_53_nts.dll<br /><br />php_pdo_sqlsrv_53_nts.dll|5.3|no|php5.dll|  
|php_sqlsrv_53_ts.dll<br /><br />php_pdo_sqlsrv_53_ts.dll|5.3|sí|php5ts.dll|  
|php_sqlsrv_54_nts.dll<br /><br />php_pdo_sqlsrv_54_nts.dll|5.4|no|php5.dll|  
|php_sqlsrv_54_ts.dll<br /><br />php_pdo_sqlsrv_54_ts.dll|5.4|sí|php5ts.dll|  
  
**Controladores de Microsoft 2.0 para PHP para SQL Server instala las siguientes versiones del controlador:**  
  
|Archivo de controlador|Versión de PHP|¿Seguridad para subprocesos?|Uso con PHP.dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_53_nts_vc6.dll<br /><br />php_pdo_sqlsrv_53_nts_vc6.dll|5.3|no|php5.dll|  
|php_sqlsrv_53_nts_vc9.dll<br /><br />php_pdo_sqlsrv_53_nts_vc9.dll|5.3|no|php5.dll|  
|php_sqlsrv_53_ts_vc6.dll<br /><br />php_pdo_sqlsrv_53_ts_vc6.dll|5.3|sí|php5ts.dll|  
|php_sqlsrv_53_ts_vc9.dll<br /><br />php_pdo_sqlsrv_53_ts_vc9.dll|5.3|sí|php5ts.dll|  
|php_sqlsrv_52_nts_vc6.dll<br /><br />php_pdo_sqlsrv_52_nts_vc6.dll|5.2|no|php5.dll|  
|php_sqlsrv_52_ts_vc6.dll<br /><br />php_pdo_sqlsrv_52_ts_vc6.dll|5.2|sí|php5ts.dll|  
  
Si el nombre del archivo de controlador contiene "vc9", se debe utilizar con una versión de PHP compilada con Visual C++ 9.0.  
## <a name="operating-systems"></a>Sistemas operativos 
Sistemas operativos compatibles con las versiones del controlador son los siguientes:

-   4.3:
    -   Windows Server 2012  
    -   Windows Server 2012 R2
    -   Windows Server 2016 
    -   Windows 8  
    -   Windows 8.1   
    -   Windows 10
    -   Ubuntu 15.10 (64 bits)
    -   Ubuntu 16.04 (64 bits)
    -   Debian 8 (64 bits)
    -   Red Hat Enterprise Linux 7 (64 bits)
    -   Mac OS Sierra (64 bits)
    -   Mac OS El capitán (64 bits)
    
-   4.0:  
    -   Windows Server 2008 SP2
    -   Windows Server 2008 R2 SP1  
    -   Windows Server 2012  
    -   Windows Server 2012 R2  
    -   Windows Vista SP2  
    -   Windows 7 SP1  
    -   Windows 8  
    -   Windows 8.1   
    -   Windows 10 
    -   Ubuntu 15.04 (64 bits)
    -   Ubuntu 16.04 (64 bits)
    -   Red Hat Enterprise Linux 7 (64 bits)

 
-   3.2 y 3.1:  
    -   Windows Server 2008 R2 SP1  
    -   Windows Vista SP2  
    -   Windows Server 2008 SP2  
    -   Windows 7 SP1  
    -   Windows Server 2012  
    -   Windows Server 2012 R2  
    -   Windows 8  
    -   Windows 8.1  
  
  
-   3.0:  
    -   Windows Server 2008 R2 SP1  
    -   Windows Vista SP2  
    -   Windows Server 2008 SP2  
    -   Windows 7 SP1  


-   2.0:
    -   [!INCLUDE[winxpsvr](../../includes/winxpsvr_md.md)] Service Pack 1  
    -   Windows XP Service Pack 3  
    -   Windows Vista Service Pack 1 o posterior  
    -   Windows Server 2008  
    -   Windows Server 2008 R2  
    -   Windows 7  
  
## <a name="see-also"></a>Vea también  
[Introducción al controlador SQL para PHP](../../connect/php/getting-started-with-the-php-sql-driver.md)
[Guía de programación para el controlador SQL para PHP](../../connect/php/programming-guide-for-php-sql-driver.md)
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
  
