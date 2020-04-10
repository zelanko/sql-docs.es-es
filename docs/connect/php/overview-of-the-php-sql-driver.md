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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1c8f5cbf011165b41b353a37d8973031f55c2db6
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922815"
---
# <a name="overview-of-the-microsoft-drivers-for-php-for-sql-server"></a>Información general de los controladores de Microsoft para PHP para SQL Server

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] constituyen una extensión de PHP que proporciona acceso a los datos de SQL Server 2005 y versiones posteriores, incluido Azure SQL Database. La extensión proporciona una interfaz de procedimientos con el controlador SQLSRV y una interfaz orientada a objetos con el controlador PDO_SQLSRV para obtener acceso a los datos en todas las versiones de SQL Server, incluida la Express, a partir de SQL Server 2005. La compatibilidad para la versión 3.1 y versiones posteriores de los controladores se ofrece a partir de SQL Server 2008. La API de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] incluye compatibilidad con la autenticación de Windows, transacciones, enlace de parámetros, transmisión por secuencias, acceso a metadatos y control de errores.  
  
Para usar [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], debe tener instalada la versión correcta de SQL Server Native Client o Microsoft ODBC Driver en el mismo equipo en que se está ejecutando PHP.  Para más información, consulte [Requisitos del sistema para los controladores de Microsoft para PHP para SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|---------|---------------|  
| ![Download-DownArrow-Circled](../../ssms/media/download-icon.png)[Para descargar los controladores para PHP para SQL Server](download-drivers-php-sql-server.md) | Vínculos para descargar los controladores de Microsoft para PHP para SQL Server. |
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

[Guía de programación para los controladores de Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Aplicación de ejemplo &#40;controlador SQLSRV&#41;](../../connect/php/example-application-sqlsrv-driver.md)
