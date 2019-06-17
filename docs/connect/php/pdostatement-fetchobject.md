---
title: PDOStatement::fetchObject | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 71ad1932-cab3-4c29-8950-f5e82547d3b5
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 94e7c29f10e2d04c77fb340b2dee6f4ecf54fa4e
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799187"
---
# <a name="pdostatementfetchobject"></a>PDOStatement::fetchObject
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera la siguiente fila como un objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
mixed PDOStatement::fetchObject([ $class_name[,$ctor_args ]] )  
```  
  
#### <a name="parameters"></a>Parámetros  
$*class_name*: una cadena opcional que especifica el nombre de la clase que se va a crear. El valor predeterminado es stdClass.  
  
$*ctor_args*: una matriz opcional con argumentos de un constructor de clase personalizada.  
  
## <a name="return-value"></a>Valor devuelto  
Si se ejecuta correctamente, devuelve un objeto con una instancia de la clase. Las propiedades se asignan a columnas. Devuelve False en caso de error.  
  
## <a name="remarks"></a>Notas  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="example"></a>Ejemplo  
  
```  
<?php  
   $server = "(local)";  
   $database = "AdventureWorks";  
   $conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetchObject();  
   print $result->Name;  
?>  
```  
  
## <a name="see-also"></a>Consulte también  
[Clase PDOStatement](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
