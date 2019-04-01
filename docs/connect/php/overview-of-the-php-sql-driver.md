---
title: Información general de los controladores de Microsoft para PHP para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 66559249-34c0-409d-b919-9b5bf0c4c9ec
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f2129745a8732fba882da6da1caf22e80df11f47
ms.sourcegitcommit: c60784d1099875a865fd37af2fb9b0414a8c9550
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2019
ms.locfileid: "58645487"
---
# <a name="overview-of-the-microsoft-drivers-for-php-for-sql-server"></a>Información general de los controladores de Microsoft para PHP para SQL Server

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] constituyen una extensión de PHP que proporciona acceso a los datos de SQL Server 2005 y versiones posteriores, incluido Azure SQL Database. La extensión proporciona una interfaz de procedimientos con el controlador SQLSRV y una interfaz orientada a objetos con el controlador PDO_SQLSRV para tener acceso a datos en todas las versiones de SQL Server, incluida la Express, empezando por SQL Server 2005. Compatibilidad con las versiones 3.1 y posteriores de los controladores comienza con SQL Server 2008. La API de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] incluye compatibilidad con la autenticación de Windows, transacciones, enlace de parámetros, transmisión por secuencias, acceso a metadatos y control de errores.  
  
Para usar el [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], debe tener la versión correcta de SQL Server Native Client o el controlador ODBC de Microsoft instalado en el mismo equipo que PHP se está ejecutando.  Para obtener más información, consulte [requisitos del sistema para el Drivers de Microsoft para PHP para SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|---------|---------------|  
| ![En círculo la flecha abajo de descarga](../../ssdt/media/download.png)[para descargar los controladores de PHP para SQL Server](download-drivers-php-sql-server.md) | Vínculos para descargar los controladores de Microsoft para PHP para SQL Server. |
|[Notas de la versión de los controladores de Microsoft para PHP para SQL Server](../../connect/php/release-notes-php-sql-driver.md)|Enumera las características que se agregaron en las versiones 4.0, 3.2, 3.1, 3.0 y 2.0.|  
|[Recursos de soporte para los controladores de Microsoft para PHP para SQL Server](../../connect/php/support-resources-for-the-php-sql-driver.md)|Proporciona vínculos a recursos que pueden ser útiles cuando desarrolle aplicaciones que usan los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].|  
|[Sobre los ejemplos de código de la documentación](../../connect/php/about-code-examples-in-the-documentation.md)|Proporciona información que podría resultar útil al ejecutar los ejemplos de código de esta documentación.|  
| &nbsp; | &nbsp; |

## <a name="reference"></a>Referencia

[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
[Referencia del controlador PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
[Constantes &#40;controladores de Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  

## <a name="see-also"></a>Consulte también

[Introducción a los controladores de Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Programación de guía para los controladores de Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Aplicación de ejemplo &#40;controlador SQLSRV&#41;](../../connect/php/example-application-sqlsrv-driver.md)
