---
title: PDOStatement::setAttribute | Microsoft Docs
ms.custom: ''
ms.date: 04/22/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 329d9b5e-1c5d-40b0-9127-1051d0646fc7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6dab577ea12544d6dd40081283b46378dd07d5e6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992939"
---
# <a name="pdostatementsetattribute"></a>PDOStatement::setAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Establece un valor de atributo, o un atributo PDO predefinido o un controlador personalizado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
bool PDOStatement::setAttribute ($attribute, $value );  
```  
  
#### <a name="parameters"></a>Parámetros  
$*attribute*: entero; una de las constantes PDO::ATTR_* o PDO::SQLSRV_ATTR_\*. Consulte la sección Comentarios para obtener la lista de atributos disponibles.  
  
$*value*: el valor (mixto) que se establecerá para el parámetro $*attribute* especificado.  
  
## <a name="return-value"></a>Valor devuelto  
Se devuelve True si se ejecuta correctamente; de lo contrario, se devuelve False.  
  
## <a name="remarks"></a>Notas  
En la tabla siguiente se incluye la lista de atributos disponibles.  
  
|attribute|Valores|Descripción|  
|-------------|----------|---------------|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|1 para el límite de memoria PHP.|Configura el tamaño de búfer que contiene el conjunto de resultados de un cursor de cliente.<br /><br />El valor predeterminado es 10 240 KB (10 MB).<br /><br />Para obtener más información sobre los cursores de cliente, vea [Cursor Types &#40;PDO_SQLSRV Driver&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md) (Tipos de cursor &#40;Controlador PDO_SQLSRV&#41;).|  
|PDO::SQLSRV_ATTR_DECIMAL_PLACES|Un entero comprendido entre 0 y 4, ambos incluidos|Especifica el número de lugares decimales al dar formato a los valores de moneda obtenidos.<br /><br />Se omitirá cualquier entero negativo o un valor mayor que 4.<br /><br />Esta opción solo funciona si PDO::SQLSRV_ATTR_FORMAT_DECIMALS es true.<br /><br />Esta opción también se puede establecer en el nivel de conexión. Si es así, esta opción invalida la opción de nivel de conexión.<br /><br />Para más información, vea [Aplicación de formato a cadenas decimales y valores de moneda (controlador PDO_SQLSRV)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md).|
|PDO::SQLSRV_ATTR_ENCODING|Integer<br /><br />PDO::SQLSRV_ENCODING_UTF8 (valor predeterminado)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|Establece el juego de caracteres que utiliza el controlador para comunicarse con el servidor.|  
|PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE|true o false|Especifica si debe recuperar tipos de fecha y hora como objetos [PHP DateTime](http://php.net/manual/en/class.datetime.php). Si el valor se deja como false, el comportamiento predeterminado es devolverlos como cadenas.<br /><br />Esta opción también se puede establecer en el nivel de conexión. Si es así, esta opción invalida la opción de nivel de conexión.<br /><br />Para más información, vea [Recuperación de los tipos de fecha y hora como objetos de fecha y hora PHP mediante el controlador PDO_SQLSRV](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|true o false|Controla los resultados numéricos de las columnas con los tipos SQL numéricos (bit, integer, smallint, tinyint, float o real).<br /><br />Cuando la marca de la opción de conexión ATTR_STRINGIFY_FETCHES está activada, el valor devuelto es una cadena incluso cuando SQLSRV_ATTR_FETCHES_NUMERIC_TYPE está activado.<br /><br />Cuando el tipo devuelto de PDO en la columna de enlace es PDO_PARAM_INT, el valor devuelto de una columna de enteros es un valor int aunque SQLSRV_ATTR_FETCHES_NUMERIC_TYPE esté desactivado.|  
|PDO::SQLSRV_ATTR_FORMAT_DECIMALS|true o false|Especifica si se agregan ceros iniciales a las cadenas decimales cuando proceda. Si se establece, esta opción habilita la opción de PDO::SQLSRV_ATTR_DECIMAL_PLACES para aplicar formato a los tipos de divisa. Si el valor se deja como false, se usa el comportamiento predeterminado de devolver la precisión exacta y omitir los ceros iniciales de los valores menores que 1.<br /><br />Esta opción también se puede establecer en el nivel de conexión. Si es así, esta opción invalida la opción de nivel de conexión.<br /><br />Para más información, vea [Aplicación de formato a cadenas decimales y valores de moneda (controlador PDO_SQLSRV)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md).| 
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
  
## <a name="see-also"></a>Consulte también  
[Clase PDOStatement](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
