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
manager: mbarwin
ms.openlocfilehash: 35626c192c3d74ad0201cee3c5e97adbce92a3aa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62669700"
---
# <a name="formatting-decimal-strings-and-money-values-pdosqlsrv-driver"></a>Aplicación de formato a cadenas decimales y valores de moneda (controlador PDO_SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Para conservar la precisión, [tipos decimales o numeric](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql) siempre se capturan como cadenas con precisión exacta y escalas. Si cualquier valor es menor que 1, falta el cero inicial. Es lo mismo con los campos de money y smallmoney ya que son campos decimales con una escala fija igual a 4.

## <a name="add-leading-zeroes-if-missing"></a>Agregar ceros a la izquierda si falta
Empezando por la versión 5.6.0, la conexión o el atributo de instrucción `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` permite al usuario dar formato a cadenas decimales. Este atributo espera un valor booleano (true o false) y solo afecta al formato de los valores decimales o numéricos en los resultados recuperados. En otras palabras, este atributo no tiene ningún efecto en otras operaciones como la inserción o actualización.

De forma predeterminada, `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` es **false**. Si se establece en true, los ceros iniciales para cadenas decimales se agregarán para cualquier valor decimal inferior a 1.

## <a name="configure-number-of-decimal-places"></a>Configurar el número de posiciones decimales
Con `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` activado de otro atributo de conexión o instrucción, `PDO::SQLSRV_ATTR_DECIMAL_PLACES`, permite a los usuarios configurar el número de posiciones decimales cuando muestra datos money y smallmoney. Acepta valores enteros en el intervalo de [0, 4], y pueden producirse de redondeo que se muestra. Sin embargo, los datos subyacentes de dinero son iguales.

Los atributos de instrucción siempre invalidan la configuración de conexión correspondiente. Tenga en cuenta que el `PDO::SQLSRV_ATTR_DECIMAL_PLACES` opción **sólo** afecta a los datos de dinero, y `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` debe establecerse en true. En caso contrario, formato está desactivado, independientemente de `PDO::SQLSRV_ATTR_DECIMAL_PLACES` configuración.

> [!NOTE]
> Puesto que los campos de dinero o smallmoney tienen escala 4, configuración `PDO::SQLSRV_ATTR_DECIMAL_PLACES` a cualquier número negativo o cualquier valor mayor que 4 se pasará por alto. No se recomienda el uso de datos con formato dinero como entradas para los cálculos.

### <a name="to-set-the-connection-attributes"></a>Para establecer los atributos de conexión

-   Establecer atributos en el punto de conexión:

    ```php
    $attrs = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => true,
                   PDO::SQLSRV_ATTR_DECIMAL_PLACES => 2);

    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password, $attrs);
    ```

-   Establecer atributos de conexión de publicación:

    ```php
    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password);
    $conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
    $conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);
    ```

## <a name="example---format-money-data"></a>Por ejemplo, dar formato a datos money
El ejemplo siguiente muestra cómo capturar datos de dinero mediante [pdostatement:: Bindcolumn](../../connect/php/pdostatement-bindcolumn.md):

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

## <a name="example---override-connection-attributes"></a>Por ejemplo, los atributos de conexión de invalidación
El ejemplo siguiente muestra cómo reemplazar los atributos de conexión:

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
