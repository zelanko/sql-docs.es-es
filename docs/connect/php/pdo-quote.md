---
title: PDO::quote | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ab9ddc48-42f8-4edf-aa8b-b0fc66706161
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7908655954c0f93bd697599ed0d6c809e97d080f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "76916372"
---
# <a name="pdoquote"></a>PDO::quote
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Procesa una cadena para utilizarla en una consulta colocando comillas alrededor de la cadena de entrada conforme a los requisitos de la base de datos de SQL Server subyacente. PDO::quote usará caracteres especiales de escape en la cadena de entrada aplicando un estilo de entrecomillado que admita SQL Server.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
string PDO::quote( $string[, $parameter_type ] )  
```  
  
#### <a name="parameters"></a>Parámetros  
$*string*: la cadena que se entrecomillará.  
  
$*parameter_type*: un símbolo opcional (valor entero) que indica el tipo de datos.  El valor predeterminado es PDO::PARAM_STR.  

Las nuevas constantes de PDO se introdujeron en PHP 7.2 para agregar compatibilidad para [enlazar cadenas Unicode y no Unicode](https://wiki.php.net/rfc/extended-string-types-for-pdo). Las cadenas Unicode se pueden incluir entre comillas con N como prefijo (es decir, N'string ' en lugar de 'string').

1. PDO::PARAM_STR_NATL: un tipo nuevo de cadenas Unicode que se aplicará como OR bit a bit a PDO::PARAM_STR
1. PDO::PARAM_STR_CHAR: un tipo nuevo de cadenas no Unicode que se aplicará como OR bit a bit a PDO::PARAM_STR
1. PDO::ATTR_DEFAULT_STR_PARAM: se establece en PDO::PARAM_STR_NATL o PDO::PARAM_STR_CHAR para indicar un valor para OR bit a bit a PDO::PARAM_STR de manera predeterminada

A partir de la versión 5.8.0, puede utilizar estas constantes con PDO::quote.
  
## <a name="return-value"></a>Valor devuelto  
Una cadena entrecomillada que puede transmitirse a una instrucción SQL, o bien un valor False si se produce un error.  
  
## <a name="remarks"></a>Observaciones  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="example"></a>Ejemplo  
  
```  
<?php  
$database = "test";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$param = 'a \' g';  
$param2 = $conn->quote( $param );  
  
$query = "INSERT INTO Table1 VALUES( ?, '1' )";  
$stmt = $conn->prepare( $query );  
$stmt->execute(array($param));  
  
$query = "INSERT INTO Table1 VALUES( ?, ? )";  
$stmt = $conn->prepare( $query );  
$stmt->execute(array($param, $param2));  
?>  
```  
  
## <a name="example"></a>Ejemplo  

El script siguiente muestra algunos ejemplos de cómo afectan los tipos de cadenas extendidas a PDO::quote() con PHP 7.2+.

```
<?php
$database = "test";
$server = "(local)";
$db = new PDO("sqlsrv:server=$server; Database=$database", "", "");

$db->quote('über', PDO::PARAM_STR | PDO::PARAM_STR_NATL); // N'über'
$db->quote('foo'); // 'foo'

$db->setAttribute(PDO::ATTR_DEFAULT_STR_PARAM, PDO::PARAM_STR_NATL);
$db->quote('über'); // N'über'
$db->quote('foo', PDO::PARAM_STR | PDO::PARAM_STR_CHAR); // 'foo'
?>
```
  
## <a name="see-also"></a>Consulte también  
[Clase PDO](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
