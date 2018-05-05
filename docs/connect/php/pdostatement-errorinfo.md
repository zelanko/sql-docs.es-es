---
title: 'Pdostatement:: ErrorInfo | Documentos de Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e45bebe8-ea4c-49b6-93db-cf1ae65f530c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 46c2cda3b7b36d534e02a8a4d3a782e3abd94240
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="pdostatementerrorinfo"></a>PDOStatement::errorInfo
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera información ampliada de errores de la operación más reciente en el identificador de instrucción.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
array PDOStatement::errorInfo();  
```  
  
## <a name="return-value"></a>Valor devuelto  
Una matriz de información de errores de la operación más reciente en el identificador de instrucción. La matriz consta de los siguientes campos:  
  
-   El código de error de SQLSTATE  
  
-   El código de error específico del controlador  
  
-   El mensaje de error específico del controlador  
  
Si no hay ningún error, o si no se establece el valor de SQLSTATE, los campos específicos del controlador tendrán el valor Null.  
  
## <a name="remarks"></a>Comentarios  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="example"></a>Ejemplo  
En este ejemplo, la instrucción SQL tiene un error, que se indica a continuación.  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks", "", "");  
$stmt = $conn->prepare('SELECT * FROM Person.Addressx');  
  
$stmt->execute();  
print_r ($stmt->errorInfo());  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[Clase PDOStatement](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
