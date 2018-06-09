---
title: sqlsrv_query | Documentos de Microsoft
ms.custom: ''
ms.date: 05/22/2018
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- sqlsrv_query
apitype: NA
helpviewer_keywords:
- sqlsrv_query
- executing queries
- API Reference, sqlsrv_query
ms.assetid: 9fa7c4c8-4da8-4299-9893-f61815055aa3
caps.latest.revision: 46
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0c1c14aaeff26111ebb66ce8aa77f9a25b599ba
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34563903"
---
# <a name="sqlsrvquery"></a>sqlsrv_query
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Prepara y ejecuta una instrucción.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sqlsrv_query(resource $conn, string $tsql [, array $params [, array $options]])  
```  
  
#### <a name="parameters"></a>Parámetros  
*$conn*: el recurso de conexión asociado a la instrucción preparada.  
  
*$tsql*: expresión de Transact-SQL que corresponde a la instrucción preparada.  
  
*$params* [opcional]: una **matriz** de valores que corresponden a parámetros en una consulta parametrizada. Cada elemento de la matriz puede ser uno de los siguientes:
  
-   Un valor literal  
  
-   Una variable PHP  
  
-   Una **matriz** con la siguiente estructura:  
  
    ```  
    array($value [, $direction [, $phpType [, $sqlType]]])  
    ```  
  
    La descripción de cada elemento de la matriz está en la tabla siguiente:  
  
    |Elemento|Descripción|  
    |-----------|---------------|  
    |*$value*|Un valor literal, una variable PHP o una variable por referencia PHP.|  
    |*$direction*[opcional]|Uno de los siguientes **SQLSRV_PARAM_\***  constantes que se utilizan para indicar la dirección del parámetro: **SQLSRV_PARAM_IN**, **SQLSRV_PARAM_OUT**, **SQLSRV_PARAM_INOUT**. El valor predeterminado es **SQLSRV_PARAM_IN**.<br /><br />Para obtener más información acerca de las constantes PHP, consulte [constantes &#40;Microsoft Drivers for PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).|  
    |*$phpType*[opcional]|A **SQLSRV_PHPTYPE_\***  constante que especifica el tipo de datos PHP del valor devuelto.<br /><br />Para obtener más información acerca de las constantes PHP, consulte [constantes &#40;Microsoft Drivers for PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).|  
    |*$sqlType*[opcional]|A **SQLSRV_SQLTYPE_\***  constante que especifica el tipo de datos de SQL Server del valor de entrada.<br /><br />Para obtener más información acerca de las constantes PHP, consulte [constantes &#40;Microsoft Drivers for PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).|  
  
*$options* [opcional]: una matriz asociativa que establece las propiedades de la consulta. Las claves admitidas son las siguientes:  
  
|Key|Valores admitidos:|Descripción|  
|-------|--------------------|---------------|  
|QueryTimeout|Valor entero positivo.|Establece el tiempo de espera de consulta en segundos. De forma predeterminada, el controlador espera indefinidamente para obtener los resultados.|  
|SendStreamParamsAtExec|**True** o **False**<br /><br />El valor predeterminado es **true**.|Configura el controlador para enviar todos los datos en la ejecución de secuencia (**true**), o para enviar datos de la secuencia en fragmentos (**false**). De manera predeterminada, este valor se establece como **True**. Para obtener más información, consulte [sqlsrv_send_stream_data](../../connect/php/sqlsrv-send-stream-data.md).|  
|De desplazamiento|SQLSRV_CURSOR_FORWARD<br /><br />SQLSRV_CURSOR_STATIC<br /><br />SQLSRV_CURSOR_DYNAMIC<br /><br />SQLSRV_CURSOR_KEYSET<br /><br />SQLSRV_CURSOR_CLIENT_BUFFERED|Para obtener más información sobre estos valores, vea [Especificación de un tipo de cursor y selección de filas](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md).|  
  
## <a name="return-value"></a>Valor devuelto  
Un recurso de instrucción. Si la instrucción no se puede crear o ejecutar, **false** se devuelve.  
  
## <a name="remarks"></a>Comentarios  
El **sqlsrv_query** función es ideal para consultas únicas y debe ser la opción predeterminada para ejecutar consultas, a menos que se apliquen circunstancias especiales. Esta función proporciona un método simplificado para ejecutar una consulta con una cantidad mínima de código. La función **sqlsrv_query** realiza los procesos de preparación y ejecución de la instrucción, y se puede usar para ejecutar consultas con parámetros.  
  
Para obtener más información, consulte [How to: Retrieve Output Parameters Using the SQLSRV Driver](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md).  
  
## <a name="example"></a>Ejemplo  
En el siguiente ejemplo, se inserta una fila única en la tabla *Sales.SalesOrderDetail* de la base de datos de AdventureWorks. El ejemplo supone que SQL Server y el [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) base de datos se instalan en el equipo local. Los resultados se agregan a la consola cuando se ejecuta el ejemplo en la línea de comandos.  
  
> [!NOTE]  
> Aunque en el ejemplo siguiente se utiliza una instrucción INSERT para mostrar el uso de **sqlsrv_query** para la ejecución de una instrucción única, el concepto se aplica a cualquier instrucción de Transact-SQL.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
    echo "Could not connect.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Set up the parameterized query. */  
$tsql = "INSERT INTO Sales.SalesOrderDetail   
        (SalesOrderID,   
         OrderQty,   
         ProductID,   
         SpecialOfferID,   
         UnitPrice,   
         UnitPriceDiscount)  
        VALUES   
        (?, ?, ?, ?, ?, ?)";  
  
/* Set parameter values. */  
$params = array(75123, 5, 741, 1, 818.70, 0.00);  
  
/* Prepare and execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if ($stmt) {  
    echo "Row successfully inserted.\n";  
} else {  
    echo "Row insertion failed.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  
?>  
```  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se actualiza un campo en el *Sales.SalesOrderDetail* tabla de la base de datos de AdventureWorks. El ejemplo supone que SQL Server y el [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) base de datos se instalan en el equipo local. Los resultados se agregan a la consola cuando se ejecuta el ejemplo en la línea de comandos.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
    echo "Could not connect.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Set up the parameterized query. */  
