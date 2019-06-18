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
manager: mbarwin
ms.openlocfilehash: 76b6d27acedcfe2ec462a764559237a1a2218f78
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62669607"
---
# <a name="formatting-decimal-strings-and-money-values-sqlsrv-driver"></a>Aplicación de formato a cadenas decimales y valores de moneda (controlador SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Para conservar la precisión, [tipos decimales o numeric](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql) siempre se capturan como cadenas con precisión exacta y escalas. Si cualquier valor es menor que 1, falta el cero inicial. Es lo mismo con los campos de money y smallmoney ya que son campos decimales con una escala fija igual a 4.

## <a name="add-leading-zeroes-if-missing"></a>Agregar ceros a la izquierda si falta
Desde la versión 5.6.0, la opción `FormatDecimals` se agrega a los niveles de conexión y la instrucción de sqlsrv, que permite al usuario dar formato a cadenas decimales. Esta opción espera un valor booleano (true o false) y solo afecta al formato de valores decimales o numéricos en los resultados recuperados. En otras palabras, el `FormatDecimals` opción no tiene ningún efecto en otras operaciones como la inserción o actualización.

De forma predeterminada, `FormatDecimals` es **false**. Si se establece en true, los ceros iniciales para cadenas decimales se agregarán para cualquier valor decimal inferior a 1.

## <a name="configure-number-of-decimal-places"></a>Configurar el número de posiciones decimales
Con `FormatDecimals` activado, la otra opción, `DecimalPlaces`, permite a los usuarios configurar el número de posiciones decimales cuando muestra datos money y smallmoney. Acepta valores enteros en el intervalo de [0, 4], y pueden producirse de redondeo que se muestra. Sin embargo, los datos subyacentes de dinero son iguales.

Ambas opciones se pueden establecer a nivel de instrucción o la conexión y la instrucción que establece siempre invalida la configuración de conexión correspondiente. Tenga en cuenta que el `DecimalPlaces` opción **sólo** afecta a los datos de dinero, y `FormatDecimals` debe establecerse en true para `DecimalPlaces` surta efecto. En caso contrario, formato está desactivado, independientemente de `DecimalPlaces` configuración.

> [!NOTE]
> Puesto que los campos de dinero o smallmoney tienen escala 4, configuración `DecimalPlaces` valor a un número negativo o cualquier valor mayor que 4 se pasará por alto. No se recomienda el uso de datos con formato dinero como entradas para los cálculos.

## <a name="example---a-simple-fetch"></a>Por ejemplo, una búsqueda simple
El ejemplo siguiente muestra cómo usar las nuevas opciones de una recopilación simple.

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

## <a name="example---format-the-output-parameter"></a>Por ejemplo, el parámetro de salida de formato
Si un campo numérico o decimal se devuelve como el [parámetro de salida](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md), el valor devuelto, se considerarán como una cadena regular varchar. Sin embargo, si se especifica SQLSRV_SQLTYPE_DECIMAL o SQLSRV_SQLTYPE_NUMERIC, puede establecer `FormatDecimals` en true para asegurarse de que no hay que faltan cero para el valor de cadena numérico. Para más información, consulte [Recuperación de los parámetros de salida con el controlador SQLSRV](../..//connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md).

En el ejemplo siguiente se muestra cómo se aplica el formato de parámetro de salida de un procedimiento almacenado que devuelve un valor decimal(8,4).

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
