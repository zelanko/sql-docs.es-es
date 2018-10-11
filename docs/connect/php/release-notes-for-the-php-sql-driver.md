---
title: Notas de la versión de los controladores de Microsoft para PHP para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 07/20/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- what's new in version 1.1
ms.assetid: 91cca3d2-ba99-4a6d-b0de-beb9699cb3f8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a22e88aef13c86179dc4cea71ed1003eadfd8661
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47624063"
---
# <a name="release-notes-for-the-microsoft-drivers-for-php-for-sql-server"></a>Notas de la versión de los controladores de Microsoft para PHP para SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Esta página describe las nuevas funciones de cada versión de la [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  

## <a name="whats-new-in-version-53"></a>Novedades de la versión 5.3

- Soporte técnico para Microsoft ODBC Driver 17.2 en todas las plataformas
- Compatibilidad con macOS High Sierra (requiere ODBC Driver 17 y versiones posteriores)
- Compatibilidad con Azure Key Vault para Always Encrypted para funcionalidades CRUD básicas tales que la característica Always Encrypted está disponible para todos admite las plataformas Windows, Linux o macOS [uso de Always Encrypted con los controladores de PHP para SQL Server](../../connect/php/using-always-encrypted-php-drivers.md)
- Compatibilidad con Ubuntu 18.04 LTS (requiere ODBC Driver 17.2)
- Compatibilidad con la resistencia de conexión en Linux o macOS también (requiere ODBC Driver 17.2)

## <a name="whats-new-in-version-52"></a>Novedades de la versión 5.2

- Compatibilidad con PHP 7.2.1 y hasta en Windows y 7.2.0 y hasta en otras plataformas
- Soporte técnico de Microsoft ODBC Driver 17
  - Versión 17 ahora es el valor predeterminado en todas las plataformas
- Compatibilidad con Ubuntu con 17.10, Debian 9 y Enterprise de Suse Linux 12
- Quita la compatibilidad para 15.10 de Ubuntu
- Compatibilidad con Always Encrypted con funcionalidades CRUD en Windows. Para obtener más información, consulte [uso de Always Encrypted con los controladores de PHP para SQL Server](../../connect/php/using-always-encrypted-php-drivers.md)
  - Compatibilidad con Windows Certificate Store
  - Always Encrypted solo es compatible con Microsoft ODBC Driver 17 y versiones posteriores
- Compatibilidad con configuraciones regionales que no sean UTF8 en Linux y macOS
  - Solo se admiten configuraciones regionales que no sean UTF8 en Linux y macOS con Microsoft ODBC Driver 17 y versiones posteriores
- Compatibilidad con Azure SQL Data Warehouse
- Compatibilidad con instancia administrada de SQL Azure (versión preliminar privada extendida)


## <a name="whats-new-in-version-43"></a>Novedades de la versión 4.3

- Compatibilidad con PHP 7.1
- Compatibilidad con macOS Sierra y macOS El capitán
- Compatibilidad con Ubuntu 15.10 y Debian 8
- Quita la compatibilidad para Ubuntu 15.04
- Compatibilidad con grupos de disponibilidad Always On a través de la resolución de direcciones IP de red transparente. Para obtener más información, consulte [Connection Options](../../connect/php/connection-options.md).
- Se agregó compatibilidad para el tipo de datos sql_variant con limitación.
- Soporte técnico de la resistencia de conexión inactiva en Windows. Para obtener más información, consulte [Connection Options](../../connect/php/connection-options.md).
- Compatibilidad con Linux y macOS de agrupación de conexiones. Para obtener más información, vea [Connection Pooling](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md) (Agrupación de conexiones).
- Compatibilidad con autenticación de Azure Active Directory con ActiveDirectoryPassword y SqlPassword. Para obtener más información, consulte [Connection Options](../../connect/php/connection-options.md).

## <a name="whats-new-in-version-40"></a>Novedades de la versión 4.0

- Compatibilidad con PHP 7.0  
- Compatibilidad con 64 bits
- Compatibilidad con Ubuntu 15.04, Ubuntu 16.04 y Red Hat 7

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
- Admite las características de alta disponibilidad y recuperación ante desastres. Para obtener más información, consulte [compatibilidad con alta disponibilidad, recuperación ante desastres](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).
- Admite cursores de cliente (almacenamiento en caché de un conjunto de resultados en memoria). Para obtener más información, vea [Cursor Types &#40;SQLSRV Driver&#41; (Tipos de cursor &#40;Controlador SQLSRV&#41;)](../../connect/php/cursor-types-sqlsrv-driver.md) y [Cursor Types &#40;PDO_SQLSRV Driver&#41; (Tipos de cursor &#40;Controlador PDO_SQLSRV&#41;)](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).
- Se ha agregado el atributo PDO::ATTR_EMULATE_PREPARES. Para obtener más información, vea [PDO::prepare](../../connect/php/pdo-prepare.md).  

## <a name="whats-new-in-version-20"></a>Novedades de la versión 2.0  
En la versión 2.0, se ha agregado la compatibilidad con el controlador PDO_SQLSRV. Para obtener más información, vea [Referencia del controlador PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md).  

## <a name="see-also"></a>Ver también  
[Información general de los controladores de Microsoft para PHP para SQL Server](../../connect/php/overview-of-the-php-sql-driver.md)
