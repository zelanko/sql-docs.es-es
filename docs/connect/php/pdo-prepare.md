---
title: 'PDO:: Prepare | Documentos de Microsoft'
ms.custom: 
ms.date: 07/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a8b16fdc-c748-49be-acf2-a6ac7432d16b
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7a83fabca6866e8e3b106d8696ef03514a93aa62
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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
  
*key_pair*: una matriz que contiene un nombre de atributo y valor. Para obtener más información, vea la sección Comentarios.  
  
## <a name="return-value"></a>Valor devuelto  
Devuelve un objeto PDOStatement si se ejecuta correctamente. En caso de error, devuelve un objeto PDOException o False, según el valor de PDO::ATTR_ERRMODE.  
  
## <a name="remarks"></a>Comentarios  
Los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] no evalúan instrucciones preparadas hasta la ejecución.  
  
En la tabla siguiente se enumera los posibles *key_pair* valores.  
  
|Key|Description|  
|-------|---------------|  
|PDO::ATTR_CURSOR|Especifica el comportamiento del cursor. El valor predeterminado es PDO::CURSOR_FWDONLY. PDO::CURSOR_SCROLL es un cursor estático.<br /><br />Por ejemplo, `array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY )`.<br /><br />Si utiliza PDO::CURSOR_SCROLL, puede utilizar PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE, que se describe a continuación.<br /><br />Vea [tipos de Cursor &#40; Controlador PDO_SQLSRV &#41; ](../../connect/php/cursor-types-pdo-sqlsrv-driver.md) para obtener más información sobre los conjuntos de resultados y los cursores en el controlador PDO_SQLSRV.|  
|PDO::ATTR_EMULATE_PREPARES|Cuando PDO:: attr_emulate_prepares está activada, los marcadores de posición en una instrucción preparada se sustituye por parámetros enlazados. Una instrucción SQL completa con ningún marcador de posición, a continuación, se envía a la base de datos en ejecución. <br /><br />PDO:: attr_emulate_prepares puede utilizarse para omitir algunas restricciones en SQL Server. Por ejemplo, SQL Server no admite parámetros con nombre o posicionales en algunas cláusulas de Transact-SQL. Además, SQL Server tiene un límite de 2100 parámetros de enlace.<br /><br />Puede establecer el atributo PDO:: attr_emulate_prepares como true. Por ejemplo:<br /><br />`PDO::ATTR_EMULATE_PREPARES => true`<br /><br />De manera predeterminada, este atributo está establecido como False.<br /><br />**Nota:** La seguridad de las consultas con parámetros no está activada cuando se usa `PDO::ATTR_EMULATE_PREPARES => true`. La aplicación debe asegurarse de que los datos que se enlaza a los parámetros no contienen código malintencionado de Transact-SQL.<br /><br />**Limitaciones:**: dado que los parámetros no se enlazan mediante la característica de consulta con parámetros de la base de datos, no se admiten parámetros input_output y de salida.|  
|PDO::SQLSRV_ATTR_ENCODING|PDO::SQLSRV_ENCODING_UTF8 (valor predeterminado)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|  
|PDO::SQLSRV_ATTR_DIRECT_QUERY|Cuando es True, especifica la ejecución de una consulta directa. False implica la ejecución de una instrucción preparada. Para obtener más información sobre PDO:: sqlsrv_attr_direct_query, consulte [Direct Statement Execution and Prepared Statement Execution en el controlador PDO_SQLSRV](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|Para obtener más información, consulte [PDO::setAttribute](../../connect/php/pdo-setattribute.md).|  
  
Cuando se usa PDO::ATTR_CURSOR = > PDO::CURSOR_SCROLL, se puede utilizar PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE. Por ejemplo,  
  
```  
array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL, PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_DYNAMIC));  
```  
  
En la siguiente tabla se muestran los posibles valores para PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE.  
  
|Valor|Description|  
|---------|---------------|  
|PDO::SQLSRV_CURSOR_BUFFERED|Crea un cursor estático de cliente (en búfer). Para obtener más información acerca de los cursores de cliente, consulte [tipos de Cursor &#40; Controlador PDO_SQLSRV &#41; ](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).|  
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
En este ejemplo se muestra cómo utilizar el método PDO::prepare con un cursor de cliente. Para obtener un ejemplo que muestra un cursor de servidor, consulte [tipos de Cursor &#40; Controlador PDO_SQLSRV &#41; ](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).  
  
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
  
## <a name="see-also"></a>Vea también  
[Clase PDO](../../connect/php/pdo-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

