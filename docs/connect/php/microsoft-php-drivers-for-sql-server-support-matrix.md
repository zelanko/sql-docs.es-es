---
title: Matriz de soporte de controladores de Microsoft para PHP para SQL Server | Documentos de Microsoft
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
caps.latest.revision: 1
author: David-Engel
ms.author: v-daveng
manager: ''
ms.openlocfilehash: b8f1fad66e906b71ff5ea247ba4615e7be774f63
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-php-drivers-for-sql-server-support-matrix"></a>Controladores de Microsoft para PHP para la matriz de compatibilidad SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

  Esta página contiene la directiva de ciclo de vida de matriz y soporte técnico de soporte técnico para los controladores de PHP de Microsoft para SQL Server.

## <a name="microsoft-php-drivers-support-lifecycle-matrix-and-policy"></a>Matriz de ciclo de vida de soporte de controladores de Microsoft para PHP y directiva
 La directiva de ciclo de vida de soporte de Microsoft (MSL) proporciona información transparente y predecible sobre el ciclo de vida de soporte de productos de Microsoft. Versiones de controladores de PHP 3.x, 4.x y 5.x tienen cinco años de soporte técnico principal desde la fecha de lanzamiento del controlador. El soporte estándar se define en el [sitio Web del ciclo de vida de soporte técnico de Microsoft](https://support.microsoft.com/lifecycle).

 Opciones de soporte extendido y personalizado no están disponibles para los controladores de PHP de Microsoft.

 Se admiten los siguientes controladores de PHP de Microsoft, hasta la fecha de finalización del soporte indicada.

|Nombre del controlador|Versión del paquete de controladores|Finalización del soporte estándar|
|-|-|-|
|Controladores de Microsoft para PHP 5.2 para SQL Server|5.2|9 de febrero de 2023|
|4.3 de controladores de Microsoft para PHP para SQL Server|4.3|6 de julio de 2022|
|Controladores de Microsoft para PHP 4.0 para SQL Server|4.0|11 de julio de 2021|
|3.2 de controladores de Microsoft para PHP para SQL Server|3.2|9 de marzo de 2020|
|3.1 de controladores de Microsoft para PHP para SQL Server|3.1|12 de diciembre de 2019|

 Ya no se admiten los siguientes controladores de PHP de Microsoft.

|Nombre del controlador|Versión del paquete de controladores|Finalización del soporte estándar|
|-|-|-|
|Controladores 3.0 de Microsoft para PHP para SQL Server|3.0|6 de marzo de 2017|
|Controladores de Microsoft para PHP 2.0 para SQL Server|2.0|10 de agosto de 2015|
|Controladores de Microsoft para PHP 1.0 para SQL Server|1,0|28 de abril de 2014|

## <a name="sql-server-version-certified-compatibility"></a>Compatibilidad de certificados de versión SQL Server
 La matriz siguiente enumera las versiones de SQL Server que se han probado y certificadas como compatibles con la versión del controlador correspondiente. Nos esforzamos por mantener la compatibilidad con versiones anteriores del controlador, pero solo los controladores más recientes compatibles se prueban y se certifican con nuevas versiones de SQL Server cuando SQL Server se publica.

|PHP para la versión del controlador de SQL Server&#8594;<br />&#8595;Versión de SQL Server|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|Instancia administrada de SQL Azure<br/> (Vista previa privada extendido)|S|S| | | | | |
|Almacenamiento de datos SQL de Azure|S|S| | | | | |
|SQL Server 2017   |S|S| | | | | |
|SQL Server 2016   |S|S|S| | | | |
|SQL Server 2014   |S|S|S|S|S| | |
|SQL Server 2012   |S|S|S|S|S|S| |
|SQL Server 2008 R2|S|S|S|S|S|S|S|
|SQL Server 2008   | | |S|S|S|S|S|

## <a name="php-version-support"></a>Compatibilidad con la versión PHP
 Se admiten las siguientes versiones de PHP con la versión de la lista de los controladores de PHP de Microsoft:

|PHP para la versión del controlador de SQL Server&#8594;<br />&#8595;Versión de PHP|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|7.2|7.2.1+ en Windows<br/>7.2.0+ en otras plataformas| | | | | | |
|7.1|7.1.0+ |7.1.0+ |       |        |        |        |        |
|7.0|7.0.0+ |7.0.0+ |7.0.0+ |        |        |        |        |
|5.6|       |       |       |5.6.4  |        |        |        |
|5.5|       |       |       |5.5.16 |5.5.16 |        |        |
|5.4|       |       |       |5.4.32  |5.4.32  |5.4.32  |        |
|5.3|       |       |       |        |        |5.3.0   |5.3.0   |
|5.2|       |       |       |        |        |        |5.2.4<br />5.2.13|

## <a name="supported-operating-systems"></a>Sistemas operativos admitidos
 Las siguientes versiones de sistema operativo de Windows son compatibles con la versión de la lista de los controladores de PHP de Microsoft:

|PHP para la versión del controlador de SQL Server&#8594;<br />&#8595;Sistema operativo|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|Windows Server 2016                 |S  |S  |   |   |   |   |   |
|Windows Server 2012 R2              |S  |S  |S  |S  |S  |   |   |
|Windows Server 2012                 |S  |S  |S  |S  |S  |   |   |
|Windows Server 2008 R2 SP1          |   |   |S  |S  |S  |S  |   |
|Windows Server 2008 R2              |   |   |   |   |   |   |S  |
|Windows Server 2008 SP2             |   |   |S  |S  |S  |S  |   |
|Windows Server 2008                 |   |   |   |   |   |   |S  |
|Windows Server 2003 SP1             |   |   |   |   |   |   |S  |
|Windows 10                          |S  |S  |S  |   |   |   |   |
|Windows 8.1                         |S  |S  |S  |S  |S  |   |   |
|Windows 8                           |   |S  |S  |S  |S  |   |   |
|Windows 7 SP1                       |   |   |S  |S  |S  |S  |   |
|Windows Vista SP2                   |   |   |S  |S  |S  |S  |S  |
|Windows XP SP3                      |   |   |   |   |   |   |S  |

 Los siguientes Linux y Mac (solo 64 bits) de versiones de sistema operativo son compatibles con la versión de la lista de los controladores de PHP de Microsoft:

|PHP para la versión del controlador de SQL Server&#8594;<br />&#8595;Sistema operativo|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|Ubuntu 17.10 (64 bits)               |S  |   |   |   |   |   |   |
|Ubuntu 16.04 (64 bits)               |S  |S  |S  |   |   |   |   |
|Ubuntu 15.10 (64 bits)               |   |S  |   |   |   |   |   |
|Ubuntu 15.04 (64 bits)               |   |   |S  |   |   |   |   |
|Debian 9 (64 bits)                   |S  |   |   |   |   |   |   |
|Debian 8 (64 bits)                   |S  |S  |   |   |   |   |   |
|Red Hat Enterprise Linux 7 (64 bits) |S  |S  |S  |   |   |   |   |
|Linux SuSE Enterprise 12 (64 bits)   |S  |   |   |   |   |   |   |
|macOS Sierra (64 bits)               |S  |S  |   |   |   |   |   |
|macOS El capitán (64 bits)           |S  |S  |   |   |   |   |   |

## <a name="see-also"></a>Vea también  
[Notas de la versión](../../connect/php/release-notes-for-the-php-sql-driver.md)

[Recursos de soporte técnico](../../connect/php/support-resources-for-the-php-sql-driver.md)

[Requisitos del sistema](../../connect/php/system-requirements-for-the-php-sql-driver.md)
