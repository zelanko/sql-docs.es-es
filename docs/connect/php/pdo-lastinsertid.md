---
title: PDO::lastInsertId | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 0c617b53-a74b-4d5b-b76b-3ec7f1b8e8de
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6106d830a48b4ef89d85b88e7264e08209947ecc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66762007"
---
# <a name="pdolastinsertid"></a>PDO::lastInsertId
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Devuelve el identificador de la fila que se insertó más recientemente en una tabla de la base de datos. La tabla debe tener una columna IDENTITY NOT NULL. Si se proporciona un nombre de secuencia, `lastInsertId` devuelve inserta el último número de secuencia para el nombre de la secuencia proporcionada (para obtener más información acerca de los números de secuencia, vea [aquí](https://docs.microsoft.com/sql/relational-databases/sequence-numbers/sequence-numbers)).
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
string PDO::lastInsertId ([ $name = NULL ] );  
```  
  
#### <a name="parameters"></a>Parámetros  
$*name*: una cadena opcional que le permite especificar un nombre de secuencia. 
  
## <a name="return-value"></a>Valor devuelto  
Si se proporciona ningún nombre de secuencia, una cadena del identificador de la fila agregado más recientemente.
Si se proporciona un nombre de secuencia, una cadena del identificador de la secuencia de agregado más recientemente.
Si se produce un error en la llamada al método, se devuelve una cadena vacía.
  
## <a name="remarks"></a>Notas  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
Entre las versiones 2.0 y 4.3, el parámetro opcional es un nombre de tabla y el valor devuelto es el identificador de la fila agregada recientemente a la tabla proporcionada.
Empezando con 5.0, el parámetro opcional se considera como un nombre de la secuencia y el valor devuelto es la secuencia de agregado más recientemente para el nombre de la secuencia proporcionada.
Si se proporciona un nombre de tabla para las versiones después 4.3, `lastInsertId` devuelve una cadena vacía.
Se admiten secuencias sólo en SQL Server 2012 y versiones posteriores.
  
## <a name="example"></a>Ejemplo
  
```
<?php
$server = "myserver";
$databaseName = "mydatabase";
$uid = "myusername";
$pwd = "mypasword";

try {
    $conn = new PDO("sqlsrv:Server=$server;Database=$databaseName", $uid, $pwd);
    
    // One sequence, two tables
    $tableName1 = 'seqtable1';
    $tableName2 = 'seqtable2';
    $sequenceName = 'sequence1';

    $stmt = $conn->query("IF OBJECT_ID('$sequenceName', 'SO') IS NOT NULL DROP SEQUENCE $sequenceName");
    $sql = "CREATE TABLE $tableName1 (seqnum INTEGER NOT NULL PRIMARY KEY, SomeNumber INT)";
    $stmt = $conn->query($sql);
    $sql = "CREATE TABLE $tableName2 (ID INT IDENTITY(1,2), SomeValue char(10))";
    $stmt = $conn->query($sql);

    $sql = "CREATE SEQUENCE $sequenceName AS INTEGER START WITH 1 INCREMENT BY 1 MINVALUE 1 MAXVALUE 100 CYCLE";
    $stmt = $conn->query($sql);

    $ret = $conn->exec("INSERT INTO $tableName1 VALUES( NEXT VALUE FOR $sequenceName, 20)");
    $ret = $conn->exec("INSERT INTO $tableName1 VALUES( NEXT VALUE FOR $sequenceName, 40)");
    $ret = $conn->exec("INSERT INTO $tableName1 VALUES( NEXT VALUE FOR $sequenceName, 60)");
    $ret = $conn->exec("INSERT INTO $tableName2 VALUES( '20' )");
    
    // return the last sequence number if sequence name is provided
    $lastSeq1 = $conn->lastInsertId($sequenceName);
    
    // defaults to $tableName2 -- because it returns the last inserted id value
    $lastRow = $conn->lastInsertId();
        
    // providing a table name in lastInsertId should return an empty string
    $lastSeq2 = $conn->lastInsertId($tableName2);
    
    echo "Last sequence number = $lastSeq1\n";
    echo "Last inserted ID     = $lastRow\n";
    echo "Last inserted ID when a table name is supplied = $lastSeq2\n";

    // One table, two sequences    
    $tableName = 'seqtable';
    $sequence1 = 'sequence1';
    $sequence2 = 'sequenceNeg1';
    $stmt = $conn->query("IF OBJECT_ID('$sequence1', 'SO') IS NOT NULL DROP SEQUENCE $sequence1");
    $stmt = $conn->query("IF OBJECT_ID('$sequence2', 'SO') IS NOT NULL DROP SEQUENCE $sequence2");
    $sql = "CREATE TABLE $tableName (ID INT IDENTITY(1,1), SeqNumInc INTEGER NOT NULL PRIMARY KEY, SomeNumber INT)";
    $stmt = $conn->query($sql);
    $sql = "CREATE SEQUENCE $sequence1 AS INTEGER START WITH 1 INCREMENT BY 1 MINVALUE 1 MAXVALUE 100";
    $stmt = $conn->query($sql);

    $sql = "CREATE SEQUENCE $sequence2 AS INTEGER START WITH 200 INCREMENT BY -1 MINVALUE 101 MAXVALUE 200";
    $stmt = $conn->query($sql);
    $ret = $conn->exec("INSERT INTO $tableName VALUES( NEXT VALUE FOR $sequence1, 20 )");
    $ret = $conn->exec("INSERT INTO $tableName VALUES( NEXT VALUE FOR $sequence2, 180 )");
    $ret = $conn->exec("INSERT INTO $tableName VALUES( NEXT VALUE FOR $sequence1, 40 )");
    $ret = $conn->exec("INSERT INTO $tableName VALUES( NEXT VALUE FOR $sequence2, 160 )");
    $ret = $conn->exec("INSERT INTO $tableName VALUES( NEXT VALUE FOR $sequence1, 60 )");
    $ret = $conn->exec("INSERT INTO $tableName VALUES( NEXT VALUE FOR $sequence2, 140 )");
    
    // return the last sequence number of 'sequence1'
    $lastSeq1 = $conn->lastInsertId($sequence1);

    // return the last sequence number of 'sequenceNeg1'
    $lastSeq2 = $conn->lastInsertId($sequence2);

    // providing a table name in lastInsertId should return an empty string
    $lastSeq3 = $conn->lastInsertId($tableName);
    
    echo "Last sequence number of sequence1    = $lastSeq1\n";
    echo "Last sequence number of sequenceNeg1 = $lastSeq2\n";
    echo "Last sequence number when a table name is supplied = $lastSeq3\n";

    $stmt = $conn->query("DROP TABLE $tableName1");
    $stmt = $conn->query("DROP TABLE $tableName2");
    $stmt = $conn->query("DROP SEQUENCE $sequenceName");
    $stmt = $conn->query("DROP TABLE $tableName");
    $stmt = $conn->query("DROP SEQUENCE $sequence1");
    $stmt = $conn->query("DROP SEQUENCE $sequence2");
    
    unset($stmt);
    unset($conn);
} catch (Exception $e) {
    echo "Exception $e\n";
}

?>
```

El resultado esperado es:

```
Last sequence number = 3
Last inserted ID     = 1
Last inserted ID when a table name is supplied =

Last sequence number of sequence1    = 3
Last sequence number of sequenceNeg1 = 198
Last sequence number when a table name is supplied = 

```

## <a name="see-also"></a>Consulte también  
[Clase PDO](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
