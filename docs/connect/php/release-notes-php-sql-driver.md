---
title: Notas de la versión de los controladores de Microsoft para PHP para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: v-dapugl, kenvh
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- what's new in version 1.1
ms.assetid: 91cca3d2-ba99-4a6d-b0de-beb9699cb3f8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 23ac53a8515f55dfc0cad282fd14294e5f285af9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935914"
---
# <a name="release-notes-for-the-microsoft-drivers-for-php-for-sql-server"></a>Notas de la versión de los controladores de Microsoft para PHP para SQL Server

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

En esta página se describe lo que se agregó en cada versión [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]de.  

<!--
Hello, We are standardizing the format of content inside our Release Notes (or What's New) articles.
Instead of bullets (or paragraphs), we have shifted to the 2-column format you see for H2 **What's New in Version 5.6**.
It is not necessary to reformat all the older H2 sections in this Release Notes file, but.....

Going forward, please be sure to use the 2-column format.

Also, all Release Notes .md file names now must begin with 'release-notes-*.md'.  And no filler words.
The 5.6 edition of this file is being renamed.....
FROM:  'release-notes-for-the-php-sql-driver.md'
TO  :  'release-notes-php-sql-driver.md'

For any questions, ask GeneMi or CraigG.
Thanks a lot.  2019-03-28  (DevO= 1467988)
-->

## <a name="whats-new-in-version-56"></a>Novedades de la versión 5.6

| Nuevo elemento | Detalles |
| :------- | :------ |
| Admite PHP 7.3. | &nbsp; |
| Se ha quitado la compatibilidad con PHP 7,0. | &nbsp; |
| Compatibilidad con Microsoft ODBC driver 17,3 en todas las plataformas. | &nbsp; |
| Compatibilidad con macOS Mojave. | Requiere el controlador ODBC 17,3 o superior. |
| Compatibilidad con Ubuntu 18,10 y SUSE Linux 15. | Ambos requieren el controlador ODBC 17,3 o superior. |
| Se ha quitado la compatibilidad con Linux Ubuntu 17,10 y macOS el Capitan. | &nbsp; |
| Compatibilidad con Azure AD token de acceso. | En Linux y macOS, requiere el controlador ODBC 17.2 + y unixODBC 2.3.6 +. |
| Compatibilidad con la autenticación con Azure AD mediante identidad administrada para recursos de Azure. | Requiere el controlador ODBC 17.3 +. |
| Nuevas funcionalidades de captura | &bull;&nbsp; Nueva marca PDO:: SQLSRV_ATTR_FETCHES_DATETIME_TYPE de pdo_sqlsrv para devolver DateTime como objetos.<br/><br/>&bull;&nbsp; Agregue la opción ReturnDatesAsStrings al nivel de instrucción para sqlsrv.<br/><br/>&bull;&nbsp; Nuevas opciones en los niveles de conexión y de instrucción para ambos Controladores para dar formato a los valores decimales en los resultados capturados. |
| Compatibilidad con la compilación estática de controladores si los usuarios deciden compilar desde el origen. | &nbsp; |
| Rendimiento mejorado al almacenar en caché los metadatos en las capturas y acelerar las conversiones de cadenas Unicode. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="whats-new-in-version-53"></a>Novedades de la versión 5.3

- Compatibilidad con Microsoft ODBC driver 17,2 en todas las plataformas
- Compatibilidad con macOS High Sierra (requiere ODBC driver 17 y versiones posteriores)
- Compatibilidad con Azure Key Vault para Always Encrypted de funcionalidades CRUD básicas, de modo que Always Encrypted característica está disponible para todas las plataformas compatibles con Windows, Linux o macOS [mediante Always Encrypted con los controladores php para SQL Server](../../connect/php/using-always-encrypted-php-drivers.md)
- Compatibilidad con Ubuntu 18,04 LTS (requiere el controlador ODBC 17,2)
- Compatibilidad con la resistencia de conexión en Linux o macOS también (requiere el controlador ODBC 17,2)

## <a name="whats-new-in-version-52"></a>Novedades de la versión 5.2

- Compatibilidad con PHP 7.2.1 y up en Windows, y 7.2.0 y en otras plataformas
- Compatibilidad con Microsoft ODBC driver 17
  - La versión 17 es ahora la predeterminada en todas las plataformas
- Compatibilidad con Ubuntu 17,10, Debian 9 y SuSE Enterprise Linux 12
- Se quitó la compatibilidad con Ubuntu 15,10
- Compatibilidad con Always Encrypted con funcionalidades CRUD en Windows. Para obtener más información, vea [Using Always Encrypted with the PHP Drivers for SQL Server](../../connect/php/using-always-encrypted-php-drivers.md) (Uso de Always Encrypted con los controladores PHP para SQL Server).
  - Compatibilidad con el almacén de certificados de Windows
  - Always Encrypted solo se admite con Microsoft ODBC driver 17 y versiones posteriores
- Compatibilidad con configuraciones regionales no UTF8 en Linux y macOS
  - Las configuraciones regionales no UTF8 en Linux y macOS solo se admiten con Microsoft ODBC driver 17 y versiones posteriores
- Compatibilidad con Azure SQL Data Warehouse
- Compatibilidad con Instancia administrada de Azure SQL (versión preliminar privada ampliada).

## <a name="whats-new-in-version-43"></a>Novedades de la versión 4.3

- Compatibilidad con PHP 7.1
- Compatibilidad con macOS Sierra y macOS el Capitan
- Compatibilidad con Ubuntu 15,10 y Debian 8
- Se quitó la compatibilidad con Ubuntu 15,04
- Compatibilidad con grupos de disponibilidad de Always On a través de la resolución de IP de red transparente. Para obtener más información, consulte [Connection Options](../../connect/php/connection-options.md).
- Compatibilidad agregada para el tipo de datos sql_variant con limitación.
- Compatibilidad con resistencia de conexión inactiva en Windows. Para obtener más información, consulte [Connection Options](../../connect/php/connection-options.md).
- Compatibilidad con la agrupación de conexiones para Linux y macOS. Para obtener más información, vea [Connection Pooling](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md) (Agrupación de conexiones).
- Compatibilidad con la autenticación de Azure Active Directory con ActiveDirectoryPassword y SqlPassword. Para obtener más información, consulte [Connection Options](../../connect/php/connection-options.md).

## <a name="whats-new-in-version-40"></a>Novedades de la versión 4.0

- Compatibilidad con PHP 7.0  
- Compatibilidad completa con 64 bits
- Compatibilidad con Ubuntu 15,04, Ubuntu 16,04 y RedHat 7

## <a name="whats-new-in-version-32"></a>Novedades de la versión 3.2

- Admite PHP 5.6.   
- Incluye las actualizaciones más recientes para las versiones anteriores de PHP 5.5 y 5.4.   
- Requiere Microsoft ODBC Driver 11 for SQL Server  

## <a name="whats-new-in-version-31"></a>Novedades de la versión 3.1

- Admite PHP 5.5.  
- Requiere Microsoft ODBC Driver 11 for SQL Server. Las versiones anteriores requerían SQL Native Client.  

## <a name="whats-new-in-version-30"></a>Novedades de la versión 3.0  

- Admite PHP 5.4.  PHP 5.2 no es compatible con la versión 3 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
- Se agrega la opción de conexión AttachDBFileName. Para obtener más información, consulte [Connection Options](../../connect/php/connection-options.md).  
- Compatibilidad con LocalDB, que se agregó en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Para obtener más información, consulte [compatibilidad con LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md).
- Se agrega la opción de conexión AttachDBFileName. Para obtener más información, consulte [Connection Options](../../connect/php/connection-options.md).  
- Admite las características de alta disponibilidad y recuperación ante desastres. Para más información, consulte [Compatibilidad con alta disponibilidad y recuperación ante desastres](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).
- Admite cursores de cliente (almacenamiento en caché de un conjunto de resultados en memoria). Para obtener más información, vea [Cursor Types &#40;SQLSRV Driver&#41; (Tipos de cursor &#40;Controlador SQLSRV&#41;)](../../connect/php/cursor-types-sqlsrv-driver.md) y [Cursor Types &#40;PDO_SQLSRV Driver&#41; (Tipos de cursor &#40;Controlador PDO_SQLSRV&#41;)](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).
- Se ha agregado el atributo PDO::ATTR_EMULATE_PREPARES. Para obtener más información, vea [PDO::prepare](../../connect/php/pdo-prepare.md).  

## <a name="whats-new-in-version-20"></a>Novedades de la versión 2.0

En la versión 2.0, se ha agregado la compatibilidad con el controlador PDO_SQLSRV. Para obtener más información, vea [Referencia del controlador PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md).  

## <a name="see-also"></a>Consulte también

[Información general de los controladores de Microsoft para PHP para SQL Server](../../connect/php/overview-of-the-php-sql-driver.md)
