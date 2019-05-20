---
title: Tipos de cursor (controlador PDO_SQLSRV) | Microsoft Docs
ms.custom: ''
ms.date: 05/03/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 49ea6a6e-78d4-40f8-85eb-180b527f0537
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aa270574d55d50e3b2d8653273027e9d5f133766
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65099736"
---
# <a name="cursor-types-pdosqlsrv-driver"></a>Tipos de cursor (controlador PDO_SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

El controlador PDO_SQLSRV le permite crear conjuntos de resultados desplazables con uno de varios cursores.

Para obtener información sobre cómo especificar un cursor con el controlador PDO_SQLSRV y acceder a ejemplos de código, vea [PDO::prepare](../../connect/php/pdo-prepare.md).

## <a name="pdosqlsrv-and-server-side-cursors"></a>PDO_SQLSRV y cursores de servidor
Antes de la versión 3.0 de [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], el controlador PDO_SQLSRV permite crear un conjunto de resultados con un cursor estático o de solo avance en el lado servidor. A partir de la versión 3.0 de [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], los conjunto de claves y los cursores dinámicos también están disponibles.

Puede indicar el tipo de cursor de servidor mediante [PDO::prepare](../../connect/php/pdo-prepare.md) para seleccionar uno de los siguientes tipos de cursor:

-   `PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY`

-   `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL`

Puede solicitar un cursor dinámico, estático o controlado por conjunto de claves al especificar `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL` y luego pasar el valor apropiado a `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE`. Los valores posibles que puede pasar a `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE` para los cursores de servidor son:

-   `PDO::SQLSRV_CURSOR_DYNAMIC`

-   `PDO::SQLSRV_CURSOR_STATIC`

-   `PDO::SQLSRV_CURSOR_KEYSET`

## <a name="pdosqlsrv-and-client-side-cursors"></a>PDO_SQLSRV y cursores de cliente
Se agregaron los cursores del lado cliente en la versión 3.0 de [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], y permiten almacenar en caché un conjunto de resultados completo en memoria. Una ventaja es que el recuento de filas está disponible después de ejecutar una consulta.

Los cursores del lado cliente deben usarse para conjuntos de resultados de tamaño pequeño a mediano. Los conjuntos de resultados grandes deben utilizar cursores de servidor.

Una consulta devolverá false si el búfer no es suficientemente grande para contener un conjunto de resultados completo cuando se usa un cursor del lado cliente. Puede aumentar el tamaño del búfer hasta el límite de memoria PHP.

Puede configurar el tamaño del búfer que contiene el conjunto de resultados con el atributo `PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE` de [PDO::setAttribute](../../connect/php/pdo-setattribute.md) o [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md). También puede establecer el tamaño máximo del búfer en el archivo php.ini con pdo_sqlsrv.client_buffer_max_kb_size (por ejemplo, pdo_sqlsrv.client_buffer_max_kb_size = 1024).

Puede solicitar un cursor del lado cliente mediante [PDO::prepare](../../connect/php/pdo-prepare.md), al especificar el tipo de cursor `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL` y, a continuación, `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_BUFFERED`.

## <a name="example"></a>Ejemplo
El ejemplo siguiente muestra cómo especificar un cursor almacenado en búfer.
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

## <a name="see-also"></a>Consulte también
[Especificación de un tipo de cursor y selección de filas](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)

