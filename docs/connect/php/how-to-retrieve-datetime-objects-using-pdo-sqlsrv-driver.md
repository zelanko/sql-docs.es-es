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
manager: mbarwin
ms.openlocfilehash: 54e5b5c9c1ba59ed64db740fbbb1a643e7cb1b2c
ms.sourcegitcommit: c1105ce638078d2c941cd656b34f78486e6b2d89
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 02/22/2019
ms.locfileid: "56676541"
---
# <a name="how-to-retrieve-date-and-time-types-as-php-datetime-objects-using-the-pdosqlsrv-driver"></a>Recuperación de los tipos de fecha y hora como objetos de fecha y hora PHP mediante el controlador PDO_SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Esta característica, agregada en la versión 5.6.0, solo es válida cuando se usa el controlador PDO_SQLSRV para el [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].

### <a name="to-retrieve-date-and-time-types-as-datetime-objects"></a>Para recuperar tipos de fecha y hora como objetos de fecha y hora

Cuando se usa PDO_SQLSRV, tipos de fecha y hora (**smalldatetime**, **datetime**, **fecha**, **tiempo**, **datetime2**, y **datetimeoffset**) están de forma predeterminada que se devuelven como cadenas. Ni el PDO::ATTR_STRINGIFY_FETCHES ni el atributo PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE tiene ningún efecto. Con el fin de recuperar tipos de fecha y hora como [DateTime PHP](http://php.net/manual/en/class.datetime.php) objetos, establezca el atributo de conexión o instrucción `PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE` a **true** (es **false** de forma predeterminada).

> [!NOTE]
> Esta conexión o el atributo de instrucción solo se aplica a capturar regular de los tipos de fecha y hora porque los objetos de fecha y hora no se puede especificar como parámetros de salida.

## <a name="example---use-the-connection-attribute"></a>Por ejemplo, use el atributo de conexión
Los ejemplos siguientes omiten comprobación de errores para mayor claridad. Éste muestra cómo establecer el atributo de conexión:

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

## <a name="example---use-the-statement-attribute"></a>Por ejemplo, use el atributo de instrucción
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

## <a name="example---use-the-statement-option"></a>Por ejemplo, use la opción de instrucción
Como alternativa, se puede establecer el atributo de instrucción como una opción:

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

## <a name="example---retrieve-datetime-types-as-strings"></a>Ejemplo: recuperar tipos de fecha y hora como cadenas
El ejemplo siguiente muestra cómo lograr el efecto contrario (que no es realmente necesario porque es false de forma predeterminada):

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