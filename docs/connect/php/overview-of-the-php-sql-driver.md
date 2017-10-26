---
title: "Introducción al controlador SQL para PHP | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 66559249-34c0-409d-b919-9b5bf0c4c9ec
caps.latest.revision: 73
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4badc426f6dbff44784bd8487b04bc0665d959ad
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="overview-of-the-php-sql-driver"></a>Información general sobre el controlador SQL para PHP

![Descarga-CTRL+MAYÚS+TAB-dentro de un círculo](../../ssdt/media/download.png)[para descargar los controladores de PHP para SQL Server](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

El [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] es una extensión PHP que proporciona acceso a los datos a SQL Server 2005 y versiones posteriores, incluido la base de datos de SQL Azure. La extensión proporciona una interfaz procedimental (el controlador SQLSRV) y una interfaz orientada a objetos (el controlador PDO_SQLSRV) para tener acceso a datos en todas las versiones (incluida la Express) a partir de SQL Server 2005 (soporte para PHP para SQL Server versión 3.1 y posteriores comienza con SQL Server 2008). La API de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] incluye compatibilidad con la autenticación de Windows, transacciones, enlace de parámetros, transmisión por secuencias, acceso a metadatos y control de errores.  
  
Para usar el [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] debe tener la versión correcta de SQL Server Native Client o el controlador ODBC de Microsoft instalado en el mismo equipo que PHP se está ejecutando.  Para obtener más información, vea [Requisitos del sistema para el controlador SQL para PHP](../../connect/php/system-requirements-for-the-php-sql-driver.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|---------|---------------|  
| ![Descarga-CTRL+MAYÚS+TAB-dentro de un círculo](../../ssdt/media/download.png)[para descargar los controladores de PHP para SQL Server](../sql-connection-libraries.md#anchor-20-drivers-relational-access) | Vínculos para descargar los controladores y el código fuente de los controladores de Microsoft para PHP para SQL Server. |
|[Notas de la versión del controlador SQL para PHP](../../connect/php/release-notes-for-the-php-sql-driver.md)|Enumera las características que se agregaron en las versiones 4.0, 3.2, 3.1, 3.0 y 2.0.|  
|[Recursos de soporte técnico para el controlador SQL para PHP](../../connect/php/support-resources-for-the-php-sql-driver.md)|Proporciona vínculos a recursos que pueden ser útiles cuando desarrolle aplicaciones que usan los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].|  
|[Sobre los ejemplos de código de la documentación](../../connect/php/about-code-examples-in-the-documentation.md)|Proporciona información que podría resultar útil al ejecutar los ejemplos de código de esta documentación.|  
  
## <a name="reference"></a>Referencia  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
[Referencia del controlador PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
[Constantes &#40;controladores de Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
[Cómo empezar a usar el controlador SQL para PHP](../../connect/php/getting-started-with-the-php-sql-driver.md)
[Guía de programación para el controlador SQL para PHP](../../connect/php/programming-guide-for-php-sql-driver.md)
[aplicación de ejemplo &#40; Controlador SQLSRV &#41;](../../connect/php/example-application-sqlsrv-driver.md)

