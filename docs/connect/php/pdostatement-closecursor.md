---
title: 'Pdostatement:: Closecursor | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8997ab61-e948-4d54-8d32-fc080d55525c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 94fc874de4136d2eb078711b135a291425b6ddb8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47682549"
---
# <a name="pdostatementclosecursor"></a>PDOStatement::closeCursor
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Cierra el cursor, lo que permite volver a ejecutar la instrucción.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
bool PDOStatement::closeCursor();  
```  
  
## <a name="return-value"></a>Valor devuelto  
Se devuelve True si la operación se realiza correctamente; de lo contrario, False.  
  
## <a name="remarks"></a>Notas  
closeCursor tiene un efecto cuando la opción de conexión MultipleActiveResultSets se define como False.  Para obtener más información sobre la opción de conexión MultipleActiveResultSets, vea [Cómo deshabilitar los conjuntos de resultados activos múltiples (MARS)](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md).  
  
En lugar de llamar a closeCursor, también puede establecer el identificador de instrucción como Null.  
  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="example"></a>Ejemplo  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "", array('MultipleActiveResultSets' => false ) );  
  
$stmt = $conn->prepare('SELECT * FROM Person.ContactType');  
  
$stmt2 = $conn->prepare('SELECT * FROM HumanResources.Department');  
  
$stmt->execute();  
  
$result = $stmt->fetch();  
print_r($result);  
  
$stmt->closeCursor();  
  
$stmt2->execute();  
$result = $stmt2->fetch();  
print_r($result);  
?>  
```  
  
## <a name="see-also"></a>Ver también  
[Clase PDOStatement](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
