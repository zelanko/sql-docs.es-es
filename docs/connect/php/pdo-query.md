---
title: 'PDO:: Query | Documentos de Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f6f5e6d4-8ca9-4f06-89ed-de65ad3952a2
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b0ca9c3ffb50dc24d70f4db143d665a20794f65d
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="pdoquery"></a>PDO::query
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Ejecuta una consulta SQL y devuelve un conjunto de resultados como un objeto PDOStatement.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
PDOStatement PDO::query ($statement[, $fetch_style);  
```  
  
#### <a name="parameters"></a>Parámetros  
*$statement*: la instrucción SQL que se quiere ejecutar.  
  
*$fetch_style*: las instrucciones opcionales sobre cómo realizar la consulta. Para obtener información más detallada, consulte la sección Comentarios. $*fetch_style* de PDO:: Query puede reemplazarse por $*fetch_style* en PDO:: Fetch.  
  
## <a name="return-value"></a>Valor devuelto  
Si la llamada se realiza correctamente, PDO::query devuelve un objeto PDOStatement. Si se produce un error en la llamada, PDO::query lanza un objeto PDOException o devuelve el valor False, en función de la configuración de PDO::ATTR_ERRMODE.  
  
## <a name="exceptions"></a>Excepciones  
PDOException.  
  
## <a name="remarks"></a>Comentarios  
Una consulta ejecutada con PDO:: Query puede ejecutar una instrucción preparada o directa, en función del valor de PDO:: sqlsrv_attr_direct_query. Para obtener más información, vea [Direct Statement Execution and Prepared Statement Execution in the PDO_SQLSRV Driver (Ejecución de la instrucción preparada o directa en el controlador PDO_SQLSRV)](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md).  
  
PDO:: sqlsrv_attr_query_timeout también afecta al comportamiento de PDO:: exec; Para obtener más información, consulte [PDO:: setAttribute](../../connect/php/pdo-setattribute.md).  
  
Puede especificar las siguientes opciones para $*fetch_style*.  
  
|style|Description|  
|---------|---------------|  
|PDO::FETCH_COLUMN, *num*|Consultas de datos de la columna especificada. La primera columna de la tabla es 0.|  
|Fetch_class, '*classname*', matriz ( *arglist* )|Crea una instancia de una clase y asigna nombres de columna a las propiedades de la clase. Si el constructor de clase toma uno o varios parámetros, también se puede transmitir un objeto *arglist*.|  
|PDO::FETCH_CLASS, '*classname*'|Asigna nombres de columna a las propiedades de una clase existente.|  
  
Llame a PDOStatement::closeCursor para liberar recursos de base de datos asociados al objeto PDOStatement antes de volver a llamar a PDO::query.  
  
Puede cerrar un objeto PDOStatement si se establece el valor en Null.  
  
Si no se recuperan todos los datos de un conjunto de resultados, la siguiente llamada a PDO::query se realizará correctamente.  
  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="example"></a>Ejemplo  
En este ejemplo se muestran varias consultas.  
  
```  
<?php  
$database = "AdventureWorks";  
$conn = new PDO( "sqlsrv:server=(local) ; Database = $database", "", "");  
$conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
$conn->setAttribute( PDO::SQLSRV_ATTR_QUERY_TIMEOUT, 1 );  
  
$query = 'select * from Person.ContactType';  
  
// simple query  
$stmt = $conn->query( $query );  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print_r( $row['Name'] ."\n" );  
}  
  
echo "\n........ query for a column ............\n";  
  
// query for one column  
$stmt = $conn->query( $query, PDO::FETCH_COLUMN, 1 );  
while ( $row = $stmt->fetch() ){  
   echo "$row\n";  
}  
  
echo "\n........ query with a new class ............\n";  
$query = 'select * from HumanResources.Department order by GroupName';  
// query with a class  
class cc {  
   function __construct( $arg ) {  
      echo "$arg";  
   }  
  
   function __toString() {  
      return $this->DepartmentID . "; " . $this->Name . "; " . $this->GroupName;  
   }  
}  
  
$stmt = $conn->query( $query, PDO::FETCH_CLASS, 'cc', array( "arg1 " ));  
  
while ( $row = $stmt->fetch() ){  
   echo "$row\n";  
}  
  
echo "\n........ query into an existing class ............\n";  
$c_obj = new cc( '' );  
$stmt = $conn->query( $query, PDO::FETCH_INTO, $c_obj );  
while ( $stmt->fetch() ){  
   echo "$c_obj\n";  
}  
  
$stmt = null;  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[Clase PDO](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
