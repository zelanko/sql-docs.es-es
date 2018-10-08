---
title: 'PDO:: Prepare | Microsoft Docs'
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a8b16fdc-c748-49be-acf2-a6ac7432d16b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca5e1a4d0dd3f76b3fabefa6549eb644a894845a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47745143"
---
# <a name="pdoprepare"></a>PDO::prepare
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Prepara una instrucción para su ejecución.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
PDOStatement PDO::prepare ( $statement [, array(key_pair)] )  
```  
  
#### <a name="parameters"></a>Parámetros  
$*statement*: una cadena que contiene la instrucción SQL.  
  
*key_pair*: una matriz que contiene un valor y un nombre de atributo. Para obtener más información, vea la sección Comentarios.  
  
## <a name="return-value"></a>Valor devuelto  
Devuelve un objeto PDOStatement si se ejecuta correctamente. En caso de error, devuelve un objeto PDOException o False, según el valor de PDO::ATTR_ERRMODE.  
  
## <a name="remarks"></a>Notas  
Los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] no evalúan instrucciones preparadas hasta la ejecución.  
  
En la siguiente tabla se incluyen los posibles valores *key_pair*.  
  
|Key|Descripción|  
|-------|---------------|  
|PDO::ATTR_CURSOR|Especifica el comportamiento del cursor. El valor predeterminado es PDO::CURSOR_FWDONLY. PDO::CURSOR_SCROLL es un cursor estático.<br /><br />Por ejemplo, `array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY )`.<br /><br />Si utiliza PDO::CURSOR_SCROLL, puede utilizar PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE, que se describe a continuación.<br /><br />Vea [Cursor Types &#40;PDO_SQLSRV Driver&#41; (Tipos de cursor &#40;Controlador PDO_SQLSRV&#41;)](../../connect/php/cursor-types-pdo-sqlsrv-driver.md) para obtener más información sobre los conjuntos de resultados y los cursores del controlador PDO_SQLSRV.|  
|PDO::ATTR_EMULATE_PREPARES|De forma predeterminada, este atributo es false, que se puede cambiar este `PDO::ATTR_EMULATE_PREPARES => true`. Consulte [emular preparar](#emulate-prepare) para obtener detalles y ejemplo.|
|PDO::SQLSRV_ATTR_ENCODING|PDO::SQLSRV_ENCODING_UTF8 (valor predeterminado)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|  
|PDO::SQLSRV_ATTR_DIRECT_QUERY|Cuando es True, especifica la ejecución de una consulta directa. False implica la ejecución de una instrucción preparada. Para obtener más información sobre PDO::SQLSRV_ATTR_DIRECT_QUERY, vea [Direct Statement Execution and Prepared Statement Execution in the PDO_SQLSRV Driver](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md) (Ejecución de la instrucción preparada o directa en el controlador PDO_SQLSRV).|  
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|Para obtener más información, consulte [PDO::setAttribute](../../connect/php/pdo-setattribute.md).|  
  
Cuando se usa PDO::ATTR_CURSOR = > PDO::CURSOR_SCROLL, se puede utilizar PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE. Por ejemplo,  
  
```  
array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL, PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_DYNAMIC));  
```  
  
En la siguiente tabla se muestran los posibles valores para PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE.  
  
|Valor|Descripción|  
|---------|---------------|  
|PDO::SQLSRV_CURSOR_BUFFERED|Crea un cursor estático de cliente (en búfer). Para obtener más información sobre los cursores de cliente, vea [Cursor Types &#40;PDO_SQLSRV Driver&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md) (Tipos de cursor &#40;Controlador PDO_SQLSRV&#41;).|  
|PDO::SQLSRV_CURSOR_DYNAMIC|Crea un cursor dinámico de servidor (no almacenado en búfer), que le permite acceder a las filas en cualquier orden y reflejará los cambios de la base de datos.|  
|PDO::SQLSRV_CURSOR_KEYSET_DRIVEN|Crea un cursor de conjunto de claves de servidor. Los cursores de conjunto de claves no actualizan el recuento de filas si se elimina una fila de la tabla (las filas eliminadas se devuelven sin valores).|  
|PDO::SQLSRV_CURSOR_STATIC|Crea un cursor estático de servidor, que le permite acceder a las filas en cualquier orden, pero no reflejará los cambios de la base de datos.<br /><br />PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL implica PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_STATIC.|  
  
Puede cerrar un objeto PDOStatement si se establece el valor en Null.  
  
## <a name="example"></a>Ejemplo  
En este ejemplo se muestra cómo usar el método PDO::prepare con marcadores de parámetros y un cursor de solo avance.  
  
```  
<?php  
$database = "Test";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$col1 = 'a';  
$col2 = 'b';  
  
