---
title: Tipos de datos de SQL Server predeterminados
description: En este tema se enumeran todos los tipos de datos de SQL Server predeterminados basados en tipos de datos PHP cuando se usa el controlador SQLSRV de Microsoft para PHP en SQL Server.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- default data types
- converting data types
ms.assetid: 65c7c211-96d3-4e65-a1de-1fe8d21348e7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5f60111e8a98e3f187e4db39eec06ab35e38195
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680780"
---
# <a name="default-sql-server-data-types"></a>Tipos de datos de SQL Server predeterminados
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Al enviar datos al servidor, los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] convierten los datos de su tipo de datos PHP a un tipo de datos de SQL Server si el usuario no ha especificado ningún tipo de datos de SQL Server. En la siguiente tabla se muestra el tipo de datos PHP (el tipo de datos que se envían al servidor) y el tipo de datos de SQL Server predeterminado (el tipo de datos al que se convierten los datos). Para obtener información más detallada sobre cómo especificar tipos de datos al enviar datos al servidor, vea [Cómo especificar tipos de datos de SQL Server cuando se usa el controlador SQLSRV](../../connect/php/how-to-specify-sql-server-data-types-when-using-the-sqlsrv-driver.md).  
  
|Tipo de datos PHP|Tipo de datos de SQL Server predeterminados en el controlador SQLSRV|Tipo de datos de SQL Server predeterminados en el controlador PDO_SQLSRV Driver|  
|-----------------|------------------------------------------------|-----------------------------------------------------|  
|NULL|varchar(1)|no admitido|  
|Boolean|bit|bit|  
|Entero|int|int|  
|Float|float(24)|no admitido|  
|String (longitud inferior a 8000 bytes)|varchar(<string length>)|varchar(<string length>)|  
|String (longitud superior a 8000 bytes)|ntext|ntext|  
|Recurso|No compatible.|No se admite.|  
|Stream (codificación: no binaria)|ntext|ntext|  
|Stream (codificación: binaria)|varbinary|varbinary|  
|Array|No compatible.|No se admite.|  
|Objeto|No compatible.|No se admite.|  
|DateTime (1)|datetime|No se admite.|  
  
## <a name="see-also"></a>Consulte también  
[Constantes &#40;controladores de Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[Conversión de tipos de datos](../../connect/php/converting-data-types.md)

[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)

[Tipos de datos PHP](https://php.net/manual/language.types.php)

[Tipos de datos (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql)  
  
