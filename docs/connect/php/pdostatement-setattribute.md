---
title: 'Pdostatement:: setAttribute | Documentos de Microsoft'
ms.custom: ''
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 329d9b5e-1c5d-40b0-9127-1051d0646fc7
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dbbb53da59f463c8dc601963f02b5b77ef6ec4b6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="pdostatementsetattribute"></a>PDOStatement::setAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Establece un valor de atributo, o un atributo PDO predefinido o un controlador personalizado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
bool PDOStatement::setAttribute ($attribute, $value );  
```  
  
#### <a name="parameters"></a>Parámetros  
$*atributo*: un entero, uno de los attr_ * o PDO:: sqlsrv_attr_\* constantes. Consulte la sección Comentarios para obtener la lista de atributos disponibles.  
  
$*valor*: el valor (mixto) que puede establecer para la especificada $*atributo*.  
  
## <a name="return-value"></a>Valor devuelto  
Se devuelve True si se ejecuta correctamente; de lo contrario, se devuelve False.  
  
## <a name="remarks"></a>Comentarios  
En la tabla siguiente se incluye la lista de atributos disponibles.  
  
|attribute|Valores|Description|  
|-------------|----------|---------------|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|1 para el límite de memoria PHP.|Configura el tamaño de búfer que contiene el conjunto de resultados de un cursor de cliente.<br /><br />El valor predeterminado es 10240 KB (10 MB).<br /><br />Para obtener más información acerca de los cursores de cliente, consulte [tipos de Cursor &#40;controlador PDO_SQLSRV&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_ENCODING|Integer<br /><br />PDO:: sqlsrv_encoding_utf8 (valor predeterminado)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|Establece el juego de caracteres que utiliza el controlador para comunicarse con el servidor.|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|true o false|Controla capturas numéricos de las columnas con tipos SQL numéricos (bit, integer, smallint, tinyint, float o real).<br /><br />Cuando marca de la opción de conexión ATTR_STRINGIFY_FETCHES está activada, el valor devuelto es una cadena aunque SQLSRV_ATTR_FETCHES_NUMERIC_TYPE está activado.<br /><br />Cuando el tipo devuelto de PDO en la columna de enlace es PDO_PARAM_INT, el valor devuelto de una columna de tipo entero es un tipo int aunque SQLSRV_ATTR_FETCHES_NUMERIC_TYPE está desactivada.|  
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|Integer|Establece el tiempo de espera de consulta en segundos.<br /><br />De forma predeterminada, el controlador esperará indefinidamente para obtener los resultados. No se permiten números negativos.<br /><br />0 significa sin tiempo de espera.|  
  
## <a name="example"></a>Ejemplo  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "", array('MultipleActiveResultSets'=>false )  );  
  
$stmt = $conn->prepare('SELECT * FROM Person.ContactType');  
  
echo $stmt->getAttribute( constant( "PDO::ATTR_CURSOR" ) );  
  
echo "\n";  
  
$stmt->setAttribute(PDO::SQLSRV_ATTR_QUERY_TIMEOUT, 2);  
echo $stmt->getAttribute( constant( "PDO::SQLSRV_ATTR_QUERY_TIMEOUT" ) );  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[Clase PDOStatement](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