$query = "insert into Table1(col1, col2) values(?, ?)";  
$stmt = $conn->prepare( $query, array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY, PDO::SQLSRV_ATTR_QUERY_TIMEOUT => 1  ) );  
$stmt->execute( array( $col1, $col2 ) );  
print $stmt->rowCount();  
echo "\n";  
  
$query = "insert into Table1(col1, col2) values(:col1, :col2)";  
$stmt = $conn->prepare( $query, array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY, PDO::SQLSRV_ATTR_QUERY_TIMEOUT => 1  ) );  
$stmt->execute( array( ':col1' => $col1, ':col2' => $col2 ) );  
print $stmt->rowCount();  
  
$stmt = null  
?>  
```  

## <a name="example"></a>Ejemplo  
En este ejemplo se muestra cómo utilizar el método PDO::prepare con un cursor de cliente. Para obtener un ejemplo que muestra un cursor de servidor, vea [Cursor Types &#40;PDO_SQLSRV Driver&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md) (Tipos de cursor &#40;Controlador PDO_SQLSRV&#41;).  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "select * from Person.ContactType";  
$stmt = $conn->prepare( $query, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL));  
$stmt->execute();  
  
echo "\n";  
  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print "$row[Name]\n";  
}  
echo "\n..\n";  
  
$row = $stmt->fetch( PDO::FETCH_BOTH, PDO::FETCH_ORI_FIRST );  
print_r($row);  
  
$row = $stmt->fetch( PDO::FETCH_ASSOC, PDO::FETCH_ORI_REL, 1 );  
print "$row[Name]\n";  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_NEXT );  
print "$row[1]\n";  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_PRIOR );  
print "$row[1]..\n";  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_ABS, 0 );  
print_r($row);  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_LAST );  
print_r($row);  
?>  
```  

<a name="emulate-prepare" />

## <a name="example"></a>Ejemplo 

En este ejemplo se muestra cómo usar el método PDO:: Prepare con `PDO::ATTR_EMULATE_PREPARES` establecido en true. 

```
<?php
$serverName = "yourservername";
$username = "yourusername";
$password = "yourpassword";
$database = "tempdb";
$conn = new PDO("sqlsrv:server = $serverName; Database = $database", $username, $password);

$pdo_options = array();
$pdo_options[PDO::ATTR_EMULATE_PREPARES] = true;
$pdo_options[PDO::SQLSRV_ATTR_ENCODING] = PDO::SQLSRV_ENCODING_UTF8;

$stmt = $conn->prepare("CREATE TABLE TEST([id] [int] IDENTITY(1,1) NOT NULL, 
                                          [name] nvarchar(max))", 
                                          $pdo_options);
$stmt->execute();

$prefix = '가각';
$name = '가각ácasa';
$name2 = '가각sample2';

$stmt = $conn->prepare("INSERT INTO TEST(name) VALUES(:p0)", $pdo_options);
$stmt->execute(['p0' => $name]);
unset($stmt);

$stmt = $conn->prepare("SELECT * FROM TEST WHERE NAME LIKE :p0", $pdo_options);
$stmt->execute(['p0' => "$prefix%"]);
foreach ($stmt as $row) {
    echo "\n" . 'FOUND: ' . $row['name'];
}

unset($stmt);
unset($conn);
?>
```

