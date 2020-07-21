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
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "68265150"
---
# <a name="formatting-decimal-strings-and-money-values-pdo_sqlsrv-driver"></a>Aplicación de formato a cadenas decimales y valores de moneda (controlador PDO_SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Para conservar la precisión, los [tipos decimales o numéricos](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql) siempre se capturan como cadenas con precisiones y escalas exactas. Si cualquier valor es inferior a 1, falta el cero inicial. Lo mismo ocurre con los campos money y smallmoney, ya que son campos decimales con una escala fija igual a 4.

## <a name="add-leading-zeroes-if-missing"></a>Adición de ceros iniciales si faltan
A partir de la versión 5.6.0, el atributo de instrucción o conexión `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` permite al usuario aplicar formato a las cadenas decimales. Este atributo espera un valor booleano (true o false) y solo afecta al formato de los valores decimales o numéricos de los resultados capturados. Es decir, este atributo no tiene ningún efecto en otras operaciones como la inserción o la actualización.

De forma predeterminada, `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` es **false**. Si se establece en true, se agregarán los ceros iniciales a las cadenas decimales para cualquier valor decimal inferior a 1.

## <a name="configure-number-of-decimal-places"></a>Configuración del número de posiciones decimales
Con `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` activados, otro atributo de instrucción o conexión, `PDO::SQLSRV_ATTR_DECIMAL_PLACES`, permite a los usuarios configurar el número de posiciones decimales al mostrar los datos money y smallmoney. Acepta valores enteros en el intervalo de [0, 4] y el redondeo puede producirse al mostrarse. Sin embargo, los datos money subyacentes no cambian.

Los atributos de instrucción siempre invalidan la configuración de conexión correspondiente. Tenga en cuenta que la opción `PDO::SQLSRV_ATTR_DECIMAL_PLACES` **solo** afecta a los datos money y `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` debe establecerse en true. De lo contrario, el formato se desactiva independientemente del valor `PDO::SQLSRV_ATTR_DECIMAL_PLACES`.

> [!NOTE]
> Puesto que los campos money y smallmoney tienen una escala 4, se omitirá el establecimiento de `PDO::SQLSRV_ATTR_DECIMAL_PLACES` en cualquier número negativo o cualquier valor superior a 4. No se recomienda usar los datos money con formato como entradas a cualquier cálculo.

### <a name="to-set-the-connection-attributes"></a>Para establecer los atributos de conexión

-   Establezca atributos en el punto de conexión:

    ```php
    $attrs = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => true,
                   PDO::SQLSRV_ATTR_DECIMAL_PLACES => 2);

    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password, $attrs);
    ```

-   Establezca atributos después de la conexión:

    ```php
    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password);
    $conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
    $conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);
    ```

## <a name="example---format-money-data"></a>Ejemplo: dar formato a datos money
En el siguiente ejemplo se muestra cómo capturar los datos money mediante [PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md):

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
En el siguiente ejemplo se muestra cómo invalidar los atributos de conexión:

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
