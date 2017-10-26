---
title: 'Pdostatement:: RowCount | Documentos de Microsoft'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0569f26a-2376-4c20-8813-bd3c87d0ae9f
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e471f6f6ada3cd76bb3b0a3b373b13d7266eea37
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="pdostatementrowcount"></a>PDOStatement::rowCount
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Devuelve el número de filas agregadas, eliminadas o cambiadas en la última instrucción.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
int PDOStatement::rowCount ();  
```  
  
## <a name="return-value"></a>Valor devuelto  
El número de filas agregadas, eliminadas o cambiadas.  
  
## <a name="remarks"></a>Comentarios  
Si la última instrucción SQL ejecutada mediante la clase PDOStatement asociado fue SELECT, el cursor PDO::CURSOR_FWDONLY devuelve -1. Un cursor PDO::CURSOR_SCROLLABLE devuelve el número de filas del conjunto de resultados.  
  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="example"></a>Ejemplo  
En este ejemplo se muestran dos usos de rowCount. En el primero, se devuelve el número de filas que se agregaron a la tabla. En el segundo, se muestra que rowCount puede devolver el número de filas en un conjunto de resultados al especificar un cursor desplazable.  
  
```  
<?php  
$database = "Test";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$col1 = 'a';  
$col2 = 'b';  
  
$query = "insert into Table2(col1, col2) values(?, ?)";  
$stmt = $conn->prepare( $query );  
$stmt->execute( array( $col1, $col2 ) );  
print $stmt->rowCount();  
  
echo "\n\n";  
  
$con = null;  
$database = "AdventureWorks";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "select * from Person.ContactType";  
$stmt = $conn->prepare( $query, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL));  
$stmt->execute();  
print $stmt->rowCount();  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[Clase PDOStatement](../../connect/php/pdostatement-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

