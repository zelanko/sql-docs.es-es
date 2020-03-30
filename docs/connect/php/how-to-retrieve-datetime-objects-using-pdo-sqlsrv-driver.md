---
title: Recuperación de los tipos de fecha y hora como objetos de fecha y hora PHP mediante el controlador PDO_SQLSRV | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date and time types, retrieving as datetime objects
author: yitam
ms.author: v-yitam
manager: v-mabarw
ms.openlocfilehash: 165e91cee3b0b4592f9b746f8b35b46bc73bce50
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "68264566"
---
# <a name="how-to-retrieve-date-and-time-types-as-php-datetime-objects-using-the-pdo_sqlsrv-driver"></a>Recuperación de los tipos de fecha y hora como objetos de fecha y hora PHP mediante el controlador PDO_SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Esta característica, agregada en la versión 5.6.0, solo es válida cuando se utiliza el controlador PDO_SQLSRV para dichos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].

### <a name="to-retrieve-date-and-time-types-as-datetime-objects"></a>Para recuperar los tipos de fecha y hora como objetos DateTime

Al usar PDO_SQLSRV, los tipos de fecha y hora (**smalldatetime**, **datetime**, **date**, **time**, **datetime2** y **datetimeoffset**) se devuelven de forma predeterminada como cadenas. Ni el atributo PDO::ATTR_STRINGIFY_FETCHES ni PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE tienen ningún efecto. Para recuperar los tipos de fecha y hora como objetos [DateTime PHP](http://php.net/manual/en/class.datetime.php), establezca el atributo de conexión o instrucción `PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE` en **true** (es **false** de forma predeterminada).

> [!NOTE]
> Este atributo de conexión o instrucción solo se aplica a la captura normal de tipos de fecha y hora, ya que los objetos DateTime no se pueden especificar como parámetros de salida.

## <a name="example---use-the-connection-attribute"></a>Ejemplo: usar el atributo de conexión
En los siguientes ejemplos se omite la comprobación de errores para una mayor claridad. En este se muestra cómo establecer el atributo de conexión:

```php
<?php
$server = 'myserver';
$databaseName = 'mydatabase';
$username = 'myusername';
$passwd = 'mypasword';
$tableName = 'mytable';

$conn = new PDO("sqlsrv:Server = $server; Database = $databaseName", $username, $passwd);

// To set the connection attribute
$conn->setAttribute(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE, true);
$query = "SELECT DateTimeCol FROM $tableName";
$stmt = $conn->prepare($query);
$stmt->execute();

// Expect a DateTimeCol value as a PHP DateTime type
$row = $stmt->fetch(PDO::FETCH_ASSOC);
var_dump($row);

unset($stmt);
unset($conn);
?>
```

## <a name="example---use-the-statement-attribute"></a>Ejemplo: usar el atributo de instrucción
En este ejemplo se muestra cómo establecer el atributo de instrucción:

```php
<?php
$database = "test";
$server = "(local)";
$conn = new PDO("sqlsrv:server = $server; Database = $database", "", "");
$query = "SELECT DateTimeCol FROM myTable";
$stmt = $conn->prepare($query);
$stmt->setAttribute(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE, true);
$stmt->execute();

// Expect a DateTimeCol value as a PHP DateTime type
$row = $stmt->fetch(PDO::FETCH_NUM);
var_dump($row);

unset($stmt);
unset($conn);
?>
```

## <a name="example---use-the-statement-option"></a>Ejemplo: usar la opción de instrucción
Como alternativa, el atributo de instrucción se puede establecer como opción:

```php
<?php
$database = "test";
$server = "(local)";
$conn = new PDO("sqlsrv:server = $server; Database = $database", "", "");

$dateObj = null;
$query = "SELECT DateTimeCol FROM aTable";
$options = array(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE => true);
$stmt = $conn->prepare($query, $options);
$stmt->execute();
$stmt->bindColumn(1, $dateObj, PDO::PARAM_LOB);
$row = $stmt->fetch(PDO::FETCH_BOUND);
var_dump($dateObj);

unset($stmt);
unset($conn);
?>
```

## <a name="example---retrieve-datetime-types-as-strings"></a>Ejemplo: recuperar los tipos de fecha y hora como cadenas
En el siguiente ejemplo se muestra cómo lograr lo contrario (que no es realmente necesario, puesto que es false de forma predeterminada):

```php
<?php
$database = "MyData";
$conn = new PDO("sqlsrv:server = (local); Database = $database");

$dateStr = null;
$query = 'SELECT DateTimeCol FROM table1';
$options = array(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE => false);
$stmt = $conn->prepare($query, $options);
$stmt->execute();
$stmt->bindColumn(1, $dateStr);
$row = $stmt->fetch(PDO::FETCH_BOUND);
echo $dateStr . PHP_EOL;

unset($stmt);
unset($conn);
?>
```

## <a name="see-also"></a>Consulte también
[Recuperación de datos](../../connect/php/retrieving-data.md)

[Recuperación de los tipos de fecha y hora como cadenas con el controlador SQLSRV](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)