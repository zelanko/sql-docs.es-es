---
title: Comparación de funciones de ejecución | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
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
ms.openlocfilehash: 68575f3a0227c6400ed5d927ff603b66bd6f440d
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925866"
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
  
