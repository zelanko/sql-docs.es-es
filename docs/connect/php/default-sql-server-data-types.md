---
title: Valor predeterminado de tipos de datos SQL Server | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- default data types
- converting data types
ms.assetid: 65c7c211-96d3-4e65-a1de-1fe8d21348e7
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e1d49ff27e0698f0c475f8150654b01bbaf1d283
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35307234"
---
# <a name="default-sql-server-data-types"></a>Tipos de datos de SQL Server predeterminados
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Al enviar datos al servidor, los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] convierten los datos de su tipo de datos PHP a un tipo de datos de SQL Server si el usuario no ha especificado ningún tipo de datos de SQL Server. En la siguiente tabla se muestra el tipo de datos PHP (el tipo de datos que se envían al servidor) y el tipo de datos de SQL Server predeterminado (el tipo de datos al que se convierten los datos). Para obtener información más detallada sobre cómo especificar tipos de datos al enviar datos al servidor, vea [Cómo especificar tipos de datos de SQL Server cuando se usa el controlador SQLSRV](../../connect/php/how-to-specify-sql-server-data-types-when-using-the-sqlsrv-driver.md).  
  
|Tipo de datos PHP|Tipo de datos de SQL Server predeterminados en el controlador SQLSRV|Tipo de datos de SQL Server predeterminados en el controlador PDO_SQLSRV Driver|  
|-----------------|------------------------------------------------|-----------------------------------------------------|  
|NULL|varchar(1)|No compatible|  
|Boolean|bit|bit|  
|Integer|INT|INT|  
|float|float(24)|No compatible|  
|String (longitud inferior a 8000 bytes)|varchar (<string length>)|varchar (<string length>)|  
|String (longitud superior a 8000 bytes)|ntext|ntext|  
|Recurso|No compatible.|No compatible.|  
|Stream (codificación: no binaria)|ntext|ntext|  
|Stream (codificación: binaria)|varbinary|varbinary|  
|Array|No compatible.|No compatible.|  
|Objeto|No compatible.|No compatible.|  
|DateTime (1)|DATETIME|No compatible.|  
  
## <a name="see-also"></a>Vea también  
[Constantes &#40;controladores de Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[Conversión de tipos de datos](../../connect/php/converting-data-types.md)

[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)

[Tipos de PHP](http://php.net/manual/language.types.php)

[Tipos de datos (Transact-SQL)](https://docs.microsoft.com/en-us/sql/t-sql/data-types/data-types-transact-sql)  
  
