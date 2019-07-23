---
title: PDOStatement::fetch | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4368e362-5bda-4da1-8462-33714683c39f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a69b1093240112a804504f8d0e636ffbdfe8439e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993059"
---
# <a name="pdostatementfetch"></a>PDOStatement::fetch
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera una fila de un conjunto de resultados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
mixed PDOStatement::fetch ([ $fetch_style[, $cursor_orientation[, $cursor_offset]]] );  
```  
  
#### <a name="parameters"></a>Parámetros  
$*fetch_style*: símbolo opcional (entero) que especifica el formato de los datos de la fila. Vea la sección Comentarios para obtener la lista de posibles valores de $*fetch_style*. El valor predeterminado es PDO::FETCH_BOTH.El parámetro  $*fetch_style* del método fetch reemplaza al parámetro $*fetch_style* especificado en el método PDO::query.  
  
$*cursor_orientation*: símbolo opcional (entero) que indica la fila que se va a recuperar cuando la instrucción prepare especifica `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL`. Vea la sección Comentarios para obtener la lista de posibles valores de $*cursor_orientation*. Consulte [PDO::prepare](../../connect/php/pdo-prepare.md) para obtener un ejemplo donde se utiliza un cursor desplazable.  
  
$*cursor_offset*: símbolo opcional (entero) que especifica la fila que se va a capturar cuando $*cursor_orientation* es PDO::FETCH_ORI_ABS o PDO::FETCH_ORI_REL, y PDO::ATTR_CURSOR es PDO::CURSOR_SCROLL.  
  
## <a name="return-value"></a>Valor devuelto  
Un valor mixto que devuelve una fila o False.  
  
## <a name="remarks"></a>Notas  
Cuando se llama al método de captura, el cursor avanza automáticamente. La tabla siguiente contiene la lista de posibles valores de $*fetch_style*.  
  
|$*fetch_style*|Descripción|  
|-------------------|---------------|  
|PDO::FETCH_ASSOC|Especifica una matriz indizada por el nombre de columna.|  
|PDO::FETCH_BOTH|Especifica una matriz indizada por el nombre de columna y el orden basado en 0. Ésta es la opción predeterminada.|  
|PDO::FETCH_BOUND|Devuelve el valor True y asigna los valores tal y como se especifica en [PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md).|  
|PDO::FETCH_CLASS|Crea una instancia y asigna las columnas a las propiedades con nombre.<br /><br />Llame a [PDOStatement::setFetchMode](../../connect/php/pdostatement-setfetchmode.md) antes que al método de captura.|  
|PDO::FETCH_INTO|Actualiza una instancia de la clase solicitada.<br /><br />Llame a [PDOStatement::setFetchMode](../../connect/php/pdostatement-setfetchmode.md) antes que al método de captura.|  
|PDO::FETCH_LAZY|Crea nombres de variables durante el acceso y crea un objeto sin nombre.|  
|PDO::FETCH_NUM|Especifica una matriz indizada por el orden de columna de base cero.|  
|PDO::FETCH_OBJ|Especifica un objeto sin nombre con los nombres de propiedad que se asignan a los nombres de columna.|  
  
Si el cursor se encuentra al final del conjunto de resultados (se ha recuperado la última fila y el cursor ha avanzado más allá del límite del conjunto de resultados) y si es de solo avance (PDO::ATTR_CURSOR = PDO::CURSOR_FWDONLY), se producirá un error en las llamadas de recuperación posteriores.  
  
Si el cursor es desplazable (PDO::ATTR_CURSOR = PDO::CURSOR_SCROLL), el método de captura moverá el cursor dentro del límite del conjunto de resultados. La tabla siguiente contiene la lista de posibles valores de $*cursor_orientation*.  
  
|$*cursor_orientation*|Descripción|  
|--------------------------|---------------|  
|PDO::FETCH_ORI_NEXT|Recupera la fila siguiente. Ésta es la opción predeterminada.|  
|PDO::FETCH_ORI_PRIOR|Recupera la fila anterior.|  
|PDO::FETCH_ORI_FIRST|Recupera la primera fila.|  
|PDO::FETCH_ORI_LAST|Recupera la última fila.|  
|PDO::FETCH_ORI_ABS, *num*|Recupera la fila solicitada en $*cursor_offset* por número de fila.|  
|PDO::FETCH_ORI_REL, *num*|Recupera la fila solicitada en $*cursor_offset* por posición relativa desde la posición actual.|  
  
Si el valor especificado para $*cursor_offset* o $*cursor_orientation* se traduce en una posición fuera del límite del conjunto de resultados, se produce un error de captura.  
  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="example"></a>Ejemplo  
  
```  
<?php  
   $server = "(local)";  
   $database = "AdventureWorks";  
   $conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
   print( "\n---------- PDO::FETCH_CLASS -------------\n" );  
   $stmt = $conn->query( "select * from HumanResources.Department order by GroupName" );  
  
   class cc {  
      function __construct( $arg ) {  
         echo "$arg";  
      }  
  
      function __toString() {  
         return $this->DepartmentID . "; " . $this->Name . "; " . $this->GroupName;  
      }  
   }  
  
   $stmt->setFetchMode(PDO::FETCH_CLASS, 'cc', array( "arg1 " ));  
   while ( $row = $stmt->fetch(PDO::FETCH_CLASS)) {   
      print($row . "\n");   
   }  
  
   print( "\n---------- PDO::FETCH_INTO -------------\n" );  
   $stmt = $conn->query( "select * from HumanResources.Department order by GroupName" );  
   $c_obj = new cc( '' );  
  
   $stmt->setFetchMode(PDO::FETCH_INTO, $c_obj);  
   while ( $row = $stmt->fetch(PDO::FETCH_INTO)) {   
      echo "$c_obj\n";  
   }  
  
   print( "\n---------- PDO::FETCH_ASSOC -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_ASSOC );  
   print_r( $result );  
  
   print( "\n---------- PDO::FETCH_NUM -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_NUM );  
   print_r ($result );  
  
   print( "\n---------- PDO::FETCH_BOTH -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_BOTH );  
   print_r( $result );  
  
   print( "\n---------- PDO::FETCH_LAZY -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_LAZY );  
   print_r( $result );  
  
   print( "\n---------- PDO::FETCH_OBJ -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_OBJ );  
   print $result->Name;  
   print( "\n \n" );  
  
   print( "\n---------- PDO::FETCH_BOUND -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $stmt->bindColumn('Name', $name);  
   $result = $stmt->fetch( PDO::FETCH_BOUND );  
   print $name;  
   print( "\n \n" );  
?>  
```  
  
## <a name="see-also"></a>Consulte también  
[Clase PDOStatement](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
