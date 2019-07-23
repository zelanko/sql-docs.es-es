---
title: Aplicación de formato a cadenas decimales y valores de moneda (controlador SQLSRV) | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- formatting, decimal types, money values
author: yitam
ms.author: v-yitam
manager: v-mabarw
ms.openlocfilehash: 4a5ac641a98077c09bb38a5fc8fbd3fb1a4bf73d
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265142"
---
# <a name="formatting-decimal-strings-and-money-values-sqlsrv-driver"></a>Aplicación de formato a cadenas decimales y valores de moneda (controlador SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Para conservar la precisión, los [tipos decimales o numéricos](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql) siempre se capturan como cadenas con precisión y escalas exactas. Si un valor es menor que 1, falta el cero inicial. Es lo mismo que los campos Money y smallmoney, ya que son campos decimales con una escala fija igual a 4.

## <a name="add-leading-zeroes-if-missing"></a>Agregar ceros a la izquierda si falta
A partir de la versión 5.6.0 del, `FormatDecimals` se agrega la opción a los niveles de conexión y de instrucción sqlsrv, lo que permite al usuario dar formato a las cadenas decimales. Esta opción espera un valor booleano (true o false) y solo afecta al formato de los valores decimales o numéricos de los resultados capturados. En otras palabras, la `FormatDecimals` opción no tiene ningún efecto en otras operaciones, como la inserción o actualización.

De forma predeterminada, `FormatDecimals` es **false**. Si se establece en true, se agregarán los ceros iniciales a las cadenas decimales para cualquier valor decimal inferior a 1.

## <a name="configure-number-of-decimal-places"></a>Configurar el número de posiciones decimales
Con `FormatDecimals` activada, otra opción, `DecimalPlaces`, permite a los usuarios configurar el número de posiciones decimales al mostrar los datos de Money y smallmoney. Acepta valores enteros en el intervalo de [0, 4] y el redondeo puede producirse cuando se muestra. Sin embargo, los datos monetarios subyacentes siguen siendo los mismos.

Ambas opciones se pueden establecer en el nivel de conexión o de instrucción, y el valor de la instrucción siempre invalida la configuración de conexión correspondiente. Tenga en cuenta `DecimalPlaces` que la opción **solo** afecta a los `FormatDecimals` datos Money y debe establecerse `DecimalPlaces` en true para que surta efecto. De lo contrario, el formato se desactiva `DecimalPlaces` independientemente de la configuración.

> [!NOTE]
> Dado que los campos Money o smallmoney tienen una escala `DecimalPlaces` 4, se omitirá el valor en cualquier número negativo o cualquier valor superior a 4. No se recomienda usar ningún dato de moneda con formato como entradas para cualquier cálculo.

## <a name="example---a-simple-fetch"></a>Ejemplo: una captura simple
En el ejemplo siguiente se muestra cómo usar las nuevas opciones en una captura simple.

```php
<?php
$username = 'myusername';
$password = 'mypasword';
$tableName = 'mytable';

$connectionInfo = array("UID" => $username, "PWD" => $password, "Database" => "myDB", "FormatDecimals" => true);  
$server = "myServer";  // IP address also works
$conn = sqlsrv_connect( $server, $connectionInfo);  

$numDigits = 2;
$query = "SELECT money1 FROM $tableName";
$options = array("DecimalPlaces" => $numDigits);
$stmt = sqlsrv_prepare($conn, $query, array(), $options);
sqlsrv_execute($stmt);

if (sqlsrv_fetch($stmt)) {
    $field = sqlsrv_get_field($stmt, 0);  
    echo $field;   // expect a numeric value string with 2 decimal places
}

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);
?>
```

## <a name="example---format-the-output-parameter"></a>Ejemplo: dar formato al parámetro de salida
Si se devuelve un campo decimal o numérico como [parámetro de salida](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md), el valor devuelto se considerará una cadena VARCHAR normal. Sin embargo, si se especifica SQLSRV_SQLTYPE_DECIMAL o SQLSRV_SQLTYPE_NUMERIC, se puede establecer `FormatDecimals` en true para asegurarse de que no falta cero a la izquierda para el valor de cadena numérico. Para más información, consulte [Recuperación de los parámetros de salida con el controlador SQLSRV](../..//connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md).

En el ejemplo siguiente se muestra cómo dar formato al parámetro de salida de un procedimiento almacenado que devuelve un valor decimal (8,5).

```php
$outString = '';
$outSql = '{CALL myStoredProc(?)}';
$stmt = sqlsrv_prepare($conn, 
                       $outSql, 
                       array(array(&$outString, SQLSRV_PARAM_OUT, null, SQLSRV_SQLTYPE_DECIMAL(8, 4))),
                       array('FormatDecimals' => true));

if (sqlsrv_execute($stmt)) {
    echo $outString;  // expect a numeric value string with no missing leading zero
}
```

## <a name="see-also"></a>Consulte también
[Aplicación de formato a cadenas decimales y valores de moneda (controlador PDO_SQLSRV)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)

[Recuperación de datos](../../connect/php/retrieving-data.md)
