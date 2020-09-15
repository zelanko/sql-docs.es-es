---
description: Recuperación de datos
title: Recuperación de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3414992c-61c0-4e7d-b509-72517e52c1bb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 35a9d9131b7c1cb382ab4e64baa26809d58c90d3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88414431"
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
  
A partir de la versión 1.1 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], puede utilizar [sqlsrv_has_rows](../../connect/php/sqlsrv-has-rows.md) para comprobar si un conjunto de resultados tiene filas.  
  
## <a name="pdo_sqlsrv-driver"></a>Controlador PDO_SQLSRV  
El controlador PDO_SQLSRV de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] proporciona las siguientes opciones para recuperar datos de un conjunto de resultados:  
  
-   [PDOStatement::fetch](../../connect/php/pdostatement-fetch.md)  
  
-   [PDOStatement::fetchAll](../../connect/php/pdostatement-fetchall.md)  
  
-   [PDOStatement::fetchColumn](../../connect/php/pdostatement-fetchcolumn.md)  
  
-   [PDOStatement::fetchObject](../../connect/php/pdostatement-fetchobject.md)  
  
Si una consulta recupera más de un conjunto de resultados, puede desplazarse al siguiente conjunto de resultados con [PDOStatement::nextRowset](../../connect/php/pdostatement-nextrowset.md).  
  
Puede ver cuántas filas se encuentran en un conjunto de resultados si especifica un cursor desplazable y, luego, llamar a [PDOStatement::rowCount](../../connect/php/pdostatement-rowcount.md).  
  
[PDO::prepare](../../connect/php/pdo-prepare.md) permite especificar un tipo de cursor. Después, con [PDOStatement::fetch](../../connect/php/pdostatement-fetch.md) puede seleccionar una fila. Consulte [PDO::prepare](../../connect/php/pdo-prepare.md) para ver un ejemplo y obtener más información.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|---------|---------------|  
|[Recuperación de datos como una cadena](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)|Proporciona una visión general de cómo transmitir datos del servidor y proporciona vínculos a casos de uso específicos.|  
|[Uso de parámetros direccionales](../../connect/php/using-directional-parameters.md)|Describe cómo usar parámetros direccionales cuando se llama a un procedimiento almacenado.|  
|[Especificación de un tipo de cursor y selección de filas](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)|Muestra cómo crear un conjunto de resultados con filas a las que acceder en cualquier orden.|  
|[Procedimientos: Recuperación de los tipos de fecha y hora como cadenas con el controlador SQLSRV](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)|Describe cómo recuperar los tipos de fecha y hora como cadenas con el controlador SQLSRV.|  
|[Procedimientos: Recuperación de los tipos de fecha y hora como objetos de fecha y hora PHP mediante el controlador PDO_SQLSRV](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)|Describe cómo recuperar los tipos de fecha y hora como objetos mediante el controlador PDO_SQLSRV.|  
|[Aplicación de formato a cadenas decimales con el controlador SQLSRV](../../connect/php/formatting-decimals-sqlsrv-driver.md)|Muestra cómo aplicar formato a valores decimales o monetarios mediante el controlador SQLSRV.|  
|[Aplicación de formato a cadenas decimales con el controlador PDO_SQLSRV](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)|Muestra cómo aplicar formato a valores decimales o monetarios mediante el controlador PDO_SQLSRV.|  
  
## <a name="related-sections"></a>Secciones relacionadas  
[Procedimientos: Especificación de los tipos de datos PHP](../../connect/php/how-to-specify-php-data-types.md)  
  
## <a name="see-also"></a>Consulte también  
[Guía de programación para los controladores de Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Recuperación de datos](../../connect/php/retrieving-data.md)  
  
