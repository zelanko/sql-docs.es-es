---
title: Comparación de las funciones de ejecución
description: En este tema se enumeran las diferentes funciones de ejecución de consultas al usar los controladores de Microsoft para PHP en SQL Server.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- executing queries
ms.assetid: 130fc0fd-87dd-46b2-918f-de9dc572c769
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 33d7ebe420dd59d4f659dbe2ce6c784b49b89d04
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680750"
---
# <a name="comparing-execution-functions"></a>Comparación de las funciones de ejecución
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] ofrecen varias opciones para ejecutar funciones.  

## <a name="sqlsrv-execution-functions"></a>Funciones de ejecución SQLSRV  
Si está utilizando el controlador SQLSRV, use [sqlsrv_query](../../connect/php/sqlsrv-query.md) para ejecutar una consulta única y [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) con [sqlsrv_execute](../../connect/php/sqlsrv-execute.md) para ejecutar varias veces una instrucción preparada con distintos valores de parámetros en cada ejecución.  

## <a name="pdo_sqlsrv-execution-functions"></a>Funciones de ejecución PDO_SQLSRV 
Si está utilizando el controlador PDO_SQLSRV, puede ejecutar una consulta con una de las siguientes instrucciones:  
  
-   [PDO::exec](../../connect/php/pdo-exec.md)  
  
-   [PDO::query](../../connect/php/pdo-query.md)  
  
-   [PDO::prepare](../../connect/php/pdo-prepare.md) e [PDOStatement::execute](../../connect/php/pdostatement-execute.md).  
  
## <a name="see-also"></a>Consulte también  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Referencia del controlador PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)

[Guía de programación para los controladores de Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)
  
