---
title: Tipos de cursor (controlador PDO_SQLSRV) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 49ea6a6e-78d4-40f8-85eb-180b527f0537
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 621bfe1f20b9ca656bf442377b1f453503b86a8f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47833473"
---
# <a name="cursor-types-pdosqlsrv-driver"></a>Tipos de cursor (controlador PDO_SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

El controlador PDO_SQLSRV le permite crear conjuntos de resultados desplazables con uno de varios cursores.  
  
Para obtener información sobre cómo especificar un cursor con el controlador PDO_SQLSRV y ejemplos de código, consulte [PDO:: Prepare](../../connect/php/pdo-prepare.md).  
  
## <a name="pdosqlsrv-and-server-side-cursors"></a>PDO_SQLSRV y cursores de servidor  
Antes de la versión 3.0 de la [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], el controlador PDO_SQLSRV permite crear un conjunto de resultados con un cursor de servidor estático o de solo avance. A partir de la versión 3.0 de la [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], conjunto de claves y los cursores dinámicos también están disponibles.  
  
Puede indicar el tipo de cursor de servidor mediante el uso de PDO:: Prepare o pdostatement:: setAttribute seleccionar cualquier tipo de cursor:  
  
-   PDO:: ATTR_CURSOR = &GT; PDO:: CURSOR_FWDONLY  
  
-   PDO:: ATTR_CURSOR = &GT; PDO:: CURSOR_SCROLL  
  
Puede solicitar un cursor keyset o dynamic especificando PDO:: attr_cursor = > PDO:: cursor_scroll y, a continuación, pase el valor adecuado para PDO:: sqlsrv_attr_cursor_scroll_type. Los valores posibles que puede pasar a PDO:: sqlsrv_attr_cursor_scroll_type son:  
  
-   PDO::SQLSRV_CURSOR_BUFFERED  
  
-   PDO::SQLSRV_CURSOR_DYNAMIC  
  
-   PDO::SQLSRV_CURSOR_KEYSET_DRIVEN  
  
-   PDO::SQLSRV_CURSOR_STATIC  
  
## <a name="pdosqlsrv-and-client-side-cursors"></a>PDO_SQLSRV y cursores de cliente  
Se agregaron los cursores del lado cliente en la versión 3.0 de la [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] que permite almacenar en caché un completo conjunto de resultados en memoria. Una ventaja es que el recuento de filas está disponible después de ejecutar una consulta.  
  
Los cursores de cliente deben usarse para conjuntos de resultados de tamaño pequeño a mediano. Conjuntos de resultados grandes deben utilizar cursores de servidor.  
  
Una consulta devolverá false si el búfer no es suficientemente grande para contener un completo conjunto de resultados cuando mediante un cursor de cliente. Puede aumentar el tamaño del búfer hasta el límite de memoria PHP.  
  
Puede configurar el tamaño del búfer que contiene el conjunto de resultados con el atributo PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE de [PDO:: setAttribute](../../connect/php/pdo-setattribute.md) o [pdostatement:: setAttribute](../../connect/php/pdostatement-setattribute.md). También puede establecer el tamaño máximo del búfer en el archivo php.ini con pdo_sqlsrv.client_buffer_max_kb_size (por ejemplo, pdo_sqlsrv.client_buffer_max_kb_size = 1024).  
  
Indicar que desea un cursor de cliente mediante el uso de PDO:: Prepare o pdostatement:: setAttribute y seleccione el PDO:: attr_cursor = > PDO:: cursor_scroll tipo de cursor.  A continuación, especifique PDO:: sqlsrv_attr_cursor_scroll_type = > PDO::SQLSRV_CURSOR_BUFFERED.  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "select * from Person.ContactType";  
$stmt = $conn->prepare( $query, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL, PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_BUFFERED));  
$stmt->execute();  
print $stmt->rowCount();  
  
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
  
## <a name="see-also"></a>Ver también  
[Especificación de un tipo de cursor y selección de filas](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)  
  
