---
title: Notas de la versión de los controladores de Microsoft para PHP para SQL Server | Documentos de Microsoft
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- what's new in version 1.1
ms.assetid: 91cca3d2-ba99-4a6d-b0de-beb9699cb3f8
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6fc3b3b4e815aaa5dba9d49e90ce7e2a4774c2a9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="release-notes-for-the-microsoft-drivers-for-php-for-sql-server"></a>Notas de la versión de los controladores de Microsoft para PHP para SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Esta página describe las características agregadas en cada versión de la [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  

## <a name="whats-new-in-version-52"></a>¿Qué es nuevo en la versión 5.2

- Compatibilidad con PHP 7.2.1 y de seguridad en Windows y 7.2.0 y hasta en otras plataformas
- Soporte técnico de Microsoft ODBC Driver 17
  - Versión 17 es ahora el predeterminado en todas las plataformas
- Compatibilidad con Linux Suse Enterprise 12, 9 Debian y Ubuntu 17.10
- Quita la compatibilidad para Ubuntu 15.10
- Compatibilidad con Always Encrypted con las funcionalidades CRUD en Windows. Para obtener más información, vea [usar Always Encrypted con los controladores de PHP para SQL Server](../../connect/php/using-always-encrypted-php-drivers.md)
  - Soporte técnico para el almacén de certificados de Windows
  - Always Encrypted solo es compatible con Microsoft ODBC Driver 17 y versiones posteriores
- Compatibilidad con configuraciones regionales no UTF8 en Linux y Mac OS
  - Configuraciones regionales no UTF8 en Linux y Mac OS sólo son compatibles con Microsoft ODBC Driver 17 y versiones posteriores
- Compatibilidad con almacenamiento de datos SQL Azure
- Compatibilidad con la instancia administrada de SQL Azure (vista previa privada extendido)


## <a name="whats-new-in-version-43"></a>¿Qué es nuevo en la versión 4.3

- Compatibilidad con PHP 7.1
- Compatibilidad con macOS Sierra y macOS El capitán
- Compatibilidad con Ubuntu 15.10 y Debian 8
- Quita la compatibilidad para Ubuntu 15.04
- Compatibilidad con grupos de disponibilidad de AlwaysOn por medio de resolución de IP de red transparente. Para obtener más información, consulte [Connection Options](../../connect/php/connection-options.md).
- Ha agregado compatibilidad para el tipo de datos sql_variant con limitación.
- Compatibilidad de resistencia de conexión inactiva en Windows. Para obtener más información, consulte [Connection Options](../../connect/php/connection-options.md).
- Compatibilidad con Linux y macOS de agrupación de conexiones. Para obtener más información, consulte [agrupación de conexiones](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md).
- Compatibilidad con la autenticación de Azure Active Directory con ActiveDirectoryPassword y SqlPassword. Para obtener más información, consulte [Connection Options](../../connect/php/connection-options.md).

## <a name="whats-new-in-version-40"></a>Novedades de la versión 4.0

- Compatibilidad con PHP 7.0  
- Compatibilidad con 64 bits
- Compatibilidad con Ubuntu 15.04, Ubuntu 16.04 y RedHat 7

## <a name="whats-new-in-version-32"></a>Novedades de la versión 3.2

- Admite PHP 5.6.   
- Incluye las actualizaciones más recientes para las versiones anteriores de PHP 5.5 y 5.4.   
- Requiere Microsoft ODBC Driver 11 para SQL Server  

## <a name="whats-new-in-version-31"></a>Novedades de la versión 3.1

- Admite PHP 5.5.  
- Requiere Microsoft ODBC Driver 11 para SQL Server. Las versiones anteriores requerían SQL Native Client.  

## <a name="whats-new-in-version-30"></a>Novedades de la versión 3.0  

- Admite PHP 5.4.  PHP 5.2 no es compatible con la versión 3 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
- Se agrega la opción de conexión AttachDBFileName. Para obtener más información, consulte [Connection Options](../../connect/php/connection-options.md).  
- Admite LocalDB, que se agregó en [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]. Para obtener más información, consulte [admite LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md).
- Se agrega la opción de conexión AttachDBFileName. Para obtener más información, consulte [Connection Options](../../connect/php/connection-options.md).  
- Admite las características de alta disponibilidad y recuperación ante desastres. Para obtener más información, consulte [compatibilidad con alta disponibilidad, recuperación ante desastres](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).
- Admite cursores de cliente (almacenamiento en caché de un conjunto de resultados en memoria). Para obtener más información, consulte [tipos de Cursor &#40;controlador SQLSRV&#41; ](../../connect/php/cursor-types-sqlsrv-driver.md) y [tipos de Cursor &#40;controlador PDO_SQLSRV&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).
- Se ha agregado el atributo PDO::ATTR_EMULATE_PREPARES. Para obtener más información, consulte [PDO:: Prepare](../../connect/php/pdo-prepare.md).  

## <a name="whats-new-in-version-20"></a>Novedades de la versión 2.0  
En la versión 2.0, se ha agregado la compatibilidad con el controlador PDO_SQLSRV. Para obtener más información, vea [Referencia del controlador PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md).  

## <a name="see-also"></a>Vea también  
[Información general sobre controladores de Microsoft para PHP para SQL Server](../../connect/php/overview-of-the-php-sql-driver.md)
