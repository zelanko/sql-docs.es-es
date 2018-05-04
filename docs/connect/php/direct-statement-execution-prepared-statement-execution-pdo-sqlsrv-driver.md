---
title: Dirigir la instrucción - preparado el controlador PDO_SQLSRV de ejecución de instrucción | Documentos de Microsoft
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 05544ca6-1e07-486c-bf03-e8c2c25b3024
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aaa67ec16086dcfac895422c58c8cdddc50ef243
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="direct-statement-execution-and-prepared-statement-execution-in-the-pdosqlsrv-driver"></a>Direct Statement Execution and Prepared Statement Execution in the PDO_SQLSRV Driver (Ejecución de la instrucción preparada o directa en el controlador PDO_SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

En este tema se describe el uso del atributo PDO:: sqlsrv_attr_direct_query para especificar la ejecución de la instrucción directa en lugar del predeterminado, que es la ejecución de la instrucción preparada. Mediante una instrucción preparada, se puede producir un mejor rendimiento si la instrucción se ejecuta más de una vez utilizando enlace de parámetro.  
  
## <a name="remarks"></a>Comentarios  
Si desea enviar un [!INCLUDE[tsql](../../includes/tsql_md.md)] instrucción directamente al servidor sin preparación de instrucciones por el controlador, puede establecer el atributo PDO:: sqlsrv_attr_direct_query con [PDO:: setAttribute](../../connect/php/pdo-setattribute.md) (o como una opción de controlador que se pasa a [PDO:: __construct](../../connect/php/pdo-construct.md)) o cuando se llama a [PDO:: Prepare](../../connect/php/pdo-prepare.md). De forma predeterminada, el valor de PDO:: sqlsrv_attr_direct_query es False (use la ejecución de la instrucción preparada).  
  
Si usa [PDO:: Query](../../connect/php/pdo-query.md), es recomendable la ejecución directa. Antes de llamar a [PDO:: Query](../../connect/php/pdo-query.md), llame a [PDO:: setAttribute](../../connect/php/pdo-setattribute.md) y PDO:: sqlsrv_attr_direct_query se establece en True.  Cada llamada a [PDO:: Query](../../connect/php/pdo-query.md) puede ejecutarse con una configuración diferente para PDO:: sqlsrv_attr_direct_query.  
  
Si usa [PDO:: Prepare](../../connect/php/pdo-prepare.md) y [pdostatement:: Execute](../../connect/php/pdostatement-execute.md) para ejecutar una consulta varias veces con parámetros enlazados, la ejecución de la instrucción preparada optimiza la ejecución de la consulta repetida.  En esta situación, llame a [PDO:: Prepare](../../connect/php/pdo-prepare.md) con PDO:: sqlsrv_attr_direct_query establecida en False en el parámetro de matriz de opciones de controlador. Cuando sea necesario, puede ejecutar las instrucciones preparadas con PDO:: sqlsrv_attr_direct_query establecida en False.  
  
Después de llamar a [PDO:: Prepare](../../connect/php/pdo-prepare.md), no se puede cambiar el valor de PDO:: sqlsrv_attr_direct_query al ejecutar la consulta preparada.  
  
Si una consulta requiere el contexto que estaba establecido en una consulta anterior, a continuación, ejecute las consultas con PDO:: sqlsrv_attr_direct_query establecida en True. Por ejemplo, si utiliza tablas temporales en las consultas, PDO:: sqlsrv_attr_direct_query debe establecerse en True.  
  
El ejemplo siguiente se muestra que, cuando se requiere el contexto de una instrucción anterior, debe establecer PDO:: sqlsrv_attr_direct_query como True.  Este ejemplo utiliza las tablas temporales, que solo están disponibles para las instrucciones posteriores en el programa cuando se ejecutan consultas directamente.  
  
```  
<?php  
   $conn = new PDO('sqlsrv:Server=(local)', '', '');  
   $conn->setAttribute(constant('PDO::SQLSRV_ATTR_DIRECT_QUERY'), true);  
  
   $stmt1 = $conn->query("DROP TABLE #php_test_table");  
  
   $stmt2 = $conn->query("CREATE TABLE #php_test_table ([c1_int] int, [c2_int] int)");  
  
   $v1 = 1;  
   $v2 = 2;  
  
   $stmt3 = $conn->prepare("INSERT INTO #php_test_table (c1_int, c2_int) VALUES (:var1, :var2)");  
  
   if ($stmt3) {  
      $stmt3->bindValue(1, $v1);  
      $stmt3->bindValue(2, $v2);  
  
      if ($stmt3->execute())  
         echo "Execution succeeded\n";       
      else  
         echo "Execution failed\n";  
   }  
   else  
      var_dump($conn->errorInfo());  
  
   $stmt4 = $conn->query("DROP TABLE #php_test_table");  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[Programación de guía para los controladores de Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)
  