El controlador PDO_SQLSRV reemplaza internamente los marcadores de posición con los parámetros que están enlazados por [PDOStatement::bindParam()](../../connect/php/pdostatement-bindparam.md). Por lo tanto, una cadena de consulta SQL con ningún marcador de posición se envía al servidor. Considere este ejemplo,

```
$statement = $PDO->prepare("INSERT into Customers (CustomerName, ContactName) VALUES (:cus_name, :con_name)");
$statement->bindParam(:cus_name, "Cardinal");
$statement->bindParam(:con_name, "Tom B. Erichsen");
$statement->execute();
```

Con `PDO::ATTR_EMULATE_PREPARES` establecido en false (el caso predeterminado), los datos enviados a la base de datos están:

```
"INSERT into Customers (CustomerName, ContactName) VALUES (:cus_name, :con_name)"
Information on :cus_name parameter
Information on :con_name parameter
```

El servidor ejecuta la consulta con su característica de consulta con parámetros para enlazar parámetros. Por otro lado, con `PDO::ATTR_EMULATE_PREPARES` establecido en true, la consulta enviada al servidor es esencialmente:

```
"INSERT into Customers (CustomerName, ContactName) VALUES ('Cardinal', 'Tom B. Erichsen')"
```

Establecer `PDO::ATTR_EMULATE_PREPARES` en true puede omitir algunas restricciones en SQL Server. Por ejemplo, SQL Server no admite parámetros con nombre o posicionales en algunas cláusulas de Transact-SQL. Además, SQL Server tiene un límite de 2100 parámetros de enlace.

> [!NOTE]
> Con emulate prepara establecido en true, la seguridad de las consultas con parámetros no está en vigor. Por lo tanto, la aplicación debe asegurarse de que los datos enlazados a los parámetros no contengan código Transact-SQL malintencionado.

### <a name="encoding"></a>Encoding

Si el usuario desea enlazar parámetros con distintas codificaciones (por ejemplo, UTF-8 o binario), usuario debe especificar claramente la codificación en el script PHP.

El controlador PDO_SQLSRV comprueba primero la codificación especificada en `PDO::bindParam()` (por ejemplo, `$statement->bindParam(:cus_name, "Cardinal", PDO::PARAM_STR, 10, PDO::SQLSRV_ENCODING_UTF8)`). 

Si no se encuentra, el controlador comprueba si cualquier codificación está establecido `PDO::prepare()` o `PDOStatement::setAttribute()`. En caso contrario, el controlador utilizará la codificación especificada en `PDO::__construct()` o `PDO::setAttribute()`.

### <a name="limitations"></a>Limitaciones

Como puede ver, enlace se realiza internamente por el controlador. En el servidor, se envía una consulta válida para la ejecución sin ningún parámetro. En comparación con el caso normal, como resultado algunas limitaciones cuando la característica de consulta con parámetros no está en uso.

- No funciona para los parámetros que se enlazan como `PDO::PARAM_INPUT_OUTPUT`.
    - Cuando el usuario especifica `PDO::PARAM_INPUT_OUTPUT` en `PDO::bindParam()`, se produce una excepción de DOP.
- No funciona para los parámetros que están enlazados como parámetros de salida.
    - Cuando el usuario crea una instrucción preparada con marcadores de posición que está destinado a los parámetros de salida (es decir, inmediatamente después de un marcador de posición, teniendo un signo igual, al igual que `SELECT ? = COUNT(*) FROM Table1`), se produce una excepción de DOP.
    - Cuando una instrucción preparada, invoca un procedimiento almacenado con un marcador de posición como argumento para un parámetro de salida, se produce ninguna excepción porque el controlador no puede detectar el parámetro de salida. Sin embargo, la variable que el usuario proporciona para el parámetro de salida permanecerá sin cambios.
- Duplicados marcadores de posición para un parámetro codificado binario no funcionará.

## <a name="see-also"></a>Ver también  
[Clase PDO](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