$tsql = "UPDATE Sales.SalesOrderDetail   
         SET OrderQty = (?)   
         WHERE SalesOrderDetailID = (?)";  
  
/* Assign literal parameter values. */  
$params = array(5, 10);  
  
/* Execute the query. */  
if (sqlsrv_query($conn, $tsql, $params)) {  
    echo "Statement executed.\n";  
} else {  
    echo "Error in statement execution.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Free connection resources. */  
sqlsrv_close($conn);  
?>  
```  
  
> [!NOTE]
> Se recomienda usar cadenas como entradas al enlazar los valores para un [columna decimal o numeric](https://docs.microsoft.com/en-us/sql/t-sql/data-types/decimal-and-numeric-transact-sql) para garantizar la precisión y la exactitud PHP limitó precisión para [números de punto flotante](http://php.net/manual/en/language.types.float.php). Lo mismo se aplica a columnas bigint, especialmente cuando los valores que están fuera del intervalo de un [entero](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md).

## <a name="example"></a>Ejemplo  
Este ejemplo de código muestra cómo enlazar un valor decimal como un parámetro de entrada.  

```
<?php
$serverName = "(local)";
$connectionInfo = array("Database"=>"YourTestDB");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
     echo "Could not connect.\n";  
     die(print_r(sqlsrv_errors(), true));  
}  

// Assume TestTable exists with a decimal field 
$input = "9223372036854.80000";
$params = array($input);
$stmt = sqlsrv_query($conn, "INSERT INTO TestTable (DecimalCol) VALUES (?)", $params);

sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  

?>
```


## <a name="see-also"></a>Vea también  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  

[Realización de consultas con parámetros](../../connect/php/how-to-perform-parameterized-queries.md)  

[Sobre los ejemplos de código de la documentación](../../connect/php/about-code-examples-in-the-documentation.md)  

[Envío de datos como una secuencia](../../connect/php/how-to-send-data-as-a-stream.md)  

[Uso de parámetros direccionales](../../connect/php/using-directional-parameters.md)  

  
