---
title: 'PDO:: ErrorInfo | Documentos de Microsoft'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9d5481d5-13bc-4388-b3aa-78676c0fc709
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7a77f638863921d36cfcab10f65b260b73985730
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="pdoerrorinfo"></a>PDO::errorInfo
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera información ampliada de errores de la operación más reciente en el identificador de la base de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
array PDO::errorInfo();  
```  
  
## <a name="return-value"></a>Valor devuelto  
Una matriz de información de errores de la operación más reciente en el identificador de la base de datos. La matriz consta de los siguientes campos:  
  
-   El código de error de SQLSTATE  
  
-   El código de error específico del controlador  
  
-   El mensaje de error específico del controlador.  
  
Si no hay ningún error, o si no se establece el valor de SQLSTATE, los campos específicos del controlador tendrán el valor Null.  
  
## <a name="remarks"></a>Comentarios  
PDO::errorInfo solo recupera información de error para operaciones realizadas directamente en la base de datos. Utilice PDOStatement::errorInfo cuando se cree una instancia de PDOStatement con PDO::prepare o PDO::query.  
  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="example"></a>Ejemplo  
En este ejemplo, el nombre de la columna está mal escrito (`Cityx` en lugar de `City`), que produce un error, que se indica a continuación.  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks ", "");  
$query = "SELECT * FROM Person.Address where Cityx = 'Essen'";  
  
$conn->query($query);  
print $conn->errorCode();  
echo "\n";  
print_r ($conn->errorInfo());  
?>  
```  
  
## <a name="see-also"></a>Vea también  
[Clase PDO](../../connect/php/pdo-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

