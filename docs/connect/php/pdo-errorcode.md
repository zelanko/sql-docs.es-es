---
title: PDO::errorCode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5864b1d8-6814-41cd-a88d-415124484c13
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 143a7bef0a0be2d125068a7f003b0b941ff39617
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="pdoerrorcode"></a>PDO::errorCode
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PDO::errorCode recupera el valor de SQLSTATE de la operación más reciente realizada en el identificador de la base de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
mixed PDO::errorCode();  
```  
  
## <a name="return-value"></a>Valor devuelto  
PDO::errorCode devuelve un valor de SQLSTATE de cinco caracteres como una cadena o Null si no hay ninguna operación en el identificador de la base de datos.  
  
## <a name="remarks"></a>Comentarios  
PDO:: ErrorCode del controlador PDO_SQLSRV devuelve advertencias sobre algunas operaciones correctas. Por ejemplo, en una conexión correcta, PDO:: ErrorCode devuelve "01000", que indica SQL_SUCCESS_WITH_INFO.  
  
PDO::errorCode solo recupera los códigos de error de las operaciones realizadas directamente en la conexión de base de datos. Si crea una instancia de PDOStatement a través de PDO:: Prepare o PDO:: Query y un error se genera en el objeto de instrucción, PDO:: ErrorCode no recuperar ese error. Debe llamar a PDOStatement::errorCode para devolver el código de error de una operación realizada en un objeto de instrucción concreto.  
  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="example"></a>Ejemplo  
En este ejemplo, el nombre de la columna está mal escrito (`Cityx` en lugar de `City`), que produce un error, que se indica a continuación.  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks ", "", "");  
$query = "SELECT * FROM Person.Address where Cityx = 'Essen'";  
  
$conn->query($query);  
print $conn->errorCode();  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[Clase PDO](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
