---
title: Recuperación de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3414992c-61c0-4e7d-b509-72517e52c1bb
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 433635c8260ca4ae2d3a3132f093f8eb5341fad0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="retrieving-data"></a>Recuperación de datos
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

En este tema y en los de esta sección se describe cómo recuperar los datos.  
  
## <a name="sqlsrv-driver"></a>Controlador SQLSRV  
El controlador SQLSRV de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] proporciona las siguientes opciones para recuperar datos de un conjunto de resultados:  
  
-   [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)  
  
-   [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md)  
  
-   [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)/[sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md)  
  
> [!NOTE]  
> Cuando se utiliza cualquiera de las funciones mencionadas anteriormente, evite utilizar como criterio de los bucles de salida comparaciones con valor Null. Como las funciones de **sqlsrv** devuelven un valor False cuando se produce un error, en ese caso, el siguiente código podría producir un bucle infinito en [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md):  
>   
> `/*``This code could result in an infinite loop. It is recommended that`  
>   
> `you do NOT use null comparisons as the criterion for exiting loops,`  
>   
> `as is done here. */`  
>   
> `do{`  
>   
> `$result = sqlsrv_fetch_array($stmt);`  
>   
> `} while( !is_null($result));`  
  
Si una consulta recupera más de un conjunto de resultados, puede desplazarse al siguiente conjunto de resultados con [sqlsrv_next_result](../../connect/php/sqlsrv-next-result.md).  
  
A partir de la versión 1.1 de la [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], puede usar [sqlsrv_has_rows](../../connect/php/sqlsrv-has-rows.md) para comprobar si un conjunto de resultados tiene filas.  
  
## <a name="pdosqlsrv-driver"></a>Controlador PDO_SQLSRV  
El controlador PDO_SQLSRV de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] proporciona las siguientes opciones para recuperar datos de un conjunto de resultados:  
  
-   [PDOStatement::fetch](../../connect/php/pdostatement-fetch.md)  
  
-   [PDOStatement::fetchAll](../../connect/php/pdostatement-fetchall.md)  
  
-   [PDOStatement::fetchColumn](../../connect/php/pdostatement-fetchcolumn.md)  
  
-   [PDOStatement::fetchObject](../../connect/php/pdostatement-fetchobject.md)  
  
Si una consulta recupera más de un conjunto de resultados, puede desplazarse al siguiente conjunto de resultados con [PDOStatement::nextRowset](../../connect/php/pdostatement-nextrowset.md).  
  
Puede ver cuántas filas se encuentran en un conjunto de resultados si especifica un cursor desplazable y, luego, llamar a [PDOStatement::rowCount](../../connect/php/pdostatement-rowcount.md).  
  
[PDO::prepare](../../connect/php/pdo-prepare.md) permite especificar un tipo de cursor. Después, con [PDOStatement::fetch](../../connect/php/pdostatement-fetch.md) puede seleccionar una fila. Consulte [PDO::prepare](../../connect/php/pdo-prepare.md) para ver un ejemplo y obtener más información.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|---------|---------------|  
|[Recuperación de datos como una cadena](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)|Proporciona una visión general de cómo transmitir datos del servidor y proporciona vínculos a casos de uso específicos.|  
|[Uso de parámetros direccionales](../../connect/php/using-directional-parameters.md)|Describe cómo usar parámetros direccionales cuando se llama a un procedimiento almacenado.|  
|[Especificación de un tipo de cursor y selección de filas](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)|Muestra cómo crear un conjunto de resultados con filas a las que acceder en cualquier orden cuando se utiliza el controlador SQLSRV.|  
|[Cómo recuperar el tipo de fecha y hora como cadenas con el controlador SQLSRV](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)|Describe cómo recuperar tipos de fecha y hora como cadenas.|  
  
## <a name="related-sections"></a>Secciones relacionadas  
[Cómo especificar tipos de datos PHP](../../connect/php/how-to-specify-php-data-types.md)  
  
## <a name="see-also"></a>Vea también  
[Programación de guía para los controladores de Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Recuperación de datos](../../connect/php/retrieving-data.md)  
  
