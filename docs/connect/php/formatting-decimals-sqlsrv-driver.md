---
title: Aplicación de formato a cadenas decimales y valores de moneda (controlador SQLSRV)
description: Obtenga información sobre cómo usar las opciones FormatDecimals y DecimalPlaces para aplicar formato a los valores decimales o de moneda al usar el controlador SQLSRV de Microsoft para PHP en SQL Server.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- formatting, decimal types, money values
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b111dd925a98c4f0380dfceb0a09ddffadb96592
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726829"
---
# <a name="formatting-decimal-strings-and-money-values-sqlsrv-driver"></a>Aplicación de formato a cadenas decimales y valores de moneda (controlador SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Para conservar la precisión, los [tipos decimales o numéricos](../../t-sql/data-types/decimal-and-numeric-transact-sql.md) siempre se capturan como cadenas con precisiones y escalas exactas. Si cualquier valor es inferior a 1, falta el cero inicial. Lo mismo ocurre con los campos money y smallmoney, ya que son campos decimales con una escala fija igual a 4.

## <a name="add-leading-zeroes-if-missing"></a>Adición de ceros iniciales si faltan
A partir de la versión 5.6.0, la opción `FormatDecimals` se agrega a los niveles de instrucción y conexión sqlsrv, permitiendo al usuario dar formato a las cadenas decimales. Esta opción espera un valor booleano (true o false) y solo afecta al formato de los valores decimales o numéricos de los resultados capturados. Es decir, la opción `FormatDecimals` no tiene ningún efecto en otras operaciones como la inserción o la actualización.

De forma predeterminada, `FormatDecimals` es **false**. Si se establece en true, se agregarán los ceros iniciales a las cadenas decimales para cualquier valor decimal inferior a 1.

## <a name="configure-number-of-decimal-places"></a>Configuración del número de posiciones decimales
Con `FormatDecimals` activados, otra opción, `DecimalPlaces`, permite a los usuarios configurar el número de posiciones decimales al mostrar los datos money y smallmoney. Acepta valores enteros en el intervalo de [0, 4] y el redondeo puede producirse al mostrarse. Sin embargo, los datos money subyacentes no cambian.

Ambas opciones se pueden establecer en el nivel de conexión o instrucción, y la configuración de instrucción siempre invalida la configuración de conexión correspondiente. Tenga en cuenta que la opción `DecimalPlaces`**solo** afecta a los datos money y `FormatDecimals` debe establecerse en true para que `DecimalPlaces` tenga efecto. De lo contrario, el formato se desactiva independientemente del valor `DecimalPlaces`.

> [!NOTE]
> Puesto que los campos money y smallmoney tienen una escala 4, se omitirá el establecimiento del valor `DecimalPlaces` en cualquier número negativo o cualquier valor superior a 4. No se recomienda usar los datos money con formato como entradas a cualquier cálculo.

## <a name="example---a-simple-fetch"></a>Ejemplo: una captura simple
En el siguiente ejemplo se muestra cómo usar las nuevas opciones en una captura simple.

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
Si se devuelve un campo decimal o numérico como [parámetro de salida](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md), el valor devuelto se considerará como una cadena varchar normal. Sin embargo, si se especifica SQLSRV_SQLTYPE_DECIMAL o SQLSRV_SQLTYPE_NUMERIC, puede establecer `FormatDecimals` en true para garantizar que no falte ningún cero inicial para el valor de cadena numérico. Para más información, consulte [Recuperación de los parámetros de salida con el controlador SQLSRV](../..//connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md).

En el siguiente ejemplo se muestra cómo dar formato al parámetro de salida de un procedimiento almacenado que devuelve un valor decimal (8,4).

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