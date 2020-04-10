---
title: PDO::errorCode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5864b1d8-6814-41cd-a88d-415124484c13
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df9bce6acf829e39e5082d63f6a910731b709ef8
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919377"
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
  
## <a name="remarks"></a>Observaciones  
El valor de PDO::errorCode del controlador PDO_SQLSRV devuelve advertencias sobre algunas operaciones correctas. Por ejemplo, en una conexión correcta, PDO::errorCode devuelve "01000", que indica SQL_SUCCESS_WITH_INFO.  
  
PDO::errorCode solo recupera los códigos de error de las operaciones realizadas directamente en la conexión de base de datos. Si crea una instancia de PDOStatement a través de PDO::prepare o PDO::query y se genera un error en el objeto de instrucción, PDO::errorCode no recupera ese error. Debe llamar a PDOStatement::errorCode para devolver el código de error de una operación realizada en un objeto de instrucción concreto.  
  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="example"></a>Ejemplo  
En este ejemplo, no se ha escrito correctamente el nombre de la columna (`Cityx` en lugar de `City`), lo que ha provocado un error, del que se informa después.  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks ", "", "");  
$query = "SELECT * FROM Person.Address where Cityx = 'Essen'";  
  
$conn->query($query);  
print $conn->errorCode();  
?>  
```  
  
## <a name="see-also"></a>Consulte también  
[Clase PDO](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
