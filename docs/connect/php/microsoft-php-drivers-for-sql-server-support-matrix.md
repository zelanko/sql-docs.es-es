---
title: Matriz de compatibilidad de los controladores de Microsoft para PHP para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: genemi
manager: ''
ms.openlocfilehash: c542a77c3a7cfbbe9c54786116e3e9e800a3dda0
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "76917809"
---
# <a name="microsoft-php-drivers-for-sql-server-support-matrix"></a>Matriz de compatibilidad de los controladores de Microsoft para PHP para SQL Server

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Esta página contiene la matriz de compatibilidad y la directiva de ciclo de vida de soporte técnico de los controladores de Microsoft para PHP para SQL Server.

## <a name="microsoft-php-drivers-support-lifecycle-matrix-and-policy"></a>Directiva y matriz de ciclo de vida de soporte técnico de los controladores de Microsoft para PHP

La directiva de ciclo de vida de soporte de Microsoft (MSL) proporciona información transparente y predecible sobre el ciclo de vida de soporte de productos de Microsoft. Las versiones 3.x, 4.x y 5.x de los controladores PHP incluyen cinco años de soporte técnico estándar del controlador a partir de la fecha de publicación. El soporte estándar se define en el [sitio web del ciclo de vida de soporte técnico de Microsoft](https://support.microsoft.com/lifecycle).

Las opciones de soporte técnico extendido y personalizado no están disponibles para controladores de Microsoft para PHP.

Se admiten los siguientes controladores de Microsoft para PHP hasta la fecha indicada de finalización del soporte técnico.

|Nombre del controlador|Versión del paquete de controladores|Finalización del soporte estándar|
|-|:-:|-|
|Controladores PHP de Microsoft 5.8 para SQL Server|5.8|31 de enero de 2025|
|Controladores PHP de Microsoft 5.6 para SQL Server|5.6|21 de febrero de 2024|
|Controladores PHP de Microsoft 5.3 para SQL Server|5.3|20 de julio de 2023|
|Controladores PHP de Microsoft 5.2 para SQL Server|5.2|9 de febrero de 2023|
|Controladores PHP de Microsoft 4.3 para SQL Server|4.3|6 de julio de 2022|
|Controladores PHP de Microsoft 4.0 para SQL Server|4.0|11 de julio de 2021|
|Controladores PHP de Microsoft 3.2 para SQL Server|3.2|9 de marzo de 2020|
| &nbsp; | &nbsp; | &nbsp; |

Ya no se admiten los siguientes controladores de Microsoft para PHP.

|Nombre del controlador|Versión del paquete de controladores|Finalización del soporte estándar|
|-|:-:|-|
|Controladores PHP de Microsoft 3.1 para SQL Server|3.1|12 de diciembre de 2019|
|Controladores PHP de Microsoft 3.0 para SQL Server|3.0|6 de marzo de 2017|
|Controladores PHP de Microsoft 2.0 para SQL Server|2.0|10 de agosto de 2015|
|Controladores PHP de Microsoft 1.0 para SQL Server|1.0|28 de abril de 2014|
| &nbsp; | &nbsp; | &nbsp; |

## <a name="sql-server-version-certified-compatibility"></a>Compatibilidad certificada con la versión de SQL Server
 En la matriz siguiente se enumeran las versiones de SQL Server probadas y certificadas como compatibles con la versión de controlador correspondiente. Nos esforzamos por mantener la compatibilidad con versiones anteriores del controlador, pero solo se prueba y certifica el último controlador compatible con las nuevas versiones de SQL Server, ya que es SQL Server lo que se publica.

|Versión del controlador de PHP para SQL Server &#8594;<br />&#8595; versión de SQL Server|5.8|5.6|5.3|5.2|4.3|4.0|3.2|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Instancia administrada de Azure SQL|Y|Y|Y|Y|Y| | |
|Azure SQL Data Warehouse|Y|Y|Y|Y|Y| | |
|SQL Server 2019         |Y| | | | | | |
|SQL Server 2017         |Y|Y|Y|Y|Y| | |
|SQL Server 2016         |Y|Y|Y|Y|Y|Y| |
|SQL Server 2014         |Y|Y|Y|Y|Y|Y|Y|
|SQL Server 2012         |Y|Y|Y|Y|Y|Y|Y|
|SQL Server 2008 R2      | |Y|Y|Y|Y|Y|Y|
|SQL Server 2008         | | | | | |Y|Y|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

## <a name="php-version-support"></a>Compatibilidad de versiones de PHP

Se admiten las versiones siguientes de PHP con la versión indicada de los controladores de Microsoft para PHP:

|Versión del controlador de PHP para SQL Server &#8594;<br />&#8595; versión de PHP|5.8|5.6|5.3|5.2|4.3|4.0|3.2|
|:---:|---|---|---|---|---|---|---|
|7.4|7.4.0+          |                |                |                |       |        |        |
|7.3|7.3.0+          |7.3.0+          |                |                |       |        |        |
|7.2|7.2+<sup>1</sup>|7.2+<sup>1</sup>|7.2+<sup>1</sup>|7.2+<sup>1</sup>|       |        |        |
|7.1|                |7.1.0+          |7.1.0+          |7.1.0+          |7.1.0+ |        |        |
|7.0|                |                |7.0.0+          |7.0.0+          |7.0.0+ |7.0.0+  |        |
|5.6|                |                |                |                |       |        |5.6.4+  |
|5.5|                |                |                |                |       |        |5.5.16+ |
|5.4|                |                |                |                |       |        |5.4.32  |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

1. Las versiones 7.2.1 y posteriores se admiten en Windows, mientras que las versiones 7.2.0 y versiones posteriores se admiten en Linux y macOS.

## <a name="supported-operating-systems"></a>Sistemas operativos compatibles

Las versiones siguientes del sistema operativo Windows son compatibles con la versión indicada de los controladores de Microsoft para PHP:

|Versión del controlador de PHP para SQL Server &#8594;<br />&#8595; sistema operativo|5.8|5.6|5.3|5.2|4.3|4.0|3.2|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Windows Server 2019                 |Y  |Y  |   |   |   |   |   |
|Windows Server 2016                 |Y  |Y  |Y  |Y  |Y  |   |   |
|Windows Server 2012 R2              |Y  |Y  |Y  |Y  |Y  |Y  |Y  |
|Windows Server 2012                 |Y  |Y  |Y  |Y  |Y  |Y  |Y  |
|Windows Server 2008 R2 SP1          |   |   |   |   |   |Y  |Y  |
|Windows Server 2008 R2              |   |   |   |   |   |   |   |
|Windows Server 2008 SP2             |   |   |   |   |   |Y  |Y  |
|Windows 10                          |Y  |Y  |Y  |Y  |Y  |Y  |   |
|Windows 8.1                         |Y  |Y  |Y  |Y  |Y  |Y  |Y  |
|Windows 8                           |   |   |   |   |Y  |Y  |Y  |
|Windows 7 SP1                       |   |   |   |   |   |Y  |Y  |
|Windows Vista SP2                   |   |   |   |   |   |Y  |Y  |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

Las versiones siguientes de los sistemas operativos Linux y Mac (solo de 64 bits) son compatibles con la versión indicada de los controladores de Microsoft para PHP:

|Versión del controlador de PHP para SQL Server &#8594;<br />&#8595; sistema operativo|5.8|5.6|5.3|5.2|4.3|4.0|3.2|
|--|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Ubuntu 19.10 (64 bits)               |Y  |   |   |   |   |   |   |
|Ubuntu 18.10 (64 bits)               |   |Y  |   |   |   |   |   |
|Ubuntu 18.04 (64 bits)               |Y  |Y  |Y  |   |   |   |   |
|Ubuntu 17.10 (64 bits)               |   |   |Y  |Y  |   |   |   |
|Ubuntu 16.04 (64 bits)               |Y  |Y  |Y  |Y  |Y  |Y  |   |
|Ubuntu 15.10 (64 bits)               |   |   |   |   |Y  |   |   |
|Ubuntu 15.04 (64 bits)               |   |   |   |   |   |Y  |   |
|Debian 10 (64 bits)                  |Y  |   |   |   |   |   |   |
|Debian 9 (64 bits)                   |Y  |Y  |Y  |Y  |   |   |   |
|Debian 8 (64 bits)                   |Y  |Y  |Y  |Y  |Y  |   |   |
|Red Hat Enterprise Linux 8 (64 bits) |Y  |   |   |   |   |   |   |
|Red Hat Enterprise Linux 7 (64 bits) |Y  |Y  |Y  |Y  |Y  |Y  |   |
|Suse Enterprise Linux 15 (64 bits)   |Y  |Y  |   |   |   |   |   |
|Suse Enterprise Linux 12 (64 bits)   |Y  |Y  |Y  |Y  |   |   |   |
|Alpine Linux 3.11 (64 bits)<sup>1</sup>|Y  |   |   |   |   |   |   |
|macOS Catalina (64 bits)             |Y  |   |   |   |   |   |   |
|macOS Mojave (64 bits)               |Y  |Y  |   |   |   |   |   |
|macOS High Sierra (64 bits)          |Y  |Y  |Y  |   |   |   |   |
|macOS Sierra (64 bits)               |   |Y  |Y  |Y  |Y  |   |   |
|macOS El Capitan (64 bits)           |   |   |Y  |Y  |Y  |   |   |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

<sup>1</sup> La compatibilidad con Alpine Linux es experimental para la versión 5.8.

## <a name="see-also"></a>Consulte también

[Notas de la versión](../../connect/php/release-notes-php-sql-driver.md)

[Recursos de soporte técnico](../../connect/php/support-resources-for-the-php-sql-driver.md)

[Requisitos del sistema](../../connect/php/system-requirements-for-the-php-sql-driver.md)
