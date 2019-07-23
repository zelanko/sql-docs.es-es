---
title: Aplicación de formato a cadenas decimales y valores de moneda (controlador PDO_SQLSRV) | Microsoft Docs
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
ms.openlocfilehash: 76c314159faf15e63bf77b17a8a45abf217b205c
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265150"
---
# <a name="formatting-decimal-strings-and-money-values-pdosqlsrv-driver"></a>Aplicación de formato a cadenas decimales y valores de moneda (controlador PDO_SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Para conservar la precisión, los [tipos decimales o numéricos](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql) siempre se capturan como cadenas con precisión y escalas exactas. Si un valor es menor que 1, falta el cero inicial. Es lo mismo que los campos Money y smallmoney, ya que son campos decimales con una escala fija igual a 4.

## <a name="add-leading-zeroes-if-missing"></a>Agregar ceros a la izquierda si falta
A partir de la versión 5.6.0 del, el atributo `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` Connection o Statement permite al usuario dar formato a las cadenas decimales. Este atributo espera un valor booleano (true o false) y solo afecta al formato de los valores decimales o numéricos de los resultados capturados. En otras palabras, este atributo no tiene ningún efecto en otras operaciones, como la inserción o actualización.

De forma predeterminada, `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` es **false**. Si se establece en true, se agregarán los ceros iniciales a las cadenas decimales para cualquier valor decimal inferior a 1.

## <a name="configure-number-of-decimal-places"></a>Configurar el número de posiciones decimales
Con `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` activado, otro atributo de conexión o instrucción, `PDO::SQLSRV_ATTR_DECIMAL_PLACES`, permite a los usuarios configurar el número de posiciones decimales al mostrar los datos de Money y smallmoney. Acepta valores enteros en el intervalo de [0, 4] y el redondeo puede producirse cuando se muestra. Sin embargo, los datos monetarios subyacentes siguen siendo los mismos.

Los atributos de instrucción siempre invalidan la configuración de conexión correspondiente. Tenga en cuenta `PDO::SQLSRV_ATTR_DECIMAL_PLACES` que la opción **solo** afecta a los `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` datos Money y debe establecerse en true. De lo contrario, el formato se desactiva `PDO::SQLSRV_ATTR_DECIMAL_PLACES` independientemente de la configuración.

> [!NOTE]
> Dado que los campos Money o smallmoney tienen una escala `PDO::SQLSRV_ATTR_DECIMAL_PLACES` 4, se omitirá la configuración en cualquier número negativo o en cualquier valor superior a 4. No se recomienda usar ningún dato de moneda con formato como entradas para cualquier cálculo.

### <a name="to-set-the-connection-attributes"></a>Para establecer los atributos de conexión

-   Establecer atributos en el punto de conexión:

    ```php
    $attrs = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => true,
                   PDO::SQLSRV_ATTR_DECIMAL_PLACES => 2);

    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password, $attrs);
    ```

-   Establecer atributos después de la conexión:

    ```php
    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password);
    $conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
    $conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);
    ```

## <a name="example---format-money-data"></a>Ejemplo: formato de datos Money
En el ejemplo siguiente se muestra cómo capturar datos de Money mediante [PDOStatement:: bindColumn](../../connect/php/pdostatement-bindcolumn.md):

```php
<?php
$database = "myDB";
$server = "(local)";
$conn = new PDO( "sqlsrv:server=$server; Database = $database", "", "");
$conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);

$numDigits = 3;
$query = "SELECT smallmoney1 FROM aTable";
$options = array(PDO::SQLSRV_ATTR_DECIMAL_PLACES => $numDigits);
$stmt = $conn->prepare($query, $options);
$stmt->execute();

$stmt->bindColumn('smallmoney1', $field);
$result = $stmt->fetch(PDO::FETCH_BOUND);
echo $field;    // expect a number string with 3 decimal places

unset($stmt);
unset($conn);
?>
```

## <a name="example---override-connection-attributes"></a>Ejemplo: invalidar atributos de conexión
En el ejemplo siguiente se muestra cómo invalidar los atributos de conexión:

```php
<?php
$database = 'myDatabase';
$server = 'myServer';
$username = 'myuser';
$password = 'mypassword'

$conn = new PDO("sqlsrv:server=$server; Database = $database", $username, $password);
$conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
$conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);

$query = 'SELECT smallmoney1 FROM testTable1';
$options = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => false);
$stmt = $conn->prepare($query, $options);
$stmt->execute();

$stmt->bindColumn('smallmoney1', $field);
$result = $stmt->fetch(PDO::FETCH_BOUND);  
echo $field;   // expect a number string showing the original scale -- 4 decimal places

unset($stmt);
unset($conn);
?>
```

## <a name="see-also"></a>Consulte también
[Aplicación de formato a cadenas decimales y valores de moneda (controlador SQLSRV)](../../connect/php/formatting-decimals-sqlsrv-driver.md)

[Recuperación de datos](../../connect/php/retrieving-data.md)
