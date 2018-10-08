---
title: PDOStatement::getColumnMeta | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c92a21cc-8e53-43d0-a4bf-542c77c100c9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dd67f3492788a38dfac635f51a16014d926578a3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47670863"
---
# <a name="pdostatementgetcolumnmeta"></a>PDOStatement::getColumnMeta
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera los metadatos de una columna.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
array PDOStatement::getColumnMeta ( $column );  
```  
  
#### <a name="parameters"></a>Parámetros  
*$conn*: (entero) número basado en cero de la columna cuyos metadatos se van a recuperar.  
  
## <a name="return-value"></a>Valor devuelto  
Una matriz asociativa (clave y valor) que contiene los metadatos de la columna. Consulte la sección Comentarios para obtener una descripción de los campos de la matriz.  
  
## <a name="remarks"></a>Notas  
En la tabla siguiente se describen los campos de la matriz que devuelve getColumnMeta.  
  
|NAME|VALUES|  
|--------|----------|  
|native_type|Especifica el tipo PHP de la columna. Siempre es una cadena.|  
|driver:decl_type|Especifica el tipo SQL que se utiliza para representar el valor de columna en la base de datos. Si la columna del conjunto de resultados es el resultado de una función, PDOStatement::getColumnMeta no devuelve este valor.|  
|flags|Especifica las marcas establecidas para esta columna. Siempre es 0.|  
|NAME|Especifica el nombre de la columna de la base de datos.|  
|table|Especifica el nombre de la tabla que contiene la columna de la base de datos. Siempre en blanco.|  
|len|Especifica la longitud de columnas.|  
|precisión|Especifica la precisión numérica de esta columna.|  
|pdo_type|Especifica el tipo de esta columna tal y como representan las constantes de PDO::PARAM_*. Siempre es PDO::PARAM_STR (2).|  
  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="example"></a>Ejemplo  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$stmt = $conn->query("select * from Person.ContactType");  
$metadata = $stmt->getColumnMeta(2);  
var_dump($metadata);  
  
print $metadata['sqlsrv:decl_type'] . "\n";  
print $metadata['native_type'] . "\n";  
print $metadata['name'];  
?>  
```  
  
## <a name="see-also"></a>Ver también  
[Clase PDOStatement](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
