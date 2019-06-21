---
title: PDOStatement::bindColumn | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: bbdcea53-d23d-4769-89a0-95c7cf4d5390
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: de72eb899274502e6a99e160e4911b5e4bf275b8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66761960"
---
# <a name="pdostatementbindcolumn"></a>PDOStatement::bindColumn
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Enlaza una variable a una columna de un juego de resultados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
bool PDOStatement::bindColumn($column, &$param[, $type[, $maxLen[, $driverdata ]]] );  
```  
  
#### <a name="parameters"></a>Parámetros  
$*column*: el número (mixto) de la columna (índice basado en 1) o el nombre de la columna del conjunto de resultados.  
  
&$*param*: el nombre mixto de la variable PHP a la que se enlazará la columna.  
  
$*type*: el tipo de datos opcional del parámetro, que se representa mediante una constante PDO::PARAM_*.  
  
$*maxLen*: un valor entero opcional que no usan los controladores de Microsoft para PHP para SQL Server.  
  
$*driverdata*: parámetros mixtos opcionales del controlador. Por ejemplo, podría especificar PDO::SQLSRV_ENCODING_UTF8 para enlazar la columna a una variable como una cadena codificada en UTF-8.  
  
## <a name="return-value"></a>Valor devuelto  
Se devuelve el valor TRUE si la operación se realiza correctamente; de lo contrario, se devuelve FALSE.  
  
## <a name="remarks"></a>Notas  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="example"></a>Ejemplo  
En este ejemplo se muestra cómo se puede enlazar una variable a una columna de un conjunto de resultados.  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "SELECT Title, FirstName, EmailAddress FROM Person.Contact where LastName = 'Estes'";  
$stmt = $conn->prepare($query);  
$stmt->execute();  
  
$stmt->bindColumn('EmailAddress', $email);  
while ( $row = $stmt->fetch( PDO::FETCH_BOUND ) ){  
   echo "$email\n";  
}  
?>  
```  
  
## <a name="see-also"></a>Consulte también  
[Clase PDOStatement](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
