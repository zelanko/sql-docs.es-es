---
title: Matriz de compatibilidad de controladores de Microsoft para PHP para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daveng
manager: ''
ms.openlocfilehash: ec5a151d79d9a66bfd65342336ad7aa3afcf567d
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744405"
---
# <a name="microsoft-php-drivers-for-sql-server-support-matrix"></a>Controladores de Microsoft para PHP para SQL Server Support Matrix
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

  Esta página contiene la matriz de compatibilidad y la directiva de ciclo de vida de soporte técnico de los controladores de Microsoft para PHP para SQL Server.

## <a name="microsoft-php-drivers-support-lifecycle-matrix-and-policy"></a>Matriz de ciclo de vida de compatibilidad de controladores de Microsoft para PHP y la directiva
 La directiva de ciclo de vida de soporte de Microsoft (MSL) proporciona información transparente y predecible sobre el ciclo de vida de soporte de productos de Microsoft. Las versiones 3.x, 4.x y 5.x de los controladores PHP incluyen cinco años de soporte técnico estándar del controlador a partir de la fecha de publicación. El soporte estándar se define en el [sitio web del ciclo de vida de soporte técnico de Microsoft](https://support.microsoft.com/lifecycle).

 Las opciones de soporte técnico extendido y personalizado no están disponibles para controladores de Microsoft para PHP.

 Se admiten los siguientes controladores de Microsoft para PHP hasta la fecha indicada de finalización del soporte técnico.

|Nombre del controlador|Versión del paquete de controladores|Finalización de soporte técnico|
|-|:-:|-|
|Controladores de Microsoft para PHP 5.6 para SQL Server|5.6|21 de febrero de 2024|
|Controladores de Microsoft para PHP 5.3 para SQL Server|5.3|20 de julio de 2023|
|Controladores de Microsoft para PHP 5.2 para SQL Server|5.2|9 de febrero de 2023|
|4.3 de controladores de Microsoft para PHP para SQL Server|4.3|6 de julio de 2022|
|Microsoft PHP Driver 4.0 for SQL Server|4.0|11 de julio de 2021|
|3.2 de controladores de Microsoft para PHP para SQL Server|3.2|9 de marzo de 2020|
|3.1 de controladores de Microsoft para PHP para SQL Server|3.1|12 de diciembre de 2019|

 Ya no se admiten los siguientes controladores de Microsoft para PHP.

|Nombre del controlador|Versión del paquete de controladores|Finalización de soporte técnico|
|-|:-:|-|
|Controladores 3.0 de Microsoft para PHP para SQL Server|3.0|6 de marzo de 2017|
|Controladores de Microsoft para PHP 2.0 para SQL Server|2.0|10 de agosto de 2015|
|Controladores de Microsoft para PHP 1.0 para SQL Server|1,0|28 de abril de 2014|

## <a name="sql-server-version-certified-compatibility"></a>Certificada de compatibilidad de versión de SQL Server
 La siguiente matriz enumera las versiones de SQL Server que se han probado y certificadas como compatibles con la versión del controlador correspondiente. Nos esforzamos por mantener la compatibilidad con versiones anteriores del controlador, pero solo el controlador más reciente compatible con se prueban y se certifican con nuevas versiones de SQL Server como SQL Server se libera.

|PHP para la versión del controlador de SQL Server&#8594;<br />&#8595; versión de SQL Server|5.6|5.3|5.2|4.3|4.0|3.2|3.1|3.0|2.0|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Instancia administrada de Azure SQL<br/> (Versión preliminar privada extendida)|S|S|S|S| | | | | |
|Almacenamiento de datos SQL de Azure|S|S|S|S| | | | | |
|SQL Server 2017         |S|S|S|S| | | | | |
|SQL Server 2016         |S|S|S|S|S| | | | |
|SQL Server 2014         |S|S|S|S|S|S|S| | |
|SQL Server 2012         |S|S|S|S|S|S|S|S| |
|SQL Server 2008 R2      |S|S|S|S|S|S|S|S|S|
|SQL Server 2008         | | | | |S|S|S|S|S|

## <a name="php-version-support"></a>Compatibilidad de versiones de PHP
 Se admiten las siguientes versiones de PHP con la versión de la lista de los controladores de PHP de Microsoft:

|PHP para la versión del controlador de SQL Server&#8594;<br />&#8595; versión de PHP|5.6|5.3|5.2|4.3|4.0|3.2|3.1|3.0|2.0|
|:---:|---|---|---|---|---|---|---|---|---|
|7.3|7.3.0+          |                |                |       |       | | | | |
|7.2|7.2+<sup>1</sup>|7.2+<sup>1</sup>|7.2+<sup>1</sup>|       |       | | | | |
|7.1|7.1.0+          |7.1.0+          |7.1.0+          |7.1.0+ |       |        |        |        |        |
|7.0|                |7.0.0+          |7.0.0+          |7.0.0+ |7.0.0+ |        |        |        |        |
|5.6|                |                |                |       |       |5.6.4+  |        |        |        |
|5.5|                |                |                |       |       |5.5.16+ |5.5.16+ |        |        |
|5.4|                |                |                |       |       |5.4.32  |5.4.32  |5.4.32  |        |
|5.3|                |                |                |       |       |        |        |5.3.0   |5.3.0   |
|5.2|                |                |                |       |       |        |        |        |5.2.4<br />5.2.13|

1. Versiones 7.2.1 y más adelante se admiten en Windows, mientras que las versiones 7.2.0 y versiones posteriores se admiten en Linux y macOS.

## <a name="supported-operating-systems"></a>Sistemas operativos admitidos
 Las siguientes versiones de sistema operativo Windows son compatibles con la versión de la lista de los controladores de PHP de Microsoft:

|PHP para la versión del controlador de SQL Server&#8594;<br />&#8595; sistema operativo|5.6|5.3|5.2|4.3|4.0|3.2|3.1|3.0|2.0|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Windows Server 2016                 |S  |S  |S  |S  |   |   |   |   |   |
|Windows Server 2012 R2              |S  |S  |S  |S  |S  |S  |S  |   |   |
|Windows Server 2012                 |S  |S  |S  |S  |S  |S  |S  |   |   |
|Windows Server 2008 R2 SP1          |   |   |   |   |S  |S  |S  |S  |   |
|Windows Server 2008 R2              |   |   |   |   |   |   |   |   |S  |
|Windows Server 2008 SP2             |   |   |   |   |S  |S  |S  |S  |   |
|Windows Server 2008                 |   |   |   |   |   |   |   |   |S  |
|Windows Server 2003 SP1             |   |   |   |   |   |   |   |   |S  |
|Windows 10                          |S  |S  |S  |S  |S  |   |   |   |   |
|Windows 8.1                         |S  |S  |S  |S  |S  |S  |S  |   |   |
|Windows 8                           |   |   |   |S  |S  |S  |S  |   |   |
|Windows 7 SP1                       |   |   |   |   |S  |S  |S  |S  |   |
|Windows Vista SP2                   |   |   |   |   |S  |S  |S  |S  |S  |
|Windows XP SP3                      |   |   |   |   |   |   |   |   |S  |

 Los siguientes Linux y Mac (solo 64 bits) de versiones de sistema operativo son compatibles con la versión de la lista de los controladores de PHP de Microsoft:

|PHP para la versión del controlador de SQL Server&#8594;<br />&#8595; sistema operativo|5.6|5.3|5.2|4.3|4.0|3.2|3.1|3.0|2.0|
|--|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Ubuntu 18.10 (64 bits)               |S  |   |   |   |   |   |   |   |   |
|Ubuntu 18.04 (64 bits)               |S  |S  |   |   |   |   |   |   |   |
|Con Ubuntu 17.10 (64 bits)               |   |S  |S  |   |   |   |   |   |   |
|Ubuntu 16.04 (64 bits)               |S  |S  |S  |S  |S  |   |   |   |   |
|Ubuntu 15.10 (64 bits)               |   |   |   |S  |   |   |   |   |   |
|Ubuntu 15.04 (64 bits)               |   |   |   |   |S  |   |   |   |   |
|Debian 9 (64 bits)                   |S  |S  |S  |   |   |   |   |   |   |
|Debian 8 (64 bits)                   |S  |S  |S  |S  |   |   |   |   |   |
|Red Hat Enterprise Linux 7 (64 bits) |S  |S  |S  |S  |S  |   |   |   |   |
|SUSE Enterprise Linux 15 (64 bits)   |S  |   |   |   |   |   |   |   |   |
|SUSE Enterprise Linux 12 (64 bits)   |S  |S  |S  |   |   |   |   |   |   |
|macOS Mojave (64 bits)               |S  |   |   |   |   |   |   |   |   |
|macOS High Sierra (64 bits)          |S  |S  |   |   |   |   |   |   |   |
|macOS Sierra (64 bits)               |S  |S  |S  |S  |   |   |   |   |   |
|macOS El capitán (64 bits)           |   |S  |S  |S  |   |   |   |   |   |

## <a name="see-also"></a>Consulte también  
[Notas de la versión](../../connect/php/release-notes-for-the-php-sql-driver.md)

[Recursos de soporte técnico](../../connect/php/support-resources-for-the-php-sql-driver.md)

[Requisitos del sistema](../../connect/php/system-requirements-for-the-php-sql-driver.md)
